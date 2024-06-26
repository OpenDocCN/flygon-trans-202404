# 8Mutation: 结构和变量

又到了另一个

这些中哪些是相同的？

> +   f = 3
> +   
> +   o.f = 3
> +   
> +   f = 3

假设这三个都是在 Java 中，第一个和第三个可能会像第二个一样完全相同，或者完全像第二个一样：这完全取决于 f 是一个局部标识符（例如参数）还是对象的字段（即，代码实际上是 this.f = 3）。

无论哪种情况，我们都要求评估器永久更改绑定到 f 的值。这对其他观察者有重要的影响。直到现在，对于给定的一组输入，计算始终返回相同的值。现在，答案取决于何时调用它：在上面，它取决于在 f 的值更改之前还是之后调用了它。时间的引入对于关于程序的推理有深远的影响。

但是，上述统一语法中实际上有两种完全不同的更改概念。更改字段的值（o.f = 3 或 this.f = 3）与更改标识符的值（f = 3，其中 f 是在方法内部绑定的，而不是由对象绑定的）极为不同。我们将依次探讨这些。我们将在下文中处理字段，并在 Variables)中返回标识符。

## 8.1 可变结构

### 8.1.1 可变结构的简单模型

对象是结构的泛化，我们很快就会看到 [REF]。因此，对象中的字段是结构中字段的泛化，并且为了理解突变，大多数情况下（但不完全是！[REF]）理解可变对象就足够了。为了更加简化，我们不需要一个结构有很多字段：一个字段就足够了。我们称之为箱子。在 Racket 中，箱子仅支持三种操作：

> | box : ('a -> (boxof 'a)) |
> | --- |
> | unbox : ((boxof 'a) -> 'a) |
> | set-box! : ((boxof 'a) 'a -> void) |

因此，box 接受一个值并将其包装在可变容器中。unbox 提取容器内的当前值。最后，set-box! 更改容器中的值，在类型化语言中，新值应与之前的类型一致。因此，您可以将箱子视为等同于具有参数化类型的 Java 容器类，该类具有具有获取器和设置器的单个成员字段：box 是构造函数，unbox 是获取器，而 set-box! 是设置器。（因为只有一个字段，它的名称无关紧要。）

> | class Box<T> { |
> | --- |
> |     private T the_value; |
> |     Box(T v) { |
> |         this.the_value = v; |
> |     } |
> |     T get() { |
> |         return the_value; |
> |     } |
> |     void set(T v) { |
> |         the_value = v; |
> |     } |
> | } |

因为我们有时必须以组的形式进行突变（例如，从一个银行帐户中取钱并将其存入另一个帐户），因此能够对一组可变操作进行排序是有用的。在 Racket 中，begin 允许您编写一系列操作；它按顺序评估它们并返回最后一个的值。

练习

> 通过解糖为 let（因此转换为 lambda）来定义 begin。

这是非规范 desguaring 的绝佳示例。我们选择向核心添加一个明显不必要的构造。如果我们的目标是缩小解释器的大小——也许会增加输入程序的大小——我们不会做出这个选择。但是我们在本书中的目标是研究教学解释器，因此我们选择一个更大的语言，因为这更具教育意义。尽管可以消除 begin 作为语法糖，但它将非常有助于理解突变是如何工作的。因此，我们将在核心中添加一个简单的、两项的序列版本。

### 8.1.2 搭脚手架

首先，让我们扩展我们的核心语言数据类型：

> | (define-type ExprC |
> | --- |
> |   [numC (n : number)] |
> |   [idC (s : symbol)] |
> |   [appC (fun : ExprC) (arg : ExprC)] |
> |   [plusC (l : ExprC) (r : ExprC)] |
> |   [multC (l : ExprC) (r : ExprC)] |
> |   [lamC (arg : symbol) (body : ExprC)] |
> |   [boxC (arg : ExprC)] |
> |   [unboxC (arg : ExprC)] |
> |   [setboxC (b : ExprC) (v : ExprC)] |
> |   [seqC (b1 : ExprC) (b2 : ExprC)]) |

观察到在 setboxC 表达式中，盒子位置和其新值都是表达式。后者并不奇怪，但前者可能会让人感到意外。这意味着我们可以在对应的 Racket 中编写这样的程序：

> | (let ([b0 (box 0)] |
> | --- |
> |       [b1 (box 1)]) |
> |   (let ([l (list b0 b1)]) |
> |     (begin |
> |       (set-box! (first l) 1) |
> |       (set-box! (second l) 2) |
> |       l))) |

这将计算出一个包含 1 和 2 的盒子列表。你的输出可能看起来像'(#&1 #&2)。#&符号是 Racket 的缩写语法前缀，表示“盒子”。观察到第一个 set-box!指令的第一个参数是(first l)，即一个计算结果为盒子的表达式，而不仅仅是一个文字盒子或标识符。这与诸如 Java 之类的语言完全类似，其中可以（在某种类型的自由度下）编写

> | public static void main (String[] args) { |
> | --- |
> |     Box<Integer> b0 = new Box<Integer>(0); |
> |     Box<Integer> b1 = new Box<Integer>(1); |
> |   |
> |     ArrayList<Box<Integer>> l = new ArrayList<Box<Integer>>(); |
> |     l.add(b0); |
> |     l.add(b1); |
> |   |
> |     l.get(0).set(1); |
> |     l.get(1).set(2); |
> | } |

观察到 l.get(0)是一个复合表达式，用于找到适当的盒子，并计算出在其上调用 set 的盒子对象。

为方便起见，我们假设已经实现了解糖功能，提供了（a）let 和（b）在序列中超过两个项时必要的功能（这些可以被解糖为嵌套序列）。我们有时也会用原始的 Racket 语法编写表达式，这样做既是为了简洁（因为核心语言术语可能变得相当庞大和笨重），也是为了您可以在 Racket 中运行相同的术语并观察它们产生的答案。由此可见，我们将 Racket 中的行为——<wbr>这与几乎所有支持可变对象和结构的主流语言中的行为类似——视为参考行为。

### 8.1.3 与闭包的交互

考虑一个简单的计数器：

> | (define new-loc |
> | --- |
> |   (let ([n (box 0)]) |
> |     (lambda () |
> |       (begin |
> |         (set-box! n (add1 (unbox n))) |
> |         (unbox n))))) |

每次调用它时，它都会产生下一个整数：

| > (new-loc) |
| --- |
| - number |
| 1 |
| > (new-loc) |
| - number |
| 2 |

这为什么有效？因为盒子只创建一次，并绑定到 n，然后关闭。所有后续的变异都影响同一个盒子。相反，交换两行会产生很大的不同：

> | (define new-loc-broken |
> | --- |
> |   (lambda () |
> |     (let ([n (box 0)]) |
> |       (begin |
> |         (set-box! n (add1 (unbox n))) |
> |         (unbox n))))) |

观察：

| > (new-loc-broken) |
| --- |
| - number |
| 1 |
| > (new-loc-broken) |
| - number |
| 1 |

在这种情况下，每次调用函数时都会分配一个新的盒子，因此每次答案都相同（尽管过程内部发生了变异）。我们的盒子实现应确保保留此区别。

上面的示例暗示了实施必要性。显然，无论 new-loc 中的环境闭合多少次，都必须每次都引用同一个盒子。然而，还需要确保该盒子中的值每次都不同！仔细看看：它在词法上必须是相同的，但在动态上不同。这种区别将是我们实现的核心。

### 8.1.4 理解盒子的解释

让我们从复制我们当前的解释器开始：

<interp-take-1>)) ::=

> | (define (interp [expr : ExprC] [env : Env]) : Value |
> | --- |
> |   (type-case ExprC expr |
> |     [numC (n) (numV n)] |
> |     [idC (n) (lookup n env)] |
> |     [appC (f a) (local ([define f-value (interp f env)]) |
> |                   (interp (closV-body f-value) |
> |                           (extend-env (bind (closV-arg f-value) |
> |                                             (interp a env)) |
> |                                       (closV-env f-value))))] |
> |     [plusC (l r) (num+ (interp l env) (interp r env))] |
> |     [multC (l r) (num* (interp l env) (interp r env))] |
> |     [lamC (a b) (closV a b env)] |
> |     <boxC-case> |
> |     <unboxC-case> |
> |     <setboxC-case> |
> |     <seqC-case>)) |

由于我们引入了一种新的值类型，盒子，我们必须更新值集合：

<value-take-1>)) ::=

> | (define-type Value |
> | --- |
> |   [numV (n : number)] |
> |   [closV (arg : symbol) (body : ExprC) (env : Env)] |
> |   [boxV (v : Value)]) |

这两种情况应该很容易。当我们得到一个盒子表达式时，我们只需评估它并将其包装在 boxV 中返回：

<boxC-case-take-1>)) ::=

> [boxC (a) (boxV (interp a env))]

同样，从盒子中提取值很容易：

<unboxC-case-take-1>)) ::=

> [unboxC (a) (boxV-v (interp a env))]

到目前为止，您应该正在构建一组健康的测试用例，以确保它们的行为符合您的预期。

当然，我们还没有做任何艰苦的工作。所有有趣的行为可能隐藏在 setboxC 的处理中。因此，您可能会感到惊讶，我们将首先查看 seqC（您将看到为什么我们将其包含在核心中）。

让我们考虑两个指令序列的最自然实现：

<seqC-case-take-1>)) ::=

> | [seqC (b1 b2) (let ([v (interp b1 env)]) |
> | --- |
> |                 (interp b2 env))] |

也就是说，我们首先评估第一个术语，然后是第二个术语，并返回第二个的结果。

您应该立即发现一些令人不安的事情。我们绑定了评估第一个术语的结果，但随后没有做任何事情。没关系：很可能第一个术语包含某种变异表达式，其值并不重要（实际上，请注意 set-box！返回一个空值）。因此，另一种实现可能是这样的：

<seqC-case-take-2>)) ::=

> | [seqC (b1 b2) (begin |
> | --- |
> |                 (interp b1 env) |
> |                 (interp b2 env))] |

这不仅让人稍感不满，因为它只是使用了类似的 Racket 顺序构造，而且肯定是错误的！只有在变异���结果被存储在某处时，这才能起作用。但是，由于我们的解释器只计算值，并且不执行任何变异操作，因此在（interp b1 env）中的任何变异都完全丢失。这显然不是我们想要的。

### 8.1.5 环境有助于吗？

这里有另一个示例可以帮助：

> | (let ([b (box 0)]) |
> | --- |
> |   (begin (begin (set-box! b (+ 1 (unbox b))) |
> |                 (set-box! b (+ 1 (unbox b)))) |
> |          (unbox b))) |

在 Racket 中，这将评估为 2。练习

> 在 ExprC 中表示这个表达式。

让我们考虑内部序列的评估。在两种情况下，表达式（（set-box！...）的表示）完全相同。然而，在底层发生了一些变化，因为这些导致盒子的值从 0 变为 2！如果我们改为评估

> | (let ([b (box 0)]) |
> | --- |
> |   (+ (begin (set-box! b (+ 1 (unbox b))) |
> |             (unbox b)) |
> |      (begin (set-box! b (+ 1 (unbox b))) |
> |             (unbox b)))) |

在此处求值为 3。在加法规则中，对 interp 的两次调用在两种情况下都发送完全相同的文本表达式。然而，某种方式上左侧加法分支的影响会在右侧分支产生作用，我们必须排除远距作用。

如果解释器被给予完全相同的表达式，那么它如何可能避免产生完全相同的答案呢？最明显的方式是，如果解释器的另一个参数，即环境，有所不同。截至目前，完全相同的环境被发送到序列的两个分支和加法的两个分支，因此我们的解释器—对于给定的输入每次都产生相同的输出—不可能产生我们想要的答案。

到目前为止，我们知道以下内容：

1.  我们必须确保解释器在预计可能产生不同结果的调用时被提供不同的参数。

1.  我们必须在解释器中返回对其参数表达式求值时所做的变异记录。

因为表达式是什么样的，第一个观点表明我们可能尝试使用环境来反映调用之间的差异。反过来，第二个观点表明解释器的每次调用还应返回环境，以便传递给下一次调用。大致上，然后，解释器的类型可能变成：

> | ; interp : ExprC * Env -> Value * Env |
> | --- |

换句话说，解释器接受一个表达式和环境；它在该环境中进行评估，并在进行时更新环境；当表达式完成评估时，解释器返回答案（就像以前一样），以及一个更新后的环境，该环境又被发送到解释器的下一次调用。而 setboxC 的处理在某种程度上会影响环境以反映变异。然而，在我们深入实现之前，我们应该考虑这种变化的后果。环境已经有一个重要的用途：它保存了延迟的替换。在这方面，它已经有了明确的语义—由替换给出—我们必须小心不要改变它。与替换的联系的一个后果是，它也是词法作用域信息的存储库。例如，如果我们允许扩展环境逃离加法的一个分支并在另一个分支中使用它，请考虑以下程序的影响：

> | (+ (let ([b (box 0)]) |
> | --- |
> |      1) |
> |    b) |

很明显，这个程序有一个错误：加法的右侧分支中的 b 是未绑定的（左侧分支中的 b 的作用域在 let 的关闭时结束—如果这不明显，请对上述表达式进行解糖以使用函数）。但在解释 let 结束时扩展的环境中，b 显然已经被绑定。练习

> 详细解决上述问题并确保你理解它。

你可以尝试各种其他相关的提议，但它们很可能都有类似的缺陷。例如，你可能会决定，由于问题涉及环境中的额外绑定，你将在返回的环境中删除所有添加的绑定。听起来不错？你还记得我们有闭包吗？

练习

> 考虑以下程序的表示： 
> 
> > | (let ([a (box 1)]) |
> > | --- |
> > |   (let ([f (lambda (x) (+ x (unbox a)))]) |
> > |     (begin |
> > |       (set-box! a 2) |
> > |       (f 10)))) |
> > 
> 这个例子会引起什么问题？

相反，我们应该注意到，虽然上述约束都是有效的，但我们提出的解决方案并不是唯一的解决方案。我们需要的是上述列出的两个条件；请注意，实际上两者都不需要环境成为负责任的代理。事实上，很明显，环境不能是主要代理。

### 8.1.6 引入存储

前面的讨论告诉我们，我们需要两个存储库来配合表达式，而不是一个。其中之一，环境，继续负责维护词法作用域。但是环境不能直接将标识符映射到它们的值，因为值可能会改变。相反，需要有其他东西负责维护已变异盒子的动态状态。这个后者数据结构被称为存储。

像环境一样，存储是一个部分映射。它的域可以是任何抽象名称集合，但自然地将其视为数字，用于代表内存位置。这是因为语义中的存储直接映射到机器中（抽象的）物理存储器，传统上是用数字进行寻址的。因此，环境将名称映射到位置，而存储将位置映射到值：

> | (define-type-alias Location number) |
> | --- |
> |   |
> | (define-type Binding |
> |   [bind (name : symbol) (val : Location)]) |
> |   |
> | (define-type-alias Env (listof Binding)) |
> | (define mt-env empty) |
> | (define extend-env cons) |
> |   |
> | (define-type Storage |
> |   [cell (location : Location) (val : Value)]) |
> |   |
> | (define-type-alias Store (listof Storage)) |
> | (define mt-store empty) |
> | (define override-store cons) |

我们还将配备一个用于查找存储中值的函数，就像我们已经为环境配备了一个一样（现在返回位置而不是值）：

> | (define (lookup [for : symbol] [env : Env]) : Location |
> | --- |
> |   ...) |
> | (define (fetch [loc : Location] [sto : Store]) : Value |
> |   ...) |

有了这个，我们就可以将我们对值的概念精炼到正确的位置：

> | (define-type Value |
> | --- |
> |   [numV (n : number)] |
> |   [closV (arg : symbol) (body : ExprC) (env : Env)] |
> |   [boxV (l : Location)]) |

练习

> 填写查找和提取的主体。

### 8.1.7 解释盒子

现在我们有了环境可以返回的东西，更新后反映了在表达式评估过程中的变化，而无需以任何方式更改环境。因为函数只能返回一个值，让我们定义一个数据结构来保存解释器的新结果：

> | (define-type Result |
> | --- |
> |   [v*s (v : Value) (s : Store)]) |

因此，解释器的类型变为：<interp-mut-struct>)) ::=

> | (define (interp [expr : ExprC] [env : Env] [sto : Store]) : Result |
> | --- |
> |   <ms-numC-case>)) |
> |   <ms-idC-case>)) |
> |   <ms-appC-case>)) |
> |   <ms-plusC/multC-case>)) |
> |   <ms-lamC-case>)) |
> |   <ms-boxC-case>)) |
> |   <ms-unboxC-case>)) |
> |   <ms-setboxC-case>)) |
> |   <ms-seqC-case>))) |

最容易分派的是数字。记住，我们必须返回反映在评估给定表达式时发生的所有变化的存储。因为数字是一个常数，没有可能发生变化，所以返回的存储与传入的存储相同：

<ms-numC-case>)) ::=

> [numC (n) (v*s (numV n) sto)]

类似的论点适用于闭包的创建；请注意，我们谈论的是闭包的创建，而不是使用： 

<ms-lamC-case>)) ::=

> [lamC (a b) (v*s (closV a b env) sto)]

标识符几乎一样简单，但如果你过于简单，你会得到一个类型错误，提醒你要获取一个值，你现在必须在环境和存储中查找：

<ms-idC-case>)) ::=

> [idC (n) (v*s (fetch (lookup n env) sto) sto)]

注意查找和提取如何组合以产生与之前仅查找产生的相同结果。

现在事情变得有趣起来。

让我们来看一下顺序。显然，我们需要解释这两个术语：

> | (interp b1 env sto) |
> | --- |
> | (interp b2 env sto) |

哦，但等等。整个重点是在第一个术语返回的存储中评估第二个术语，否则所有这些更改就没有意义。因此，我们必须评估第一个术语，捕获结果存储，并使用它来评估第二个术语。（评估第一个术语也会产生其值，但顺序会忽略这个值，并假定第一次运行纯粹是为了其潜在的变化。）我们将以一种程式化的方式写出这个：<ms-seqC-case>)) ::=

> | [seqC (b1 b2) (type-case Result (interp b1 env sto) |
> | --- |
> |                 [v*s (v-b1 s-b1) |
> |                      (interp b2 env s-b1)])] |

这表示要(interp b1 env sto);给结果命名，并将 v-b1 和 s-b1 分别存储，然后在第一个存储器中评估第二个项：(interp b2 env s-b1)。结果将是第二项返回的值和存储器，这是我们预期的。从代码中可以看出，第一个项的效果仅对存储器有影响，因为虽然我们绑定了 v-b1，但我们从未随后使用它。

现在开始吧！

> 花点时间思考上面的代码。您很快就需要调整眼睛以流畅地阅读此模式。

现在让我们继续讨论二进制算术原语。这些与序列类似，因为它们有两个子项，但在这种情况下，我们确实关心每个分支的值。和往常一样，我们只看 plusC，因为 multC 几乎相同。

<ms-plusC/multC-case>)) ::= 

> | [plusC (l r) (type-case Result (interp l env sto) |
> | --- |
> |                [v*s (v-l s-l) |
> |                     (type-case Result (interp r env s-l) |
> |                       [v*s (v-r s-r) |
> |                            (v*s (num+ v-l v-r) s-r)])])] |

请注意，我们已经展开了另一层序列模式，这样我们就可以保存两个结果并将它们提供给 num+。

这是一个重要区别。当我们评估一个术语时，通常根据语言的作用域规则，我们为所有其子项使用相同的环境。因此，环境以递归下降的模式流动。相比之下，存储器是线程化的：我们不是在所有分支中使用相同的存储器，而是从一个分支中取出存储器并将其传递到下一个分支，然后取出结果并将其发送回。这种模式称为传递存储器的风格。

现在一切都清楚了。我们看到传递存储器的风格是我们的秘密武器：它使环境能够保留词法范围，同时仍然提供可以反映更改的绑定结构。我们的直觉告诉我们，环境必须以某种方式参与获取同一表达式的不同结果，我们现在可以看到它是如何做到的：不是直接地，通过自身的更改，而是间接地，通过引用存储器，后者会更新。现在我们只需要看看存储器本身是如何“变化”的。

让我们从装箱开始。要将值存储到箱子中，我们必须首先在存储器中分配一个新的位置，该位置将存放其值。然后，与箱子对应的值将记住此位置，供箱子突变时使用。

<ms-boxC-case>)) ::= 

> | [boxC (a) (type-case Result (interp a env sto) |
> | --- |
> |             [v*s (v-a s-a) |
> |                  (let ([where (new-loc)]) |
> |                    (v*s (boxV where) |
> |                         (override-store (cell where v-a) |
> |                                         s-a)))])] |

现在开始吧！

> 注意我们以上依赖于 new-loc，它本身是以盒子为基础实现的！这是彻头彻尾的作弊。你会如何修改解释器，以便我们不再需要一个变异实现的 new-loc？

要消除这种 new-loc 风格，最简单的选择是向解释器添加另一个参数，并从中返回值，表示迄今为止使用的最大地址。每个在存储中分配的操作都会返回一个递增的地址，而其他操作则会返回不变。换句话说，这正是存储传递模式的另一个应用。以这种方式编写解释器会使其非常笨重，可能会掩盖存储传递模式对存储本身更重要的用途，这就是为什么我们没有这样做的原因。然而，重要的是要确保我们能够做到：这告诉我们我们不依赖于盒子来向语言中添加盒子。

现在盒子记录了内存中的位置，获取与之对应的值就很容易了。

<ms-unboxC-case>)) ::=

> | [unboxC (a) (type-case Result (interp a env sto) |
> | --- |
> |               [v*s (v-a s-a) |
> |                    (v*s (fetch (boxV-l v-a) s-a) s-a)])] |

这与我们之前看到的模式相同，我们必须使用 fetch 来获取实际驻留在那个位置的值。请注意，我们依赖 Racket 在底层值实际上不是 boxV 时停止并显示错误；否则，不检查将是危险的，因为这等同于对任意内存进行解引用（就像 C 程序有时会导致灾难性后果一样）。

现在让我们看看如何更新盒子中保存的值。首先，我们必须评估盒子表达式以获得一个盒子，以及评估值表达式以获得要存储在其中的新值。盒子的值将是一个包含位置的 boxV。

原则上，我们希望“更改”或覆盖存储中该位置的值。我们可以通过两种方式实现这一点。

1.  有两种方法可以更新存储在那个位置的值，一种是遍历存储空间，找到该位置的旧绑定，并用新的替换它，同时保留所有其他存储绑定不变。

1.  另一种更懒惰的选择是简单地为该位置扩展存储空间，这样做可以确保我们总是获得该位置的最新绑定（这就是环境中查找的工作方式，所以在存储中获取也应该是这样）。

下面的代码是独立于这些选项的：<ms-setboxC-case>)) ::=

> | [setboxC (b v) (type-case Result (interp b env sto) |
> | --- |
> |                  [v*s (v-b s-b) |
> |                       (type-case Result (interp v env s-b) |
> |                         [v*s (v-v s-v) |
> |                              (v*s v-v |
> |                                   (override-store (cell (boxV-l v-b) |
> |                                                         v-v) |
> |                                                   s-v))])])] |

但是，由于我们将`override-store`实现为上述的`cons`，我们实际上选择了更懒惰的（并且稍微有风险，因为它依赖于`fetch`的实现）选项。

练习

> 实现存储改变的另一种版本，通过这种方式我们更新一个现有的绑定，从而避免了存储中一个位置的多个绑定。

练习

> 当我们寻找要覆盖其上存储的值的位置时，该位置可能不存在吗？如果是这样，请编写一个演示此情况的程序。如果不是，请解释解释器的不变量防止这种情况发生的原因。

好的，除了应用之外，我们现在已经完成了所有内容！大部分应用程序应该已经很熟悉了：评估函数位置，评估参数位置，解释闭包体在闭包环境的扩展中...但是存储如何与此交互？

<ms-appC-case>)) ::=

> | appC (f a) |
> | --- |
> |       (type-case Result (interp f env sto) |
> |         [v*s (v-f s-f) |
> |              (type-case Result (interp a env s-f) |
> |                [v*s (v-a s-a) |
> |                     [<ms-appC-case-main>))])])] |

让我们首先考虑扩展闭包环境。我们要扩展的名称显然是函数的形式参数的名称。但我们将它绑定到哪个位置？为了避免与已使用的位置混淆（这是我们稍后将明确介绍的混淆！[REF]），让我们只分配一个新位置。此位置在环境中使用，并且参数的值驻留在存储中的此位置上：

<ms-appC-case-main>)) ::=

> | (let ([where (new-loc)]) |
> | --- |
> |   (interp (closV-body v-f) |
> |           (extend-env (bind (closV-arg v-f) |
> |                             where) |
> |                       (closV-env v-f)) |
> |           (override-store (cell where v-a) s-a))) |

因为我们没有说函数参数是可变的，所以没有真正需要以这种方式实现过程调用。我们可以选择像以前一样遵循相同的策略。实际上，注意到此位置的可变性永远不会被使用：只有`setboxC`改变了现有存储位置中的内容（上面的`override-store`在技术上是存储初始化），而且仅当它们被`boxVs`引用时才这样做，但是上面并没有分配任何盒子。您可以将其称为无用的应用商店。但是，我们选择以这种方式实现应用程序是为了统一性，并减少我们需要处理的情况数量。

练习

> 尝试仅将存储位置的使用限制为盒子是一项有用的练习。您需要做多少改变？

### 8.1.8 整体情况

即使我们已经完成了实现，仍然有许多微妙之处和见解需要讨论。

1.  我们实现中隐含的一个微妙而重要的决定是评估的顺序。例如，为什么我们没有这样实现加法呢？

    > | [plusC (l r) (type-case Result (interp r env sto) |
    > | --- |
    > |                [v*s (v-r s-r) |
    > |                     (type-case Result (interp l env s-r) |
    > |                       [v*s (v-l s-l) |
    > |                            (v*s (num+ v-l v-r) s-l)])])] |

    这样做也是完全一致的。同样，在传递存储的模式中体现的是在评估函数位置之前评估参数的决定。请注意：

    1.  以前，我们将这样的决定委托给底层语言实现。现在，传递存储迫使我们将计算序列化，因此我们必须自己做出这个决定（无论我们是否意识到）。

    1.  更重要的是，这个决定现在是一个语义决定。在没有变异之前，例如，加法的一个分支不能影响另一个分支产生的值。它们唯一能产生的影响是停止并出现错误或无法终止——这确实是可观察的效果，但在更粗略的层面上。一个程序不会因为评估的顺序不同而以两个不同的答案终止。因为每个分支都可能有影响另一个值的变异，我们必须选择某种顺序，以便程序员可以预测他们的程序将要做什么！被迫编写一个传递存储的解释器已经让这一点变得清晰。

1.  注意，在应用规则中，我们传递的是动态存储，即，由评估函数和参数得到的存储。这恰恰与我们在环境中所说的相反。这种区别至关重要。存储实际上是“动态作用域的”，因为它反映了计算的历史，而不是其词法形状。然而，由于我们已经使用术语“作用域”来指代标识符的绑定，因此说“动态作用域”来指代存储会令人困惑。相反，我们只说它是持久的。

    有时语言会危险地混淆这两者。例如，在 C 语言中，绑定到本地标识符的值（默认情况下）是在堆栈上分配的。然而，堆栈与环境匹配，因此在调用完成后会消失。然而，如果调用返回对这些值的任何引用，这些引用现在指向未使用或甚至被覆盖的内存：这是 C 程序中严重错误的真正来源。问题在于值本身是持久的；只有引用这些值的标识符具有词法作用域。

1.  我们已经讨论过有两种覆盖存储的策略：简单地扩展它（并依赖于提取最新的值）或“搜索和替换”。后一种策略的优点是不保留永远无法再次获得的无用存储绑定。

    但是，这并不覆盖所有的浪费内存。随着时间的推移，我们不再能够完全访问某些箱子：例如，如果它们只绑定到一个标识符，而该标识符不再在范围内。这些位置被称为垃圾。更多概念上的思考，垃圾位置是那些其消除对程序产生的值没有任何影响的位置。有许多识别和回收垃圾位置的策略，通常称为垃圾收集 [REF]。

1.  对于每个表达式位置都评估并线程化结果存储非常重要。例如，考虑一下 unboxC 的这个实现：

    > | [unboxC (a) (type-case Result (interp a env sto) |
    > | --- |
    > |               [v*s (v-a s-a) |
    > |                    (v*s (fetch (boxV-l v-a) sto) s-a)])] |

    你注意到了吗？我们从 sto 中获取了位置，而不是 s-a。但 sto 反映了在 unboxC 表达式的评估之前发生的变异，而不是其中的任何变异。可能还会有吗？Mais oui！

    > | (let ([b (box 0)]) |
    > | --- |
    > |   (unbox (begin (set-box! b 1) |
    > |                 b))) |

    以上的错误代码将导致评估结果为 0，而不是 1。

1.  这里有另一个类似的错误：

    > | [unboxC (a) (type-case Result (interp a env sto) |
    > | --- |
    > |               [v*s (v-a s-a) |
    > |                    (v*s (fetch (boxV-l v-a) s-a) sto)])] |

    我们如何打破这个？嗯，我们正在返回旧的存储，即在 unboxC 中的任何变异之前的存储。因此，我们只需要外部上下文依赖于其中一个。

    > | (let ([b (box 0)]) |
    > | --- |
    > |   (+ (unbox (begin (set-box! b 1) |
    > |                    b)) |
    > |      (unbox b))) |

    这应该评估为 2，但由于返回的存储是一个其中 b 的位置被绑定到表示 0 的表示形式的存储，结果是 1。

    如果我们结合上述两个错误——即在最后一行两次使用 sto 而不是两次使用 s-a——这个表达式将评估为 0 而不是 2。

    练习

    > 通过解释器；将对更新后的存储的每个引用替换为更新之前的引用；确保你的测试案例捕获所有引入的错误！

1.  注意，这些“旧”存储的使用使我们能够执行一种时间旅行：因为变异引入了时间的概念，所以这些使我们能够回到变异尚未发生的时刻。这听起来既有趣又反常；它有什么用处吗？

    它可以！想象一下，我们不直接对存储进行变异，而是引入了一个关于对存储预期更新的日志的概念。日志像真实的存储本身一样以线程方式流动。某些指令创建一个新的日志；之后，所有查找都首先检查日志，只有在日志找不到位置的绑定时才会在实际存储中查找。还有两个新指令：一个是丢弃日志（即，执行时间旅行），另一个是提交它（即，将其所有编辑应用于实际存储）。

    这就是软件事务内存的本质。每个线程维护自己的日志。因此，一个线程在提交之前看不到其他线程所做的编辑（因为每个线程只看到自己的日志和全局存储器，但不看其他线程的日志）。同时，每个线程都可以获得自己的一致视图（它可以看到它所做的编辑，因为这些编辑记录在日志中）。如果事务成功结束，所有线程都会原子地看到更新后的全局存储器。如果事务中止，被丢弃的日志将带走所有更改，并且线程的状态将恢复（除了其他线程提交的全局更改）。

    如果我们坚持使用共享可变状态进行编程，软件事务内存提供了一种最明智的解决多线程编程困难的方法之一。然而，由于大多数计算机只有一个全局存储器，维护日志可能很昂贵，并且需要大量工作来对其进行优化。作为一种替代方案，一些硬件架构已经开始提供对事务内存的直接支持，使得创建、维护和提交日志与使用全局存储器一样高效，消除了采用这一想法的一个重要障碍。

    练习

    > 增加语言与软件事务内存日志的日志功能。

练习

> 另一种实现策略是将环境映射到装箱值的名称。我们在这里不这样做，因为：（a）这将是作弊，（b）不会告诉我们如何在没有箱子的语言中实现相同的功能，（c）不一定适用于其他变异操作，（d）最重要的是，这并不能真正让我们了解到这里发生了什么。
> 
> 然而，了解这一点仍然是有用的，至少因为在实现自己的语言时，您可能会发现这是一种有用的策略。因此，修改实现以遵循这个策略。你是否仍然需要传递存储样式？为什么？

## 8.2 变量

现在我们已经弄清楚了结构变异，让我们考虑另一种情况：变量变异。

### 8.2.1 术语

首先，我们的术语选择。我们之前一直坚持使用“标识符”一词，因为我们想保留“变量”一词来研究我们即将学习的内容。在 Java 中，当我们说（假设 x 是本地绑定的，例如作为方法参数时）

> | x = 1; |
> | --- |
> | x = 3; |

我们要求改变 x 的值。在第一次赋值之后，x 的值是 1；在第二次赋值之后，它是 3。因此，在方法执行过程中，x 的值会变化。

现在，我们在数学中也使用术语“变量”来指代函数参数。例如，在\(f(y) = y+3\)中，我们说\(y\)是一个“变量”。这被称为变量，因为它在每次调用时都会变化；然而，在每次调用中，它在其作用域内具有相同的值。直到现在，我们的标识符对应于这种变量的概念。如果标识符绑定���一个盒子，那么它仍然绑定到相同的盒子值。改变的是盒子的内容，而不是标识符绑定到的盒子。相比之下，编程变量甚至在每次调用中都可能变化，就像上面的 Java x 一样。

因此，当我们指的是一个在其作用域内可以改变值的标识符时，我们将使用“变量”，而当这种情况不会发生时，我们将使用“标识符”。如果有疑问，我们可能会选择更保守的“变量”；如果区别并不重要，我们可能会两者都使用。比起纠结于这些具体术语，更重要的是理解它们代表了一个重要的区别[REF]。

### 8.2.2 语法

而其他语言会重载突变语法（=或:=），在 Racket 中它们保持不同：set!用于突变变量。这迫使 Racket 程序员面对我们在突变：结构和变量开头介绍的区别。当然，在我们的核心语言中，我们将通过使用不同的构造来避开这些语法问题，用于盒子和变量。

关于变量突变的第一件事是，尽管它也有两个子项像盒子突变（setboxC）一样，但其语法基本上是不同的。为了理解为什么，让我们回到我们的 Java 片段：

> | x = 3; |
> | --- |

在这种情况下，我们不能在 x 的位置写一个任意表达式：我们必须字面上写下标识符本身的名称。这是因为，如果它是一个表达式位置，那么我们可以对其求值，得到一个值：例如，如果 x 先前绑定到 1，这将等同于写下以下语句：

> | 1 = 3; |
> | --- |

但这当然是荒谬的！我们不能给 1 赋一个新值，而且 1 基本上就是不可变的定义。因此，我们真正想要的是找到 x 在存储中的位置，并改变那里保存的值。这里有另一种看待这个问题的方式。假设局部变量 o 绑定到某个 String 对象；让我们称这个对象为\(s\)。假设我们写下

> | o = new String("a new string"); |
> | --- |

我们是否试图改变\(s\)的任何方式？当然不是：这个语句的意图是让\(s\)保持不变。它只想改变 o 所引用的值，以便后续引用评估为这个新的字符串对象。

### 8.2.3 解释变量

我们将从语法上反映这一点：

> | (define-type ExprC |
> | --- |
> |   [numC (n : number)] |
> |   [varC (s : symbol)] |
> |   [appC (fun : ExprC) (arg : ExprC)] |
> |   [plusC (l : ExprC) (r : ExprC)] |
> |   [multC (l : ExprC) (r : ExprC)] |
> |   [lamC (arg : symbol) (body : ExprC)] |
> |   [setC (var : symbol) (arg : ExprC)] |
> |   [seqC (b1 : ExprC) (b2 : ExprC)]) |

请注意，我们已经放弃了盒子操作，但保留了序列化，因为它在突变周围很方便。重要的是，我们现在已经添加了 setC 情况，它的第一个子项不是一个表达式，而是一个变量的字面名称。我们还将 idC 重命名为 varC。因为我们已经摆脱了盒子，所以我们也可以摆脱特殊的盒子值。当您只有一种变量的变异时，您不需要新的值类型。

> | (define-type Value |
> | --- |
> |   [numV (n : number)] |
> |   [closV (arg : symbol) (body : ExprC) (env : Env)]) |

正如您可能想象的那样，为了支持变量，我们需要与我们之前看到的相同的传递存储器样式（解释盒子）），原因也是如此。不同之处在于我们如何准确地使用它。因为序列化以完全相同的方式解释（请注意，其代码不依赖于盒子与变量之间的区别），这使我们只需要处理变量突变案例。

首先，我们可以评估值表达式并获得更新后的存储器：

<setC-case>)) ::=

> | setC (var val) (type-case Result (interp val env sto) |
> | --- |
> |                   [v*s (v-val s-val) |
> |                        [<rest-of-setC-case>))])] |

现在呢？请记住，我们刚刚说过，我们不想完全评估变量，因为那只会给出它绑定的值。相反，我们想知道它对应哪个内存位置，并更新存储在该内存位置的内容；后者与突变盒子时所做的事情完全相同：

<rest-of-setC-case>)) ::=

> | (let ([where (lookup var env)]) |
> | --- |
> |   (v*s v-val |
> |        (override-store (cell where v-val) |
> |                        s-val))) |

这里我们有一个非常有趣的新模式。当我们添加了盒子时，在 idC 情况下，我们在环境中查找标识符，并立即从存储器中获取该位置的值；组合产生了一个值，就像我们在添加存储器之前一样。现在，我们有了一个新模式：在环境中查找标识符，而不随后从存储器中获取其值。只调用 lookup 的结果传统上称为 l-value，“赋值语句左边的值”。这是一种花哨的说法，“内存地址”，与存储器产生的实际值形成对比：请注意，它与类型 Value 中的任何内容都没有直接对应。

我们完成了！当我们实现传递存储器样式时，我们做了所有艰苦的工作（并且在那个应用程序中为变量分配了新位置）。

## 8.3 有状态语言操作的设计

尽管大多数编程语言包含我们研究过的一种或两种状态，但它们的引入不应被视为微不足道或不可避免的事情。一方面，状态带来了一些重要的好处：

+   状态提供了一种模块化的形式。正如我们的解释器所示，没有显式的状态操作，要实现相同的效果：

    +   我们需要添加显式参数和返回值，以传递等效的存储。

    +   这些更改必须针对所有可能涉及生产者和消费者之间通信路径的过程进行。

    因此，思考编程语言中状态的另一种方式是，它是隐式参数，已经传递给并从所有过程返回，而不会对程序员施加负担。这使得过程能够在“距离上”进行通信，而无需所有中介者都意识到通信。

+   状态使得构建动态循环数据结构成为可能，或者至少相对简单（递归和循环：过程和数据）。

+   状态为程序提供了内存，例如上面的 new-loc。如果一个过程不能自己记住事情，调用者将需要代表它执行记忆，采用存储传递的道德等效物。这不仅笨拙，还会导致调用者为自己的不良目的而干涉记忆（例如，调用者可能有意地发送回一个旧的存储，从而获得已经授予给其他方的引用，通过它可能发起正确性或安全攻击）。

另一方面，状态对程序员以及处理程序的程序（如编译器）也会产生实际成本。一个是“别名”，我们稍后会讨论 [REF]。另一个是“引用透明度”，我也希望能够回顾一下 [REF]。最后，我们已经描述了状态如何提供一种模块化形式。然而，同样的描述也可以被视为中介者不知道并且无法监视的通信后通道。在某些（特别是安全和分布式系统）环境中，这些后通道可能导致串通，因此可能非常危险和不受欢迎。

因为没有最佳答案，可能明智的做法是包括变异运算符，但要仔细划分它们。例如，在标准 ML 中，没有变量突变，因为被认为是不必要的。相反，语言具有等效的盒子（称为 refs）。可以使用盒子轻松模拟变量（例如，参见 new-loc 并考虑如何使用变量而不是盒子编写它），因此不会失去表达能力，尽管这会比仅使用变量更容易引起别名（[REF 别名]）如果盒子不小心使用。

但换取的是开发人员获得了丰富的类型：每个数据结构都被认为是不可变的，除非它包含一个 ref，并且 ref 的存在是对开发人员和程序（如编译器）的警告，即底层值可能会持续变化。因此，例如，如果 b 是一个盒子，开发人员应该意识到用 v 替换所有实例的 (unbox b)，其中 v 绑定到 (unbox b) 是不明智的：前者总是获取盒子中的当前值，而后者可能引用的是较旧的内容。（相反，如果开发人员想要在某个时间点上的值，而不关心将来对盒子的突变，他们应该确保检索和绑定它，而不是总是使用 unbox。）

## 8.4 参数传递

在我们当前的实现中，在每次函数调用时，我们都会为参数在存储中分配一个新的位置。这意味着以下程序

> | (let ([f (lambda (x) (set! x 3))]) |
> | --- |
> |   (let ([y 5]) |
> |     (begin |
> |       (f y) |
> |       y))) |

计算结果是 5，而不是 3。这是因为形式参数 x 的值保存在与实际参数 y 不同的位置，因此突变会影响 x 的位置，使 y 不受影响。

现在假设，相反地，应用程序的行为如下。当实际参数是一个变量，因此在内存中有一个位置时，它不是为值分配一个新位置，而是简单地将现有的位置传递给变量。现在形式参数引用的是实际参数的相同存储位置：即，它们是变量别名。因此，对形式参数的任何突变都会泄漏到调用上下文中；上述程序将计算为 3 而不是 5。这被称为按引用传递参数传递策略。相反，我们的解释器实现了按值传递，这是 Java 等语言遵循的相同策略。这会引起混淆，因为当值本身是可变的时，调用者会观察到调用者对值所做的更改。然而，这只是可变值的副作用，而不是调用策略的副作用。请避免这种混淆！

多年来，这种功能被认为是一个好主意。这是有用的，因为程序员可以编写像 swap 这样的抽象，它交换了调用者中两个变量的值。然而，其缺点远远超过了优点：

+   一个粗心的程序员可以在调用者中为变量创建别名，并在不知情的情况下进行修改，而调用者甚至可能不会意识到发生这种情况，直到某些模糊的条件触发它。

+   有些人认为这对效率是必要的：他们认为替代方案是复制大型数据结构。然而，按值传递与仅传递数据结构的地址兼容。只有在 (a) 数据结构是可变的，(b) 您不希望调用者能够对其进行突变，以及 (c) 语言本身没有提供不可变性注释或其他机制时，才需要进行复制。

+   它可能强制进行非统一的、因此非模块化的推理。例如，假设我们有以下过程：

    > | (定义 (f g) |
    > | --- |
    > |   (让 ([x 10]) |
    > |     (开始 |
    > |       (g x) |
    > |       ...))) |

    如果语言允许按引用传递参数，那么程序员无法从上述代码中局部地—<wbr>即，仅仅从上面的代码—<wbr>确定省略号中 x 的值。

至少，如果语言允许按引用传递参数，那么它应该让调用者确定是否传递引用—<wbr>即，让被调用方分享调用方变量的内存地址—<wbr>或不传递。然而，即使有这个选项，也并不像听起来那么吸引人，因为现在被调用方面临着对称的问题，不知道它的参数是否别名。在传统的、顺序执行的程序中，这不是很令人担心，但如果过程是可重入的，被调用方将面临完全相同的困境。

因此，我们应该考虑在某个时候是否值得费这么大的劲。相反，希望被调用方执行变异的调用方可以简单地向被调用方发送一个装箱值。该箱子表示调用方接受—<wbr>甚至邀请—<wbr>被调用方执行变异，并且在完成后，调用方可以提取该值。这确实消除了编写一个简单的交换程序的能力，但这是为了真正的软件工程问题所付出的小代价。

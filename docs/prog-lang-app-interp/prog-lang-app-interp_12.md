# 12 表示决策

回头再看看我们对函数作为值的解释器[REF]。你是否发现了一些奇怪的不一致之处？

现在就做！

> 不，真的，做吧。你会吗？

考虑我们选择如何表示我们两种不同类型的值：数字和函数。忽略表面的 numV 和 closV 包装，关注底层数据表示。我们将解释语言的数字表示为 Racket 数字，但我们没有将解释语言的函数（闭包）表示为 Racket 函数（闭包）。

这就是我们的不一致性。使用 Racket 的表示形式来表示两者更加一致，或者干脆两者都不使用 Racket 的表示形式会更加一致。那么为什么我们做出了这个特定的选择呢？

我们试图阐明和指出，而这一点就是我们现在要探讨的。

## 12.1 改变表示

让我们暂时探讨一下数字。Racket 的数字是一个很好的重用目标，因为它们非常强大：我们可以得到任意大小的整数（大整数），有理数（受益于整数的大整数表示），复数等等。因此，它们可以表示大多数普通编程语言的数字系统。然而，这并不意味着它们就是我们想要的：它们可能太少或太多。

+   如果我们想要一个更受限制的数字系统，这些就太多了。例如，Java 规定了一个非常具体的固定大小表示集合（例如，int 被指定为 32 位）。超出这些集合范围的数字不能直接表示为数字，算术运算必须遵守这些集合（例如，溢出，使得将 1 加到 2147483647 不会产生 2147483648）。

+   如果我们想要更丰富的数字，无论是四元数还是带有相关概率的数字，它们就太少了。

更糟糕的是，我们甚至没有停下来问自己我们想要什么，而是轻率地继续使用 Racket 数字。

我们这样做的原因是因为我们并不真正关心数字的研究；相反，我们对函数作为值等编程语言特性感兴趣。然而，作为语言设计者，你应该确保提出这些艰难的问题。

现在让我们谈谈我们对闭包的表示。我们本可以通过利用 Racket 的相应概念来表示闭包，相应地，使用 Racket 应用来表示函数应用。

现在就做！

> 用代表函数作为值的 Racket 函数替换闭包数据结构。

准备好了：

> | (define-type Value |
> | --- |
> |   [numV (n : number)] |
> |   [closV (f : (Value -> Value))]) |
> |   |
> | (define (interp [expr : ExprC] [env : Env]) : Value |
> |   (type-case ExprC expr |
> |     [numC (n) (numV n)] |
> |     [idC (n) (lookup n env)] |
> |     [appC (f a) (local ([define f-value (interp f env)] |
> |                         [define a-value (interp a env)]) |
> |                   ((closV-f f-value) a-value))] |
> |     [plusC (l r) (num+ (interp l env) (interp r env))] |
> |     [multC (l r) (num* (interp l env) (interp r env))] |
> |     [lamC (a b) (closV (lambda (arg-val) |
> |                          (interp b |
> |                                  (extend-env (bind a arg-val) |
> |                                              env))))])) |

练习

> 注意一个奇怪的变化。在我们之前的实现中，环境在 appC 情况下被扩展。在这里，它在 lamC 情况下被扩展。其中一个是错误的吗？如果不是，为什么会发生这种变化？

这确实很简洁，但我们失去了非常重要的东西：理解。说源语言函数对应于 lambda 几乎告诉我们什么都没有：如果我们已经准确知道 lambda 做什么，我们可能不会学习它，如果我们不知道，这种映射将完全教会我们什么都不知道（实际上，可能会在我们的无知之上增加混乱）。出于同样的原因，我们没有使用 Racket 的状态来理解有状态操作符的各种变体[参考]。

一旦我们理解了这个特性，我们应该感到可以将其用作表示。事实上，这样做可能会产生更简洁的解释器，因为我们不是手动做所有事情。事实上，一些后续的解释器[参考]如果我们没有利用这些更丰富的表示，将变得几乎无法阅读。这有点像说，“现在我们理解了递增一的加法，我们可以使用加法来定义乘法：我们不必只使用递增一来定义它。”然而，利用宿主语言特性存在危险，我们应该加以防范。

## 12.2 错误

当程序出错时，程序员需要仔细呈现错误。使用宿主语言特性会导致用户看到宿主语言错误的风险，而他们将无法理解。因此，我们必须仔细地将错误条件转化为我们语言的用户能理解的术语，而不让宿主语言“泄漏出来”。

更糟糕的是，应该出错的程序可能不会出错！例如，假设我们决定函数只能出现在顶层位置。如果我们未明确检查这一点，将宏展开为更宽松的 lambda 可能会导致解释器产生应该出错而未出错的答案。因此，我们必须非常小心，只允许预期的表面语言映射到宿主语言。

举个例子，考虑不同的变异操作。在我们的语言中，尝试变异未绑定的变量会产生错误。在一些语言中，这样做会导致变量被定义。未明确确定我们的预期语义是常见的语言设计错误，而是说，“它是实现所做的任何事情”。这种态度(a)��惰和马虎，(b)可能会产生意想不到的负面后果，(c)使您难以将您的语言从一个实现平台移动到另一个。永远不要犯这个错误！

## 12.3 意义的改变

将函数作为值映射到 lambda 的工作特别适用，因为我们打算让这两者具有相同的含义。然而，这使得更改函数的含义变得困难。让我举个例子：假设我们希望我们的语言实现动态作用域。请不要让这超出假设阶段。在我们最初的解释器中，这很容易（几乎太容易了，正如历史所显示的那样）。但是尝试使使用 lambda 的解释器实现动态作用域。将急切求值映射到具有惰性应用的语言中可能同样困难或至少微妙[REF]。

练习

> 将上述解释器转换为使用动态作用域。

重点是，原始数据结构表示并不特别简单，但通常也不会妨碍。相比之下，映射到主机语言特性可以使一些意图——<wbr>主要是与主机语言已经做的事情匹配的那些！——<wbr>特别容易，而其他一些则可能微妙或困难。还有一个额外的危险，我们可能不确定主机语言的特性是什么（例如，它的“lambda”是否实际实现了静态作用域？）。

结论是，这是一个很好的特性，只有当我们想要“穿透”基础语言的含义时才能利用它——<wbr>-这样做尤其明智，因为它确保我们不会意外改变其含义。然而，如果我们想要利用基础语言的一个重要部分并仅增强其含义，也许其他实现策略[REF]会起到同样好的作用，而不是编写一个解释器。

## 12.4 另一个例子

让我们考虑另一个表示更改。什么是环境？

环境是从名称到值（或位置，一旦我们有了变异）的映射。我们选择通过数据结构实现映射，但是...我们有另一种表示映射的方式吗？当然可以用函数！因此，环境是一个函数，它以名称作为参数并返回其绑定的值（或错误）：

> | (define-type-alias Env (symbol -> Value)) |
> | --- |

什么是空环境？无论您尝试查找什么名称，它都会返回错误：

> | (define (mt-env [name : symbol]) |
> | --- |
> |   (error 'lookup "name not found")) |

（原则上，我们应该在返回值上放置一个类型注释，它应该是 Value，除非当然这是空洞的。）通过绑定扩展环境会创建一个函数，它接受一个名称并检查它是否是刚刚扩展的名称；如果是，则返回相应的值，否则将其传递给被扩展的环境：

> | (define (extend-env [b : Binding] [e : Env]) |
> | --- |
> |   (lambda ([name : symbol]) : Value |
> |     (if (symbol=? name (bind-name b)) |
> |         (bind-val b) |
> |         (lookup name e)))) |

最后，我们如何在环境中查找名称？我们只需应用环境！

> | (define (lookup [n : symbol] [e : Env]) : Value |
> | --- |
> |   (e n)) |

至此，我们完成了！

# 16 检查程序不变量的动态性：合同

|     16.1 合同作为谓词) |
| --- |
|     16.2 标签、类型和对值的观察) |
|     16.3 高阶合同) |
|     16.4 语法便利) |
|     16.5 扩展到复合数据结构) |
|     16.6 更多关于合同和观察) |
|     16.7 合同和突变) |
|     16.8 合并合同) |
|     16.9 责备) |

类型系统提供了丰富而有价值的方法来表示程序不变量。然而，它们也代表着一个重要的权衡，因为并非所有程序的非平凡属性都可以静态验证，这是一个正式的属性，被称为[Rice's Theorem](http://en.wikipedia.org/wiki/Rice's_theorem)。此外，即使我们可以设计一种方法来静态解决某个属性，注释和计算复杂性的负担可能过重。因此，我们关心的一些属性不可避免地必须被忽略或仅在运行时解决。在这里，我们将讨论运行时执行。

几乎每种编程语言都有一种断言机制，使程序员能够编写比语言的静态类型系统允许的更丰富的属性。在没有静态类型的语言中，这些属性可能从简单的类似类型的断言开始：例如，一个参数是否是数字。然而，断言的语言通常是整个编程语言，因此任何谓词都可以用作断言：例如，加密包的实现可能希望确保某些参数通过素数测试，或者平衡的二叉搜索树可能希望确保其子树确实是平衡的并保留搜索树的顺序。

## 16.1 合同作为谓词

因此，很容易看出如何实现简单的合同。在接下来的内容中，我们将使用语言 #lang plai，有两个原因。首先，这更好地模拟了在无类型语言中编程。其次，为了简单起见，我们将将类型样式的断言写成合同，但在有类型的语言中，这些将被类型检查器本身标记，不让我们看到运行时行为。实际上，关闭类型检查器更容易。然而，合同即使在有类型的世界中也是有意义的，因为它们增强了程序员可以表达的不变性集合。合同体现了一个谓词。它消耗一个值并将谓词应用于该值。如果值通过了谓词，合同将返回该值；如果值失败，合同将报告一个错误。它的唯一行为是返回提供的值或报错：它不应以任何方式改变值。简而言之，在通过谓词的值上，合同本身就像是一个恒等函数。

我们可以在以下函数中编码这个本质：

> | (define (make-contract pred?) |
> | --- |
> |   (lambda (val) |
> |     (if (pred? val) val (blame "violation")))) |
> |   |
> | (define (blame s) (error 'contract "~a" s)) |

这里有一个示例合同：

> | (define non-neg?-contract |
> | --- |
> |   (make-contract |
> |    (lambda (n) (and (number? n) |
> |                     (>= n 0))))) |

（在一个有类型的语言中，number? 检查当然是不必要的，因为它可以被编码—<wbr>并静态检查！—<wbr>在使用合同的函数类型中。）假设我们想确保在计算平方根时不会得到虚数；我们可能会写

> | (define (real-sqrt-1 x) |
> | --- |
> |   (sqrt (non-neg?-contract x))) |

在许多语言中，断言是作为语句而不是表达式编写的，因此另一种编写方式是：

> | (define (real-sqrt-2 x) |
> | --- |
> |   (begin |
> |     (non-neg?-contract x) |
> |     (sqrt x))) |

（在某些情况下，这种形式更清晰，因为它在函数的开头清晰地说明了参数的期望。它还使得参数只需检查一次。实际上，在某些语言中，合同可以直接写在函数头部，从而提高接口中给定的信息。）现在如果将 real-sqrt-1 或 real-sqrt-2 应用于 4，它们会产生 2，但如果应用于 -1，它们会引发合同违规错误。

## 16.2 标签、类型和值的观察

到目前为止，我们已经在大多数语言中复制了断言系统的本质。还有什么要说的？让我们假设一下，我们的语言不是静态类型的。那么我们将希望编写至少复制传统类型样式不变性的断言，如果可能的话更多。上面的 make-contract 可以捕捉所有标准类型样式的属性，比如检查数字、字符串等，假设适当的谓词要么由语言提供，要么可以从给定的谓词中制作。或者可以吗？

请记住，即使是我们最简单的类型语言也不仅仅有基本类型，比如数字，还有构造类型。虽然其中一些，比如列表和向量，看起来似乎并不是很具有挑战性，但是一旦我们关心变异、性能和责任，它们就会变得复杂，我们将在下面讨论这些问题。然而，函数立即成为问题。

作为一个工作示例，我们将采用以下函数：

> | (define d/dx |
> | --- |
> |   (lambda (f) |
> |     (lambda (x) |
> |       (/ (- (f (+ x 0.001)) |
> |             (f x)) |
> |          0.001)))) |

静态地，我们会给这个类型

> | ((number -> number) -> (number -> number)) |
> | --- |

（它接受一个函数，并产生其导数—<wbr>另一个函数）。假设我们想要用合同保护这个函数。

根本问题在于，在大多数语言中，我们无法直接将其表达为谓词。大多数语言运行时系统对值的类型存储的信息非常有限—<wbr>如此有限，以至于相对于我们迄今为止看到的类型，我们应该使用不同的名称来描述这些信息；传统上它们被称为标签。有一些努力通过从源程序到汇编语言的更低层抽象来保留丰富的类型信息，但这些都是研究工作。有时标签与我们可能认为的类型相符：例如，一个数字将具有标识它为数字的标签（甚至可能是特定类型的数字），一个字符串将具有标识它为字符串的标签，依此类推。因此，我们可以根据这些标签的值编写谓词。

然而，当我们涉及结构化值时，情况就更加复杂了。一个向量会有一个声明它是向量的标签，但不会规定其元素是什么类型的值（它们甚至可能不全是同一种类型）；然而，程序通常也可以获取其大小，从而遍历它，以收集这些信息。（然而，关于结构化值还有更多内容要讨论[REF]。）

现在就做！

> 编写一个检查列表是否完全由偶数组成的合同。

这里是：

> | (define list-of-even?-contract |
> | --- |
> |   (make-contract |
> |    (lambda (l) |
> |      (and (list? l) (andmap number? l) (andmap even? l))))) |

（再次注意，如果我们静态地知道我们有一个数字列表，那么前两个问题就不需要问了。同样，一个对象可能只是将自己标识为一个对象，而不提供额外的信息。但是在允许反射对象结构的语言中，合同仍然可以收集所需的信息。）

然而，在每种语言中，当我们遇到函数时，这变得棘手。我们可能认为函数有一个针对其定义域和值域的类型，但对于运行时系统而言，函数只是一个带有函数标签的不透明对象，也许还带有一些非常有限的元数据（例如函数的元数）。运行时系统几乎无法判断函数是否消耗和产生函数，<wbr>而不是其他类型的值，<wbr>更不用说它是否消耗和产生（number -> number）类型的函数了。

这个问题在 JavaScript 中的（错误命名的）typeof 操作符中得到了很好的体现。对于基本类型（如数字和字符串）的值，typeof 返回一个对应的字符串（例如，"number"）。对于对象，它返回"object"。最重要的是，对于函数，它返回"function"，没有其他附加信息。因此，也许 typeof 是这个操作符的一个糟糕的名称。它应该被称为 tagof，留下了 JavaScript 未来的静态类型系统可以提供真正的 typeof 的可能性。

总结一下，这意味着在面对一个函数时，函数契约只能检查它确实是一个函数（如果不是，那显然是一个错误）。它不能检查函数的定义域和值域。我们应该放弃吗？

## 16.3 高阶契约

要确定该做什么，最好回顾一下契约首先提供了什么样的保证。在上面的 real-sqrt-1 中，我们要求参数是非负的。然而，这仅在实际使用 real-sqrt-1 时进行检查，然后仅对传递给它的实际值进行检查。例如，如果程序包含以下片段

> | (lambda () (real-sqrt-1 -1)) |
> | --- |

但是如果这个惰性求值永远不被调用，程序员就永远看不到这个契约违规。事实上，也许在程序的这次运行中不会调用这个惰性求值，但在后续的运行中会调用它；因此，程序存在潜在的契约错误。出于这个原因，最好通过静态类型来表达不变式；但是当我们使用契约时，我们了解到，只有当程序被适当地运行时，我们才会收到错误通知。

这是一个有用的见解，因为它提供了解决函数问题的方法。我们立即检查所谓的函数值确实是一个函数。然而，我们没有忽视定义域和值域契约，而是推迟了它们。当（每次）函数实际应用于一个值时，我们检查定义域契约，并且当函数实际返回一个值时，我们检查值域契约。

这显然是与 make-contract 的不同模式。因此，我们应该给 make-contract 一个更具描述性的名称：它检查立即合同（即，现在可以完全检查的合同）。在 Racket 合同系统中，立即合同称为 flat。这个术语有点误导，因为它们也可以保护数据结构。

> | (define (immediate pred?) |
> | --- |
> |   (lambda (val) |
> |     (if (pred? val) val (blame val)))) |

相反，函数合同接受两个合同作为参数——表示要在定义域和值域上进行检查——并返回一个谓词。这是应用于声称满足该合同的值的谓词。首先，这检查给定值实际上是一个函数：这部分仍然是立即的。然后，我们创建一个替代者过程，应用“剩余”合同——检查定义域和值域——但在其他方面行为与原始函数相同。

创建这样一个替代者代表了与传统断言机制的分离，后者简单地检查值，然后将其保持不变。相反，对于函数，如果我们想要合同检查，我们必须使用创建的替代者。因此，一般来说，有一个消耗合同和值，并创建该值的受保护版本的包装器是有用的：

> | (define (guard ctc val) (ctc val)) |
> | --- |

作为一个非常简单的例子，让我们假设我们想要在数字合同中包装 add1 函数（其中函数是函数合同的构造函数，稍后将定义）：

> | (define a1 (guard (function (immediate number?) |
> | --- |
> |                             (immediate number?)) |
> |                   add1)) |

我们希望 a1 被绑定到基本上以下代码：

> | (define a1 |
> | --- |
> |   (lambda (x) |
> |     (num?-con (add1 (num?-con x))))) |

这里，(lambda (x) ...) 是替代者；它在调用 add1 周围应用了两个数字合同。请记住，合同在没有违规行为时必须像恒等函数一样运行，因此在未违反使用时，此过程与非违反使用的 add1 完全相同。为了实现这一点，我们使用以下函数定义。为了简单起见，我们在这里假设单参数函数，但对于多个参数的扩展是直接的。事实上，更复杂的合同甚至可以检查参数之间的关系。请记住，我们还必须确保给定的值确实是一个函数（就像上面的 add1 确实是的，而且可以立即检查，这就是为什么在将替代者绑定到 a1 时检查已经消失的原因）：

> | (define (function dom rng) |
> | --- |
> |   (lambda (val) |
> |     (if (procedure? val) |
> |         (lambda (x) (rng (val (dom x)))) |
> |         (blame val)))) |

要理解这是如何工作的，让我们替换参数。为了保持结果代码的可读性，我们将首先构造 number?合同检查器并给它一个名字：

> |   (define num?-con (immediate number?)) |
> | --- |
> | = (define num?-con |
> |     (lambda (val) |
> |       (如果（number? val）val (blame val)))) |

现在让我们回到 a1 的定义。首先我们应用保护：

> | (define a1 |
> | --- |
> |   ((function num?-con num?-con) |
> |    add1)) |

现在我们应用函数合同构造器：

> | (define a1 |
> | --- |
> |   ((lambda (val) |
> |      (if (procedure? val) |
> |          (lambda (x) (num?-con (val (num?-con x)))) |
> |          (blame val))) |
> |    add1)) |

应用左-左-λ得：

> | (define a1 |
> | --- |
> |   (if (procedure? add1) |
> |       (lambda (x) (num?-con (add1 (num?-con x)))) |
> |       (blame add1))) |

请注意，这立即检查受保护的值是否确实是一个函数。因此我们得到

> | (define a1 |
> | --- |
> |   (lambda (x) |
> |     (num?-con (add1 (num?-con x))))) |

这恰好是我们想要的替代品，具有对非违规执行的 add1 行为。现在做吧！

> 有多少种方式违反上述 add1 合同？

有三种方式，对应三种合同构造器：

1.  包装的值可能不是一个函数；

1.  包装的值可能是一个应用于非数字值的函数；或者，

1.  包装的值可能是一个接受数字但产生非数字类型值的函数。

练习

> 编写执行这三种违规行为的示例，并观察合同系统的行为。您能改进错误消息以更好地区分这些情况吗？

相同的封装技术也适用于 d/dx：

> | (define d/dx |
> | --- |
> |   (guard (function (function (immediate number?) (immediate number?)) |
> |                    (function (immediate number?) (immediate number?))) |
> |          (lambda (f) |
> |            (lambda (x) |
> |              (/ (- (f (+ x 0.001)) |
> |                    (f x)) |
> |                 0.001))))) |

练习

> 有七种违反这个合同的方式，对应七个合同构造器。通过传递参数或修改代码来违反它们中的每一个。您能改进错误报告以正确识别每种违规吗？

请注意，嵌套的函数合同延迟对两个应用的即时合同的检查，而不是一个。这是我们应该期望的，因为即时合同只报告实际值的问题，所以它们在应用到实际值之前无法报告任何问题。然而，这确实意味着“违反”的概念是微妙的：传递给 d/dx 的函数值实际上可能确实违反了合同，但是直到传递或返回数值才会观察到这种违反。

## 16.4 语法便利

早些时候我们看到了两种使用平面合约的风格，如 real-sqrt-1 和 real-sqrt-2 所体现的那样。这两种风格都有缺点。后者，让人想起传统的断言系统，简单地不能用于高阶值，因为计算必须使用包装后的值。(毫不奇怪，传统的断言系统只处理即时合同，所以它们未能注意到这种微妙之处。)在前者的风格中，我们将每个使用都用合约包装起来，在理论上是可行的，但存在三个缺点：

1.  开发人员可能会忘记包装一些用法。

1.  每次使用都会检查合约，当有多个使用时会浪费资源。

1.  程序将合同检查与其功能行为混合在一起，降低了可读性。

幸运的是，在常见情况下，适度使用语法糖可以解决这个问题。例如，假设我们想要方便地将合同附加到函数参数上，这样开发人员可以编写

> | (define/contract (real-sqrt (x :: (immediate positive?))) |
> | --- |
> |   (sqrt x)) |

以保护 x 为 positive?，但只在函数调用时执行检查。这应该转换为，比如说，

> | (define (real-sqrt new-x) |
> | --- |
> |   (let ([x (guard (immediate positive?) new-x)]) |
> |     (sqrt x))) |

也就是说，该宏为每个标识符生成一个新的名称，然后将用户给定的名称与提供给该新名称的值的包装版本关联起来。以下宏完全实现了这一点：

> | (define-syntax (define/contract stx) |
> | --- |
> |   (syntax-case stx (::) |
> |     [(_ (f (id :: c) ...) b) |
> |      (with-syntax ([(new-id ...) (generate-temporaries #'(id ...))]) |
> |        #'(define f |
> |            (lambda (new-id ...) |
> |              (let ([id (guard c new-id)] |
> |                    ...) |
> |                b))))])) |

借助诸如此类的便利，合同语言的设计者可以提高合同使用的可读性、效率和健壮性。

## 扩展到复合数据结构

正如我们已经讨论过的，扩展合同到结构化数据类型，如列表、向量和用户定义的递归数据类型，似乎很容易。这只需要确保适当的运行时观察可用即可。这通常是可能的，直到语言中的类型解析。例如，正如我们已经讨论过的[REF]，一种带有数据类型的语言不需要类型谓词，但仍将提供谓词来区分变体；这是一种情况，其中类型级别的“合同”检查最好（甚至必须）留给静态类型系统，而合同则断言更精细的结构性质。

然而，这种策略可能会遇到重大的性能问题。例如，假设我们构建了一个平衡二叉搜索树，以执行对数时间（相对于树的大小）的插入和查找。现在假设我们已经将这棵树包装在了一个合适的合同中。遗憾的是，仅仅检查合同的行为会访问整棵树，从而花费线性时间！因此，理想情况下，我们更希望一种策略，即在构建时已经增量地检查合同，并且在查找时不需要再次检查。

更糟糕的是，平衡和搜索树排序都是递归属性。原则上，它们附加到每个子树上，因此应该在每个递归调用上应用。在插入期间，这是一个递归过程，合同将在每个访问的子树上进行检查。在大小为\(t\)的树中，合同谓词适用于\(t \over 2\)个元素的子树，然后适用于\(t \over 4\)个元素的子子树，依此类推，导致在最坏情况下访问总共\(t \over 2\) + \(t \over 4\) + \(\cdots\) + \(t \over t\)个元素...使得我们旨在实现对数时间插入过程花费线性时间。

在这两种情况下，很多情况下都有现成的缓解方法可供使用。每个值都需要与其已经通过的一系列合同相关联（可以是固有的，也可以通过存储在哈希表中）。然后，当一个合同准备应用时，它首先检查该值是否已经被检查过，如果已经检查过，则不再重复检查。这本质上是合同检查的一种记忆化形式，因此可以减少检查的算法复杂度。同样地，就像记忆化一样，当值是不可变的时候，这种方法效果最好。如果值可以变化，并且合同执行任意计算，则执行此优化可能不安全。

我们可以以更微妙的方式来考虑数据结构的问题。例如，考虑我们之前编写的合同，用于检查数字列表中的所有值是否都是偶数。假设我们已经将列表包装在此合同中，但只对列表的第一个元素感兴趣。自然而然地，我们要付出检查列表中所有值的成本，这可能需要很长时间。然而，更重要的是，用户可能会认为报告列表第二个元素的违规行为本身就违反了我们对合同检查的期望，因为我们实际上并没有使用该元素。

这表明，甚至可以推迟对一些可以立即检查的值的检查。例如，整个列表可以转换为一个包含延迟检查的封装值，并且只有在访问时才检查每个值。这种策略可能很吸引人，但编码起来并不是微不足道的，并且尤其在存在别名时会遇到问题：如果两个不同的标识符引用相同的列表，一个带有合约保护，另一个没有，我们必须确保它们都按预期工作（这通常意味着我们不能在列表本身存储任何可变状态）。

## 16.6 更多关于合约和观察

对于任何合约实现来说，一个普遍的问题——这在处理复杂数据时变得更加严重——是一个耐人寻味的问题。早些时候，我们抱怨检查函数合约很困难，因为我们缺乏足够的观察能力：我们只能检查一个值是否是一个函数，仅此而已。而在实际的语言中，对于数据结构的问题实际上恰恰相反：我们有太多的观察能力。例如，如果我们实现了一个推迟检查列表的策略，我们很可能需要使用一个结构来保存实际的列表，并修改 first 和 rest 以通过这个结构获取它们的值（在检查合约之后）。然而，像 list?这样的过程现在可能返回 false 而不是 true，因为结构不是列表；因此，list?需要重新绑定到一个过程，该过程在表示这些特殊的延迟合约列表的结构上也返回 true。但合约系统的作者还需要记住解决 cons?、pair?以及其他许多执行观察的过程。

一般来说，一个观察基本上是不可能“修复”的：eq?。通常，我们具有每个值都与自己 eq?的属性，即使对于函数也是如此。然而，函数的包装值是一个新的过程，它不仅不等于自身，而且可能不应该等于自身，因为其行为确实是不同的（尽管只在合约违规时，且只在足够的值被提供以观察到违规之后）。然而，这意味着程序不能偷偷地保护自己，因为保护的行为是可观察到的。因此，一个恶意的模块有时可以检测到是否传递了受保护的值，只有在没有传递时才表现异常！

## 16.7 合约和变异

我们应该对合约和突变之间的相互作用感到担忧，尤其是当我们的合约要么本质上是推迟的，要么以推迟的方式实现时。有两件事需要担心。一是将受合约保护的值存储在可变状态中。另一个是为可变状态编写合约。

当我们存储一个被约定的值时，包装策略确保了合同检查的顺利进行。在每个阶段，合同会尽可能地检查手头上的值，并创建一个包含剩余检查的包装值。因此，即使这个包装值存储在可变状态中并在以后被检索以供使用，它仍然包含这些检查，并且当值最终被使用时，这些检查将被执行。

另一个问题是为可变数据编写合同，例如框和向量。在这种情况下，我们可能必须为整个数据类型创建一个记录预期合同的包装器。然后，当数据类型内的一个值被替换为一个新值时，执行更新的操作—<wbr>例如 set-box!—<wbr>需要从包装器中检索预期的合同，将其应用于值，并存储包装的值。因此，这需要改变数据结构变异操作符的行为，以使其对约定值敏感。然而，变异并不改变违规被捕获的时机：立即合同立即被捕获，延迟合同在适当（不适当）使用时被捕获。

## 16.8 合并合同

现在我们已经讨论了所有基本数据类型的组合器，自然而然地，我们应该讨论如何组合合同。正如我们在类型中看到的联合[REF]和交集[REF]一样，我们应该考虑联合和交集（分别是“或”和“与”）；此外，我们还可以考虑否定。然而，合同只是表面上类似于类型，因此我们必须根据合同的实际情况考虑这些问题，而不是试图将我们从类型中学到的含义映射到合同的领域。

一如既往，立即情况是很简单的。联合合同与析取组合—<wbr>实际上，作为谓词，它们的结果可以直接与或组合—<wbr>和交集合同与合取组合。我们依次应用谓词，进行短路，然后生成错误或返回约定值。交集合同与合取（与）。否定合同只是将原始的立即合同应用并将决定否定（用 not）。

在延迟、高阶情况下，合并合同要困难得多。例如，考虑将函数合同从数字到数字的否定。究竟什么意思？它是否意味着函数不应该接受数字？还是说如果接受了数字，就不应该产生它们？还是两者兼而有之？特别是，我们如何执行这样的合同？例如，我们如何检查一个函数不接受数字——我们期望当给定一个数字时，它会产生一个错误吗？但现在考虑一下用这样一个合同包裹的恒等函数；因为显然当给定一个数字（或者任何其他值）时它不会产生错误，这是否意味着我们应该等到它产生一个值，如果它确实产生一个数字，我们就拒绝它？但最糟糕的是，请注意，这意味着我们将在其未定义的域上运行函数：这是摧毁程序不变量、污染堆或使程序崩溃的一种确定方法。

交集合同要求值通过所有的子合同。这意味着将高阶值重新包装成一些检查所有域子合同以及所有范围子合同的东西。未能满足一个子合同甚至意味着该值已经失败了整个交集。

联合合同更加微妙，因为不满足任何一个子合同并不意味着可以拒绝。相反，它只意味着那个子合同不再是代表包装值的候选合同；其他子合同可能仍然是候选合同，并且只有当没有其他合同时才必须拒绝该值。这意味着联合合同的实现必须保持哪些子合同已经通过和尚未通过的记忆——在这种情况下，记忆是使用突变的一种复杂术语。在像 Racket 这样的多线程语言中，这还需要锁定以避免竞争条件。当每个子合同失败时，它都会从候选列表中移除，而所有剩余的子合同仍然继续应用。当没有候选合同时，合同系统必须报告一个违规。错误报告可能会提供消除每个子合同的每个部分的实际值（请记住，这些值可能会嵌套多个函数深）。

在 Racket 中的合同构造器和组合器的实现版本对可接受的子合同形式施加了限制。这些限制使得实现既高效又能产生有用的错误消息。此外，上述更极端的情况在实践中很少发生——虽然现在你知道如果需要的话如何实现它们。

## 16.9 责备

现在让我们回到报告合同违规的问题上。我指的不是要打印什么字符串，而是更重要的问题，即要报告什么，正如我们即将看到的那样，这实际上是一个语义上的考虑。

为了说明问题，回想一下我们上面对 d/dx 的定义，并假设我们在没有任何合同检查的情况下运行它。现在假设我们将这个函数应用于完全不恰当的 string-append（既不消耗也不产生数字）。这只会产生一个值：

| > (define d/dx-sa (d/dx string-append)) |
| --- |

（注意，即使开启了合同检查，这也会成功，因为函数合同的即时部分认识到 string-append 是一个函数。）现在假设我们将 d/dx-sa 应用于一个数字，正如我们应该能够做的那样：

| > (d/dx-sa 10) |
| --- |
| string-append: 合同违规 |
|   期望: 字符串？ |
|   给定: 10.001 |

请注意，错误报告深入到了 d/dx 的主体内部。一方面，这是完全合理的：这就是错误地应用 string-append 的地方。然而，错误并不是 d/dx 的错——<wbr>相反，是那些将 string-append 作为一个从数字到数字的合法函数提供给它的代码的错。然而，那么做的代码早已逃离现场；它不再在栈上，并且因此不在传统错误报告机制的范围之内。

这个问题并不是 d/dx 的特殊情况；事实上，它经常在大型系统中发生。这是因为系统，特别是带有图形、网络和其他外部接口的系统，大量使用回调：注册对某个实体感兴趣并被调用以信号某种状态或值的函数（或方法）。（在这里，d/dx 是图形层的道德等价物，而 string-append 是提供给它的回调（并由它存储的回调）。）最终，系统层调用回调。如果这导致错误，那么系统层——<wbr>给定一个据称是正确合同的回调——<wbr>以及回调本身的错误都不是，后者可能具有合法用途，但被错误地提供给了函数。相反，错在引入这两个实体的实体。然而，在这一点上，调用堆栈只包含回调（顶部）和系统（其下）——<wbr>而唯一的有罪者已经不在场了。因此，这种错误可能极其难以调试。

解决方案是将合同系统扩展到包含责任的概念。思路是有效记录导致一对组件相遇的介绍，这样，如果它们之间发生合同违规，我们就可以归因于执行介绍的表达式的失败。注意，这只在函数的上下文中才真正有趣，但为了一致性，我们将自然地将责任扩展到即时合同中。

对于函数而言，注意到有两种可能的失败点：要么它被给了错误类型的值（前置条件），要么它产生了错误类型的值（后置条件）。区分这两种情况很重要，因为在前一种情况下，我们应该责备环境——<wbr>特别是，实际参数表达式——<wbr>而在后一种情况下（假设参数已经通过了审查），我们应该责备函数本身。（对于即时值的自然扩展是，我们只能责备值本身不满足合同，这类似于“后置条件”。）

对于合同，我们将引入术语正位置和负位置。对于一阶函数，负位置是前置条件，正位置是后置条件。因此，这可能看起来是多余的额外术语。然而，正如我们很快将看到的，这些术语具有更一般的含义。

现在我们将一般化合同消耗的参数。之前，即时合同消耗谓词，函数合同消耗域和范围合同。这仍然是这样。然而，它们各自返回的内容将是两个参数的函数：正位置和负位置的标签。（这些标签可以来自任何合理的数据类型：抽象语法节点、缓冲区偏移或其他描述。为简单起见，我们将使用字符串。）因此，函数合同将封闭于这些程序位置的标签，以后指责无效函数的提供者。

现在，保护函数负责通过合同应用位置的标签：

> | (define (guard ctc val pos neg) ((ctc pos neg) val)) |
> | --- |

让我们还让责备显示适当的标签（我们将从合同实现中传递给它）：

> | (define (blame s) (error 'contract s)) |
> | --- |

假设我们像以前一样保护 add1 的使用。对于正位置和负位置来说，有哪些有用的名称呢？正位置是后置条件：即，在这里的任何失败都必须归咎于 add1 的主体。负位置是前置条件：即，在这里的任何失败都必须归咎于 add1 的参数。因此：

> | (define a1 (guard (function （即时数？） |
> | --- |
> |                             （即时数？） |
> |                   add1 |
> |                   "add1 body" |
> |                   "add1 input")) |

如果我们给 guard 提供了一个非函数，我们期望在“后条件”位置出现错误：这实际上不是后条件的失败，但是如果应用程序未能成为函数，那么参数肯定无法受到责备。（但是，这表明我们确实在非常伸展术语“后条件”，而术语“正面”提供了一个有用的替代方案。）因为我们相信 add1 的实现只会产生数字，所以我们期望不可能违反后条件。但是，我们期望像 (a1 "x") 这样的表达式触发前条件错误，可能在 "add1 input" 位置发出契约错误的信号。相反，如果我们保护一个违反后条件的函数，比如这样一个函数，

> | (define bad-a1 (guard (function (immediate number?) |
> | --- |
> |                             (immediate number?)) |
> |                   number->string |
> |                                       "bad-add1 body" |
> |                   "bad-add1 input")) |

我们期望责备归咎于 "bad-add1 body"。现在让我们看看如何实现这些契约构造函数。对于即时契约，我们已经看到责备应该归咎于正位置：

> | (define (immediate pred?) |
> | --- |
> |  (lambda (pos neg) |
> |    (lambda (val) |
> |       (if (pred? val) val (blame pos))))) |

对于函数，我们可能会尝试写

> | (define (function dom rng) |
> | --- |
> |  (lambda (pos neg) |
> |         (lambda (val) |
> |       (if (procedure? val) |
> |           (lambda (x) (dom (val (rng x)))) |
> |           (blame pos))))) |

但是这种方法在非常根本的方式上失败了：它违反了契约的预期签名。这是因为现在所有的契约都期望被给予正负位置的标签，这意味着 dom 和 rng 不能像上面那样使用。（另一个提示是，尽管我们已经看到了期望位置被责备的例子，但在正文中我们并未使用 pos 而不是 neg。）相反，显然，我们以某种方式实例化域和值域契约，使用 pos 和 neg，以便它们“知道”和“记住”潜在违规的函数是在哪里应用的。最明显的反应将是使用相同的 dom 和 rng 值来实例化这些契约构造函数：

> | (define (function dom rng) |
> | --- |
> |   (lambda (pos neg) |
> |     (let ([dom-c (dom pos neg)] |
> |           [rng-c (rng pos neg)]) |
> |       (lambda (val) |
> |               (if (procedure? val) |
> |             (lambda (x) (rng-c (val (dom-c x)))) |
> |             (blame pos)))))) |

现在所有的签名都匹配起来了，我们可以运行我们的契约。但是当我们这样做时，答案有点奇怪。例如，在我们最简单的契约违反示例中，我们得到了

| > (a1 "x") |
| --- |
| contract: add1 body |

嗯？也许我们应该展开 a1 的代码来看看发生了什么。

> |  (a1 "x") |
> | --- |
> | = (guard (function (immediate number?) |
> |                              (immediate number?)) |
> |         add1 |
> |         "add1 body" |
> |       "add1 input") |
> | = (((function (immediate number?) (immediate number?)) |
> |     "add1 body" "add1 input") |
> |    add1) |
> | = (let ([dom-c ((immediate number?) "add1 body" "add1 input")] |
> |         [rng-c ((immediate number?) "add1 body" "add1 input")]) |
> |     (lambda (x) (rng-c (add1 (dom-c x))))) |
> | = (let ([dom-c (lambda (val) |
> |                  (if (number? val) val (blame "add1 body")))] |
> |         [rng-c (lambda (val) |
> |                  (if (number? val) val (blame "add1 body")))]) |
> |     (lambda (x) (rng-c (add1 (dom-c x))))) |

可怜的 add1：它从未有过机会！唯一剩下的责备标签是“add1 body”，所以它是唯一可能被责备的东西。

我们将在一会儿回到这个问题，但是请注意，在上述代码中，几乎没有真正的函数合同的痕迹留下。我们所拥有的只是即时合同，一旦发生就会责备实际值。这与我们之前关于只能观察到即时值的说法是完全一致的 [REF]。当然，这仅适用于一阶函数；当我们涉及到高阶函数时，情况将不再如此。

出了什么问题？请注意，只有绑定到 rng-c 的合同应该责怪 add1 的主体。相比之下，绑定到 dom-c 的合同应该责怪 add1 的输入。这就好像在函数合同的域位置中，正负标签应该被...交换了一样。

考虑到受合同保护的 d/dx，我们确实可以看到这一点。关键的洞察力在于，当应用作为参数传递的函数时，“外部”变为“内部”，反之亦然。也就是说，d/dx 的主体——<wbr>原本处于正位置——<wbr>现在成为要区分的函数的调用者，将该函数的主体放在正位置，而调用者——<wbr>d/dx 的主体——<wbr>处于负位置。因此，在合同的域方面，每个嵌套的函数合同都会导致正位置和负位置交换。

在范围一侧，没有必要交换。再次考虑一下 d/dx。它返回的函数表示导数，因此应该给它一个数字（表示计算导数的点），并且应该返回一个数字（该点的导数）。这个函数的负位置确实是使用导数函数的客户端——<wbr>前置条件——<wbr>而正位置确实是 d/dx 本身的主体——<wbr>后置条件——<wbr>因为它负责生成导数。

结果，我们得到了一个更新的，而且正确的函数构造器的定义：

> | (define (function dom rng) |
> | --- |
> |   (lambda (pos neg) |
> |     (let ([dom-c (dom neg pos)] |
> |           [rng-c (rng pos neg)]) |
> |       (lambda (val) |
> |         (if (procedure? val) |
> |             (lambda (x) (rng-c (val (dom-c x)))) |
> |             (blame pos)))))) |

练习

> 将此应用到我们之前的示例中，并确认我们得到了预期的责任。手动展开代码也可以看出为什么会发生这种情况。

进一步假设，我们用标签"d/dx body"表示它的正位置，用"d/dx input"表示它的负位置来定义 d/dx。假设我们提供了显然不计算导数的函数 number->string，并将结果应用于 10：

> | ((d/dx (guard (function (immediate number?) |
> | --- |
> |                         (immediate string?)) |
> |               number->string |
> |               "n->s body" |
> |               "n->s input")) |
> |  10) |

这正确地表明责任应归因于将 number->string 作为一个假定为数值函数输入给 d/dx 的表达式—<wbr>而不是 d/dx 本身。练习

> 手动评估 d/dx，将其应用于所有相关的违例示例，并确认结果的责任是准确的。如果您向带有函数契约指示它将字符串映射到数字的字符串->数字提供 d/dx 会发生什么？如果您向相同的函数提供没有任何契约的情况会怎样？

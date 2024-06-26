# 从替换到环境

虽然我们已经有了函数的工作定义，但你可能对此感到有些不安。当解释器看到一个标识符时，你可能会觉得它需要“查找”。但它并没有查找任何东西，我们定义它的行为是一个错误！虽然绝对正确，但这也有点令人惊讶。更重要的是，我们编写解释器来理解和解释语言，而这个实现可能会让你觉得它并没有做到这一点，因为它与我们的直觉不符。

使用替换还存在另一个困难，即我们遍历源程序的次数。希望只需遍历实际评估的程序部分，而且只在必要时才遍历。但是替换会遍历一切——例如，未访问的条件分支——并且迫使程序在替换时和解释时各遍历一次。

练习

> 替换对评估的时间复杂度有何影响？

替换还存在另一个问题，即它是根据程序源代码的表示来定义的。显然，我们的解释器需要访问并使用源代码来解释它。然而，其他实现，比如编译器，无需为此目的存储源代码。编译器可能会出于其他原因存储源代码的版本或信息，比如报告运行时错误，而即时编译器可能需要在需要时重新编译它。采用更具移植性的机制将是一个不错的选择。

## 引入环境

解决第一个问题的直觉是让解释器在某种目录中“查找”标识符。解决第二个问题的直觉是推迟替换。幸运的是，这两种直觉在以一种同时解决第三个问题的方式上很好地融合了。该目录记录了替换的意图，而不是立即重写程序源代码；通过记录意图而不是立即替换，我们可以推迟替换；而产生的数据结构，称为环境，避免了源代码到源代码的重写，并且很好地映射到低级机器表示。环境中的每个名称关联都称为绑定。

请仔细观察，我们要改变的是编程语言的实现策略，而不是语言本身。因此，我们用来表示程序的数据类型都不应该改变，甚至解释器提供的答案也不应该改变。因此，我们应该把先前的解释器视为一个“参考实现”，我们即将编写的解释器应该与之匹配。实际上，我们应该创建一个生成器，生成大量的测试，通过两个解释器运行它们，并确保它们的答案是相同的。理想情况下，我们应该证明这两个解释器的行为是相同的，这是一个高级研究的好话题。

> > > 一个微妙之处在于准确定义“相同”意味着什么，特别是在失败方面。

让我们首先定义我们的环境数据结构。环境是一个名称与...关联的对列表？

现在做！

> 在这里提出的一个自然问题可能是环境将名称映射到什么。但一个更好、更基本的问题是：如何确定“自然”问题的答案？

记住，我们的环境是为了推迟替换而创建的。因此，答案在于替换。我们之前讨论过（哦，等等，还有更多！），我们希望替换将名称映射到答案，对应于急切的函数应用策略。因此，环境应将名称映射到答案。

> | (define-type Binding |
> | --- |
> |   [bind (name : symbol) (val : number)]) |
> |   |
> | (define-type-alias Env (listof Binding)) |
> | (define mt-env empty) |
> | (define extend-env cons) |

## 6.2 使用环境进行解释

现在我们可以着手解释器了。一个案例很容易，但我们应该重新审视所有其他案例：

<*>)) ::=

> | (define (interp [expr : ExprC] [env : Env] [fds : (listof FunDefC)]) : number |
> | --- |
> |   (type-case ExprC expr |
> |     [numC (n) n] |
> |     <idC-case>)) |
> |     <appC-case>)) |
> |     <plusC/multC-case>)))) |

算术操作最简单。请记住，在以前，解释器在不执行任何新替换的情况下进行了递归。因此，也没有新的延迟替换要执行，这意味着环境不会改变：

<plusC/multC-case>)) ::=

> | [plusC (l r) (+ (interp l env fds) (interp r env fds))] |
> | --- |
> | [multC (l r) (* (interp l env fds) (interp r env fds))] |

现在让我们处理标识符。显然，遇到标识符不再是错误：这正是这种变化的最初动机。相反，我们必须在目录中查找其值：

<idC-case>)) ::=

> [idC (n) (lookup n env)]

现在做！

> 实现查找。

最后，应用。观察到在替换解释器中，导致发生新替换的唯一情况是应用。因此，这应该是构建绑定的情况。让我们首先提取函数定义，就像以前一样：

<appC-case>)) ::=

> | [appC (f a) (local ([define fd (get-fundef f fds)]) |
> | --- |
> |               <appC-interp>)))] |

以前，我们进行替换，然后解释。由于我们没有替换步骤，所以我们可以继续解释，只要我们记录替换的延迟。

<appC-interp>)) ::=

> | (interp (fdC-body fd) |
> | --- |
> |         <appC-interp-bind-in-env>)) |
> |         fds) |

也就是说，函数定义集保持不变；我们像以前一样解释函数的主体；但是我们必须在绑定形式参数的环境中执行。现在让我们定义这个绑定过程：

<appC-interp-bind-in-env-take-1>)) ::=

> | (extend-env (bind (fdC-arg fd) |
> | --- |
> |                   (interp a env fds)) |
> |             env) |

被绑定的名称是形式参数（之前替换的同名）。它被绑定到解释参数的结果（因为我们决定了急切的应用语义）。最后，这扩展了我们已经有的环境。对这个进行类型检查有助于确保我们把所有的小细节都搞对了。

一旦我们有了查找的定义，我们就会有一个完整的解释器。所以这是一个：

> | (define (lookup [for : symbol] [env : Env]) : number |
> | --- |
> |   (cond |
> |     [(empty? env) (error 'lookup "找不到名称")] |
> |     [else (cond |
> |             [(symbol=? for (bind-name (first env))) |
> |              (bind-val (first env))] |
> |             [else (lookup for (rest env))])])) |

注意，查找自由标识符仍会产生错误，但错误已经从解释器移动了——<wbr>解释器本身无法确定标识符是否自由——<wbr>移到了查找，它根据环境的内容来确定这一点。

现在我们有一个完整的解释器。当然，你应该测试它，确保它按照你期望的方式工作。例如，以下测试通过：

> | (test (interp (plusC (numC 10) (appC 'const5 (numC 10))) |
> | --- |
> |               mt-env |
> |               (list (fdC 'const5 '_ (numC 5)))) |
> |       15) |
> |   |
> | (test (interp (plusC (numC 10) (appC 'double (plusC (numC 1) (numC 2)))) |
> |               mt-env |
> |               (list (fdC 'double 'x (plusC (idC 'x) (idC 'x))))) |
> |       16) |
> |   |
> | (test (interp (plusC (numC 10) (appC 'quadruple (plusC (numC 1) (numC 2)))) |
> |               mt-env |
> |               (list (fdC 'quadruple 'x (appC 'double (appC 'double (idC 'x)))) |
> |                     (fdC 'double 'x (plusC (idC 'x) (idC 'x))))) |
> |       22) |

所以我们结束了，对吧？

现在！

> 找出错误。

## 6.3 正确推迟

这是另一个测试：

> | (interp (appC 'f1 (numC 3)) |
> | --- |
> |                   mt-env |
> |                   (list (fdC 'f1 'x (appC 'f2 (numC 4))) |
> |                         (fdC 'f2 'y (plusC (idC 'x) (idC 'y))))) |

在我们的解释器中，这个求值结果为 7。应该吗？

将这个测试翻译成 Racket，对应以下两个定义和表达式：

> | (define (f1 x) (f2 4)) |
> | --- |
> | (define (f2 y) (+ x y)) |
> |   |
> | (f1 3) |

这应该产生什么？(f1 3)在 f1 的主体中用 3 替换 x，然后调用 (f2 4)。但值得注意的是，在 f2 中，标识符 x 没有被绑定！果不其然，Racket 会产生一个错误。

实际上，我们基于替换的解释器也会！

替换过程为什么会导致错误？因为当我们在 f1 的表示中用 3 的表示替换 x 的表示时，我们只在 f1 中这样做。这个“表示的”是不是有点烦人？因此，我会停止说这个，但请确保你理解为什么我不得不这么说。这是一个重要的一点学究精神。（显然：x 是 f1 的参数；即使另一个函数有一个名为 x 的参数，那也是另一个 x。）因此，当我们开始评估 f2 的主体时，它的 x 尚未被替换，导致错误。

当我们切换到环境时出了什么问题？请仔细观察：这很微妙。我们可以关注应用程序，因为只有它们会影响环境。当我们用实际值扩展形式参数时，我们扩展了当前环境。就我们的示例而言，我们要求解释器不仅替换了 f2 体中 f2 的替换，而且还替换了当前的（调用者 f1 的替换），以及所有过去的替换。也就是说，环境只会增长，永远不会缩小。

因为我们同意环境仅是替换的另一种实现策略——<wbr>特别是，语言的含义不应更改——<wbr>我们必须修改解释器。具体来说，我们不应要求它携带所有过去的延迟替换请求，而应该让它为每个新函数重新开始，就像基于替换的解释器一样。这是一个简单的改变：

<appC-interp-bind-in-env>)) ::=

> | (extend-env (bind (fdC-arg fd) |
> | --- |
> |                   (interp a env fds)) |
> |             mt-env) |

现在我们真正复制了替换解释器的行为。如果你想知道如何编写一个能捕捉错误的测试用例，请查阅 test/exn。

## 6.4 范围

上面的破坏的环境解释器实现了所谓的动态作用域。这意味着环境会在程序执行时累积绑定。因此，标识符是否被绑定甚至取决于程序执行的历史。我们应该毫不含糊地将这视为编程语言设计的缺陷。它对所有读取和处理程序的工具产生不利影响：编译器、IDE 和人类。

相比之下，替换和环境，如果正确执行，给我们词法作用域或静态作用域。在这个上下文中，“词法”意味着“根据源程序确定”，而计算机科学中的“静态”意味着“不运行程序”，因此这些对同样的直觉具有吸引力。当我们检查一个标识符时，我们想知道两件事：（1）它是否被绑定？（2）如果是，绑定在哪里？通过“在哪里”我们指的是：如果同一个名称有多个绑定，哪一个控制了这个标识符？换句话说，哪一个的替换会给这个标识符一个值？一般来说，在动态作用域语言中这些问题无法静态回答：因此，例如，你的 IDE 不能覆盖箭头来显示这些信息（就像 DrRacket 那样）。另一种思考方式是，在动态作用域语言中，对这些问题的回答对所有标识符都是相同的，它简单地指向动态环境。换句话说，它提供不了有用的信息。因此，尽管随着名称空间变得更加丰富（例如，对象、线程等），作用域规则变得更加复杂，我们应该始终努力保持静态作用域的精神。

### 6.4.1 有多糟糕？

你可能会看着我们的运行示例，想知道我们是否在小题大做。作为回报，你应该考虑两种情况：

1.  要理解程序的绑定结构，你可能需要查看整个程序。无论你将程序分解成多么小、可理解的片段，如果你在任何地方有一个自由标识符，那就没关系。

1.  理解绑定结构不仅取决于程序的大小，还取决于其控制流的复杂性。想象一个具有众多回调的交互式程序；你也必须跟踪每一个回调，才能知道哪个绑定控制了一个标识符。

需要更多的提示吗？让我们用这个表达式替换我们示例程序的表达式：

> | (if (moon-visible?) |
> | --- |
> |   (f1 10) |
> |   (f2 10)) |

假设 moon-visible?是一个函数，据推测在新月之夜会评估为 false，在其他时间会评估为 true。那么，这个程序会得出一个答案，除了在新月之夜，那时会因为未绑定的标识符错误而失败。练习

> 阴天会发生什么？

### 6.4.2 顶层作用域

当我们考虑许多语言中的顶层定义时，事情变得更加复杂。例如，Scheme 的一些版本（它是词法作用域的典范）允许你写出这样的代码：

> | (define y 1) |
> | --- |
> | (define (f x) (+ x y)) |

这似乎很清楚地表明了 f 主体中 y 的来源，除了：

> | (define y 1) |
> | --- |
> | (define (f x) (+ x y)) |
> | (define y 2) |

是合法的，而(f 10)会产生 12。等等，你可能会想，总是取最后一个！但是：

> | (define y 1) |
> | --- |
> | (define f (let ((z y)) (lambda (x) (+ x y z)))) |
> | (define y 2) |

在这里，z 被绑定到 y 的第一个值，而内部的 y 被绑定到第二个值。大多数“脚本”语言都存在类似的问题。因此，在网络上你会发现关于某种语言是静态作用域还是动态作用域的巨大混淆，而实际上读者是在比较函数内部的行为（通常是静态的）与顶层的行为（通常是动态的）。小心！实际上，有一个关于这种行为的词法作用域的有效解释，但它可能变得复杂，也许一个更明智的选择是防止这种重新定义。Racket 正是这样做的，因此提供了顶层的便利而没有其痛苦。

## 6.5 暴露环境

如果我们正在构建供他人使用的实现，那么将只接受一个表达式和函数定义列表，并用空环境调用我们定义的 interp 的导出解释器是明智的且礼貌的。这既省去了用户一个实现细节的烦恼，又避免了使用带有错误环境的解释器。然而，在某些情况下，暴露环境参数可能很有用。例如，环境可以表示一组预定义的绑定：例如，如果语言希望将 pi 自动绑定到 3.2（在印第安纳州）。

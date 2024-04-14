# 4A 解糖的第一次尝试

我们从一个非常简约的算术语言开始。让我们看看如何通过更多可以用现有操作来表达的算术操作来扩展它。我们只会添加两个，因为这些足以说明问题。

## 4.1 扩展：二进制减法

首先，我们将添加减法。因为我们的语言已经有了数字、加法和乘法，所以定义减法很容易：\(a - b = a + -1 \times b\)。

好的，这很容易！但现在我们应该将其转化为具体的代码。为此，我们面临一个决定：这个新的减法运算符应该放在哪里？诱人的做法，也许看起来很自然，就是在我们现有的 ArithC 数据类型中添加一条规则。

现在就做！

> 修改 ArithC 的负面后果是什么？

这会带来一些问题。首先，显而易见的问题是，我们现在必须修改所有处理 ArithC 的程序。到目前为止，只有我们的解释器，它非常简单，但在更复杂的实现中，这可能已经是一个问题。其次，我们试图添加可以根据现有构造定义的新构造；以一种非模块化的方式这样做似乎有点自我打击。第三，最微妙的是，在修改 ArithC 方面存在概念上的错误。这是因为 ArithC 代表我们的核心语言。相比之下，减法和其他附加项代表我们面向用户的表面语言。在不同的数据类型中记录概念上不同的想法比将它们硬塞到一个数据类型中更明智。有时分离可能看起来有点笨拙，但这使得未来开发人员更容易阅读和维护程序。此外，出于不同的目的，您可能希望添加不同的扩展，将核心与表面分开使这成为可能。

因此，我们将定义一个新的数据类型来反映我们预期的表面语法术语：

> | (定义类型 ArithS |
> | --- |
> |   [numS (n : number)] |
> |   [plusS (l : ArithS) (r : ArithS)] |
> |   [bminusS (l : ArithS) (r : ArithS)] |
> |   [multS (l : ArithS) (r : ArithS)]) |

这看起来几乎和 ArithC 一样，除了添加的情况，遵循熟悉的递归模式。

鉴于这个数据类型，我们应该做两件事。首先，我们应该修改我们的��析器，以便解析 - 表达式，并始终构造 ArithS 术语（而不是任何 ArithC 术语）。其次，我们应该实现一个解糖函数，将 ArithS 值转换为 ArithC 值。

让我们写出解糖的明显部分：

<解糖>)) ::=

> | (定义 (解糖 [as : ArithS]) : ArithC |
> | --- |
> |   (type-case ArithS as |
> |     [numS (n) (numC n)] |
> |     [plusS (l r) (plusC (解糖 l) |
> |                         (解糖 r))] |
> |     [multS (l r) (multC (解糖 l) |
> |                         (解糖 r))] |
> |     <bminusS-case>)))) |

现在让我们将上面的减法数学描述转换为代码：<bminusS-case>)) ::=

> | [bminusS (l r) (plusC (desugar l) |
> | --- |
> |                       (multC (numC -1) (desugar r)))] |

现在动手！

> 忘记在 l 和 r 上的 desugar 递归调用是一个常见的错误。当你忘记它们时会发生什么？自己试试看。

## 4.2 扩展：一元否定

现在让我们考虑另一个更有趣的扩展：一元否定。这会使你在解析器中做更多的工作，因为根据你的表面语法，你可能需要向前查看来确定你是处于一元还是二元的情况。但那甚至不是有趣的部分！

我们可以以许多方式解开一元否定。我们可以自然地将其定义为 \(-b = 0 - b\)，或者我们可以通过这个展开来抽象二元减法的解糖：\(-b = 0 + -1 \times b\)。

现在动手！

> 你更喜欢哪一个？为什么？

选择第一个扩展很诱人，因为它简单得多。想象一下，我们已经扩展了 ArithS 数据类型，其中包含一种表示一元否定的方法：

> | [uminusS (e : ArithS)] |
> | --- |

现在 desugar 中的实现很简单：

> | [uminusS (e) (desugar (bminusS (numS 0) e))] |
> | --- |

让我们确保类型匹配。观察到 e 是一个 ArithS 术语，因此可以将其用作 bminusS 的参数，并且整个术语可以合法地传递给 desugar。因此，重要的是不要解糖 e，而是直接将其嵌入到生成的术语中。这种在解糖工具中嵌入输入术语并递归调用 desugar 的模式是常见的模式；这被称为宏（具体来说，在这里，“宏”是 uminusS 的定义）。但是，上述定义存在两个问题： 

1.  第一，递归是生成式的，这迫使我们格外小心。如果你之前没听说过生成式递归，请阅读[《如何设计程序》](http://www.htdp.org/)中的相关部分。本质上，在生成式递归中，子问题是输入的计算函数，而不是其结构的一部分。这是生成式递归的一个特别简单的情况，因为“函数”很简单：它只是 bminusS 构造函数。我们可能会想通过使用不同的重写来修复这个问题：

    > | [uminusS (e) (bminusS (numS 0) (desugar e))] |
    > | --- |

    确实消除了生成性。现在动手！

    > 不幸的是，这个展开转换根本行不通！你知道为什么吗？如果不知道，尝试运行它。

1.  第二个问题是，我们在隐式地依赖于 bminusS 的确切含义；如果其含义发生变化，uminusS 的含义也会改变，即使我们不希望如此。相比之下，定义一个功能抽象，该抽象接受两个术语并生成一个代表第一个术语加上第二个术语的负数的抽象，并使用此来定义 uminusS 和 bminusS 的展开，更具有容错性。

    你可能会说减法的含义永远不会改变，所以为什么要费心呢？是的和不是。是的，它的含义不太可能改变；但不是，它的实现可能会改变。例如，开发者可能决定记录所有二进制减法的使用情况。在宏展开中，所有一元否定的使用情况也会被记录下来，但在第二次展开中则不会。

幸运的是，在这种特殊情况下，我们有一个更简单的选项，即定义\(-b = -1 \times b\)。这种展开适用于我们拥有的原语，并遵循结构递归。然而，我们上面的绕道之所以有所警示，是为了提醒您这些问题，并警告您可能并不总是如此幸运。
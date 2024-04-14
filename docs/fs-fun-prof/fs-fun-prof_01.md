# 书籍内容

## 入门指南

+   [安装和使用 F#](index3.html) 将帮助你入门。

+   [为什么使用 F#？](index2.html) F# 的互动介绍。

+   [学习 F#](index4.html) 提供了帮助你更有效地学习的提示。

+   [F# 故障排除](index5.html) 解决代码编译问题。

然后你可以尝试…

+   [在工作中使用 F# 的二十六种低风险方法](low-risk-ways-to-use-fsharp-at-work1.html)。你可以立即开始 - 无需许可！

## 教程

以下系列是关于 F# 的关键概念的教程。

+   [函数式思考](thinking-functionally.html) 从基础开始解释函数的工作方式以及原因。

+   [表达式和语法](expressions-and-syntax.html) 包括常见的表达式，如模式匹配，并有一篇关于缩进的文章。

+   [理解 F# 类型](understanding-fsharp-types.html) 解释了如何定义和使用各种类型，包括元组、记录、联合和选项。

+   [设计与类型](designing-with-types.html) 解释了如何在设计过程中使用类型，使非法状态不可表示。

+   [选择集合函数](list-module-functions.html)。如果你是从 C# 转到 F#，那么大量的列表函数可能会让你感到不知所措，因此我写了这篇文章来帮助你找到你想要的函数。

+   [基于属性的测试](property-based-testing.html)：懒惰程序员编写数千个测试的指南。

+   [理解计算表达式](computation-expressions.html) 揭秘它们并展示如何创建自己的表达式。

## 函数式模式

这些文章解释了函数式编程中的一些核心模式 - 如“映射”、“绑定”、“单子”等等。

+   [铁路导向编程](recipe-part2.html)：一个处理错误的函数式方法

+   [状态单子](handling-state.html)：通过 Dr Frankenfunctor 和 Monadster 的故事介绍处理状态的方法。

+   [阅读器单子](elevated-world-6.html)：重新发明阅读器单子。

+   [映射、绑定、应用、提升、序列化和遍历](map-and-bind-and-apply-oh-my.html)：一系列描述处理通用数据类型的核心函数。

+   [无泪单子](monoids-without-tears.html)：一个关于常见函数模式的大部分无数学讨论。

+   [折叠和递归类型](recursive-types-and-folds.html)：研究递归类型、折叠函数、尾递归、左右折叠的区别等等。

+   [理解解析器组合子](understanding-parser-combinators1.html)：从头开始创建解析器组合子库。

+   [观察海龟的十三种方式](13-ways-of-looking-at-a-turtle.html)：演示了许多不同的技术，用于实现海龟图形 API，包括状态单子、代理、解释器等等！

## 工作示例

这些文章提供了大量代码的详细示例！

+   为正确性设计[Designing for correctness](designing-for-correctness.html)：如何使非法状态不可表示（购物车示例）。

+   基于堆栈的计算器[Stack based calculator](stack-based-calculator.html)：使用简单堆栈演示组合子的强大。

+   [解析命令行](pattern-matching-command-line.html)：使用模式匹配结合自定义类型。

+   [罗马数字](roman-numerals.html)：另一个模式匹配的例子。

+   计算器设计指南[Calculator Walkthrough](calculator-design.html)：设计计算器的类型优先方法。

+   企业级井字游戏[Enterprise Tic-Tac-Toe](enterprise-tic-tac-toe.html)：纯函数实现中的设计决策指南

+   [编写 JSON 解析器](understanding-parser-combinators-4.html).

## F# 中的特定主题

通用：

+   区别 F# 与标准命令式语言的[四个关键概念](key-concepts.html)。

+   理解 F# 缩进[Understanding F# indentation](fsharp-syntax.html)。

+   使用方法的[缺点](type-extensions.html#downsides-of-methods)。

函数：

+   [柯里化](currying.html).

+   [部分应用](partial-application.html)。

控制流：

+   [匹配..with 表达式](match-expression.html) 和[创建折叠隐藏匹配](match-expression.html#folds)。

+   [If-then-else 和循环](control-flow-expressions.html)。

+   异常[Exceptions](exceptions.html)。

类型：

+   选项类型[Option Types](the-option-type.html)，特别是为什么[None 不同于 null](the-option-type.html#option-is-not-null)。

+   记录类型[Record Types](records.html)。

+   元组类型[Tuple Types](tuples.html)。

+   [区分联合](the-option-type.html)。

+   代数类型的大小和领域建模[Algebraic type sizes and domain modelling](type-size-and-design.html)。

## 有争议的帖子

+   你的编程语言[是否合理](is-your-language-unreasonable.html)？或者，为什么可预测性很重要。

+   对'罗马数字 Kata 的评论'的评论[Commentary on 'Roman Numerals Kata with Commentary'](roman-numeral-kata.html)。我对罗马数字 Kata 的方法。

+   [不使用静态类型的函数式编程语言的十个理由](ten-reasons-not-to-use-a-functional-programming-language.html)。针对我不理解的事物的一篇怒斥。

+   我们不需要[这些没用的 UML 图表](no-uml-diagrams.html)，或者说，在许多情况下，使用 UML 绘制类图并不是必需的。

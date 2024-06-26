# 第 11 课简介

## 元循环评估器

你还记得第 6 课中的 Racket-1/Scheme-1 吗？现在是时候探索 Racket 和 Scheme 如何评估表达式了！

你可以通过在终端中键入以下内容来下载本课程的代码：

```
 cp ~cs61as/lib/mceval.scm . 
```

代码也可以在线查看[这里](http://inst.eecs.berkeley.edu/~cs61as/library/mceval.scm)

## 先决条件和期望

对 Racket-1/Scheme-1 如何工作有一个良好的理解将有助于本章。你还应该熟悉第 8 课中的评估环境模型。本课程涵盖的材料将与迄今为止涵盖的其他材料有很大不同，所以要做好准备！

## 阅读材料

这些是本课程的相关阅读材料：

+   [SICP 第四章简介](http://mitpress.mit.edu/sicp/full-text/book/book-Z-H-25.html)

+   [SICP 4.1.1-6](http://mitpress.mit.edu/sicp/full-text/book/book-Z-H-26.html)

+   [讲座笔记](http://www-inst.eecs.berkeley.edu/~cs61as/reader/notes.pdf#page=78)

## 什么是评估器？

到目前为止，我们已经学会了如何编写输出我们想要的过程。一旦我们定义了这些过程并在 Scheme 提示符中键入它们，我们就得到了值。但是你是否想过这些过程实际上是如何被评估和在 Scheme 中工作的？Scheme 如何知道表达式的含义？这就是**评估器**的作用。

一个**评估器**（或**解释器**）用于编程语言是一个过程，当应用于语言的表达式时，执行评估该表达式所需的操作。

*等等，什么？评估器只是一个过程？*

是的，就是这样。评估器只是另一个程序！

## 什么是元循环评估器？

![](http://mitpress.mit.edu/sicp/full-text/sicp/book/chapter-4/figs/eval- apply.gif)

我们为 Scheme 编写的评估器将作为一个 Scheme 程序实现。考虑到使用一个在 Scheme 中实现的评估器来评估 Scheme 程序可能看起来循环。然而，评估是一个过程，因此用 Scheme 来描述评估过程是合适的，毕竟，Scheme 是我们描述过程的工具。用相同语言编写的评估器来评估自身的语言被称为元循环。

元循环评估器本质上是在第 8 课中描述的评估环境模型的 Scheme 公式。回想一下，该模型有两个基本部分：

+   要评估一个组合（一个除了特殊形式之外的复合表达式），需要评估子表达式，然后将运算子子表达式的值应用于操作数子表达式的值。

+   要将一个复合过程应用于一组参数，需要在一个新环境中评估过程的主体。为了构建这个环境，需要通过一个框架扩展过程对象的环境部分，其中过程的形式参数绑定到过程应用的参数。

这两条规则描述了评估过程的本质，一个基本循环，在这个循环中，要在环境中评估的表达式被简化为要应用于参数的过程，然后又被简化为要在新环境中评估的新表达式，依此类推，直到我们到达符号，其值在环境中查找，以及原始过程，这些过程直接应用。这个评估循环将由评估器中两个关键过程 `eval` 和 `apply` 之间的互动体现出来。我们将很快详细介绍 `eval` 和 `apply`。

评估器的实现将依赖于定义要评估的表达式的语法的过程。我们将使用数据抽象使评估器独立于语言的表示。例如，我们不会选择将赋值表示为以符号 `set!` 开头的列表，而是使用抽象谓词 `assignment?` 来测试赋值，并使用抽象选择器 `assignment-variable` 和 `assignment-value` 来访问赋值的部分。我们将学习表达式和操作的实现，这些操作指定了过程和环境的表示。例如，`make-procedure` 构造复合过程，`lookup-variable-value` 访问变量的值，`apply-primitive-procedure` 将原始过程应用于给定的参数列表。

## 要点

在这个小节中，你学到了：

1.  评估器的定义

1.  元循环评估器的定义

## 接下来是什么？

现在是时候了解 Scheme 是如何实际工作的！令人兴奋！

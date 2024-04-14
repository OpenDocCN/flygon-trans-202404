# Racket 简介

## 介绍

请注意，在前一页中，几乎没有提到[编程语言](http://en.wikipedia.org/wiki/Programming_language)。这是因为在整个事物的大局中，编程语言并不重要。它们只重要是因为对于任何给定的问题，一种语言可能比另一种语言更少的代码行数来解决问题，或者一种语言可能让我们更有效地解决问题，等等。

那么如何教授计算机科学的问题呢？我们应该使用哪种语言？我们选择了 Racket，这是[Lisp](http://en.wikipedia.org/wiki/Lisp_programming_language)的一个方言。今天我们将展示语言的基础知识，之后您可以开始思考计算机科学。随着您学习更多计算机科学知识，我们将逐步向您展示更多语言的内容。

让我们开始。

## 基本规则

1.  在 Racket 中，括号（也称为*括号*）很重要。

1.  当你要求一个过程执行其操作时，你会*调用*它。这也被称为*调用*一个过程。每当你调用一个过程时，你必须将过程调用（对过程的调用）包裹在一对括号中。

1.  每次我们调用一个过程时，我们必须遵循**前缀表示法**：我们调用的过程的名称始终是括号中最左边的项目。所有其他项目都是该过程的*参数*—我们向该过程提供的用于得到答案的东西。

这是一个演示上述三条规则的表达式示例：

```
(+ 1 2) 
```

在这个例子中，我们将参数`1`和`2`传递给加法过程`+`，它会将数字相加。我们应该期望答案是 3。

## Racket 解释器

当然，如果没有人说这种语言，那这种语言就没用了。对于编程语言来说，对话通常发生在程序员和计算机之间。**解释器**是一个将特定语言转换为计算机执行的操作和计算的程序。解释器是让计算机执行任务的一种方式，比如计算大素数或计算莎士比亚所有剧本中使用的所有不同单词。

让我们开始我们的 Racket 解释器。我们通过打开一个终端，然后输入`racket`并按回车键来做到这一点。您刚刚启动了 Racket 解释器！

您现在可以输入 Racket 表达式以供解释器评估：

```
-> (+ 1 2)
3 
```

## Racket 会输出什么？

将下面的每个示例输入解释器以尝试它。在输入每个示例之前，花点时间思考输出应该是什么。其中一些示例会导致错误—为什么会这样？（如果出现错误，解释器将输出错误消息。）

```
5
(+ 2 3)
(+ 5 6 7 8)
(+ (* 3 4) 5)
(+)
+
(sqrt 16)
(/ 3 2)
(/ 3 0)

'hello
(first 'hello)
(first hello)
(butfirst 'hello)
(bf 'hello)
(first (bf 'hello))
(first 274)
(+ (first 23) (last 45))

(define pi 3.14159)
pi
'pi
(+ pi 7)
'(good morning)
'(+ 2 3) 
```

## 总结

在这一部分，我们学习了 Racket 的基础知识。我们也尝试了 Racket 解释器。
# 表达式

## 什么是表达式？

表达式是你输入到 Racket 解释器中的任何内容。

例如，

`2`

是一个表达式。另一个例子是

`(+ 2 3)`

如上所示的组合是一个表达式，其中使用括号显示何时调用一个过程。在这种情况下，+被称为*运算符*，而 2 和 3 被称为*操作数*。一个组合的值是通过将运算符应用于操作数得到的。

## 前缀表示法

你已经在第 0.1 单元介绍了前缀表示法，所以这里是一个快速回顾。

在 Racket 中，我们使用前缀表示法。因此，我们不是在解释器中输入`2 + 3`，而是输入`(+ 2 3)` --也就是说，运算符在操作数或参数之前。

这有几个好处。目前最明显的一个好处是它可以接受接受可变数量参数的过程，比如+或*。例如，在前缀表示法中，添加 5 个数字看起来像`(+ 1 2 3 4 5)`，而在中缀表示法中，看起来像`1 + 2 + 3 + 4 + 5`。

另一个好处是它使得*嵌套*程序在彼此之间非常容易。例如，`(+ (- 4 3) (/ 4 2))`的计算结果为 3。这些表达式的深度可以任意扩展，因此

`(+ (- (/ 4 2) (+ 3 4 2 (/ 4 3))) (* 4 (- 3 4)))`

也是有效的 Racket 表达式，尽管这对我们人类来说非常难以理解。

另一个优点是它使得解析 Racket 非常容易，这在编写解释器时非常有用。如果你还不知道这意味着什么，不用担心。

即使是最复杂的表达式，解释器也会执行相同的操作：读取表达式，计算它，并将其打印到屏幕上。这被称为[读取-求值-打印循环](https://edge.edx.org/courses/uc-berkeley/cs61as-1x/SICP/wiki/cs61as-1x/read-eval-print-loop/)。

# Python 解释器

## Python 简介

我们将学习 Python，这是 CS61A 使用的语言。你在 CS61A 的朋友们正在用 Python 写一个 Scheme 解释器。在 CS61AS 这里，你将为你的最后一个项目编写一个用 Scheme 编写的 Python 解释器。

## 打开 Python

要打开 Python，请进入终端并键入 "python"。将出现 ">>>" 提示符，这相当于 Scheme 的 "->"。

如你所学，Python 中的空格非常重要。对于 Python 来说，空格就像 Scheme 中的括号。

## 与 Python 玩耍

在解释器中尝试这些命令。这些命令大多数都来自于项目规范，加上了一些更多的示例。其中一些示例应该会出错。如果有您不希望的行为，请问！

### print

你会如何让 Python 打印 "Hello World"？嗯，

```
 >>> print "Hello World"
     Hello World 
```

就是这样了！（是的，真的）。正如你从这个简单的例子中注意到的那样，Python 不需要左括号来调用函数；你不需要在 'print' 前加上左括号。Python 区分大小写，所以 "PRINT" 是不会起作用的。另一个关键的区别是，Python 只支持中缀运算符，运算符位于其操作数之间：

```
 >>> print 2 + 2
     4 
```

你实际上不需要 'print' 语句；解释器会自动评估在提示符下输入的任何内容，使用一个非常类似于元循环求值器中使用的读-求值-打印循环。例如：

```
 >>> 2 + 2
     4 
```

#### 以下内容的输出是什么？

```
 >>> 3 + 1 - 5 * 1
    >>> 3 + (1 - 5) * 1
    >>> 10/2
    >>> 10/0
    >>> (5+1)
    >>> (10) 
```

### 赋值

Python 中的赋值与其他语言中的赋值类似。例如，如果你想要为名为 'x' 的变量提供一个值：

```
 >>> x = 2
     >>> print x
     2 
```

与 Scheme 不同，Python 不区分 DEFINE 和 SET!。如果变量 'x' 还不存在，则上述赋值将在全局环境中创建一个新变量 'x'；否则，任何先前的 'x' 的值都将被覆盖。

#### 尝试以下内容：

```
 >>> num
    >>> num = 3
    >>> num
    >>> num = num + 1
    >>> num
    >>> num = "Berkeley"
    >>> num 
```

### 布尔值

"如果我们使用 "=" 来赋值变量，那么如何检查相等性？"。Python（以及大多数其他语言）使用 "=="。

#### 尝试以下内容：

```
 >>> 5 == 1
     >>> 5 == 5
     >>> 5 = 5
     >>> x = 10
     >>> x == 5
     >>> x == 10
     >>> x == x 
```

Python 支持布尔运算符 'and' 和 'or'，其工作方式与对应的 Scheme 特殊形式完全相同：

```
 >>> x = 3
     >>> (x == 3) and (x == 4)
     False

     >>> True and 3 and 5
     5

     >>> True and 3 and False
     False

     >>> True or 3 or False
     True 
```

#t 和 #f 的 Python 等效值分别为 True 和 False（大小写很重要）。

#### 尝试以下内容：

```
 >>> True and True and False
    >>> True and True and True
    >>> (1 == 0) and (42 == 42)
    >>> (1 == 1) and (42 == (1 / 0))
    >>> (1 == 0) and (42 == (1 / 0))
    >>> 2 and 3 and 4

    >>> (1 == 0) or (42 == (1 / 0))
    >>> (1 == 1) or (42 == (1 / 0))
    >>> True or 5
    >>> False or 5
    >>> 5 or True
    >>> 10 or 5
    >>> False or (1 == 0) or 5

    >>> not True
    >>> not False
    >>> not (1==0)
    >>> not 5
    >>> not "world"  
    >>> not "" 
```

### 列表

Python 有列表！（为什么不呢？）

```
 >>> x = [1, 2, 3] 
```

"x" 现在是一个存储着三个数字的变量。你可以猜到，Scheme 的类比是 "(list 1 2 3)"。Python 列表也可以是深层次的：

```
 >>> x = [[1, 2, 3], 2, 3] 
```

不幸的是，我们不能像在 Python 列表中一样进行 CAR 或 CDR。要访问列表的特定元素：

```
 >>> x[1]
     2 
```

表示法 "x[1]" 返回列表的第二个元素（Python 使用基于零的计数）。同样，在这种情况下，"[" 字符可以被视为一个中缀运算符。

#### 尝试以下内容：

```
 >>> [0,1,3,-1,5]
    >>> lst = [0,1,3,-1,5]
    >>> lst
    >>> 0 in lst
    >>> 4 in lst
    >>> 0 not in lst
    >>> 4 not in lst

    >>> newlst = ["hey","I am", "a list", "too", ["boo", 100]]
    >>> newlst
    >>> "hey" in newlst
    >>> "am" in newlst
    >>> newlst[0]
    >>> newlst[0] == "hey"
    >>> newlst[1]
    >>> newlst[4]
    >>> newlst[5] 
```

## 块

### If 条件语句

Python 的一个重要方面，源自其对可读代码的承诺，是其对缩进的使用。在大多数其他语言中，包括 Scheme，在这些语言中，缩进不是问题，因为这些语言忽略空格的数量，而是使用空格来界定符号、数字和单词。但是，在 Python 中，一行开头的空格数量是重要的。

```
 >>> x = 2
     >>> if x == 1:
     ...   x = x + 1
     ...   print x 
```

（您将不得不在显示“...”提示后再次按 ENTER 键一次，以表示您已经完成了 'if'-语句。）Python 中的 'if'-语句与 Scheme 中的等效语句工作方式相同：如果 'if'-语句的条件满足，则评估体。请注意，我们使用了 '==' 而不是 '='：由于 '=' 字符已用于赋值，因此我们使用 '==' 来检查相等性。还请注意，体是缩进的：体中的所有语句都需要以相同的缩进开始。因此，以下内容将不起作用：

```
 >>> x = 2
     >>> if x > 1:
     ...   x = x + 1
     ...    print x 
```

因为体中的第二个语句的缩进大于第一个语句。类似地，以下内容也将不起作用：

```
 >>> x = 2
     >>> if x > 1:
     ...    x = x + 1
     ...   print x 
```

因为体中的第二个语句的缩进小于第一个语句。通常，只有在完成一组相关语句或块时，您才需要取消缩进。块中的所有语句都需要具有相同数量的空格缩进。例如，'if'-语句也可以有 'else'-子句，如果条件不满足，则评估该子句。

```
 >>> x = 2
     >>> if x > 1:
     ...   x = x + 1
     ...   print x
     ... else:
     ...    x = x - 1
     ...    print x 
```

请注意，与 'if'-语句及其 'else'-子句对应的块中的行具有相同的缩进量，但块本身的缩进量不同（虽然它们不必如此！）。但是，'if'-语句和 'else'-子句需要具有相同的缩进量，因为它们属于同一语句。但是，*所有不属于块或子块的语句都不应缩进*。尝试在 Python 解释器提示符处尝试以下语句（在“>>>”之后缩进了两个空格）：

```
 >>>   2 + 3 
```

缩进强制执行清晰的代码，但可能需要一段时间来习惯；需要记住的关键是，只有在开始新的语句块时才需要缩进。

#### 尝试以下操作：

```
 >>> if x == 3:
     ...   print x + 1
     ... elif x < 4:
     ...   print x + 2
     ... elif x > 5:
     ...   print x + 3
     ... else:
     ...   print x + 4 
```

### 定义函数

Python 也有函数，它类似于 Scheme 的过程。以下定义了 'square' 函数：

```
 >>> def square(x):
     ...   return x * x 
```

（再次，在显示“...”提示后，您将不得不再次按 ENTER 键一次，以表示您已经完成了过程体。）这种语法类似于 C 语言，其中函数的参数被括在括号中，并且紧跟在函数名称之后。要调用函数：

```
 >>> square(3)
     9 
```

从这个意义上讲，左括号可以被视为一个中缀运算符，其中运算符位于其操作数之间。要了解为什么会这样，回想一下，在 Scheme 中，左括号可以被视为一个前缀运算符，它在后续参数上“调用”其第一个参数。同样，在 Python 中，左括号在下一个参数（'3'）上“调用”其第一个参数（'square'）。此外，如果 Python 过程需要返回值，我们必须在主体中显式添加一个'return'语句来返回答案；相比之下，在 Scheme 中，过程定义的最后一行总是返回的。这使我们能够区分返回值的 Python 函数和主要用于副作用的 Python 函数：

```
 >>> def foo():
     ...   print "Hello World" 
```

#### 尝试以下内容：

```
>>> def sum_of_squares(x,y):
...   return square(x) + square(y)

>>> sum_of_squares(3,4)
>>> square(square(2)) 
```

### 循环

Python 有用于循环的结构。项目规范有更详细的解释，但试试以下代码：

#### while

“while”循环接受一个谓词，并将继续评估主体，直到谓词评估为 False。

```
>>> x = 3
>>> while x < 5:
...   print x
...   x = x + 1

>>> y = 1
>>> while y < 50:
...   print y
...   y = y*2 
```

#### for

“for”循环接受一个列表（或任何类型的序列）并对序列的每个元素运行主体。这类似于您在第 9 课中学到的循环。

```
>>> for i in [1, 3, 5, 2, 4]:
     ...   print i

>>> for wd in ["Twinkle","twinkle","little","stars"]:
...   print wd 
```
# 逻辑编程是否是数学逻辑

## 逻辑编程是否是数学逻辑？

查询语言中使用的组合方法一开始可能看起来与数学逻辑的操作和，或和非完全相同，而查询语言规则的应用实际上是通过一种合法的推理方法完成的。尽管如此，将查询语言与数学逻辑等同起来并不真正有效，因为查询语言提供了一种解释逻辑语句的控制结构。我们通常可以利用这种控制结构。例如，要查找所有程序员的监督者，我们可以以两种逻辑等价形式之一来制定查询：

```
(and (job ?x (computer programmer))
     (supervisor ?x ?y)) 
```

或者

```
(and (supervisor ?x ?y)
     (job ?x (computer programmer))) 
```

如果一家公司的主管比程序员多得多（通常情况下），最好使用第一种形式而不是第二种形式，因为必须对每个由第一个 and 子句产生的中间结果（帧）进行扫描。

逻辑编程的目标是为程序员提供将计算问题分解为两个单独问题的技术：“什么”应该计算以及“如何”计算。这是通过选择数学逻辑语句的子集来实现的，这些子集足够强大，可以描述任何人可能想要计算的东西，但足够弱以具有可控的过程性解释。这里的意图是，一方面，在逻辑编程语言中指定的程序应该是一种可以由计算机执行的有效程序。控制（“如何”计算）通过使用语言的评估顺序来实现。我们应该能够安排子句的顺序和每个子句中子目标的顺序，以便计算按照被认为是有效和高效的顺序进行。与此同时，我们应该能够将计算的结果（“什么”计算）视为逻辑法则的简单结果。

我们的查询语言可以被视为数学逻辑的可过程解释子集。一个断言代表一个简单的事实（一个原子命题）。规则表示规则结论在规则体成立的情况下成立的蕴含关系。规则具有自然的过程性解释：要建立规则的结论，就要建立规则的体。因此，规则指定了计算。然而，由于规则也可以被视为数学逻辑的陈述，我们可以通过断言在数学逻辑中完全工作来证明逻辑程序实现的任何“推理”都是合理的。

## 无限循环

逻辑程序的过程性解释的一个结果是，可能构建出解决某些问题的无望低效程序。当系统陷入无限循环进行推断时，效率低下的极端情况发生。作为一个简单的例子，假设我们正在建立一个包括著名婚姻的数据库，其中包括

```
(assert! (married Minnie Mickey)) 
```

如果我们现在问

```
(married Mickey ?who) 
```

我们将得不到任何响应，因为系统不知道如果 A 与 B 结婚，那么 B 也与 A 结婚。因此，我们断言这个规则。

```
(assert! (rule (married ?x ?y)
               (married ?y ?x))) 
```

再次查询

```
(married Mickey ?who) 
```

不幸的是，这将使系统陷入无限循环，如下所示：

+   系统发现适用于结婚规则；也就是说，规则结论`(married ?x ?y)`成功地与查询模式`(married Mickey ?who)`统一，产生一个框架，其中`?x`绑定到 Mickey，`?y`绑定到`?who`。因此，解释器继续在这个框架中评估规则主体`(married ?y ?x)` -- 实际上，处理查询`(married ?who Mickey)`。

+   一个答案直接出现在数据库中作为断言：`(married Minnie Mickey).`

+   结婚规则也适用，因此解释器再次评估规则主体，这次等效于`(married Mickey ?who)`。

系统现在陷入无限循环。实际上，系统是否会在陷入循环之前找到简单答案`(married Minnie Mickey)`取决于关于系统检查数据库中项目顺序的实现细节。这是循环可能发生的种类的一个非常简单的例子。相关规则的集合可能导致更难以预料的循环，循环的出现可能取决于`and`子句中的顺序或关于系统处理查询的顺序的低级细节。

## `not`存在的问题

查询系统中的另一个怪癖涉及`not`。考虑前面介绍的 Microshaft 数据库，考虑以下两个查询：

```
(and (supervisor ?x ?y)
     (not (job ?x (computer programmer))))
(and (not (job ?x (computer programmer)))
     (supervisor ?x ?y)) 
```

这两个查询不会产生相同的结果。第一个查询首先找到与数据库中匹配`(supervisor ?x ?y)`的所有条目，然后通过删除`?x`的值满足`(job ?x (computer programmer))`的框架来过滤结果框架。第二个查询首先通过过滤传入的框架来删除可以满足`(job ?x (computer programmer))`的框架。由于唯一的传入框架为空，它检查数据库是否有任何满足`(job ?x (computer programmer))`的模式。由于通常存在这种形式的条目，`not`子句过滤掉空框架并返回一个空的框架流。因此，整个复合查询返回一个空的框架流。

麻烦的是，我们对`not`的实现实际上是作为变量的值的过滤器。如果在处理`not`子句时，存在一些变量仍然未绑定（就像上面的示例中的`?x`一样），系统将产生意料之外的结果。类似的问题也会出现在使用`lisp-value`时——如果它的一些参数未绑定，Lisp 谓词无法工作。

查询语言中的`not`与数学逻辑中的`not`有一种更严重的区别。在逻辑中，我们解释语句“not P”表示 P 不是真的。然而，在查询系统中，“not P”意味着从数据库的知识中无法推导出 P。例如，给定 Microshaft 数据库，系统会愉快地推导出各种`not`语句，比如 Ben Bitdiddle 不是棒球迷，外面不下雨，以及 2 + 2 不等于 4.78。换句话说，逻辑编程语言中的`not`反映了所谓的封闭世界假设，即所有相关信息都已包含在数据库中。

## 要点

在这个小节中，你学到了：

+   逻辑编程是数学逻辑的一个可过程解释的子集。

+   存在一些陷阱：循环和`not`。

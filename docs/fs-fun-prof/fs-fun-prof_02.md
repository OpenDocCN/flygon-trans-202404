# 在一页上了解“为什么使用 F#？”

尽管 F# 在科学或数据分析等专业领域表现出色，但它也是企业开发的一个极好选择。以下是您考虑在下一个项目中使用 F# 的五个好理由。

## ![](glyphicons_030_pencil.png) 简洁性

F# 没有被 [编码的“噪音”](fvsc-sum-of-squares.html) 所混淆，例如花括号、分号等。

由于强大的 [类型推断系统](conciseness-type-inference.html)，你几乎不需要指定对象的类型。

与 C# 相比，通常需要 [更少的代码行](fvsc-download.html) 来解决相同的问题。

```
// one-liners
[1..100] |> List.sum |> printfn "sum=%d"

// no curly braces, semicolons or parentheses
let square x = x * x
let sq = square 42 

// simple types in one line
type Person = {First:string; Last:string}

// complex types in a few lines
type Employee = 
  | Worker of Person
  | Manager of Employee list

// type inference
let jdoe = {First="John";Last="Doe"}
let worker = Worker jdoe 
```

## ![](glyphicons_343_thumbs_up.png) 便利性

许多常见的编程任务在 F# 中都要简单得多。这包括创建和使用 [复杂的类型定义](conciseness-type-definitions.html)，进行 [列表处理](conciseness-extracting-boilerplate.html)，[比较和相等性](convenience-types.html)，[状态机](designing-with-types-representing-states.html)等等。

由于函数是第一类对象，通过创建具有 [其他函数作为参数的函数](conciseness-extracting-boilerplate.html)，或者 [组合现有函数](conciseness-functions-as-building-blocks.html) 来创建新功能非常容易实现强大且可重用的代码。

```
// automatic equality and comparison
type Person = {First:string; Last:string}
let person1 = {First="john"; Last="Doe"}
let person2 = {First="john"; Last="Doe"}
printfn "Equal? %A"  (person1 = person2)

// easy IDisposable logic with "use" keyword
use reader = new StreamReader(..)

// easy composition of functions
let add2times3 = (+) 2 >> (*) 3
let result = add2times3 5 
```

## ![](glyphicons_150_check.png) 正确性

F# 拥有 [强大的类型系统](correctness-type-checking.html)，可以防止许多常见错误，如 [空引用异常](the-option-type.html#option-is-not-null)。

默认情况下，值是 [不可变的](correctness-immutability.html)，这可以防止大量的错误。

此外，您还可以经常使用 [类型系统](correctness-exhaustive-pattern-matching.html) 对业务逻辑进行编码，使得编写不正确的代码或混淆 [度量单位](units-of-measure.html) 实际上变得 [不可能](designing-for-correctness.html)，从而大大减少了单元测试的需求。

```
// strict type checking
printfn "print string %s" 123 //compile error

// all values immutable by default
person1.First <- "new name"  //assignment error 

// never have to check for nulls
let makeNewString str = 
   //str can always be appended to safely
   let newString = str + " new!"
   newString

// embed business logic into types
emptyShoppingCart.remove   // compile error!

// units of measure
let distance = 10<m> + 10<ft> // error! 
```

## ![](glyphicons_054_clock.png) 并发性

F# 有许多内置库可以帮助处理同时发生的多个事情。异步编程 [非常容易](concurrency-async-and-parallel.html)，并行编程也是如此。

F# 还具有内置的 [actor 模型](concurrency-actor-model.html)，以及出色的事件处理和 [函数式响应式编程](concurrency-reactive.html) 支持。

当然，由于数据结构默认是不可变的，因此共享状态和避免锁定要容易得多。

```
// easy async logic with "async" keyword
let! result = async {something}

// easy parallelism
Async.Parallel [ for i in 0..40 -> 
      async { return fib(i) } ]

// message queues
MailboxProcessor.Start(fun inbox-> async{
    let! msg = inbox.Receive()
    printfn "message is: %s" msg
    }) 
```

## ![](glyphicons_280_settings.png) 完备性

尽管在本质上是一种函数式语言，F# 也支持其他不是 100% 纯粹的风格，这使得它与非纯净的网站、数据库、其他应用程序等进行交互变得更加容易。

特别地，F# 被设计为一种混合函数式/OO语言，因此它可以做 [几乎和 C# 一样的事情](completeness-anything-csharp-can-do.html)。

当然，F# 是 [.NET 生态系统的一部分](completeness-seamless-dotnet-interop.html)，这使您可以无缝访问所有第三方 .NET 库和工具。它可以在大多数平台上运行，包括 Linux 和智能手机（通过 Mono 和新的 .NET Core）。

最后，它与 Visual Studio（Windows）和 Xamarin（Mac）很好地集成，这意味着您可以获得一个带有 IntelliSense 支持、调试器和许多插件用于单元测试、源代码控制和其他开发任务的优秀 IDE。或者在 Linux 上，您可以使用 MonoDevelop IDE。

```
// impure code when needed
let mutable counter = 0

// create C# compatible classes and interfaces
type IEnumerator<'a> = 
    abstract member Current : 'a
    abstract MoveNext : unit -> bool 

// extension methods
type System.Int32 with
    member this.IsEven = this % 2 = 0

let i=20
if i.IsEven then printfn "'%i' is even" i

// UI code
open System.Windows.Forms 
let form = new Form(Width= 400, Height = 300, 
   Visible = true, Text = "Hello World") 
form.TopMost <- true
form.Click.Add (fun args-> printfn "clicked!")
form.Show() 
```

## “为什么使用 F#？”系列

以下一系列文章演示了 F# 的每个优势，使用独立的 F# 代码片段（通常与 C# 代码进行比较）。

+   [为什么使用 F# 系列介绍](why-use-fsharp-intro.html)。F# 的好处概述

+   [60秒内了解 F# 语法](fsharp-in-60-seconds.html)。如何快速浏览 F# 代码

+   [用 F# 比较 C#: 简单求和](fvsc-sum-of-squares.html)。在这里我们尝试对从 1 到 N 的平方求和而不使用循环

+   [用 F# 比较 C#: 排序](fvsc-quicksort.html)。在这里我们看到 F# 比 C# 更具声明性，并且介绍了模式匹配。

+   [用 F# 比较 C#: 下载网页](fvsc-download.html)。在这里我们看到 F# 擅长回调，并介绍了“use”关键字

+   [四个关键概念](key-concepts.html)。区分 F# 与标准命令式语言的概念

+   [简洁性](conciseness-intro.html)。为什么简洁性很重要？

+   [类型推断](conciseness-type-inference.html)。如何避免被复杂的类型语法分散注意力

+   [低开销的类型定义](conciseness-type-definitions.html)。创建新类型没有任何惩罚

+   [使用函数提取样板代码](conciseness-extracting-boilerplate.html)。DRY 原则的函数式方法

+   [将函数用作构建块](conciseness-functions-as-building-blocks.html)。函数组合和迷你语言使代码更易读

+   [用于简洁性的模式匹配](conciseness-pattern-matching.html)。模式匹配可以在一步中匹配和绑定

+   [便利性](convenience-intro.html)。减少编程枯燥和样板代码的特性

+   [类型的即插即用行为](convenience-types.html)。不需要编码的不可变性和内置相等性

+   [将函数用作接口](convenience-functions-as-interfaces.html)。当使用函数时，OO 设计模式可以变得微不足道

+   [部分应用](convenience-partial-application.html)。如何固定函数的一些参数

+   [活动模式](convenience-active-patterns.html)。强大匹配的动态模式

+   [正确性](correctness-intro.html)。如何编写“编译时单元测试”

+   [不可变性](correctness-immutability.html)。使��的代码可预测

+   [穷尽模式匹配](correctness-exhaustive-pattern-matching.html)。确保正确性的强大技术

+   [利用类型系统确保正确的代码](correctness-type-checking.html)。在 F# 中，类型系统是你的朋友，而不是敌人

+   [示例：为正确性设计](designing-for-correctness.html)。如何使非法状态不可表示

+   [并发性](concurrency-intro.html)。我们编写软件的下一个重大革命？

+   [异步编程](concurrency-async-and-parallel.html)。使用 Async 类封装后台任务

+   [消息和代理](concurrency-actor-model.html)。让并发思考变得更容易

+   [函数式响应式编程](concurrency-reactive.html)。将事件转化为流

+   [完整性](completeness-intro.html)。F# 是整个 .NET 生态系统的一部分

+   [与 .NET 库无缝互操作](completeness-seamless-dotnet-interop.html)。与 .NET 库一起工作的一些便利功能

+   [C# 能做的任何事情...](completeness-anything-csharp-can-do.html)。在 F# 中进行面向对象编程的快速浏览

+   [为什么使用 F#：结论](why-use-fsharp-conclusion.html)。

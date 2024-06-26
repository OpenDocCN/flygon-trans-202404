# 第一章：路线图

# 路线图

本书遵循熟悉的惯例。在正式介绍语言之前，它涉及了一些常规性的话题（比如这一章），这包括从简单的主题（变量和数据类型）开始，逐渐向更复杂的领域发展，例如泛型。

## 忽略的细节

本书不会详细讨论一些主题。它主要关注 TypeScript 语言。因此，本书不提供关于下载 TypeScript、安装它或配置它的逐步说明。这些以及类似的主题在其他地方有更详细的介绍。最后一章，“我接下来该去哪里？”指向了一些关注这些事情的有用在线资源。

## 实践考虑

本章覆盖了更高层次的 TypeScript 开发经验。它回答了一些问题，例如：

+   我如何首先编写 TypeScript 应用程序？

+   TypeScript 在浏览器中是如何运行的？（实际上并不是 - 它会“转译”为 JavaScript）。

+   如何调试 TypeScript 应用程序？

这里的目标是帮助你立足于 TypeScript 的“世界”，描述在构建 TypeScript 解决方案时发生的大局。正如你将看到的那样，它并不是非常复杂^(1)。

## 介绍类型

TypeScript 提供了静态类型。你不需要使用它们，但它们非常有用。本章首先描述了原始类型（整数、字符串等）。它展示了声明变量类型如何帮助良好的集成开发环境（IDE）提供有用的编辑时和编译时反馈。我们还将有机会试图用强类型的优点打动 TypeScript 的怀疑者们 :)^(2)。

## 深入类型

现实世界是复杂的，有着复杂的数据结构。TypeScript 提供了`接口`的概念来帮助我们描述和管理它们。本章介绍了接口作为一种描述它们的方式，从一个平面对象开始，然后转向来自 REST 服务的更复杂的 JSON 格式响应。

TypeScript 接口看起来感觉非常类似于 C# 和 Java 中的接口。一般来说，接口是许多常见且重要的设计模式和原则（想想[SOLID](http://williamdurand.fr/2013/07/30/from-stupid-to-solid-code/)）的支柱之一。TypeScript 接口使我们能够更直接地实现这些设计模式^(3)。

TypeScript 提供了几种描述数据的方式。本章介绍了其中几种最有用的方式。这些包括：

+   枚举：给固定值分配一个标签。

+   联合类型：定义一个可以容纳两种或更多不同类型值（包括硬编码字符串）的新自定义类型。

TypeScript 提供了其他类型，比如交叉类型。本书暂时不涉及这些类型 - 它们感觉像是边缘情况，虽然在可以使用时很有趣且至关重要，但大多数人并不常用。

## 模板字符串

通过模板字符串的魔力消除繁琐的字符串操作！

## 函数

深入了解 TypeScript 如何增强标准 JavaScript 函数，包括类型化参数、void 返回值、默认函数参数值等。

另外，学习箭头函数，通常被称为“匿名”或“lambda”函数。

## 介绍类和深入了解类

正如人们所说，TypeScript 的静态类型是[绝佳选择](http://www.phrases.org.uk/meanings/the-bees-knees.html)。类就像蜜蜂采集的蜜，这两章对它们进行了相当彻底的讨论：

+   类语法

+   类和接口

+   继承

+   抽象类

+   静态类成员

类是面向对象编程的重要组成部分，TypeScript 在这里提供了可靠的支持。

## 泛型

学习 TypeScript 版本的泛型，就像你从 C# 和 Java 中所了解的那样。

## 继续学习

一个大长串的链接，希望能带领你走向 TypeScript 的伟大。

> ¹. 这总是这样吗？在我们这个后现代 JavaScript 世界里，没有什么特别复杂的事情。不过，当然，事情终究会变得复杂起来。 ↩
> 
> ². 如果你或你认识的人对 TypeScript 感到怀疑，请看看这一章及其视频。在这里投资十五分钟左右，然后决定是否想要在此之后继续投资更多时间。 ↩
> 
> ³. 正如古老的国度所说，“为了静态类型而来，为了接口而留下。” ↩

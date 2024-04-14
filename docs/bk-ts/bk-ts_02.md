# 第二章：略过部分

## 略过部分

本书关注的是我认为是 TypeScript 语言的“主要”部分。这缩小了它的范围，因此，一些你可能认为一个常识性目录应该包括的主题实际上并没有包括^(1)。例如：

![](https://www.flickr.com/photos/35237092540@N01/8167731771/)- TypeScript 的历史：这是一个有趣的话题^(2)，但并不有助于实现本书的实际目标。如果你想了解更多 TypeScript 的历史，请[咨询维基百科上的专家们开始](https://en.wikipedia.org/wiki/TypeScript#History)。

+   IDEs、部署流程、webpack 和任务运行器：这些东西几乎每周都在变化。如果我全力推荐某个特定的“TypeScript 入门”，当你读到我的推荐时，它可能已经被更新更简化的解决方案取代了。此外，你在网络上找到的各种入门项目往往依赖于框架。一类入门项目支持 Angular，另一类支持 React，等等。这本书不涉及这些框架。

除了那些非语言特性外，这本书还忽略了我认为更高级和/或情景化的主题。这些包括：

+   装饰器。装饰器允许你增强 TypeScript 的构件，比如类或属性的功能。这种赋值是以声明方式完成的，可以增强目标构件而不需要构件的知识或同意。我知道这有点元编程 :). 它们非常强大，随着时间的推移，可能会成为人们普遍做的事情。然而，我认为它们对我的目标读者来说太过高级。在*继续学习*章节中，我指出了一些展示它们的优秀博客文章和 github 项目。

+   模块：模块并不特别复杂，但它们主要支持捆绑和其他工具（比如 webpack）。我在写这篇文章时对是否包括一个关于模块的章节持保留态度。目前，我不会包括，而是会在*继续学习*章节中推荐给你一些关于模块的好概述。

+   混入、交叉类型等：我涵盖了我认为是“核心”语言特性。与装饰器一样，一些主题相当高级，同时在相当狭窄的业务应用范围内有用。我不想把太多概念扔给读者。因此，我将这些内容排除在书外，并邀请你从其他来源学习。

关于未涵盖的内容就说这么多。让我们继续讨论第一个重要的主题，TypeScript 到底是如何工作的？

> ¹. 当然，我们并不一定有相同的共识。如果你不喜欢我的观点，可以写一本自己的书 :). 或者，通过 github issue 或直接给我发邮件建议我添加更多内容。导言章节提供了这两种选择的链接。↩
> 
> ². 你知道 TypeScript 已经超过五岁了吗？在美国，当微软发布这种语言时，巴拉克·奥巴马总统刚刚准备连任。巧合？谁知道呢？（巴拉克·奥巴马的照片来自 Peter Prodoehl @ [`www.flickr.com/photos/raster/`](https://www.flickr.com/photos/raster/)）。 ↩
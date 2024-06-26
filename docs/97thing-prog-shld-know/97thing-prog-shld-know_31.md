# 不要碰那段代码！

# 不要碰那段代码！

这种情况每个人都遇到过。你的代码被部署到测试服务器进行系统测试，测试经理回复说她遇到了问题。你的第一反应是“快点，让我来修复 — 我知道怎么回事。”

从更大的意义上讲，不对的是，作为一个开发者，你认为你应该访问测试服务器。

在大多数基于 Web 的开发环境中，架构可以分解如下：

+   开发者的本地开发和单元测试。

+   开发服务器，用于手动或自动集成测试。

+   测试服务器，由 QA 团队和用户进行验收测试。

+   生产服务器

是的，那里还有其他的服务器和服务，比如源代码控制和票务，但你明白我的意思。按照这个模型，一个开发者 — 即使是一位高级开发者 — 不应该超出开发服务器的访问范围。大多数开发都是在开发者的本地机器上完成的，使用他们喜爱的 IDE 混合，虚拟机，并适量地撒上适当的黑魔法来祈求好运。

一旦自动或手动检入 SCC，它应该被部署到开发服务器上，在那里可以测试和调整，如果需要确保一切配合良好。然而，从这一点开始，开发者就是这个过程的旁观者。

验收经理应该将代码打包并部署到测试服务器供 QA 团队使用。就像开发者不应该访问开发服务器之外的任何内容一样，QA 团队和用户也不需要触碰开发服务器上的任何东西。如果准备好进行验收测试，就发布并部署，不要让用户在开发服务器上“快速查看一下”。请记住，除非你独自编码项目，否则其他人也在那里编码，而他们可能还没准备好让用户看到。发布经理是唯一有权访问两者的人。

在任何情况下 — 永远，无论如何 — 开发者都不应该访问生产服务器。如果出现问题，您的支持人员应该修复它或请求您修复它。在检入 SCC 后，他们将从那里部署补丁。我参与的一些最大的编程灾难之所以发生，是因为某人**咳咳**我**咳咳**违反了这个最后的规则。如果它坏了，生产环境不是修复的地方。

由[Cal Evans](http://programmer.97things.oreilly.com/wiki/index.php/Cal_Evans)撰写

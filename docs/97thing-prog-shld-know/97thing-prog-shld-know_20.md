# 早期和频繁地部署

# 早期和频繁地部署

调试部署和安装过程通常被推迟到项目接近尾声时才进行。在一些项目中，编写安装工具被委托给一个承担任务的发布工程师，作为一种“必要之恶”。从手工制作的环境中进行审查和演示以确保一切正常。结果是团队在可能为时已晚时才获得有关部署过程或部署环境的经验。

安装/部署过程是客户看到的第一件事，简单的安装/部署过程是拥有可靠（或至少易于调试）的生产环境的第一步。部署的软件是客户将要使用的。如果不确保部署正确设置应用程序，您将在客户使用软件之前引起客户的疑问。

从安装过程开始您的项目将使您有时间在产品开发周期中逐步演变过程，并有机会对应用程序代码进行更改以使安装更容易。定期在干净的环境中运行和测试安装过程还可以检查您是否在代码中做出了依赖于开发或测试环境的假设。

将部署放在最后意味着部署过程可能需要更复杂的工作来解决代码中的假设。在 IDE 中看起来很棒的想法，在那里您对环境有完全控制，可能会导致更加复杂的部署过程。更好的做法是尽早了解所有权衡。

“能够部署”在早期似乎与在开发人员的笔记本电脑上运行应用程序相比没有太多的商业价值，但简单的事实是，在你能够在目标环境中展示应用程序之前，还有很多工作要做才能提供商业价值。如果你推迟部署过程的理由是因为它微不足道，那么无论如何都要去做，因为成本很低。如果太复杂，或者存在太多不确定性，就像处理应用程序代码一样：在进行过程中进行实验，评估，并重构部署过程。

安装/部署过程对于您的客户或专业服务团队的生产力至关重要，因此您应该在进行过程中测试和重构此过程。我们在整个项目中测试和重构源代码。部署过程也不例外。

作者：[Steve Berczuk](http://programmer.97things.oreilly.com/wiki/index.php/Steve_Berczuk)

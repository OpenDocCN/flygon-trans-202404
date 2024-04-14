# 当程序员和测试员合作时

# 当程序员和测试员合作时

当测试员和程序员开始合作时，会发生一些神奇的事情。不再花费大量时间通过缺陷跟踪系统来回发送错误。不再浪费时间尝试弄清楚某事到底是一个错误还是一个新功能，而是更多的时间用于开发满足客户期望的优秀软件。在编码甚至开始之前就有许多开始协作的机会。

测试员可以帮助客户使用领域语言编写和自动化验收测试，使用诸如 Fit（集成测试框架）之类的工具。当这些测试在编码开始之前提供给程序员时，团队正在实践验收测试驱动开发（ATDD）。程序员编写用于运行测试的固定装置，然后编写代码使测试通过。然后，这些测试成为回归套件的一部分。当这种协作发生时，功能测试会尽早完成，为边界条件的探索测试或整体流程的工作流程留出时间。

我们可以再进一步。作为一名测试员，在程序员开始编写新功能代码之前，我可以提供大部分的测试想法。当我询问程序员是否有任何建议时，他们几乎总是提供了能帮助我更好地测试覆盖范围的信息，或者帮助我避免在不必要的测试上浪费大量时间。通常，我们能够因为测试澄清了许多最初的想法而预防缺陷。例如，在我参与的一个项目中，我给程序员提供的 Fit 测试显示了查询的预期结果以响应通配符搜索。程序员完全打算只编写完整词语搜索。我们能够与客户交谈并在编码开始之前确定正确的解释。通过合作，我们防止了缺陷，节省了我们大量的浪费时间。

程序员还可以与测试员合作创建成功的自动化。他们了解良好的编码实践，并且可以帮助测试员建立适合整个团队的强大的测试自动化套件。我经常看到测试自动化项目失败，因为测试设计不佳。测试试图测试太多，或者测试员对技术了解不足，无法保持测试的独立性。测试员通常是瓶颈，因此程序员与他们合作完成自动化等任务是有意义的。与测试员合作，了解什么可以早期测试，也许提供一个简单的工具，将为程序员提供另一个反馈周期，从长远来看将帮助他们提供更好的代码。

当测试人员不再认为他们的唯一工作是破坏软件并在程序员的代码中寻找错误时，程序员也不再认为测试人员是在‘针对他们’，而更愿意进行合作。当程序员开始意识到他们负责将质量融入他们的代码中时，代码的可测试性就是一个自然的副产品，团队可以一起自动化更多的回归测试。成功团队合作的魔力开始展现。

[Janet Gregory](http://programmer.97things.oreilly.com/wiki/index.php/Janet_Gregory)
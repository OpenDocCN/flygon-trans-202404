# 对注释的评论

# 对注释的评论

在我大学的第一门编程课上，我的老师发了两张 BASIC 编码表。在黑板上，作业写着“编写一个程序，输入并计算 10 个保龄球得分的平均值。”然后老师离开了教室。这有多难呢？我不记得我的最终解决方案，但我确信其中有一个`FOR/NEXT`循环，并且总共不会超过 15 行。编码表——对于你们读到这个的孩子们，是的，我们过去写代码时常常先手写出来，然后再输入到电脑里——每张表允许大约有 70 行代码。我对老师为什么给了我们两张表感到非常困惑。因为我的书写一直很糟糕，所以我用第二张表很整洁地复制了我的代码，希望能因为风格得到几个额外的分数。

让我感到惊讶的是，当我在下一堂课开始时收到了作业，我只得了一个勉强及格的分数。（这成为我大学生涯中的一个预兆。）在我整洁地复制的代码的顶部，写着“没有注释？”

仅仅是老师和我知道程序应该做什么是不够的。这项作业的一部分目的是教会我，我的代码应该向后面的程序员解释清楚。这是我没有忘记的一课。

注释并不邪恶。它们和基本的分支或循环结构一样，对编程是必要的。大多数现代语言都有类似 javadoc 的工具，可以解析正确格式的注释，自动生成 API 文档。这是一个非常好的开始，但还远远不够。在你的代码中应该有关于代码应该做什么的解释。按照“如果写起来很难，那么阅读起来也应该很难”的古老格言写代码，对你的客户、雇主、同事和未来的自己都是一种伤害。

另一方面，你的注释也可以过分。确保你的注释澄清了你的代码，但不要让它变得晦涩。在你的代码中加入相关的注释，解释代码的目标是什么。你的头部注释应该给任何程序员足够的信息来使用你的代码，而你的内联注释应该帮助下一个开发者修复或扩展它。

在一家工作中，我不同意上面的人做出的设计决定。感觉相当刻薄，就像年轻的程序员经常做的那样，我将指示我使用他们的设计的电子邮件文本粘贴到了文件的头部注释块中。结果，这家特定商店的经理在提交代码时实际上审核了代码。这是我第一次听到“职业发展受限的行为”这个词。

by [卡尔·埃文斯](http://programmer.97things.oreilly.com/wiki/index.php/Cal_Evans)

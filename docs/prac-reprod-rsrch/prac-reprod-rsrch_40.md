# 使用 R 开发、测试和部署分层模型的高效 MCMC 算法

# 使用 R 开发、测试和部署分层模型的高效 MCMC 算法

## 丹尼尔·图尔克

我叫丹尼尔·图尔克，是威廉姆斯学院数学和统计系的助理教授。我的研究领域是计算统计学和算法，经常涉及生态统计学的应用。我描述的工作流程是从想法产生到发表的过程，即创建一个自动化程序来提高马尔可夫链蒙特卡洛（MCMC）采样的效率。MCMC 是一种易于接近且常用的统计技术，用于对分层模型结构进行推断。

### 工作流程

![图表](img/dturck.png) 这个过程始于团队的头脑风暴，讨论如何制定一个自动化程序来提高 MCMC 效率。这可以说是整个过程中最有趣的部分。这需要两到四个人真正走到白板前讨论想法。每个阶段持续几个小时。我们在这些阶段之间也会回顾理论和文献。这个初步探索阶段需要一到两周时间。

一个可行的想法被构想出来，现在必须进行原型制作以评估其有效性。项目负责人在 R 中实现了算法，因为我们用于运行 MCMC 的引擎是原生的。这对我们团队来说效果很好，因为每个人都很熟悉 R，代码可以轻松共享和审查。我们创建了一个私人 GitHub 存储库，团队成员在其中编写/审查/修改算法。这是我们之间的私人存储库，因为在这一点上，它完全是实验性的，不是为公众服务的。在这一点上几乎没有（或者没有）文档。

在这个阶段可能会进行多次迭代，其中实现想法并进行初步测试。根据每次迭代的结果，我们会多次回到起点，找出之前算法失败的地方，或者如何改进它。再次，我们实现一个改进版本，并使用我们设计的少量测试进行测试。这个过程耗时，可能令人沮丧，因为会遇到很多死胡同。前进的道路并不总是清晰的。这个修改和测试算法的过程可能需要三到六个月的时间。

最终，这个过程会收敛到一个可用的算法。我们团队的所有成员都对结果感到满意，并同意该算法已经准备好进行更专业的实现，希望能够发表。

一两名团队成员（与 MCMC 引擎最接近的人）对我们的算法进行更正式的实现。这个实现被添加到一个现有的公共 GitHub 存储库中，该存储库包含了用于公共使用的 MCMC 引擎的基础。由于算法已经定义并最终确定，这一步应该只需几周时间。还编写了适当的文档，以 R 帮助文件的形式存在，并将其添加到公共存储库中。

下一个目标是撰写一篇描述算法和结果的已发表研究论文。为此，我们组装了一套可重现的示例。这些示例来自已知的、标准的、现有的模型和已发表的数据集，这些模型和数据集被选择为 MCMC 的“常见”或“困难”应用。创建了一个新的公共 GitHub 存储库，并将这些示例模型和数据集添加为 R 数据文件的形式。此外，还添加了用于在这些示例上运行我们新算法的 bash 脚本，以及一个有用的 README 文件。这个存储库的唯一目的是在我们的手稿中引用，作为包含完全自动化脚本的地方，用于再现手稿中呈现的结果。

我们的可重现示例包括在可执行脚本中固定随机数生成器种子，因此我们可以保证每个 MCMC 运行的采样结果相同（否则是随机算法）。然而，每个 MCMC 运行的确切*时间*将在运行和计算平台之间变化，并且因此最终的效率度量也将变化。因此，确切的结果并不完全可再现，但在运行之间变化约为 5%。

团队成员共同起草一份描述我们新算法的手稿，其中呈现了一套示例模型的结果。这是由团队成员共同使用 LaTeX 编写的。手稿特别引用了可重现示例的存储库，并解释了结果的精确再现中的注意事项——即，它们会与呈现的结果略有不同，以及为什么会这样。然而，审阅者们对我们研究的算法和可重现性非常满意，并乐意接受手稿发表。

### 痛点

我们设计和测试算法的迭代过程没有得到良好的文档记录，也不太具有再现性。唯一的救赎是 GitHub 用于版本控制，所以理论上如果有必要的话，我们可以回顾以前的工作。但实际上，提交消息很短，也不太描述性，因为一切都是实验性的。更不用说，我们的代码没有任何文档。如果有必要，实际上很难去审查算法或结果的先前版本。

此外，我们的“可重复”的示例集并非完全可重复是一个小小的争议点。我们为称呼这些示例为可重复而感到矛盾，因为我们手稿中呈现的结果实际上无法重新创建。团队成员一致认为这似乎是不可避免的。我们在手稿中解释了这一点，尽管如此，我们仍然将我们的结果称为“可重复”。

为了准备我们的手稿，数值结果被手动输入到一个 tex 文档中。诸如 knitr 和 sweave 等工具可用于自动化此过程，这些工具会直接从 R 中自动包含数值和图形结果到 LaTeX 中。我们选择不使用这些工具来自动化 R 和手稿之间的交互，因为并非所有团队成员都熟悉或习惯使用这些工具。如果我们使用了这些工具，手稿的准备工作将会更简单，错误也会更少，这可能是一个明智的决定，但学习曲线阻止了我们的团队这样做。

### 主要优势

该项目最显着的可重复性方面是公共存储库，其中包含用于重新运行手稿中所有分析的输入数据和脚本。这包括用于运行每个特定分析的单独 bash 脚本，以及一个重新运行所有分析的单个“主”脚本。评审员可以轻松地再现（在较小的误差范围内）手稿中出现的所有数值结果，并且阅读随后发表的文章的研究人员可以很容易地使用该算法。

### 问题

#### 对您来说，“可重复性”意味着什么？

在我的案例研究中，可重复性意味着用户/评审可以重新创建我们手稿中呈现的结果（MCMC 效率的改进）。但是，由于算法运行时间的微小差异，结果不会完全匹配。

#### 你认为在你的领域中，为什么可重复性很重要？

可重复性很重要，这样其他人可以验证我们出版物中给出的结果。这确保了结果是真实的，并为其他人使用我们的算法提供了明确的路径。

#### 您是如何或在何处了解到可重复性的？

主要是通过使用 GitHub，来自加州大学伯克利分校的同事以及一般的编程经验。没有特定的课程或研讨会让我想起来。

#### 您认为在您的领域进行可重复研究的主要挑战是什么，您有什么建议吗？

在计算统计领域，除了无知或技术无能之外，可重复研究没有太多障碍。然而，这个案例研究确实凸显了一个真正的障碍：各种机器和计算平台之间的性能差异，这将影响算法运行时间，这是我们效率衡量的因素之一。

#### 您认为进行可重复研究的主要动机是什么？

主要是为了让其他人（如果他们选择的话）能够实际（而且容易地）验证我们的结果。
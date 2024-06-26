# 评估可重复性

# 评估可重复性

## Ariel Rokem，Ben Marwick 和 Valentina Staneva

虽然理解导致可重复性的所有因素是重要的，但将这些因素分解为可以立即纳入现有研究计划并立即提高其可重复性的步骤可能也很困难。其中一项首要步骤是评估当前情况，并在采取措施进一步增加可重复性时跟踪改进。本章提供了一些关于这种评估的关键要点。

### 使研究可重复的含义

尽管本书的一个目标是发现研究人员如何为自己定义和实施可重复性，但在这一点上，简要回顾一下当前学术讨论中关于努力实现可重复研究意味着什么是很重要的。这很重要，因为最近的调查和评论强调科学家对可重复性的含义存在困惑（Baker, 2016b, 2016a）。此外，在不同领域关于如何定义“可重复”和“可复制”存在分歧（Casadevall & Fang, 2010; Drummond, 2009; Easterbrook, 2014; Stodden, Borwein, & Bailey, 2013）。例如，Goodman, Fanelli, & Ioannidis (2016)指出，在流行病学、计算生物学、经济学和临床试验中，可重复性通常被定义为：

> 研究人员复制先前研究的结果的能力，使用与原始研究者使用的相同材料。也就是说，第二位研究人员可能使用相同的原始数据构建相同的分析文件，并实施相同的统计分析，以尝试产生相同的结果。

这与可复制性不同：

> 指的是研究人员在遵循相同程序但收集新数据的情况下，能够复制先前研究的结果的能力。

值得注意的是，上述定义与本书中这些术语的使用基本一致，与计算机协会（ACM，世界上最大的科学计算学会）的定义完全相反，后者从国际计量词汇中获取其定义。以下是 ACM 的定义：

> 可重复性（不同团队，不同实验设置）可以通过不同团队、不同测量系统，在不同位置进行多次试验来获得声明精度的测量结果。对于计算实验，这意味着独立团队可以使用他们完全独立开发的工件获得相同的结果。
> 
> 可复制性（不同团队，相同实验设置）可以通过不同团队使用相同的测量程序、相同的测量系统，在相同或不同的位置进行多次试验，在相同的操作条件下获得声明精度的测量结果。对于计算实验，这意味着独立团队可以使用作者自己的工件获得相同的结果。

我们可以在物理学和科学哲学文献中看到 ACM 定义的遗产（Cartwright, 1991; Collins, 1984; Franklin & Howson, 1984）。在她关于科学实验认识论的论文中，Cartwright（1991）提出了关键术语的第一个清晰定义：“可复制性 - 再次进行相同实验”和“可重现性 - 进行新实验”。

Cartwright 的定义与我们偏好的定义相左，来自 Goodman 等人（2016）。这是因为我们追溯了“可重现”一词在使用中的不同渊源，认识到计算机在科学实践中的核心作用，对经验实验作为生成知识的主要手段的重视较少。最早以这种方式写作可重现性的人之一是地球物理学家 Jon Claerbout。他开创了“可重现研究”一词的使用，描述了他的地震学研究小组如何使用计算机文件来实现论文和出版物中图表的高效再现（Claerbout & Karrenfach，无日期）。我们最近可以在 Stodden，Leisch 和 Peng（2014）中看到这种用法：

> 复制，即独立实施科学实验以验证特定发现的实践，是发现科学真理的基石。与复制相关的是可重现性，即独立科学家使用原始数据集和方法计算定量科学结果。可重现性可以被视为一种不同的有效性标准，因为它放弃了独立数据收集，而是使用原始调查人员收集的方法和数据。由于技术的进步和计算方法在研究领域的快速传播，可重现性已成为更近期研究的重要问题。

正是这种关于可重现性的思考方式捕捉到了本书的贡献者们使用这个术语的大部分变化。本章剩余部分探讨的一个关键观点是，可重现性是一个程度问题，而不是一种性质问题。这意味着识别相对容易和快速改变的因素可以逐步增加研究计划的可重现性。识别更具挑战性的点，需要更多工作，有助于设定更具可重现性工作的长期目标，并有助于识别随着时间推移可以进行的实际变化。

可重现性可以在几个不同的层面进行评估：在个别项目层面（例如一篇论文、一个实验、一个方法或一个数据集）、个别研究人员、实验室或研究小组、一个机构，甚至一个研究领域。这些不同层面可能适用略有不同类型的标准和评估要点。例如，如果一个机构制定奖励进行可重现研究的研究人员的政策，那么该机构将支持可重现性实践。与此同时，如果一个研究领域开发了促进和实现可重现研究实践的社区维护资源，如数据存储库或共同数据共享标准，那么该研究领域可能被认为具有更高水平的可重现性。

本书侧重于这些层面中的第一个，即特定研究项目的层面。在本章中，我们考虑了研究人员如何评估可重现性的一些方法。我们将这种可重现性评估分为三个不同的广泛方面：自动化和溯源跟踪、软件和数据的可用性，以及结果的公开报告。对于每个方面，我们提供一组问题，以便关注可重现性可以得到增强的关键细节。在某些情况下，我们提供了关于如何回答这些问题的具体建议，我们认为这些建议可能在许多领域中都很有用。

与可重现研究相关的标准和工具的多样性很大，我们无法在本章中调查所有可能的选择。我们建议研究人员使用后续章节中的详细案例研究作为灵感，根据您学科的规范和标准来调整选择。

### 自动化和溯源跟踪

自动化研究过程意味着项目中的主要步骤：数据转换、各种处理步骤和计算，以及导致重要推论的可视化步骤，都被编码在软件中，并以可靠且机械化的方式记录下来，以便可靠地复制。换句话说，文章中出现的结论和插图是一组计算例程或脚本的结果，其他人可以检查并重新运行以重现这些结果。

要评估项目中自动化的充分性，可以提出以下问题：

+   所有对推断结果至关重要的图表/计算是否可以通过单击一个按钮进行再现？如果不能通过单击一个按钮，是否可以通过相当小的努力来实现这些？实现此目标的一种方法是编写软件脚本，这些脚本体现了分析中的每一步，直到图表的创建和计算的导出。在评估中，您可以询问：是否可能指出生成每个计算和数据可视化的软件脚本（或脚本）？是否可以通过相当少的努力来运行这些脚本？

+   另一组问题涉及到前一个问题中计算的起点：运行这些脚本的起始点是什么？这些脚本的计算需要什么样的设置步骤？如果设置包括对数据的手动处理，或者对计算环境的繁琐设置，这将影响研究的可重复性。

这些标准背后的主要问题是另一个研究人员首先重现研究项目的结果，然后进一步构建这些结果将会有多困难。因为研究很难，并且错误是普遍存在的（Donoho 及其同事在这个背景下指出的一个观点（2008 年）），第一个从自动化中受益的往往是进行原始研究的研究人员，当他们追踪和消除错误时。

资源追踪与自动化（请参见术语表以了解定义）密切相关。它要求跟踪和记录从原始数据到结论的完整计算事件链。在实施自动化的情况下，可以通过相当少的努力来实现和执行资源追踪。

当涉及到大数据集和复杂分析时，某些处理步骤可能需要消耗比合理要求的重复执行更多的时间和计算资源。在这些情况下，一些其他形式的资源追踪可能有助于增强可重复性，即使没有完全自动化的处理管道。这里评估的项目有：

+   如果软件用于（预）处理数据，那么该软件是否被正确描述？这包括记录所使用软件的版本，以及作为该软件输入的参数设置的文档。

+   如果查询了数据库，是否完全记录了查询？访问日期是否记录？

+   数据清理的脚本是否包含在研究材料中，并且是否包含评论来解释有关缺失数据和丢弃数据的关键决策？

资源追踪的另一个方面是跟踪软件的不同版本，并记录软件的演变，包括清晰地界定用于支持特定科学发现的软件版本。这可以通过提出以下问题来评估：

+   软件的演变是否通过公开可访问的版本控制系统进行检查？对于贡献到特定发现的版本，在版本控制历史中是否清晰标记？

### 软件和数据的可用性

数据和软件的公开可用性是计算可重现性的关键组成部分。为了便于评估，我们建议研究人员考虑以下一系列问题。

#### 数据的可用性

+   数据是否通过公开可访问的数据库提供？通常数据通过互联网共享。在这里，我们可能会问关于网址的长期可靠性：手稿中提到的网址是否永久可靠地分配给数据集？持久性网址的一个例子是数字对象标识符（DOI）。一些主要的存储库为数据集提供这些（例如，[Figshare](http://www.figshare.com)）。通过持久性网址访问的数据集相对于使用单独维护的网站（例如实验室组网站或研究人员的个人网站）提高了研究的可重复性。这是因为当单独维护的网站随着时间的推移更改其地址或结构时，先前发布的网址可能不再起作用。在许多学术机构中，由图书馆维护提供持久性网址的数据存储库。这些数据存储库为研究数据的长期引用、访问和重用提供了安全环境。

+   数据是否以常用且有文档记录的文件格式共享？对于表格数据，基于纯文本的开放文件格式，如 CSV（逗号分隔值）或 TSV（制表符分隔值）经常被使用。文本格式的主要优点在于其简单和透明性。另一方面，它们存在着数值精度损失、相对较大以及解析可能仍然困难的问题。在可用的情况下，应优先选择强类型的二进制格式。例如，多维数组数据可以存储在诸如[HDF5](http://www.hdfgroup.org/HDF5/)之类的格式中。此外，还有一些开放数据格式是在特定研究领域中开发的，用于正确存储与该研究领域的数据分析相关的数据和元数据。例如，天文数据的 FITS 数据格式（Wells，Greisen 和 Harten，1981），以及医学成像数据的 NIFTI 和 DICOM 文件格式（Larobina＆Murino，2014）。

私有文件格式对于可重现性是有问题的，因为它们可能由于知识产权限制、过时或不兼容而无法在未来的计算机系统上使用。然而，我们仍然可以问：如果开放格式不合适，是否提供了软件以便以合理的最小努力将数据读入计算机内存？

+   如果存在社区标准，文件是否以符合这些标准的方式布局在共享数据库中？例如，对于神经影像数据，文件布局是否遵循大脑成像数据结构（Gorgolewski 等，2016）格式？

+   如果数据有更新，不同版本的数据是否清晰标示？如果数据在您的分析中被处理，原始数据是否可用？

+   是否提供了足够的元数据？元数据的类型和数量因研究领域而异，但最低限度的集合可能包括研究标题、作者姓名、收集方法和测量变量的描述、日期和许可证。

+   如果数据不直接可用，例如如果数据过大以致于不便分享，或者受到与隐私问题相关的限制，那么您是否提供了获取等效数据的充分说明？例如，用于获取原始数据的实验方案是否足够详细？

#### 软件的可用性

+   软件是否可下载并安装？软件也可以存储在发行持久 URL 的存储库中，就像数据集一样。这可以提高其可访问性的持久性。

+   软件是否可以轻松安装在不同的平台上？如果使用了脚本语言如 Python 或 R，则共享源代码而不是特定于平台的编译后的二进制文件对于可重复性更好。

+   软件是否有使用条件？例如，许可费用，限制学术或非商业使用等。

+   源代码是否可供检查？

+   源代码的完整历史是否可通过公开可用的版本历史进行检查？

+   软件的依赖关系（硬件和软件）是否被正确描述了？这些依赖关系是否只需要合理的最小努力来获取和使用？例如，如果一个研究项目需要使用专门的硬件，那么它将更难以复现。如果它依赖于昂贵的商业软件，同样如此。在通用硬件上使用开源软件依赖项并不总是可能的，但是在可能的情况下选择使用这些软件会增加可复现性。

#### 软件文档

软件文档是消除重复使用障碍的另一个因素。研究存储库可以添加几种形式的文档，每种文档都可以增加可重复性。相关问题包括：

+   软件是否包含 README 文件？这提供了有关软件目的、使用方法和联系软件作者的信息（详见下文）。

+   是否有任何功能/模块文档？这些文档详细解释了代码的不同部分，包括构成代码的模块的结构；函数的输入和输出；对象的方法和属性等。

+   是否有任何叙事文档？这解释了软件的各个部分是如何相互配合的；叙事文档还可能解释软件在不同情况下应如何安装和配置，并且可以解释事物应以何种顺序执行。

+   是否有使用示例？这对科学计算特别重要，使用示例演示了可以使用软件进行的转换、分析管道和可视化的类型，并为使用软件进行新探索提供了起点。允许例子作为编译文档的一部分被定期运行的系统特别有用，因为当代码更新时，它们会自动更新。作为 PyMVPA 软件库的一部分最初开发的这样一个系统（Hanke 等人，2009）已被许多其他科学 Python 库广泛采用和进一步开发，包括 scikit-image（Van Der Walt 等人，2014）和 scikit-learn（Pedregosa 等人，2011），现在已成为[自己的软件项目](http://sphinx-gallery.readthedocs.io)。

#### 软件工程

尽管并非所有科学软件都需要应用严格的软件工程实践，但使用这些实践可以增加软件的可重现性和长期可持续性，并能扩展软件以处理工作的扩展。虽然对这些实践的全面实施对于较小的项目可能具有挑战性，但意识到它们旨在解决的问题可以引导在软件开发过程的其他领域采用更好的实践。以下是评估计算研究代码库软件工程的几条指南。

软件测试是一种实践，它自动化检查代码的较小单元，除了并支持上述完整管道的自动化外（有关软件测试的详细定义和类型学，请参见术语表）。用于评估代码测试的问题包括：

+   是否有大量的代码被自动测试覆盖，以验证软件是否正常运行且相对无错误？分析软件通常是为了处理数据分析中常见的情况而开发的，并且通常隐含地包含了关于这些常见情况的假设。然而，数据中可能会出现一些不寻常的情况（也称为“边缘情况”或“极端情况”），软件在这些情况下产生正确的结果非常重要。因此，人们可能会问：除了常见情况外，是否还涵盖了边缘情况？

+   是否设置了持续集成系统来验证软件安装机制并运行完整的测试？该系统是否定期更新软件依赖项，以便软件可以正确运行在这些依赖项的新版本上？该系统是否设置为在向后兼容的情况下维护与这些依赖项的旧版本的兼容性，以支持相关的开发工作？

进一步的开源和软件工程实践可以帮助支持用户社区。这些包括：

+   [语义化版本控制](https://semver.org/) 是一种用于沟通软件开发情况并允许其他人依赖它的方式。软件是否定期按照语义化版本控制方案发布？发布是否广泛地向用户社区通告？存在标准安装渠道时，比如包管理器（例如 apt-get、pip）和仓库（例如 CRAN、PyPi），新版本的软件是否通过这些机制提供给用户？

+   软件中是否有报告和跟踪错误的机制？当错误被修复时，这些修复是否在发布公告中报告？

+   虽然私人通信可用于帮助软件的个别用户，但这些通信方式不太适用于更大规模的用户群体。要求这种私人通信会为用户再现工作设置障碍。为软件用户建立公共沟通渠道以提问软件使用问题增加了再现性。这些渠道可以包括公共邮件列表、论坛和/或聊天室。

#### 版权问题和其他数据负担

创意工作，比如研究，受版权法保护。虽然这些法律保护创作者和研究人员的权利，但它们也会阻碍其工作的分发和验证。没有许可证或版权信息的工作仍受版权法保护。这阻止了他人对工作的任何再现或构建的权利。因此，适当的许可证的应用对增加工作的再现性至关重要。

*数据和版权.* 虽然版权法通常不保护事实或数据，但它确实保护用于选择输入数据库或编译的数据的创造性行为。为了消除有关数据版权状态的疑虑，需要选择一种许可证。为了评估可再现性，可以询问：

+   如果数据对他人开放访问，它是否以允许他们使用的许可证发布？

+   许可证是否足够自由，以允许其他人构建并扩展工作？

允许数据提供者控制数据潜在用户对数据的使用的一组许可证是[知识共享许可证](https://creativecommons.org/)，以及专门设计用于数据共享的开放许可证（Miller，Styles 和 Heath，2008）。Stodden（2009）建议对数据使用 CC-0（公共领域）许可证，以实现最大的重复使用灵活性。

*软件和版权* 相同的问题也适用于与软件和版权相关的问题，稍有不同：当免费共享软件的源代码时，研究人员被鼓励提供一个许可证，明确规定了该代码可以在何种条件下使用，而不侵犯作者的版权。允许任何人使用软件、修改它、构建它、将其包含在其他软件包中并扩展它的许可证有助于可重复性。

宽松的软件许可证将允许上述所有操作，而限制最少（例如，BSD 许可证，MIT 许可证）。BSD 许可证在包括一个特定条款，防止未来衍生品中使用软件作者的姓名方面是独特的，这保护了作者免受其软件未经授权使用的负面影响。

Copyleft 许可证允许分发和修改软件，但要求它们在相同的许可证下发布。例如，如果原始软件是开源和免费的，那么所有的副本和衍生品都应该是开源和免费的。这种许可证明确限制了软件在专有应用程序中的使用。例如，在学术背景下使用 Copyleft 许可证开发的软件不能作为商业软件包的一部分。GNU 通用公共许可证（GPL）是流行的 Copyleft 许可证的一个例子。

+   软件是否有开源许可证？

+   这个许可证是否足够宽松，以允许他人使用软件、重现结果并扩展它们？

#### 专有信息和软件

通常作者可能由于外部限制而不提供数据或软件。我们可能会问以下问题来评估这些限制可能对可重复性产生的影响：

+   数据的可用性和使用是否受到专有、隐私或道德限制的影响？（例如，由于存在敏感个人信息或客户活动记录。）。

+   是否存在贸易限制或国家安全问题，禁止数据的开放分发？

+   软件是否闭源或由于资金监管（政府限制、工业赞助商要求等）而受到限制？

尽管这些条件显然限制了可能的可复制性程度，但有改进这类研究可复制性的选项。例如，有时可以提供模拟数据集，该数据集模仿了真实数据集的关键属性。在软件受限的情况下，鼓励作者提供足够的关于关键算法的信息，以便未来的研究可以在开放可用的数据上使用更容易获得的软件进行执行。

### 开放报告结果

重现研究的关键在于通过报告、论文、实验室笔记等提供关于其执行的足够细节。研究人员通常旨在将其结果发表在期刊（或会议论文集）上，以广泛传播他们的发现。然而，期刊的选择可能会影响其研究结果的可用性和可访问性。开放获取期刊允许读者访问文章（通常在线），而无需订阅或付费。尽管开放获取可以采用多种形式，但开放获取出版有两种常见类型：

*绿色通道* - 期刊向读者收取订阅费以获取其内容的访问权限，但允许作者在电子打印网站（如[arXiv](http://arxiv.org)、[EPrints Archive](http://www.eprints.org/)）、自己的网站或机构知识库上发布其文章的版本（预印本/后印本）。

*金色通道* - 期刊不向读者收取任何费用，并在发表时提供文章的免费在线版本。通常作者需要支付文章处理费以使读者可以免费访问。

显然，金色通道期刊为文章提供了最简单和最可靠的访问方式。然而，由于金色开放获取期刊和文章没有订阅费用来支付出版费用，因此作者必须支付费用。通常，每篇文章的金额超过一千美元。作者应该向其机构查询是否提供资金来支付此类费用。作为一种妥协，期刊有时会对开放获取设置禁令（延迟开放获取），即在一段时间内无法免费访问文章，之后要么期刊自动使文章可用，要么作者被允许进行自我归档。

绿色开放获取是一种吸引人的方法，可以使文章向读者和作者都是经济实惠的。根据 2009 年一项对随机抽样文章的研究（Björk、Welling、Laakso、Majlender 和 Guðnason，2010），大约有 20%的文章是免费可访问的（9.8%在出版商网站上，11.9%在其他地方通过搜索）。一项更大规模的最新研究（Archambault 等人，2013）表明，2008 年至 2011 年间收录在 Scopus 中的论文中，到 2012 年底有 43%是免费可获取的。还有研究表明，可获取文章的比例有大幅增长。然而，仍然有很多文章已经获得了开放获取的许可，但它们尚未进行自我归档。因此，对作者来说理解期刊的出版政策并利用可用资源（包括其领域、机构以及其他资源）使他们的工作对广泛的读者群体可访问是很重要的。许多研究密集型大学通常通过图书馆为研究人员提供服务，帮助他们自我归档他们的出版物。

在研究的不同阶段（甚至在最终结果可用之前），有许多其他在线分享研究的方法。在研究中测试的假设进行预先注册可以防止过于灵活的分析实践和 HARKing（即在结果已知之后进行假设（Kerr，1998）），这会降低所报告的结果的可重复性。通过电子实验室笔记、维基页面、演示幻灯片、博客文章、技术报告、预印本等方式可以定期公开更新。分享进展可以快速传播思想，便于合作，及早发现和纠正缺陷。将初步结果和补充材料存储在集中式存储库（预注册注册表、公共版本控制存储库、机构报告）中，有可能提高作品的可发现性和可用性寿命。在评估出版解决方案时，研究人员可以提出一些重要的问题：

+   这个电子出版平台将在 2 年后还可用吗？在 5 年后呢？更长时间呢？

+   通过简单的网络搜索，能否找到与出版物和相关资料相关的链接？

考虑这些解决方案的可持续性和易于访问性是决策过程中的一个重要因素，可以提高研究的可重复性。也有经验证据表明，开放获取的出版有助于促进科学发现的下游使用，这可以通过约 10%的引用增加来证明（Hajjem、Harnad 和 Gingras，2006）（也请参阅[`opcit.eprints.org/oacitation-biblio.html`](http://opcit.eprints.org/oacitation-biblio.html)）。

### 结论

本章试图概述决定研究项目在计算上可再现程度的因素。我们调查了三个不同方面，可在其中评估再现性：自动化和溯源跟踪，软件和数据的可用性，以及结果的公开报告。针对每个主题，我们提供了一组研究人员应考虑的问题，以激发关于如何改进计算再现性的讨论。还有许多其他问题可以提出，但我们尽力限制在与改进再现性的关键障碍相关的问题上。我们观察到这些问题是使我们自己的工作更具再现性的关键点，并评估同行的工作。

本章的一个关键主题是再现性有许多程度。计算再现性存在于一个长谱系上，从完全不可再现的研究到完全的计算再现性，数据、软件和结果都可供审查、使用和进一步探索。我们希望通过提出这些问题并讨论一些选项，研究人员可以找到方法将他们的工作沿着谱系稍微推进，朝着改进再现性的方向。我们建议采取务实的方法来评估和改进再现性，从项目到项目逐步改进，关注领域的变化规范和数据格式、元数据、存储库等的不断演变的标准和规范。随着时间的推移，我们在这里提出的一些具体建议可能会过时或被更好的选项取代。然而，我们关注的一般原则，以及我们为再现性提出的问题，可能会超越技术细节，成为未来评估再现性的有用提示。

### 参考文献

Archambault, E., Amyot, D., Deschamps, P., Nicol, A., Rebout, L., & Roberge, G. (2013). *欧洲和世界水平上开放获取同行评审论文的比例—2004-2011 年*。Science-Metrix。检索自[`www.science-metrix.com/pdf/SM_EC_OA_Availability_2004-2011.pdf`](http://www.science-metrix.com/pdf/SM_EC_OA_Availability_2004-2011.pdf)

Baker, M. (2016a). 1500 名科学家揭开再现性的面纱。*自然*, *533*(7604), 452–454。

Baker, M. (2016b). 混淆的含义阻碍了解决再现性危机的努力。*自然新闻*。[`doi.org/doi:10.1038/nature.2016.20076`](http://doi.org/doi:10.1038/nature.2016.20076)

Björk, B.-C., Welling, P., Laakso, M., Majlender, H., P., & Guðnason, G. (2010). 科学期刊文献的开放获取：2009 年情况。*PLoS ONE*, *5*(6). [`doi.org/10.1371/journal.pone.0011273`](http://doi.org/10.1371/journal.pone.0011273)

Cartwright, N. (1991). 可复制性、再现性和稳健性：对哈里·柯林斯的评论。*政治经济史*, *23*(1), 143–155。期刊文章。

Casadevall, A., & Fang, F. C. (2010). 可复制的科学。*Infection and Immunity*，*78*(12)，4972–4975。[`doi.org/10.1128/IAI.00908-10`](http://doi.org/10.1128/IAI.00908-10)

Claerbout, J. F., & Karrenfach, M. (无日期). 电子文档赋予可复制研究新的意义。会议论文，勘探地球物理学会。

Collins, H. M. (1984). 科学家何时更愿意改变他们的实验？*Studies in History and Philosophy of Science Part A*，*15*(2)，169–174。期刊文章。

Donoho, D. L., Maleki, A., Rahman, I., Shahram, M., & Stodden, V. (2008). *计算谐波分析中可复制研究的 15 年*。斯坦福大学统计系。

Drummond, C. (2009). 可复制性不等于可重复性：也不是好的科学。*Proc. Eval. Methods Mach. Learn. Workshop 26th ICML, Montreal, Quebec, Canada*。从[`cogprints.org/7691/7/icmlws09.pdf`](http://cogprints.org/7691/7/icmlws09.pdf)检索。

Easterbrook, S. M. (2014). 开放科学的开源代码？*Nature Geosci*，*7*(11)，779–781。期刊文章。[`doi.org/10.1038/ngeo2283`](http://doi.org/10.1038/ngeo2283)

Franklin, A., & Howson, C. (1984). 为什么科学家更喜欢改变他们的实验？*Studies in History and Philosophy of Science Part A*，*15*(1)，51–62。期刊文章。

Goodman, S. N., Fanelli, D., & Ioannidis, J. P. A. (2016). 研究可复制性意味着什么？*Science Translational Medicine*，*8*(341)，341ps12–341ps12。[`doi.org/10.1126/scitranslmed.aaf5027`](http://doi.org/10.1126/scitranslmed.aaf5027)

Gorgolewski, K. J., Auer, T., Calhoun, V. D., Craddock, R. C., Das, S., Duff, E. P.等。 (2016). 大脑成像数据结构：组织和描述神经影像实验输出的标准。*bioRxiv*。[`doi.org/10.1101/034561`](http://doi.org/10.1101/034561)

Hajjem, C., Harnad, S., & Gingras, Y. (2006). 十年跨学科比较开放获取的增长及其如何增加研究引用影响。*arXiv Preprint Cs/0606079*。

Hanke, M., Halchenko, Y. O., Sederberg, P. B., Hanson, S. J., Haxby, J. V., & Pollmann, S. (2009). PyMVPA：用于 fMRI 数据的多变量模式分析的 Python 工具箱。*神经信息学*，*7*(1)，37–53。

Kerr, N. L. (1998). HARKing：结果知晓后的假设。*Personality and Social Psychology Review*，*2*(3)，196–217。

Larobina, M., & Murino, L. (2014). 医学图像文件格式。*数字成像杂志*，*27*(2)，200–206。

Miller, P., Styles, R., & Heath, T. (2008). 开放数据共享，一个开放数据许可证。*LDOW*，*369*。

Pedregosa, F., Varoquaux, G., Gramfort, A., Michel, V., Thirion, B., Grisel, O.等。 (2011). Scikit-learn：Python 中的机器学习。*The Journal of Machine Learning Research*，*12*，2825–2830。

Stodden, V. (2009). 促进可复制研究：科学创新的开放许可。*International Journal of Communications Law and Policy*，*13*，1–25。

Stodden, V., Borwein, J., & Bailey, D. H. (2013). 将默认设置为可重现性。*计算科学研究。SIAM 新闻*, *46*, 4–6.

Stodden, V., Leisch, F., & Peng, R. D. (2014). *实施可重现性研究*。CRC Press.

Van Der Walt, S., Schönberger, J. L., Nunez-Iglesias, J., Boulogne, F., Warner, J. D., Yager, N., … Yu, T. (2014). Scikit-image: Python 中的图像处理。*PeerJ*, *2*, e453.

Wells, D. C., Greisen, E. W., & Harten, R. H. (1981). FITS - 一种灵活的图像传输系统, *44*, 363.

## 3\. 提出和细化问题

进行数据分析需要相当多的思考，我们认为当你完成了一次良好的数据分析时，你花在思考上的时间比实际操作要多。思考始于你甚至还没有看到数据集之前，精心考虑你的问题是非常值得的。这一点无法过分强调，因为许多数据分析的“致命”陷阱都可以通过耗费精力来确保问题准确而避免。在本章中，我们将讨论一个好问题的特征，可以提出的问题类型，以及如何应用迭代的环状过程来提出和细化你的问题，以便当你开始查看数据时，你有一个明确、可回答的问题。

### 3.1 问题类型

在我们深入阐述问题之前，考虑一下不同类型的问题会很有帮助。有六种基本类型的问题，许多后续讨论来自罗杰和[杰夫·利克](http://jtleek.com)在*Science*杂志上发表的一篇[论文](http://www.sciencemag.org/content/347/6228/1314.short)。了解你所提出的问题类型可能是你能够确保最终对结果进行正确解释的最基本步骤。这六种类型的问题是：

1.  描述性

1.  探索性

1.  推论性

1.  预测性

1.  因果性

1.  机械性

你所提出的问题类型直接影响着你对结果的解释方式。

一个*描述性*问题是指寻求总结一组数据特征的问题。例如，确定男性的比例、每天新鲜水果和蔬菜摄入量的平均数，或从一组个体收集的数据中病毒性疾病的频率。结果本身没有解释，因为结果是一个事实，是你所处理的数据集的属性。

一个*探索性*问题是指你分析数据以查看是否存在模式、趋势或变量之间的关系。这些类型的分析也被称为“假设生成”分析，因为与推论性、因果性或机械性问题需要测试假设不同，你在寻找支持提出假设的模式。如果你一开始有一个大致的想法，认为饮食与病毒性疾病在某种程度上有关联，你可以通过分析各种饮食因素和病毒性疾病之间的关系来探索这个想法。在探索性分析中，你发现那些食用含有某些食物的饮食的人患病病毒性疾病较少，因此你提出假设：在成年人中，每天至少食用 5 份新鲜水果和蔬菜与每年较少的病毒性疾病有关。

一个*推断*问题将是将这个假设重新表述为一个问题，并通过分析另一组数据来回答，这个例子中，是美国成年人的代表性样本。通过分析这个不同的数据集，您既确定了您在探索性分析中观察到的关联是否在不同的样本中保持，并且它是否在代表美国成年人的样本中保持，这表明该关联适用于所有美国成年人。换句话说，您将能够从您对代表性样本进行的分析中推断出在美国成年人群中平均为真的内容。

一个*预测*问题将是一个您询问在接下来的一年中会吃高含新鲜水果和蔬菜饮食的人的类型的问题。在这种类型的问题中，您对导致某人吃某种饮食的原因不太感兴趣，只是预测某人是否会吃这种特定的饮食。例如，更高的收入可能是最终预测因子之一，您可能不知道（甚至不关心）为什么收入较高的人更有可能吃高含新鲜水果和蔬菜的饮食，但最重要的是收入是一个预测这种行为的因素。

虽然推断性问题可能告诉我们吃某种类型的食物的人 tend to 有较少的病毒性疾病，但这个问题的答案并没有告诉我们吃这些食物是否会导致病毒性疾病数量减少，这是一个*因果*问题。因果问题询问改变一个因素是否会平均在人群中改变另一个因素。有时，数据收集的基础设计默认允许您问的问题是因果性的。其中一个例子是在随机试验的背景下收集的数据，在这种试验中，人们被随机分配到吃高含新鲜水果和蔬菜的饮食或低含新鲜水果和蔬菜的饮食中。在其他情况下，即使您的数据不是来自随机试验，您也可以采取旨在回答因果问题的分析方法。

最后，到目前为止描述的所有问题都不会给出一个答案，告诉我们，饮食是否确实导致病毒性疾病数量减少，*饮食*如何导致病毒性疾病数量减少。问一个高含新鲜水果和蔬菜的饮食如何减少病毒性疾病数量的问题将是一个*机制*问题。

关于问题类型的一些其他重要要点。首先，出于必要性，许多数据分析回答了多种类型的问题。例如，如果数据分析旨在回答推断性问题，则在回答推断性问题的过程中还必须回答描述性和探索性问题。继续我们的饮食和病毒性疾病的示例，你不能直接跳到一个关于饮食高于新鲜水果和蔬菜与病毒性疾病数量之间关系的统计模型，而没有确定这种类型饮食和病毒性疾病的频率及其在这个样本中彼此之间的关系。第二点是，您所提出的问题类型部分取决于您可用的数据（除非您打算进行研究并收集所需的数据进行分析）。例如，您可能想询问有关饮食和病毒性疾病的因果问题，以了解是否吃饮食高于新鲜水果和蔬菜是否会导致病毒性疾病数量减少，而回答这个因果问题的最佳数据类型是人们的饮食从高于新鲜水果和蔬菜到不高于新鲜水果和蔬菜，或者相反。如果这种类型的数据集不存在，那么您能做的最好的事情可能是将因果分析方法应用于观察数据，或者改为回答有关饮食和病毒性疾病的推断性问题。

### 3.2 将 Epicycle 应用于陈述和调整您的问题

现在您可以使用关于问题类型和好问题特征的信息作为调整问题的指南。为了实现这一点，您可以通过以下 3 个步骤迭代：

1.  确定您对问题的期望

1.  收集关于您的问题的信息

1.  确定您的期望是否与您收集的信息相匹配，然后根据您收集的信息调整您的问题（或期望），如果您的期望与您收集的信息不匹配

### 3.3 一个好问题的特征

对于数据分析的一个好问题有五个关键特征，从基本特征，即问题不应该已经被回答，到更抽象的特征，即问题的每个可能答案都应有一个单一解释且有意义。我们将在下面更详细地讨论如何评估这一点。

作为起点，问题应该对你的受众**感兴趣**，受众的身份取决于你处理数据的背景和环境。如果你在学术界工作，受众可能是你的合作者、科学界、政府监管机构、资助方和/或公众。如果你在一家初创公司工作，你的受众是你的老板、公司领导层和投资者。例如，回答室外颗粒物污染是否与儿童发育问题相关的问题可能会引起空气污染监管者的兴趣，但可能不会引起一家杂货连锁店的兴趣。另一方面，回答当意大利辣香肠与披萨酱和披萨皮一起展示时，销售额是否更高，还是与其他包装肉一起展示时销售额更高，这对一家杂货连锁店来说是有兴趣的，但对其他行业的人来说则不是。

你还应该检查问题是否已经有了**答案**。随着数据的爆炸性增长、越来越多的公开数据以及看似无穷无尽的科学文献和其他资源，发现你感兴趣的问题已经有了答案并不罕见。一些研究和与专家的讨论可以帮助搞清楚这一点，而且也可能会有所帮助，因为即使你心中的具体问题没有答案，相关的问题可能已经有了答案，这些相关问题的答案有助于确定你是否以及如何处理你的具体问题。

问题也应该源自一个**合理的**框架。换句话说，关于意大利辣香肠销售额与其在商店内放置位置之间关系的问题是一个合理的问题，因为购买披萨配料的顾客比其他顾客更有可能对意大利辣香肠感兴趣，并且如果他们在选择其他披萨配料时看到它，他们更有可能购买。一个不太合理的问题可能是意大利辣香肠销售是否与酸奶销售相关，除非你有一些先前的知识表明它们应该相关。

如果你提出的问题的框架不合理，你很可能得到一个难以解释或信任的答案。在意大利辣香肠-酸奶问题中，如果你发现它们相关，那么结果本身会引发许多问题：它真的正确吗？这些东西为什么相关-是否有另一个解释？等等。你可以确保你的问题基于一个合理的框架，通过使用你对主题领域的知识并进行一些研究，这两者结合起来可以在帮助你确定你的问题是否基于一个合理的框架方面走得更远。

当然，问题也应该是**可回答的**。虽然这可能不需要说明，但值得指出的是，一些最好的问题是无法回答的 - 要么是因为数据不存在，要么是因为缺乏资源、可行性或伦理问题而无法收集数据。例如，大脑中某些细胞功能存在缺陷导致自闭症是很有可能的，但无法进行脑活检以收集活细胞进行研究，这是回答这个问题所需的。

**特定性** 也是一个好问题的重要特征。一个一般性问题的例子是：吃更健康的饮食对你更好吗？朝着特定性的方向努力会使你的问题更加精炼，并直接指导你在开始查看数据时应采取的步骤。在问自己“更健康”的饮食是什么意思，以及当你说某物对你更好时，一个更具体的问题就会浮现出来。增加特定性的过程应该导致一个最终的、精炼的问题，比如：“每天至少吃 5 份新鲜水果和蔬菜是否会导致较少的上呼吸道感染（感冒）？”有了这种特定性，你的行动计划就更加清晰，数据分析结束时得到的答案也更具可解释性，因为你要么推荐，要么不推荐每天至少吃 5 份新鲜水果和蔬菜作为预防上呼吸道感染的手段。

### 3.4 将问题转化为数据问题

在制定问题时需要考虑的另一个方面是将其转化为数据问题时会发生什么。每个问题都必须作为导致结果的数据分析来操作化。暂停思考数据分析的结果会是什么样子，以及它们可能如何被解释是很重要的，因为这可以防止你浪费大量时间进行无法解释结果的分析。虽然我们将在整本书中讨论许多导致可解释和有意义结果的问题的例子，但也许最容易的方法是首先考虑哪些问题*不*会导致可解释的答案。

不符合这一标准的典型问题类型是使用不恰当的数据的问题。例如，您的问题可能是服用维生素 D 补充剂是否与头痛次数减少有关，并且您计划通过使用一个人服用止痛药的次数作为他们头痛次数的标记来回答这个问题。您可能会发现服用维生素 D 补充剂与服用更少的止痛药有关，但是对于这个结果的解释并不清楚。实际上，可能是服用维生素 D 补充剂的人也倾向于不太可能服用其他非处方药，仅仅是因为他们“避免药物”，而不是因为他们实际上头痛次数更少。也可能是因为他们减少了止痛药的使用，因为他们关节疼痛较少，或者其他类型的疼痛较少，而不是头痛较少。当然，另一种解释是，他们的确头痛较少，但问题是您无法确定这是否是正确的解释，还是其他解释之一是正确的。实质上，这个问题的问题在于对于一个可能的答案，存在多种解释。当您使用的至少有一个变量（在本例中是止痛药的使用）不是您真正关心的概念（在本例中是头痛）的一个好的衡量时，会出现这种多种解释的情况。为了避免这个问题，您将希望确保用于回答您的问题的数据提供对您问题的要求因素的合理具体的度量。

干扰对结果的解释的相关问题是混杂。混杂是一个潜在的问题，当您的问题询问因素之间的关系，例如服用维生素 D 和头痛频率时。对混杂概念的简要描述是，当您在问题中并非必然考虑的因素与您感兴趣的暴露（在本例中是服用维生素 D 补充剂）和您感兴趣的结果（服用止痛药）相关时，混杂就存在。例如，收入可能是一个混杂因素，因为它可能与服用维生素 D 补充剂和头痛频率有关，因为收入较高的人可能更有可能服用补充剂，而且更不可能患慢性健康问题，如头痛。一般来说，只要您可以获得收入数据，您就可以调整这个混杂因素，并减少对您问题的答案的可能解释的数量。当您完善您的问题时，请花些时间识别潜在的混杂因素，并考虑您的数据集是否包含有关这些潜在混杂因素的信息。

当使用不适当的数据时可能出现的另一种问题是结果不可解释，因为数据收集的基本方式导致了偏倚的结果。例如，想象一下，您正在使用一份由曾经生过孩子的女性调查创建的数据集。该调查包括有关她们的孩子是否患有自闭症以及她们在怀孕期间是否报告吃过寿司的信息，您发现吃寿司与孩子患有自闭症之间存在关联。然而，由于有孩子患有健康问题的女性会对怀孕期间发生的事情，比如吃生鱼，有不同的回忆，所以观察到的寿司暴露与自闭症之间的关联可能只是母亲在她有孩子患有健康问题时更倾向于回忆怀孕期间事件的表现。这是一个回忆偏差的例子，但是可能发生许多种类型的偏差。

在完善您的问题时需要了解和考虑的另一个主要偏差是选择偏差，当你分析的数据是以一种方式收集的，以至于使得具有上述特征的人的比例超过了总体人口的比例时，就会发生选择偏差。如果一项研究宣传称它是关于孕期自闭症和饮食的研究，那么那些既吃生鱼又有孩子患有自闭症的女性更有可能回答调查问卷，而不是那些只有其中一种情况或者两种情况都没有的女性。这种情况会导致您对母亲在怀孕期间摄入寿司与其孩子患自闭症风险的问题得到偏见的答案。一个很好的经验法则是，如果您正在考察两个因素之间的关系，如果由于人群的选择方式或者一个人在回答调查时可能回忆起过去的方式而更有可能观察到具有这两种因素的个体，则偏差可能是一个问题。在接下来的章节中（推理：入门和解释您的结果）将会更多地讨论偏差，但考虑其对数据分析的影响的最佳时机是在您确定要回答的问题并考虑如何用您可获得的数据回答问题时。

### 3.5 案例研究

Joe 在一家生产各种健身追踪设备和应用的公司工作，公司的名字是 Fit on Fleek。Fit on Fleek 的目标是，像许多科技初创公司一样，利用他们从设备用户那里收集的数据来对各种产品进行定向营销。他们想要营销的产品是一款他们刚开发但尚未开始销售的新产品，这是一款睡眠追踪器和应用，可以追踪各种睡眠阶段，如快速眼动睡眠，并提供改善睡眠的建议。这款睡眠追踪器被称为 Sleep on Fleek。

Joe 的老板要求他分析公司对其健康追踪设备和应用的用户所拥有的数据，以确定用于定向 Sleep on Fleek 广告的用户。Fit on Fleek 从每位客户那里收集到以下数据：基本人口统计信息，每天步行的步数，每天爬楼梯的次数，每天久坐清醒时间，每天警觉时间，每天昏昏欲睡时间，以及每天睡眠时间（但不包括睡眠追踪器会追踪的更详细信息）。

尽管 Joe 心中有一个目标，是从与老板的讨论中得出的，他也知道 Fit on Fleek 数据库中有哪些类型的数据，但他还没有一个问题。这种情况，Joe 被给定了一个目标，但没有一个问题，是很常见的，所以 Joe 的第一个任务是将目标转化为一个问题，这将需要与老板进行一些来回沟通。在数据分析项目过程中进行的非正式沟通方式，在沟通章节中有详细介绍。经过几次讨论，Joe 确定了以下问题：“哪些 Fit on Fleek 用户睡眠不足？”他和老板一致认为，最有可能对购买 Sleep on Fleek 设备和应用感兴趣的客户是那些似乎有睡眠问题的人，而最容易追踪的问题，也可能是最常见的问题是睡眠不足。

你可能会认为，既然 Joe 现在有了一个问题，他应该开始下载数据并开始进行探索性分析，但 Joe 仍然需要做一些工作来完善问题。Joe 需要解决的两个主要任务是：（1）思考他的问题是否符合一个好问题的特征，或者不符合；（2）确定他所提出的问题类型，以便在完成数据分析后对可以（和不可以）得出的结论有一个良好的理解。

Joe 审查了一个好问题的特征，他期望他的问题具有所有这些特征：-有趣-尚未得到答案-基于一个合理的框架-可回答-具体

他分析结束后得到的答案（当他将问题转化为数据问题时）也应该是可解释的。

然后，他思考了他对这个问题的了解，在他的判断中，这个问题是有趣的，因为他的老板表达了兴趣。

他还知道这个问题以前肯定没有被回答过，因为他的老板表示没有，并且公司以前的数据分析回顾没有发现以前有针对这个问题设计的分析。

接下来，他评估问题是否基于一个合理的框架。问题“哪些 Fit on Fleek 用户睡眠不足？”似乎是建立在合理性的基础上的，因为人们普遍认为，睡眠不足的人会有兴趣尝试通过跟踪来改善他们的睡眠。然而，Joe 怀疑睡眠持续时间是否是判断一个人是否认为自己的睡眠不足的最佳标志。他知道一些人每晚只睡 5 个小时，但他们似乎对自己的睡眠感到满意。Joe 联系了一个睡眠医学专家，了解到判断某人是否受到睡眠不足或睡眠质量不佳影响的更好的标志是白天的昏昏欲睡。事实证明，他最初认为问题建立在合理框架上的期望与他与内容专家交谈时获得的信息不符。因此，他修订了问题，使其符合他对合理性的期望，修订后的问题是：哪些 Fit on Fleek 用户白天会昏昏欲睡？

Joe 暂停一下，确保这个问题确实可以用他手头的数据来回答，并确认可以。他还停顿下来考虑问题的具体性。他认为问题很具体，但还是与同事讨论问题以收集更多关于问题具体性的信息。当他提出回答这个问题的想法时，他的同事问了他很多问题，询问问题的各个部分是什么意思：所谓的“哪些用户”是什么意思？这是否意味着：哪些用户有昏昏欲睡的人口统计特征？还是其他什么？“白天昏昏欲睡”是什么意思？这个短语是否意味着任何一天都有昏昏欲睡？还是至少在至少一定数量的天数上持续一定时间的昏昏欲睡？与同事的交谈非常有启发性，并且表明问题并不是很具体。Joe 修订了他的问题，使其现在更加具体：“哪些人口统计和健康特征可以确定出最有可能有慢性昏昏欲睡的用户，慢性昏昏欲睡被定义为至少每隔一天至少有一次昏昏欲睡？”

乔现在开始思考他的问题可能的答案是什么，以及它们是否可解释。乔确定了他分析的两种可能结果：（1）没有特征可以识别出有慢性白天嗜睡的人，或者（2）有一种或多种特征可以识别出有慢性白天嗜睡的人。这两种可能性是可以解释和有意义的。对于第一种情况，乔会得出结论，将睡眠追踪器的广告定位于预测患有慢性白天嗜睡的人是不可能的，而对于第二种情况，他会得出结论，广告的定位是可能的，他会知道选择广告目标人群的特征是什么。

现在乔手上有了一个好问题，在经过迭代的历元周期的三个步骤时，他考虑了他的问题是否符合好问题的各个特征，下一步是让他弄清楚他的问题是什么类型的问题。他进行了一种类似于上面每个特征的过程的思考过程。他开始思考他的问题是一种探索性问题，但是当他回顾探索性问题的描述和例子时，他意识到尽管他将进行的一些分析部分是探索性的，但最终他的问题不仅仅是探索性的，因为它的答案将预测哪些用户可能有慢性白天嗜睡，所以他的问题是一个预测性问题。识别问题类型非常有帮助，因为除了一个好问题之外，他现在知道他需要在分析中使用预测方法，特别是在模型构建阶段（见正式建模章节）。

### 3.6 总结思考

现在，你应该准备好将历元周期的三个步骤应用于阐述和完善问题。如果你是一位经验丰富的数据分析师，那么这个过程的大部分可能会自动进行，以至于你可能并不完全意识到将你引向一个好问题的过程的某些部分。直到你达到这一点，本章可以在你面对开发一个好问题的任务时为你提供有用的资源。在接下来的章节中，我们将讨论现在你手上有了一个好问题之后应该如何处理数据。

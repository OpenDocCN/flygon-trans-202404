# 3  抽象解释中的主题

### 3.1  抽象域

抽象域是一个抽象代数结构，通常作为一个库模块实现（参见**第 5**节），提供了对抽象程序属性和描述程序指令和命令在抽象中的操作效果的抽象属性变换器的描述。抽象域通常是完备格，是幂集的一种抽象[26]。

### 3.2  有限与无限抽象域

第一个无限抽象域（区间的抽象域）是在[21]中介绍的。这个抽象域后来被用来证明，由于 widening，无限抽象域可以导致针对给定编程语言的有效静态分析，这些分析比使用有限抽象域或满足链条件的抽象域的任何其他分析都更精确且同样高效[31]。

### 3.3  在数据流分析中合并所有路径的(MOP)

第一个数据流分析通过比较沿着所有执行路径的抽象的并集（所谓的 MOP¹解）与使用转移函数（即抽象属性变换器）的不动点解来证明其正确性[67]。与将静态分析问题的一个解与另一个解进行比较不同，抽象解释理论引入了正确性/完备性应该根据形式化语义来表达的思想。一个结果是，静态分析算法可以通过近似程序语义来指定和设计。此外，“不动点解”被证明是“MOP 解”的一个抽象。这两种解在分布式抽象解释中相符（其中抽象变换器保持并集）。否则，用于不动点解的抽象域可以被最小地丰富为其*分离完成*，以在完整的抽象域上获得完全的“MOP 解”（在完整的抽象域上）[26]。

### 3.4  标准和收集语义

*收集语义*或*非标准语义*（在[22]的*静态语义*之后）是正式定义了要通过抽象分析分析的程序执行属性的语言的语义。这些程序执行本身由标准语义形式化。例如在[22]中，标准语义是一个操作语义。感兴趣的具体属性是不变性属性，因此收集语义定义了从初始状态到达的可达状态。这个收集语义被表达为使用最强后条件变换器的方程的最小不动点。因此，考虑到的抽象提供了抽象的不变性属性（对可达状态进行了近似）。

### 3.5  Galois 连接

Galois 连接可用于当抽象域始终提供任何具体属性的最精确近似时[26]。事实上，[21,22]中介绍的 Galois 连接是 Évariste Galois 引入的连接的半对偶，因此可以组成（一个抽象的抽象是一个抽象）。等效的表达涉及闭包算子、理想、同余等[26]。存在具体属性的最佳抽象的一个有趣后果是存在最佳/最精确的变换器，这为它们的[自动]设计提供了指导[17]。此外，通过将抽象点抽象为点，静态分析由表达为点形式的抽象语义指定，而静态分析器是计算或过度逼近此点的算法。在没有最佳近似的情况下，存在几种替代的形式化[94]，[30]。

### 3.6 Moore family，闭包算子

如果具体属性和抽象属性之间的对应关系由 Galois 连接给出，则抽象属性在具体属性中的图像是 *Moore family*，这是具体属性的图像由 *closure operator* 给出[26]。通过闭包算子对抽象的抽象进行形式化对于从具体属性的表示中抽象出来是有用的。具体属性的最佳抽象的存在的其他等价形式化包括主理想、完全加入同余等[26]。

### 3.7 Moore completion

如果一个抽象域对于某些具体属性没有最佳近似，那么其 *Moore completion* 就是比原始抽象域更具表达力的最抽象抽象域[26]。这引入了一个 Galois 连接。

### 3.8 Fixpoints

大多数程序属性可以表达为单调或广义性质变换器的 fixpoints，这是一种由抽象保留的属性[26]。这将程序分析简化为 fixpoint 近似，并将验证简化为 fixpoint 检查[22]。

### 3.9 推理规则

大多数（具体和抽象）程序属性也可以使用推理规则来表达，这实际上等同于使用 fixpoints、方程、约束等进行定义[34]。这种观点的优点是将（抽象）语义（或静态分析）的设计与其形式化表示分开。

### 3.10 迭代

构造不动点的标准方法是*迭代*。这可以扩展到超限迭代以证明塔斯基的不动点定理[25]。在实践中，可以使用适当的迭代策略加速不动点计算，将其形式化为混沌/异步迭代[14]。这扩展到高阶[24], [74]。

### 3.11  通过加宽/收窄加速收敛

在无限抽象域中，收敛加速是必需的，其中抽象不动点的迭代计算可能会发散。加宽/收窄及其对偶是通用的方法[22,14]。这扩展到高阶[24,6]。

### 3.12  约束解决

由于塔斯基的定理，不动点可以重新表达为相等或不等式约束，因此静态分析既可以被视为不动点近似，也可以被视为约束解决问题。一些约束解决方法仅是不动点迭代（例如基于集合的分析[35]）。

### 3.13  模块化

程序的静态分析可以分为部分进行[37]。这包括单独的过程内分析[24]。

### 3.14  抽象域组合

抽象的设计可以通过部分进行，选择基本抽象，然后使用抽象域组合器将它们组合起来[26]。这为抽象域设计提供了一个统一的视角[52]。有许多这样的抽象域组合的例子，包括*减少和*、*减少积*和*减少幂*[26]。

### 3.15  细化

将抽象域丰富到能够表达在原始域中无法表达的细化域中的属性。例如*Moore 完成* **Sec. 3.7**、*分区* [15,5,79], [69], *分解完成* [26], [53], *Heyting 完成* [59], *补集* [13]等。

### 3.16  完成

将抽象域细化为足够精确以证明给定规范的最抽象抽象域的方法[26], [93,57,58,104]。

### 3.17  抽象解释的格

通过伽罗华连接对静态分析进行形式化的一个结果是，它们可以根据其相对精度的偏序关系组织成完全格[26]。所有的语义和分析都存在于这个形式上定义的格中，因此找到有用的分析就成了真正的问题！

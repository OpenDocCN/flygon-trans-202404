# Unix 工具是你的朋友

# Unix 工具是你的朋友

如果在前往一个荒岛流放的途中，我必须在 IDE 和 Unix 工具箱之间做出选择，我会毫不犹豫地选择 Unix 工具。以下是你应该精通 Unix 工具的原因。

首先，IDE 针对特定语言，而 Unix 工具可以处理任何以文本形式出现的东西。在今天每年涌现出新语言和符号的开发环境中，学习以 Unix 方式工作是一项将一次又一次得到回报的投资。

此外，虽然 IDE 只提供其开发者构想的命令，但使用 Unix 工具可以执行任何你能想象到的任务。将它们视为（经典的 Bionicle 前）乐高积木：你只需简单地组合这些小巧但多才多艺的 Unix 工具，就可以创建自己的命令。例如，以下序列是 Cunningham 的签名分析的文本实现 —— 每个文件的分号、大括号和引号序列，可以揭示文件内容的很多信息。

```
for i in *.java; do 
    echo -n "$i: "
    sed 's/[^"{};]//g' $i | tr -d '\n'
    echo
done 
```

此外，你学到的每个 IDE 操作都是针对特定任务的；例如，在项目的调试构建配置中添加一个新步骤。相比之下，磨练你的 Unix 工具技能使你在任何任务上都更加有效。举个例子，我曾经使用在前述命令序列中使用的 sed 工具，将一个项目的构建修改为在多处理器架构上进行交叉编译。

Unix 工具是在多用户计算机只有 128kB RAM 的时代开发的。设计它们的智慧意味着现在它们可以极其高效地处理大数据集。大多数工具都像过滤器一样工作，一次只处理一行，这意味着它们处理数据的数量没有上限。你想搜索存储在半 TB 英文维基百科转储中的编辑次数？只需简单地调用

```
grep '<revision>' | wc –l 
```

将为你轻松地提供答案。如果你发现一个命令序列通常很有用，你可以很容易地将其打包成一个 shell 脚本，使用一些独特强大的编程构造，比如将数据导入循环和条件语句。更令人印象深刻的是，像前述的 Unix 命令执行管道一样，它们会自然地将负载分布在现代多核 CPU 的许多处理单元之间。

Unix 工具的小而美丽的渊源和开源实现使它们无处不在地可用，即使在资源受限的平台上，例如我的机顶盒媒体播放器或 DSL 路由器。这些设备不太可能提供强大的图形用户界面，但它们通常包含 BusyBox 应用程序，该程序提供了最常用的工具。如果你在 Windows 上开发，Cygwin 环境会为你提供所有你能想象到的 Unix 工具，无论是可执行文件还是源代码形式。

最后，如果现有的工具都不符合你的需求，那么扩展 Unix 工具的世界就非常容易。只需编写一个程序（使用你喜欢的任何语言），遵循一些简单的规则即可：你的程序应该只执行一个单一的任务；它应该从标准输入读取数据作为文本行；它应该在标准输出上显示其结果，不加任何标题和其他干扰性内容。影响工具操作的参数在命令行中给出。遵循这些规则，“地球及其中的一切都属于你。”

作者：[Diomidis Spinellis](http://programmer.97things.oreilly.com/wiki/index.php/Diomidis_Spinellis)

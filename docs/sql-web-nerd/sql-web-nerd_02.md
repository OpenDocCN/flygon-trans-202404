| ![](img/no-zoo-rhino-double-101.tcl) |
| --- |

## 介绍

由 [Philip Greenspun](http://philip.greenspun.com/) 撰写，面向 Web 极客的 SQL 的一部分 |

* * *

在写了一个嘲讽学术脑壳浪费大量墨水将关系数据库管理系统（RDBMS）放在 50 年数据库管理软件的背景下的序言后，这本书是如何开始的？通过将 RDBMS 置于其他数据库管理软件背景下的章节来开始。 

为什么呢？你应该知道为什么要支付庞大的性能、财务和管理成本来使用 RDBMS。本章不讨论人们在上世纪 70 年代停止使用的大型机系统，但它确实涵盖了你肯定曾访问过甚至可能创建过的网站采取的数据管理的替代方法。

任何新信息系统的架构师必须决定新定制软件应该承担多少数据管理责任，以及多少应该留给打包软件和操作系统。本章介绍了可用的打包数据管理软件的种类，涵盖了文件、平面文件数据库管理系统、RDBMS、对象关系数据库管理系统和对象数据库。本章还介绍了 SQL 语言。

### 文件系统的问题（以及优点）

![亚利桑那](img/old-tractor-4.4.jpg) 随着你的计算机附带的文件系统是一种非常原始的数据库管理系统。无论你的计算机是带有 Unix 文件系统、NTFS 还是 Macintosh 文件系统，其基本思想都是相同的。数据保存在称为*文件*的大型非结构化命名块中。文件系统的伟大之处在于其隐形性。你可能没有单独购买它，可能没有意识到它的存在，你不需要在报纸上刊登一则寻找*文件系统管理员*的广告，也基本上会按照广告运作。你只需要每天或每两天将文件系统备份到磁带上。

尽管它不显眼，但 Macintosh、Unix 或 Windows 机器上的文件系统能够存储以数字形式表示的任何数据。例如，假设你将邮件列表存储在文件系统文件中。如果你接受以下限制：电子邮件地址或人名不能包含换行符，你可以每行存储一个条目。然后你可以决定电子邮件地址或名字中不能包含竖线。这样你就可以用竖线字符分隔电子邮件地址和名字字段。

到目前为止，一切都很好。只要你小心永远不要尝试存储换行符或竖线，你就可以将数据保存在这个“平面文件”中。不过，搜索可能会很慢，也很昂贵。如果你想知道“philg@mit.edu”是否在邮件列表中，你的计算机必须读取整个文件进行检查。

假设你写了一个程序来处理“插入新人”请求。它的工作原理是将包含新信息的一行追加到平面文件中。然而，假设有几个用户同时使用您的网站。其中两个在完全相同的时间要求加入邮件列表。根据您编写程序的方式、您拥有的文件系统的特定类型和运气，您可能会得到以下任何一种行为：

+   两个插入都成功了。

+   其中一个插入丢失。

+   来自两个插入的信息被混合在一起，以至于两者都被破坏了。

在最后一种情况下，您编写的用于使用平面文件中数据的程序可能不再起作用。

那又怎样？Emacs 可能是古老的，但它仍然是世界上最好的文本编辑器。你喜欢使用它，所以你也可以花周末和晚上用 Emacs 手动修复你的平面文件数据库。谁需要并发控制？

一切都取决于你有什么样的炉子。

是的，就是你的炉子。假设你在哈佛广场购买了一套价值 268,500 美元的公寓。你自言自语道：“现在我的朋友们肯定会对我印象深刻”，然后邀请他们来参加早午餐。不是因为你喜欢他们，而只是为了让他们对你的豪华生活感到嫉妒。想象一下，当他们唯一能说的话是“这个旧的炉子怎么回事？你难道没有维京炉吗？”时，你会有多么恐慌。![Helgumannen 的旧渔村。法罗，哥特兰岛。瑞典](img/helgumannen-60.tcl)

维京炉？！？它们要花费 5000 美元。你能想到这种现金的唯一办法是加入日益增长的在线企业家行列。所以你开了一家互联网银行。作为一名经验丰富的 Perl 脚本/平面文件专家，你自信地构建了一个系统，其中所有支票账户余额都存储在一个文件`checking.text`中，而所有储蓄账户余额都存储在另一个文件` savings.text`中。

几天后，发生了一系列不幸的事件。Joe 用户正在将 $10,000 从储蓄账户转到支票账户。Judy 用户同时向她的储蓄账户存入 $5。你的一个 Perl 脚本成功地将支票账户的平面文件写入了 Joe 的新余额，高出 $10,000。它还将储蓄账户文件写入了 Joe 的新余额，低了 $10,000。然而，处理 Judy 存款的脚本大约在同一时间开始，并以 Joe 原始余额的版本开始。最终完成并写入 Judy 的高 $5 余额，但也用旧的高余额覆盖了 Joe 的新低余额。这让你处于什么境地？比原来少了 $10,000，用着旧的 GE 炉灶做饭，希望你有并发控制。

几个月的编程和阅读上世纪 60 年代处理互斥的操作系统理论书籍后，你解决了并发问题。恭喜。然而，像任何优秀的互联网企业家一样，你在家里经营这家企业，感到有点困倦。于是你在微波炉里加热一些咖啡，同时在烤箱里烤一个贝果。保险丝跳闸了。这时你会后悔买了一套 Calphalon 锅来搭配你的 Viking 炉灶，而不是为服务器投资一个不间断电源。你听到磁盘停止旋转的令人不安的声音。你急忙让服务器恢复运行，没有时间查看日志，注意到 Joe 用户正在将 $25,000 从储蓄账户转到支票账户。Joe 的交易发生了什么？![圣卡琳。维斯比，哥特兰岛。瑞典](img/santa-karin-22.tcl)

Joe 的好消息是，你的 Perl 脚本刚刚完成了向他的支票账户存入 $25,000。你的坏消息是，它实际上还没有开始从他的储蓄账户扣款。你正忙着为你的在线业务准备公开发行，没有注意到这笔损失。但你的承销商最终注意到了，你计划将银行出售给公众的计划泡汤了。

这让你处于什么境地？用着旧的 GE 炉灶做饭，希望你把事务的实现留给专业人士。

#### 事务处理需要什么？

数据处理人员喜欢在决定数据库管理系统是否足以处理事务时谈论“ACID 测试”。一个足够的系统具有以下特性：

原子性

事务执行的结果要么全部提交，要么全部回滚。所有更改生效，或者都不生效。这意味着，对于 Joe 用户的转账，他的储蓄和支票余额都会调整，或者都不会。对于 Web 内容管理的例子，假设用户正在编辑评论。Web 脚本告诉数据库“将旧评论值复制到审核表中，并使用新文本更新实时表”。如果硬盘在复制后但更新前已满，审核表插入将被回滚。

一致性

![环球城欢迎您（以城市街道风格建造的购物中心；加利福尼亚洛杉矶）。](img/universal-city-rules-42.tcl) 数据库从一个有效状态转换为另一个有效状态。这将一个事务定义为仅在遵守用户定义的完整性约束时才合法。不允许非法事务，如果无法满足完整性约束，则事务将被回滚。例如，假设您定义了一个规则，讨论论坛表中的帖子必须与有效的用户 ID 相关联。然后您雇佣了 Joe Novice 来编写一些管理页面。Joe 编写了一个删除用户页面，没有检查删除是否会导致孤立的讨论论坛帖子。尽管 Joe 没有检查，但数据库管理系统会检查，并中止任何导致您拥有被删除用户的讨论论坛帖子的事务。

隔离

事务的结果对其他事务是不可见的，直到事务完成。例如，如果您正在运行会计报告的同时 Joe 正在转账，会计报告程序将在 Joe 转账前或后看到余额，但永远不会看到中间状态，即支票已入账但储蓄尚未借记。

持久性

一旦提交（完成），事务的结果是永久的，并且可以在未来的系统和媒体故障中幸存。如果航空公司预订系统的计算机给您 22A 座位，然后在一毫秒后崩溃，它不会忘记您坐在 22A 座位上并将其分配给其他人。此外，如果程序员将咖啡洒入磁盘驱动器，将可以安装新磁盘并恢复直到洒咖啡的事务，显示您坐在 22A 座位上。

这听起来不难实现，是吗？毕竟，网络最令人耳目一新的事情之一就是它鼓励没有正式计算机科学背景的人来编程。那么，为什么不在刚刚发现 Perl 的英语专业人员实现的事务系统上构建您的互联网银行呢？

因为您仍然需要索引。

#### 查找您的数据（并且快速）

![斯德哥尔摩机场，跳房子](img/stockholm-airport-hopskotch-102.tcl) 数据库管理系统的一个方面是处理插入、更新和删除。这都涉及将信息放入数据库中。有时候，能够获取数据也是很好的。而且随着流行网站每秒获得 100 次点击，要注意速度是很值得的。

平面文件在非常小的情况下运行良好。一个 Perl 脚本可以在一瞬间将整个文件读入内存，然后查找其中请求的信息。但是假设你的在线银行发展到有 250,000 个账户。用户在网页上输入他的账号，要求查看最近的存款。你有一个包含 2500 万条记录的时间顺序财务交易文件。咔咔咔。你的服务器费力地查找所有 2500 万条记录，找到与用户账号匹配的记录。在它忙碌的时候，另外 25 个用户来到网站，要求查看他们账户的相同信息。

你有两个选择：（1）购买一台具有 64 个处理器和 64 GB RAM 的 Sun E10000 服务器，或者（2）构建一个索引文件。如果你构建一个将账号映射到顺序交易号的索引文件，你的服务器就不再需要搜索所有 2500 万条记录。然而，你必须修改所有插入、更新或删除数据库的程序，以保持索引的实时性。

这一切运行得很顺利，直到两年后，一位来自哈佛的全新 MBA 毕业生到来。她向你的英语专业兼 Perl 黑客要求“列出所有在支票账户中有超过 $5,000 或居住在俄克拉荷马州并在过去 17 天中从储蓄账户中提取超过 $100 的客户的报告。”结果发现你没有预料到这个查询，所以你的索引方案无法加快速度。你的服务器不得不一遍又一遍地处理所有数据。

### 进入关系数据库

你正在构建一项尖端的网络服务。你需要最新和最先进的计算机技术。这就是为什么你使用，呃，Unix。是的。无论如何，即使你的操作系统是在 1969 年开发的，你绝对不能没有最现代的数据库管理系统。也许这个叫 E.F. Codd 的家伙可以帮忙：

> "未来大型数据库的用户必须免于必须了解数据在机器中是如何组织的（内部表示）。...终端用户和大多数应用程序的活动在数据的内部表示发生变化时应保持不受影响，甚至在外部表示的某些方面发生变化时也应如此。随着查询、更新和报告流量的变化以及存储信息类型的自然增长，数据表示的变化通常是必要的。
> 
> "现有的非推理格式化数据系统为用户提供了树形文件或略微更一般的数据网络模型。在第 1 节中，讨论了这些模型的不足之处。引入了基于*n*元关系的模型，数据库关系的范式以及通用数据子语言的概念。在第 2 节中，讨论了关系上的某些操作（除了逻辑推理）并应用于用户模型中冗余和一致性的问题。"

听起来相当不错，对吧？就像你需要的一样。这是科德在 IBM 圣何塞研究实验室工作时撰写的论文《大型共享数据库的关系模型》，发表于 1970 年 6 月的*ACM 通讯*中的摘要。

![沃尔沃。Visby，Gotland，靠近 Fiskarporten。](img/visby-volvo-64.tcl)

是的，没错，1970 年。你需要做的是将你的网站带入 70 年代，使用这些新潮的关系数据库管理系统（RDBMS）。实际上，正如科德在他的论文中所指出的，我们在本章中遇到的大部分问题在 20 世纪 60 年代就已经被 IBM 和"七个小矮人"（IBM 的竞争对手所称）出售的现成大型机软件解决了。到了 20 世纪 60 年代早期，企业已经厌倦了丢失重要交易和手动修复数据库的情况。他们开始认为他们的应用程序员不应该为每个新项目按照特定情况实现事务和索引。公司开始从 IBM 等计算机供应商那里购买数据库管理软件。这些产品运行得相当不错，但导致了脆弱的数据模型。如果你第一次就正确地获取了数据表示并且你的业务需求从未改变，那么 1967 年风格的分层数据库就很好。不幸的是，如果你实施了一个系统，随后需要新的索引或新的数据格式，那么你可能需要重写所有的应用程序。

从应用程序员的角度来看，关系数据库中最大的创新是使用*声明性*查询语言 SQL（结构化查询语言的缩写，发音为"ess-cue-el"或"sequel"）。大多数计算机语言都是*过程式*的。程序员逐步告诉计算机要做什么，指定一个过程。在 SQL 中，程序员说"我想要符合以下条件的数据"，而关系数据库管理系统的查询规划器会找出如何获取这些数据。使用声明性语言有两个优点。第一个是查询不再依赖于数据表示。关系数据库管理系统可以自由地存储数据。第二个是增加软件的可靠性。在 SQL 查询中很难出现"一个小错误"，而在过程式程序中很容易。通常它要么描述你想要的数据并且始终有效，要么以明显的方式完全失败。

声明性语言的另一个好处是，不太精通的用户也能编写有用的程序。例如，许多在 20 世纪 60 年代需要专业程序员的计算任务，现在可以由非技术人员通过电子表格完成。在电子表格中，你不需要告诉计算机如何计算数字或以什么顺序进行。你只需*声明*“这个单元格将是那边那个单元格值的 1.5 倍”。

RDBMS 可以运行非常慢。根据你是在卖还是在买计算机，这可能会让你感到不安或高兴。假设系统需要 30 秒才能返回你查询的数据。这意味着你有很多数据吗？你需要添加一些索引吗？RDBMS 查询规划器做出了一些错误选择，需要一些提示吗？谁知道呢？RDBMS 是一个你没有编写过且没有源代码的极其复杂的程序。每个供应商都有追踪和调试工具声称可以帮助你，但这个过程并不简单。祝你好运，试着找出一个不同的 SQL 咒语，可以在更短的时间内返回相同的数据集。如果你做不到，打电话给 1-800-USESUNX，让他们给你寄送一台带有 32 GB RAM 的 16 处理器 Sun Enterprise 10000。或者，你可以继续运行你在 20 世纪 60 年代使用的非关系软件，这就是航空公司为他们的预订系统所做的。

### 这个 RDBMS 东西是如何工作的？

![植物园。维斯比，哥特兰岛。](img/visby-flowers-82.tcl) 数据库研究人员喜欢谈论关系代数，n-元组，正规形式和自然组合，同时使用数学符号。这种数学上的模糊光环往往会让你的注意力从他们糟糕的西装和无聊的个性中分散开来，但如果你只想使用关系数据库管理系统，这是没有价值的。

实际上，这就是你成为穴居人数据库程序员所需要知道的全部：关系数据库是一个大的电子表格，几个人可以同时更新。

数据库中的每个*表*都是一个电子表格。您告诉 RDBMS 每行有多少列。例如，在我们的邮件列表数据库中，表有两列：`name`和`email`。数据库中的每个条目都由此表中的一行组成。RDBMS 比电子表格更受限制，因为一列中的所有数据必须是相同类型的，例如，整数、小数、字符串或日期。电子表格和 RDBMS 之间的另一个区别是，RDBMS 中的行不是有序的。您可以有一个名为`row_number`的列，并要求 RDBMS 根据该列中的数据返回已排序的行，但是行编号不是像 Visicalc 或其衍生产品 Lotus 1-2-3 和 Excel 中那样隐式的。如果您定义了一个`row_number`列或某个其他表中行的唯一标识符，那么另一个表中的行可以通过包含唯一 ID 的值来引用该行。

下面是邮件列表应用程序的一些 SQL 代码示例：

> ```
> create table mailing_list ( email varchar(100) not null primary key, name varchar(100) );
> ```

表将被称为`mailing_list`，并将具有两列，都是可变长度的字符串。我们在`email`列上添加了一些完整性约束。`not null`将阻止任何程序插入其中`name`已指定但`email`未指定的行。毕竟，系统的整个目的是发送电子邮件给人们，所以拥有没有电子邮件地址的姓名没有太多价值。`primary key`告诉数据库该列的值可以用于唯一标识一行。这意味着系统将拒绝尝试插入具有与现有行相同电子邮件地址的行的尝试。这听起来像是一个很好的功能，但它可能会产生一些意想不到的性能影响。例如，每当有人尝试向该表中插入一行时，RDBMS 都必须查看表中的所有其他行，以确保没有已经存在具有相同电子邮件地址的行。对于一个非常庞大的表来说，这可能需要几分钟，但如果您还要求 RDBMS 在`email`上为`mailing_list`创建一个索引，那么检查几乎会立即完成。但是，完整性约束仍然会减慢您的速度，因为对`mailing_list`表的每次更新也将需要更新索引，因此您将对硬盘进行两倍的写入。

这就是 SQL 的乐趣和痛苦。插入两个看似无害的单词可能会使性能降低 1000 倍。然后插入一句话（创建索引）可能会让你回到只有两到三倍的程度。（请注意，包括 Oracle 在内的许多 RDBMS 实现会自动在受约束的列上定义索引。）

无论如何，现在我们已经执行了数据定义语言的"create table"语句，我们可以继续进行数据操纵语言：INSERT。

> ```
>  insert into mailing_list (name, email) values ('Philip Greenspun','philg@mit.edu'); 
> ```

请注意，我们指定了要插入哪些列。这样，如果以后有人来了

> ````
> alter table mailing_list add (phone_number varchar(20));
> 
> ````

（添加列的 Oracle 语法），我们的插入仍然有效。还要注意，在 SQL 中，字符串引用字符是单引号。嘿，那是 70 年代。如果你现在访问新闻组`comp.databases`，我敢打赌你会找到有人在问"如何在关系数据库管理系统中插入包含单引号的字符串？"这是从 AltaVista 收集的一个例子：

> ````
> demaagd@cs.hope.edu (David DeMaagd) wrote:
> 
> >hwo can I get around the fact that the ' is a reserved character in 
> >SQL Syntax?  I need to be able to select/insert fields that have 
> >apostrophies in them.  Can anyone help?
> 
> You can use two apostrophes '' and SQL will treat it as one.
> 
> ===========================================================
> Pete Nelson     | Programmers are almost as good at reading
> weasel@ecis.com | documentation as they are at writing it.
> ===========================================================
> 
> ````

我们将采纳皮特·尼尔森的建议，并将"O'Grady"中的单引号加倍：

> ````
> insert into mailing_list (name, email)
> values ('Michael O''Grady','ogrady@fastbuck.com');
> 
> ````

创建了一个表并插入了一些数据后，我们终于准备好体验 SQL SELECT 的强大威力了。想要你的数据回来吗？

> ````
> select * from mailing_list;
> 
> ````

如果你将这个查询输入到标准的 shell 风格的关系数据库管理系统客户端程序中，例如 Oracle 的 SQL*PLUS，你会得到... 一团糟。这是因为你告诉 Oracle 列的宽度可以达到 100 个字符（`varchar(100)`）。很少会有需要存储长达 100 个字符的电子邮件地址或姓名。然而，解决"丑陋报告"问题的方法不是减少数据库中允许的最大长度。你不希望系统因为某些人的名字或电子邮件地址特别长而失败。解决方案要么是使用更复杂的工具来查询数据库，要么是为 SQL*Plus 提供一些准备报告的提示：

> ```
>  SQL> column email format a25 SQL> column name format a25 SQL> column phone_number format a12 SQL> set feedback on SQL> select * from mailing_list; EMAIL NAME PHONE_NUMBER ------------------------- ------------------------- ------------ philg@mit.edu Philip Greenspun ogrady@fastbuck.com Michael O'Grady 2 rows selected. 
> ```

请注意，在`phone_number`列中没有任何值，因为我们还没有设置任何值。一旦我们开始添加电话号码，我们意识到我们的数据模型是不够的。这是互联网，典型用户乔会因为手机、寻呼机和其他个人通讯配件的重量而让裤子垂到膝盖。一个电话号码列显然是不够的，即使`work_phone`和`home_phone`列也无法容纳用户可能想要提供给我们的丰富信息。处理这个问题的干净数据库方式是从`mailing_list`表中移除我们的`phone_number`列，并为电话号码定义一个辅助表。在 Oracle 8 中，删除或重命名列是不可能的（请参阅"数据建模"章节，了解一些从 Oracle 8i 开始变得可能的 ALTER TABLE 命令），所以我们

> ```
>  drop table mailing_list; create table mailing_list ( email varchar(100) not null primary key, name varchar(100) ); create table phone_numbers ( email varchar(100) not null references mailing_list(email), number_type varchar(15) check (number_type in ('work','home','cell','beeper')), phone_number varchar(20) not null ); 
> ```

请注意，在这个表中，电子邮件列*不是*主键。这是因为我们希望允许具有相同电子邮件地址的多行。如果你和一个数据库迷友一起，你可以说`phone_numbers`表中的行与`mailing_list`表中的行之间存在*关系*。实际上，你可以说这是*多对一关系*，因为`phone_numbers`表中的许多行可能对应`mailing_list`表中的一行。如果你花足够的时间思考和讨论你的数据库，两件事会发生：

1.  你将在任何州立大学的关系数据库管理系统课程中获得 A。

1.  你会吸引《今日心理学》的读者，因为你总是谈论关系，他们会认为你很敏感、关心。[在查看任何约会建议之前，请参阅[`philip.greenspun.com/wtr/getting-dates.html`](http://philip.greenspun.com/wtr/getting-dates.html)中的"使用互联网约会"文章]

关于我们的两表数据模型还值得注意的一点是，我们不在`phone_numbers`表中存储用户的姓名。这将与`mailing_list`表中的内容重复，并且在某种程度上也是自相矛盾的，比如，"robert.loser@fastbuck.com"在输入工作电话时称自己为"Robert Loser"，然后在输入寻呼机号码时称自己为"Rob Loser"，最后在用笔记本电脑狭窄的键盘上输入手机号码时称自己为"Bob Lsr"。一个数据库迷会说，这个数据模型因此处于"第三范式"。每个表中每行的一切都仅依赖于主键，没有任何内容仅依赖于主键的一部分。`phone_numbers`表的主键是`email`和`number_type`的组合。如果在这个表中有用户的姓名，它将仅依赖于主键的电子邮件部分。

不管怎样，数据库方面的废话就到此为止。让我们填充`phone_numbers`表：

> ```
>  SQL> insert into phone_numbers values ('ogrady@fastbuck.com','work','(800) 555-1212'); ORA-02291: integrity constraint (SCOTT.SYS_C001080) violated - parent key not found 
> ```

糟糕！当我们删除`mailing_list`表时，所有行都丢失了。`phone_numbers`表有一个参照完整性约束（"references mailing_list"），以确保我们不为我们不知道姓名的人记录电子邮件��址。我们必须首先将这两个用户插入`mailing_list`：

> ```
>  insert into mailing_list (name, email) values ('Philip Greenspun','philg@mit.edu'); insert into mailing_list (name, email) values ('Michael O''Grady','ogrady@fastbuck.com'); insert into phone_numbers values ('ogrady@fastbuck.com','work','(800) 555-1212'); insert into phone_numbers values ('ogrady@fastbuck.com','home','(617) 495-6000'); insert into phone_numbers values ('philg@mit.edu','work','(617) 253-8574'); insert into phone_numbers values ('ogrady@fastbuck.com','beper','(617) 222-3456'); 
> ```

请注意，最后四个 INSERT 使用了一个邪恶的 SQL 快捷方式，并没有指定要插入数据的列。系统默认使用按定义顺序的所有列。除了用于原型设计和玩耍，我们不建议使用这种快捷方式。

前三个 INSERT 正常工作，但最后一个怎么办，O'Grady 先生拼错了"beeper"？

> ```
> ORA-02290: check constraint (SCOTT.SYS_C001079) violated
> ```

我们在表定义时要求 Oracle`check (number_type in ('work','home','cell','beeper'))`，它也做到了。数据库不能处于不一致的状态。

假设我们想要所有的数据。电子邮件、全名、电话号码。最明显的查询尝试是*连接*。

> ```
>  SQL> select * from mailing_list, phone_numbers; EMAIL NAME EMAIL TYPE NUMBER ---------------- ---------------- ---------------- ------ -------------- philg@mit.edu Philip Greenspun ogrady@fastbuck. work (800) 555-1212 ogrady@fastbuck. Michael O'Grady ogrady@fastbuck. work (800) 555-1212 philg@mit.edu Philip Greenspun ogrady@fastbuck. home (617) 495-6000 ogrady@fastbuck. Michael O'Grady ogrady@fastbuck. home (617) 495-6000 philg@mit.edu Philip Greenspun philg@mit.edu work (617) 253-8574 ogrady@fastbuck. Michael O'Grady philg@mit.edu work (617) 253-8574 6 rows selected. 
> ```

哎呀！发生了什么？`mailing_list`表中只有两行，`phone_numbers`表中有三行。但这里我们却得到了六行。这就是连接的工作原理。它们给出了两个表的*笛卡尔积*。一个表的每一行依次与另一个表的所有行配对。因此，如果将一个 N 行表与一个 M 行表连接，将得到一个包含 N*M 行的结果。在真实的数据库中，N 和 M 可能达到百万级，因此最好更具体地指定你想要哪些行：

> ```
>  select * from mailing_list, phone_numbers where mailing_list.email = phone_numbers.email; EMAIL NAME EMAIL TYPE NUMBER ---------------- ---------------- ---------------- ------ -------------- ogrady@fastbuck. Michael O'Grady ogrady@fastbuck. work (800) 555-1212 ogrady@fastbuck. Michael O'Grady ogrady@fastbuck. home (617) 495-6000 philg@mit.edu Philip Greenspun philg@mit.edu work (617) 253-8574 3 rows selected. 
> ```

可能更接近您心目中的样子。通过这种方式完善您的 SQL 语句有时可能更加令人兴奋。例如，假设您想摆脱菲利普·格林斯潘的电话号码，但不确定确切的语法。

> ```
>  SQL> delete from phone_numbers; 3 rows deleted. 
> ```

糟糕。是的，这实际上删除了表中的*所有*行。您可能希望您输入的是

> ````
> delete from phone_numbers where email = 'philg@mit.edu';
> 
> ````

但现在为时已晚。

还有一个更基本的 SQL 语句需要学习。假设菲利普搬到好莱坞实现他长久以来成为一名重要电影制片人的梦想。显然，需要更改姓名，尽管他不愿放弃自 1976 年以来一直拥有的电子邮件地址。以下是 SQL 语句：

> ```
>  SQL> update mailing_list set name = 'Phil-baby Greenspun' where email = 'philg@mit.edu'; 1 row updated. SQL> select * from mailing_list; EMAIL NAME -------------------- -------------------- philg@mit.edu Phil-baby Greenspun ogrady@fastbuck.com Michael O'Grady 2 rows selected. 
> ```

与 DELETE 一样，不要在 UPDATE 语句中玩弄，除非在最后有一个 WHERE 子句。

### 勇敢的新世界

最初的 70 年代中期关系数据库管理系统让公司存储以下类型的数据：数字、日期和字符串。经过二十多年的创新，今天您可以跑到商店花费 30 万美元购买一个“企业级”关系数据库管理系统，可以让您存储以下类型的数据：数字、日期和字符串。

使用*对象关系*数据库，您可以定义自己的数据类型。例如，您可以定义一个名为`url`的数据类型...

[`www.postgresql.org`](http://www.postgresql.org)。

### 更勇敢的新世界

![Millesgarden. Stockholm, Sweden](img/millesgarden-37.tcl) 如果您真的想走在前沿，您可以使用一个真正的对象数据库，比如 Object Design 的 ObjectStore（被 Progress Software 收购）。这些数据库持久地存储您在 Smalltalk、Common Lisp、C++或 Java 程序中创建的对象和指针结构。追踪指针和某些类型的事务可能比关系数据库快 10 到 100 倍。如果您相信对象数据库供应商的宣传资料中的一切，那么您会惊讶于拉里·埃里森仍然有 100 美元的钞票可以向过路人扔，当他驾驶他的 Acura NSX 飞驰而过时。关系数据库管理系统应该在 80 年代中期以巨大的宣传声势引入这种优越技术后早就被击垮了。

十年后，对象数据库管理系统市场每年约为 1 亿美元，可能是关系数据库市场规模的 1%。为什么会失败？对象数据库带回了 1960 年代关系数据库管理系统之前的一些不好的特征。程序员必须了解数据存储的许多细节。如果你知道你感兴趣的对象的身份，那么查询就会快速简单。但事实证明，大多数数据库用户并不关心对象的*身份*；他们关心对象的*属性*。关系数据库在根据属性提供聚合方面往往更快更好。关系数据库管理系统（RDBMS）和对象数据库管理系统（ODBMS）之间的关键区别在于程序员与数据交互的程度。在 RDBMS 中，应用程序——用诸如 C、COBOL、Fortran、Perl 或 Tcl 等过程语言编写——可能存在各种灾难性错误。然而，这些错误通常不会影响数据库中的信息，因为所有与 RDBMS 的通信都通过 SQL 语句限制。在 ODBMS 中，应用程序直接编写存储在数据库中的对象中的插槽。应用程序中的错误可能直接导致数据库损坏，这是组织中最有价值的资产之一。

### 更多

+   “大型共享数据库的关系模型”，E.F. Codd 在 1970 年 6 月的*ACM 通讯*中的论文被重新印刷在[数据库系统读物](http://www.amazon.com/exec/obidos/ASIN/1558605231/pgreenspun-20)中（Stonebraker 和 Hellerstein 1998；Morgan Kaufmann）。也许你会想知道为什么在 1999 年，世界物理学家给了我们互联网八年后，我没有将你链接到 Codd 在 www.acm.org 上的论文。然而，该组织如此热衷于同时展示全球学术计算机科学家的贪婪和无能，以至于他们要收费才能电子分发他们自己没有支付的材料。

+   有关第一个关系数据库实现的有趣历史，请访问[`www.mcjones.org/System_R/`](http://www.mcjones.org/System_R/)

+   要了解各种数据库管理系统的内部工作原理，请获取[数据库系统读物](http://www.amazon.com/exec/obidos/ASIN/1558605231/pgreenspun-20)（上述链接）。

### 参考

+   如果你想要操作 Oracle，你会发现[SQL*Plus 用户指南和参考](http://www.oradoc.com/keyword/sqlplus)很有用。

+   如果你渴望细节，你可以从[Oracle8 Server Concepts](http://www.oradoc.com/keyword/concepts)中获得上帝的真实话（好吧，至少是拉里·埃里森在企业 IT 世界中的真实话，这在公司 IT 世界中几乎是一回事）。

下一步：数据建模

* * *

[philg@mit.edu](http://philip.greenspun.com/)

### 读者评论

> 实际上，ACM 确实免费提供 [大型共享数据库的数据关系模型](http://www.acm.org/classics/nov95/toc.html)，但这只是个例外，而不是规则。
> 
> -- 汤姆·L，2003 年 11 月 26 日
> 
> 我正在使用 MySQL，并且我想评论一下我在遵循本页面教程时遇到的问题。也许其他新手可以从中受益。
> 
> 据我所知：
> 
> a) MySQL 支持不同的“存储引擎”来存储表。这可能是一件好事。但是，并非所有引擎都支持引用约束。
> 
> b) 要支持“引用”约束的 MySQL 表必须是 InnoDB 类型。在我的安装中（在 SuSE Linux 上，直接从标准 RPM 二进制包安装），这 *不是* 默认设置。因此，您必须要么更改服务器配置使其成为默认设置，要么在表定义的右括号后指定“ENGINE = InnoDB”。
> 
> c) 即使对于 InnoDB，菲尔上面描述的语法也不起作用，尽管它不被拒绝，只是被忽略。根据手册，这实际上只是对开发人员的注释，指出该列应该引用另一列，即使 mysql 不强制执行约束。
> 
> d) 因此，使此类约束生效的唯一方法是：1\. 将表设置为 InnoDB 并且 2\. 使用“FOREIGN KEY (email) REFERENCES mailing_list(email)”格式作为表定义中的单独条目。
> 
> [MySQL 甚至不会发出警告！甚至不会提醒这些引用子句只是“注释”。它只会欣然接受它们并允许该行中的任何旧值。噫。]
> 
> -- 安东尼奥·拉米雷斯，2007 年 3 月 19 日
> 
> 另一个关于 MySQL 的补充是，“CHECK 子句被所有存储引擎解析但被忽略” (http://dev.mysql.com/doc/refman/5.1/en/create-table.html)。然而，可以通过适当的触发器实现 CHECK。
> 
> -- 埃迪·马克斯，2010 年 6 月 22 日
> 
> 在学习关系型数据库时我会避开 MySQL - 它在哲学上有点不同，这一点可以从其静默错误和 InnoDB 的非默认状态中看出。我改用 PostGres - 它是免费的，命令行工具非常出色。配置和安装都很简单，并且在您想使用的任何地方都有成熟的支持。
> 
> -- 克里斯·库尼，2010 年 9 月 2 日
> 
> 默认存储引擎可以在 MySQL 配置文件中更改，在 Linux 上（例如 RHEL、CentOS、Debian、SLES 等），配置文件存储在 **/etc/my.cnf** 中
> 
> 在该文件中应该有一个标记为 [mysqld] 的部分。在该标签的下面立即添加以下行，以便结果如下：
> 
> | `[mysqld]` |
> | --- |
> | `default-storage-engine = myisam` |
> 
> 然后，您需要重新启动 mysqld 进程。根据您的 Linux 版本，有多种方法可以完成此任务。一种方式如下：
> 
> | `/etc/init.d/mysql stop` |
> | --- |
> | `/etc/init.d/mysql start` |
> 
> 祝您愉快！
> 
> -- 蔡布莱克，2011 年 6 月 9 日

添加评论
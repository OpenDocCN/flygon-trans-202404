| [![](../Images/0e5de52fc55e3be21b3d332ba62a9ba9.jpg)](/http://philip.greenspun.com/images/pcd0088/elvis-grave-43.tcl) |
| --- |

## 限制

部分来自[SQL for Web Nerds](index.html) by [Philip Greenspun](http://philip.greenspun.com/) |

* * *

[![](../Images/34eeda078480ce071cd178eaabee69d2.jpg)](/http://philip.greenspun.com/images/pcd0088/graceland-paperweight-34.tcl) Oracle中最痛苦的限制是VARCHAR的最大长度为4000字节。对于大多数Web应用程序来说，这足以容纳97%的用户输入数据。剩下的3%非常重要，以至于你可能无法使用VARCHAR。

Oracle8包括一个最大可达4GB的Character Large Objects（CLOB）数据类型。

> ```
> create table foobar 
> ( mykey integer,
>   moby clob );
> 
> insert into foobar values ( 1, 'foo');
> 
> ```

我第一次使用CLOBs是为了将我的问答论坛软件（你在[photo.net](http://www.photo.net/photo/)看到的）移植到Oracle 8。我将其用于MESSAGE列。在我的Illustra实现中，结果表中的12000行中只有46行的消息长度超过4000字节（Oracle 8中的VARCHAR限制）。但这46条消息非常有趣，有时包含其他作品的引用材料。因此，如果用户希望，允许他们发布非常长的消息似乎是值得的。

小小的注意事项：

+   CLOBs不像字符串那样工作。例如，你不能要求一个CLOB列的长度。你可以通过PL/SQL调用来解决这个问题，但这并不是很有趣。

+   LOBs不允许在GROUP BY、ORDER BY、SELECT DISTINCT、聚合和连接中使用

+   `alter table bboard modify message clob;`不起作用（即使表中没有行）。如果你想使用CLOBs，显然必须在创建表时声明。

如果你认为这些限制很糟糕，那么你还没有遇到最大的限制：Oracle SQL解析器只能处理长度不超过4000个字符的字符串字面量。SQL*Plus的限制更严格。它只能处理长度不超过2500个字符的字符串。实际上，从大多数Oracle客户端，将无法向表中插入超过4000个字符长的数据。一个能够完美处理4000个字符字符串的语句/系统，将无法完全处理4001个字符长的字符串。你必须完全重新设计你的工作方式，以处理*可能*很长的字符串。

我的合作伙伴Cotton为我定制了一个AOLserver的Oracle 8驱动程序（我首选的RDBMS客户端）。所以他决定使用C绑定变量。结果发现，这些对于超过4000个字符的字符串也不起作用。如果你事先知道列是CLOB，那么C语言中有一种特殊的CLOB类型可以使用。但当然，Cotton的C代码只是从我的AOLserver Tcl代码中获取查询。在每次插入或选择之前没有查询数据库的情况下，他无法知道哪些列将是CLOB。

Oracle 8最被吹捧的功能之一是您可以对表进行分区，例如，说“每个具有order_date列小于1997年1月1日的行都放在表空间A中；每个具有order_date小于1998年1月1日的行都放在表空间B中；其余的都放在表空间C中。”假设这些表空间都在不同的磁盘驱动器上，这意味着当您对最近一个月或两个月的订单进行GROUP BY时，Oracle不会筛选多年的数据；它只需要扫描位于表空间C中的表的分区。分区似乎是一个好主意，或者至少多年来一直在使用它的Informix客户似乎是这样认为的。但如果您是一个CLOB成就者，您将不会使用分区。

现在，我对CLOBs的看法是，它们使用起来非常不愉快，几乎不值得。Cotton花了比他的驱动程序中的其他所有功能都更长的时间来使这个功能正常工作。Informix Universal Server允许您拥有32,000个字符长的VARCHARs，我现在正在渴望那个系统...

### 参考资料

+   Oracle服务器参考，“限制”，[http://www.oradoc.com/keyword/limits](http://www.oradoc.com/keyword/limits)

下一步：[调优](tuning.html)

* * *

[philg@mit.edu](http://philip.greenspun.com/)

### 读者评论

> MySQL和MS SQL都有更高的VARCHAR限制：分别为1,048,543和8000。这是从http://dev.mysql.com/tech-resources/crash-me.php?res_id=38获取的信息
> 
> -- [Victor F](/shared/community-member?user_id=261524)，2004年8月21日
> 
> 几年前，我正在处理一个Sybase SQL Server数据库，用于存储转录医疗报告的文本。Sybase的好人们警告我们不要使用TEXT类型的列（相当于Oracle的CLOB），而是将文本*行*存储在VARCHAR列中。 （当时，Sybase将VARCHAR列限制为255字节。）只要您没有任何超过255个字符的行，这种方法就很有效。唯一的问题是您必须将文本解析为行，然后进行无限次的插入。但与使用函数操作TEXT数据相比，这样做的工作量更小。
> 
> -- [David Smith](/shared/community-member?user_id=263834)，2005年6月29日
> 
> 在Oracle 11g中，length()现在可以与NCLOBs一起使用。遗憾的是，select distinct仍然不行。
> 
> -- [Janek Bogucki](/shared/community-member?user_id=310375)，2009年7月2日

[添加评论](/comments/add?page_id=3512)

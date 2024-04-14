| [![迪士尼乐园。加利福尼亚州洛杉矶。](../Images/997c56feee4f0bd05b8b2eb03a2d95ab.jpg)](/http://philip.greenspun.com/images/pcd1647/disney-10.tcl) |
| --- |

## 视图

[SQL for Web Nerds](index.html) 的一部分，作者是 [Philip Greenspun](http://philip.greenspun.com/) |

* * *

[![查看位于Canyon de Chelly的蜘蛛岩。这是蜘蛛女降临并教导纳瓦霍人编织的地方。](../Images/58b97d62554bbe64ed6cfb423e9d4aa9.jpg)](/http://philip.greenspun.com/images/pcd2148/canyon-de-chelly-spider-rock-6.4.jpg) 关系数据库为程序员提供了与计算机物理世界高度抽象的能力。你无法知道RDBMS将表的每一行放在磁盘的哪个位置。你甚至不知道一行中的信息是否会被分割并分布在多个磁盘驱动器上。RDBMS允许你向一个拥有十亿行的表中添加一列。新信息对于每一行将放在现有列的旁边，还是会分配一个大的新磁盘空间块来保存所有十亿行的新列值？你无法知道，也不应该真的关心。

视图是构建更大抽象的一种方式。

假设市场部的简说她想看到一个包含以下信息的表：

+   用户ID

+   电子邮件地址

+   查看的静态页面数量

+   发帖数量

+   发表评论数量

这些信息分布在四个表中。然而，通过阅读本书前面的章节，你完全有能力通过以下查询满足简的需求：

> ```
> select u.user_id, 
>        u.email, 
>        count(ucm.page_id) as n_pages,
>        count(bb.msg_id) as n_msgs,
>        count(c.comment_id) as n_comments
> from users u, user_content_map ucm, bboard bb, comments c
> where u.user_id = ucm.user_id(+)
> and u.user_id = bb.user_id(+)
> and u.user_id = c.user_id(+)
> group by u.user_id, u.email
> order by upper(email)
> 
> ```

然后简（Jane）补充说：“我想每天都看到这个，更新最新信息。我想让一个程序员为我编写一些桌面软件，直接连接数据库并查看这些信息；如果你重新组织数据模型，我不希望我的桌面软件出现故障。”

> ```
> create or replace view janes_marketing_view 
> as 
> select u.user_id, 
>        u.email, 
>        count(ucm.page_id) as n_pages,
>        count(bb.msg_id) as n_msgs,
>        count(c.comment_id) as n_comments
> from users u, user_content_map ucm, bboard bb, comments c
> where u.user_id = ucm.user_id(+)
> and u.user_id = bb.user_id(+)
> and u.user_id = c.user_id(+)
> group by u.user_id, u.email
> order by upper(u.email)
> 
> ```

对简来说，当她查询时，这将看起来和表格一样：

> ```
>  select * from janes_marketing_view; 
> ```

她为什么需要知道信息来自四个表？或者你已经重新组织了RDBMS，以便随后的信息来自六个表？

### 通过视图保护隐私

视图的一个常见用途是保护机密数据。例如，假设所有在医院工作的人通过使用关系数据库进行协作。这是数据模型：

> ```
>  create table patients ( patient_id integer primary key, patient_name varchar(100), hiv_positive_p char(1), insurance_p char(1), ... ); 
> ```

如果一群嬉皮理想主义者在管理医院，他们会认为医生不应该知道患者的保险状况。因此，当医生查看患者的病历时，查看是通过以下方式进行的

> ```
>  create view patients_clinical as select patient_id, patient_name, hiv_positive_p from patients; 
> ```

会计部门的人员不应该因为他们试图从患者身上榨取钱财而获得访问患者的病历的权限：

> ```
>  create view patients_accounting as select patient_id, patient_name, insurance_p from patients; 
> ```

关系数据库拥有类似于分时计算机系统的复杂权限系统。医院中的每个人都有一个唯一的数据库用户ID。权限将根据每个用户或用户组来授予查看或修改某些表的权限。一般来说，关系数据库管理系统的权限设施对Web应用程序并不是很有用。是Web服务器在与数据库通信，而不是用户的桌面电脑。因此，Web服务器负责确定谁在请求页面以及如何响应。

### 保护自己的源代码

ArsDigita Shoppe系统在[http://philip.greenspun.com/panda/ecommerce](/panda/ecommerce)中描述，将所有订单都表示在一个表中，无论它们是被信用卡处理器拒绝、用户退回，还是商家作废。这对于交易处理来说是可以的，但你不希望你的会计或税务报告因包含失败订单而受损。你可以在一个地方做出决定，即什么构成了可报告的订单，然后让所有报告程序查询该视图：

> ```
>  create or replace view sh_orders_reportable as select * from sh_orders where order_state not in ('confirmed','failed_authorization','void'); 
> ```

请注意，在上面的隐私示例中，我们使用视图来留下不需要的列，而在这里我们使用视图来留下不需要的行。

如果我们添加一些订单状态或以其他方式更改数据模型，报告程序无需更改；我们只需要保持这个视图定义的最新即可。请注意，你可以用“create or replace view”来定义每个视图，而不是“create view”；这在以后编辑定义时可以节省一些输入。

如果你使用`select *`来定义一个视图，然后修改底层表中的任何一个，你必须重新定义视图。否则，你的视图将不包含任何新列。你可能认为这是一个bug，但Oracle已经记录了这一点，因此将这种行为转变为了一个特性。

### 即时视图和外连接

让我们回到我们第一个外连接示例，来自简单查询章节：

> ```
>  select users.user_id, users.email, classified_ads.posted from users, classified_ads where users.user_id = classified_ads.user_id(+) order by users.email, posted; ... USER_ID EMAIL POSTED ---------- ----------------------------------- ---------- 52790 dbrager@mindspring.com 37461 dbraun@scdt.intel.com 52791 dbrenner@flash.net 47177 dbronz@free.polbox.pl 37296 dbrouse@enter.net 47178 dbrown@cyberhighway.net 36985 dbrown@uniden.com 1998-03-05 36985 dbrown@uniden.com 1998-03-10 34283 dbs117@amaze.net 52792 dbsikorski@yahoo.com ... 
> ```

在`classified_ads.user_id`后面的加号是我们对Oracle的指令，即“如果无法满足此JOIN约束条件，则添加NULL行”。

假设这份报告变得非常长，我们只对邮箱地址以“db”开头的用户感兴趣。我们可以在`users`表的`email`列上添加一个WHERE子句约束：

> ```
>  select users.user_id, users.email, classified_ads.posted from users, classified_ads where users.user_id = classified_ads.user_id(+) **and users.email like 'db%'** order by users.email, posted; USER_ID EMAIL POSTED ---------- ------------------------------ ---------- 71668 db-designs@emeraldnet.net 112295 db1@sisna.com 137640 db25@umail.umd.edu 35102 db44@aol.com 1999-12-23 59279 db4rs@aol.com 95190 db@astro.com.au 17474 db@hotmail.com 248220 db@indianhospitality.com 40134 db@spindelvision.com 1999-02-04 144420 db_chang@yahoo.com 15020 dbaaru@mindspring.com ... 
> ```

假设我们决定只对1999年1月1日以后的分类广告感兴趣。让我们尝试天真的方法，添加另一个WHERE子句约束，这次是针对`classified_ads`表的一列：

> ```
>  select users.user_id, users.email, classified_ads.posted from users, classified_ads where users.user_id = classified_ads.user_id(+) and users.email like 'db%' **and classified_ads.posted > '1999-01-01'** order by users.email, posted; USER_ID EMAIL POSTED ---------- ------------------------------ ---------- 35102 db44@aol.com 1999-12-23 40134 db@spindelvision.com 1999-02-04 16979 dbdors@ev1.net 2000-10-03 16979 dbdors@ev1.net 2000-10-26 235920 dbendo@mindspring.com 2000-08-03 258161 dbouchar@bell.mma.edu 2000-10-26 39921 dbp@agora.rdrop.com 1999-06-03 39921 dbp@agora.rdrop.com 1999-11-05 8 rows selected. 
> ```

嘿！这完全破坏了我们的外连接！所有用户没有发布任何广告的行都消失了。为什么？因为它们不符合`and classified_ads.posted > '1999-01-01'`的约束条件。外连接在报告中的每一列都添加了NULL，其中`classified_ads`表中没有对应行的地方。新的约束条件是将NULL与1999年1月1日进行比较，答案是... NULL。这就是三值逻辑。任何涉及NULL的计算结果都是NULL。每个WHERE子句约束条件必须对SELECT的结果集中的行求值为true。解决方案是什么？一个“即时视图”。我们将`users`表与仅包含自1999年1月1日以来发布的广告的`classified_ads`的*视图*进行外连接，而不是与`classified_ads`进行外连接：

> ```
>  select users.user_id, users.email, ad_view.posted from users, **(select * from classified_ads where posted > '1999-01-01') ad_view** where users.user_id = ad_view.user_id(+) and users.email like 'db%' order by users.email, ad_view.posted; USER_ID EMAIL POSTED ---------- ------------------------------ ---------- 71668 db-designs@emeraldnet.net 112295 db1@sisna.com 137640 db25@umail.umd.edu 35102 db44@aol.com 1999-12-23 59279 db4rs@aol.com 95190 db@astro.com.au 17474 db@hotmail.com 248220 db@indianhospitality.com 40134 db@spindelvision.com 1999-02-04 144420 db_chang@yahoo.com 15020 dbaaru@mindspring.com ... 174 rows selected. 
> ```

请注意，我们为本次查询命名了我们的“即时视图”为`ad_view`。

### 视图的工作原理

程序员不应该考虑视图的工作原理。然而，值得注意的是，关系数据库管理系统仅存储视图定义，而不存储视图中的任何数据。针对视图与底层表的查询不会改变数据检索或缓存的方式。标准的关系数据库管理系统视图存在是为了使编程更方便或解决安全问题，而不是为了使数据访问更高效。### *物化*视图的工作原理 [![爱尔兰都柏林南部的Powerscourt。](../Images/4d87cdd0b98d5f110195d521b292ff9d.jpg)](/http://philip.greenspun.com/images/pcd0558/powerscourt-5.tcl) 从Oracle 8.1.5开始，于1999年3月推出，您可以拥有*物化视图*，也称为*摘要*。与常规视图类似，物化视图可用于为程序员构建黑盒抽象。换句话说，视图可能是使用复杂的JOIN或昂贵的GROUP BY与求和和平均值创建的。对于常规视图，每次发出查询时都会执行这个昂贵的操作。对于物化视图，这个昂贵的操作是在创建视图时完成的，因此一个单独的查询不需要涉及大量计算。

物化视图会占用空间，因为Oracle会保留数据的副本，或者至少保留可以从数据中派生的信息的副本。更重要的是，物化视图不包含最新信息。当您查询常规视图时，您的结果包括在您的SELECT之前最后一个提交的事务所做的更改。当您查询物化视图时，您得到的结果是在视图创建或刷新时的结果。请注意，Oracle允许您指定刷新间隔，物化视图将在该间隔内自动刷新。

在这一点上，您可能会期望一个经验丰富的Oracle用户说：“嘿，这些不是新的。这是我们过去用来在网络中的机器上保持表的半更新副本的旧CREATE SNAPSHOT功能！”使用物化视图的新功能是您可以使用ENABLE QUERY REWRITE选项创建它们。这授权SQL解析器查看涉及聚合或连接的查询，并转到物化视图。考虑以下查询，来自ArsDigita社区系统的/admin/users/registration-history.tcl页面：

> ```
>  select to_char(registration_date,'YYYYMM') as sort_key, rtrim(to_char(registration_date,'Month')) as pretty_month, to_char(registration_date,'YYYY') as pretty_year, count(*) as n_new from users group by to_char(registration_date,'YYYYMM'), to_char(registration_date,'Month'), to_char(registration_date,'YYYY') order by 1; SORT_K PRETTY_MO PRET N_NEW ------ --------- ---- ---------- 199805 May 1998 898 199806 June 1998 806 199807 July 1998 972 199808 August 1998 849 199809 September 1998 1023 199810 October 1998 1089 199811 November 1998 1005 199812 December 1998 1059 199901 January 1999 1488 199902 February 1999 2148 
> ```

对于每个月份，我们都有一个在photo.net注册的用户数量统计。要执行这个查询，Oracle必须顺序扫描`users`表。如果用户表变得很大，而您希望查询立即完成，您将牺牲一些统计数据的及时性。

> ```
>  create materialized view users_by_month enable query rewrite refresh complete start with 1999-03-28 next sysdate + 1 as select to_char(registration_date,'YYYYMM') as sort_key, rtrim(to_char(registration_date,'Month')) as pretty_month, to_char(registration_date,'YYYY') as pretty_year, count(*) as n_new from users group by to_char(registration_date,'YYYYMM'), to_char(registration_date,'Month'), to_char(registration_date,'YYYY') order by 1 
> ```

Oracle将在1999年3月28日午夜后立即构建此视图。此视图将每隔24小时刷新一次。由于`enable query rewrite`子句，Oracle将自由地从视图中获取数据，即使用户的查询没有提及该视图。例如，给定查询

> ```
>  select count(*) from users where rtrim(to_char(registration_date,'Month')) = 'January' and to_char(registration_date,'YYYY') = '1999' 
> ```

Oracle将完全忽略`users`表，并从`users_by_month`中提取信息。这将以更少的工作获得相同的结果。尽管当前月份是1999年3月。查询

> ```
>  select count(*) from users where rtrim(to_char(registration_date,'Month')) = 'March' and to_char(registration_date,'YYYY') = '1999' 
> ```

也将命中物化视图而不是`users`表，因此将错过自午夜以来注册的任何人（即，查询重写将导致返回不同的结果）。

更多：

### 参考

+   高级：Oracle8服务器概念，[查看部分](http://www.oradoc.com/keyword/views)。Oracle应用程序开发人员指南，[管理视图部分](http://www.oradoc.com/keyword/managing_views)。

+   低级：Oracle8服务器SQL参考，[创建视图语法](http://www.oradoc.com/keyword/create_view)，以及[创建物化视图部分](http://www.oradoc.com/keyword/create_materialized_view)

下一个：[样式](style.html)

* * *

[philg@mit.edu](http://philip.greenspun.com/)

### 读者评论

> 在这个关于视图的问题中，您指出条件“classified_ads.posted > '1999-01-01'”将不会给出期望的结果，因为'posted'列是可空的，因此当'posted'列为NULL时，此条件将计算为NULL。因此，查询永远不会返回'posted'值为NULL的行。
> 
> 为了解决这个问题，您继续创建以下查询的视图：（select * from classified_ads where posted > '1999-01-01'）
> 
> 这个视图不会遇到相同的问题吗？为什么这个视图会包含'posted'列为NULL的列。
> 
> 请解释。
> 
> -- [sanjay raj](/shared/community-member?user_id=264352)，2005年8月25日
> 
> Re Sanjay Raj的评论：嗯，距离你提出这个问题已经将近9年了，所以你可能已经在其他地方找到了答案，或者完全失去了对数据库的兴趣。但由于其他人可能会感到困惑，而且没有其他人回应，我觉得我应该回答一下。这个即时视图（ad_view）是一个所有日期在1999-01-01之后的广告列表。然后将其与用户表进行外连接（"where users.user_id = ad_view.user_id(+)"），这样在ad_view中包含的用户将在其旁边显示他们的广告，但所有其他用户（包括那些没有广告的用户以及那些最近的广告在1999-01-01之前，因此没有进入ad_view的用户）将被列出为空/空格。
> 
> 区别在于，不是先进行外连接然后按日期过滤，这样会破坏它，因为你会过滤掉空值，而是首先通过创建视图来按日期过滤，然后进行外连接，这样在创建后就不会再触及空值。
> 
> -- [Dan Cusher](/shared/community-member?user_id=348055)，2014年6月10日

[添加评论](/comments/add?page_id=3463)

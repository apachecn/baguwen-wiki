<!--yml
category: MySQL
date: 0001-01-01 00:00:00
-->

# MySQL 面试题（爪哇程序员）

# 什么是索引?

> 原文：[https://zwmst.com/639.html](https://zwmst.com/639.html)

索引是一种数据结构,可以帮助我们快速的进行数据的查找。*

# 索引是个什么样的数据结构呢?

> 原文：[https://zwmst.com/643.html](https://zwmst.com/643.html)

索引的数据结构和具体存储引擎的实现有关, 在MySQL中使用较多的索引有Hash索引,B+树索 引等,而我们经常使用的InnoDB存储引擎的默认索引实现为:B+树索引。*

# Hash索引和B+树索引有什么区别或者说优劣呢?

> 原文：[https://zwmst.com/647.html](https://zwmst.com/647.html)

首先要知道Hash索引和B+树索引的底层实现原理:

hash索引底层就是hash表,进行查找时,调用一次hash函数就可以获取到相应的键值,之后进行 回表查询获得实际数据.B+树底层实现是多路平衡查找树.对于每一次的查询都是从根节点出发, 查找到叶子节点方可以获得所查键值,然后根据查询判断是否需要回表查询数据.

那么可以看出他们有以下的不同:

*   hash索引进行等值查询更快(一般情况下),但是却无法进行范围查询.

因为在hash索引中经过hash函数建立索引之后,索引的顺序与原顺序无法保持一致,不能支持范 围查询.而B+树的的所有节点皆遵循(左节点小于父节点,右节点大于父节点,多叉树也类似),天然 支持范围.

*   hash索引不支持使用索引进行排序,原理同上.
*   hash索引不支持模糊查询以及多列索引的最左前缀匹配.原理也是因为hash函数的不可 预测.AAAA和AAAAB的索引没有相关性.
*   hash索引任何时候都避免不了回表查询数据,而B+树在符合某些条件(聚簇索引,覆盖索引 等)的时候可以只通过索引完成查询.
*   hash索引虽然在等值查询上较快,但是不稳定.性能不可预测,当某个键值存在大量重复的 时候,发生hash碰撞,此时效率可能极差.而B+树的查询效率比较稳定,对于所有的查询都 是从根节点到叶子节点,且树的高度较低.

因此,在大多数情况下,直接选择B+树索引可以获得稳定且较好的查询速度.而不需要使用hash 索引.*

# 在建立索引的时候,都有哪些需要考虑的因素呢?

> 原文：[https://zwmst.com/649.html](https://zwmst.com/649.html)

建立索引的时候一般要考虑到字段的使用频率,经常作为条件进行查询的字段比较适合.如果需 要建立联合索引的话,还需要考虑联合索引中的顺序.此外也要考虑其他方面,比如防止过多的所 有对表造成太大的压力.这些都和实际的表结构以及查询方式有关。*

# 了解过哪些存储引擎？各有什么优缺点？

> 原文：[https://zwmst.com/651.html](https://zwmst.com/651.html)

常用的是MyISAM和InnoDB。

InnoDB：支持事务、支持外键、支持行级锁、不支持全文索引

MyISAM：不支持事务、不支持外键、不支持行级锁、支持全文索引*

# 说一下什么是事务的ACID属性吧

> 原文：[https://zwmst.com/653.html](https://zwmst.com/653.html)

1.  原子性（atomicity) 一个事务要么全部提交成功，要么全部失败回滚，不能只执行其中的一部分操作，这就 是事务的原子性 2\. 一致性（consistency) 事务的执行不能破坏数据库数据的完整性和一致性，一个事务在执行之前和执行之后， 数据库都必须处于一致性状态。 如果数据库系统在运行过程中发生故障，有些事务尚未完成就被迫中断，这些未完成的 事务对数据库所作的修改有一部分已写入物理数据库，这是数据库就处于一种不正确的 状态，也就是不一致的状态

2.  隔离性（isolation） 事务的隔离性是指在并发环境中，并发的事务时相互隔离的，一个事务的执行不能不被 其他事务干扰。不同的事务并发操作相同的数据时，每个事务都有各自完成的数据空 间，即一个事务内部的操作及使用的数据对其他并发事务时隔离的，并发执行的各个事 务之间不能相互干扰。 在标准SQL规范中，定义了4个事务隔离级别，不同的隔离级别对事务的处理不同，分别 是：未授权读取，授权读取，可重复读取和串行化

3.  持久性（durability） 一旦事务提交，那么它对数据库中的对应数据的状态的变更就会永久保存到数据库中。即使发生系统崩溃或机器宕机等故障，只要数据库能够重新启动，那么一定能够将其恢 复到事务成功结束的状态*

# 事务的隔离级别了解过吗？

> 原文：[https://zwmst.com/655.html](https://zwmst.com/655.html)

1、读未提交（Read Uncommited），该隔离级别允许脏读取，其隔离级别最低；比如事务A 和事务B同时进行，事务A在整个执行阶段，会将某数据的值从1开始一直加到10，然后进行事 务提交，此时，事务B能够看到这个数据项在事务A操作过程中的所有中间值（如1变成2，2变 成3等），而对这一系列的中间值的读取就是未授权读取

2、授权读取也称为已提交读（Read Commited），授权读取只允许获取已经提交的数据。比 如事务A和事务B同时进行，事务A进行+1操作，此时，事务B无法看到这个数据项在事务A操 作过程中的所有中间值，只能看到最终的10。另外，如果说有一个事务C，和事务A进行非常类 似的操作，只是事务C是将数据项从10加到20，此时事务B也同样可以读取到20，即授权读取 允许不可重复读取。

3、可重复读（Repeatable Read)

就是保证在事务处理过程中，多次读取同一个数据时，其值都和事务开始时刻是一致的，因此 该事务级别禁止不可重复读取和脏读取，但是有可能出现幻影数据。所谓幻影数据，就是指同 样的事务操作，在前后两个时间段内执行对同一个数据项的读取，可能出现不一致的结果。在 上面的例子中，可重复读取隔离级别能够保证事务B在第一次事务操作过程中，始终对数据项 读取到1，但是在下一次事务操作中，即使事务B（注意，事务名字虽然相同，但是指的是另一 个事务操作）采用同样的查询方式，就可能读取到10或20；

4、串行化

是最严格的事务隔离级别，它要求所有事务被串行执行，即事务只能一个接一个的进行处理， 不能并发执行。*

# 有了解过“回表”的概念吗？什么情况下会出现“回表”？

> 原文：[https://zwmst.com/657.html](https://zwmst.com/657.html)

回表就是先通过数据库索引扫描出数据所在的行，再通过行主键id取出索引中未提供的数据， 即基于非主键索引的查询需要多扫描一棵索引树。 当查询的字段在二级索引上没有的时候，就需要“回表”在主键索引上再查一次。*

# MySQL索引的类型

> 原文：[https://zwmst.com/659.html](https://zwmst.com/659.html)

聚簇索引、二级（辅助）索引

B树索引、hash索引*

# 什么是聚簇索引？

> 原文：[https://zwmst.com/661.html](https://zwmst.com/661.html)

聚簇索引：将数据存储与索引放到了一块，找到索引也就找到了数据

非聚簇索引：将数据与索引分开存储，索引结构的叶子节点指向了数据的对应行*

# InnoDB有聚簇索引吗？MyIsam呢？

> 原文：[https://zwmst.com/663.html](https://zwmst.com/663.html)

InnoDB有聚簇索引，主键索引就是聚簇索引。

MyIsam没有聚簇索引，因为他的索引和记录 行是分开存储的。*

# MyIsam的数据是怎么存储的？

> 原文：[https://zwmst.com/665.html](https://zwmst.com/665.html)

MyIsam索引的节点中存储的是数据的物理地址（磁道和扇区），在查找数据时，查找到索引 后，根据索引节点中的物理地址，查找到具体的数据内容。*

# InnoDB的数据是怎么存储的？

> 原文：[https://zwmst.com/667.html](https://zwmst.com/667.html)

InnoDB的主键索引文件上直接存放该行数据，称为聚簇索引，非主索引指向对主键的引用。*

# InnoDB主键索引跟非主键索引在数据存储上的差异

> 原文：[https://zwmst.com/669.html](https://zwmst.com/669.html)

主键索引的叶子节点存的是整行数据。在 InnoDB 里，主键索引也被称为聚簇索引 （clustered index）。

非主键索引的叶子节点内容是主键的值。在 InnoDB 里，非主键索引也被称为二级索引 （secondary index）。*

# InnoDB删除某条记录后，内部会怎么处理？

> 原文：[https://zwmst.com/671.html](https://zwmst.com/671.html)

记录头信息里的delete_mask标记位设置为1（表示该记录已删除），同时将记录从记录行链 表中断开，并加入到垃圾链表中，垃圾链表的空间后续可以复用。*

# InnoDB如果没有设置主键的话，它内部会怎么处理？

> 原文：[https://zwmst.com/673.html](https://zwmst.com/673.html)

优先使用用户自定义主键作为主键，如果用户没有定义主键，则选取一个Unique键作为主 键，如果表中连Unique键都没有定义的话，则InnoDB会为表默认添加一个名为row_id的隐 藏列作为主键。所以我们从上表中可以看出：InnoDB存储引擎会为每条记录都添加 transaction_id 和 roll_pointer 这两个列，但是 row_id 是可选的（在没有自定义主键以及 Unique键的情况下才会添加该列）。这些隐藏列的值不用我们操心，InnoDB存储引擎会自己 帮我们生成的。*

# 为什么InnoDB一定会生成主键？

> 原文：[https://zwmst.com/675.html](https://zwmst.com/675.html)

因为Innodb的数据结构是通过聚簇索引组织起来的，如果没有主键的话，通过其他索引回表 的时候没法查到相应的数据行。*

# MySQL的redo日志和undo日志分别有什么用？

> 原文：[https://zwmst.com/677.html](https://zwmst.com/677.html)

1）redo

作用：保证事务的持久性

MySQL作为一个存储系统，为了保证数据的可靠性，最终得落盘。但是，又为了数据写入的速度，需要引入基于内存的"缓冲池"。其实不止MySQL，这种引入缓冲来解决速度问题的思想无处不在。既然数据是先缓存在缓冲池中，然后再以某种方式刷新到磁盘，那么就存在因宕机导致的缓冲池中的数据丢失，为了解决这种情况下的数据丢失问题，引入了redo log。在其他存储系统，比如Elasticsearch中，也有类似的机制，叫translog。 但是一般讨论数据写入时，在MySQL中，一般叫事务操作，根据事务的ACID特性，如何保证 一个事务提交后Durability的保证？而这就是 redo log 的作用。当向MySQL写用户数据时， 先写redo log，然后redo log根据"某种方式"持久化到磁盘，变成redo log file，用户数据则 在"buffer"中(比如数据页、索引页)。如果发生宕机，则读取磁盘上的 redo log file 进行数据的恢复。从这个角度来说，MySQL 事务的持久性是通过 redo log 来实现的。

2）undo

作用：实现事务回滚

Undo log是InnoDB MVCC事务特性的重要组成部分。当我们对记录做了变更操作时就会产生 undo记录，Undo记录默认被记录到系统表空间(ibdata)中，但从5.6开始，也可以使用独立的Undo 表空间。 Undo记录中存储的是老版本数据，当一个旧的事务需要读取数据时，为了能读取到老版本的 数据，需要顺着undo链找到满足其可见性的记录。当版本链很长时，通常可以认为这是个比 较耗时的操作。 大多数对数据的变更操作包括INSERT/DELETE/UPDATE，其中INSERT操作在事务提交前 只对当前事务可见，因此产生的Undo日志可以在事务提交后直接删除（谁会对刚插入的数据 有可见性需求呢！！），而对于UPDATE/DELETE则需要维护多版本信息，在InnoDB里， UPDATE和DELETE操作产生的Undo日志被归成一类，即update_undo。*

# MySQL的redo日志的刷盘时机

> 原文：[https://zwmst.com/679.html](https://zwmst.com/679.html)

log buffer空间不足时

事务提交时

后台线程不停的刷刷刷

正常关闭服务器时

做所谓的checkpoint时*

# MySQL中varchar与char的区别以及varchar(50)中的50代表的涵义

> 原文：[https://zwmst.com/681.html](https://zwmst.com/681.html)

(1)、varchar与char的区别

(2)、varchar(50)中50的涵义

(3)、int（20）中20的涵义

(4)、mysql为什么这么设计*

# MySQL有哪些日志，分别是什么用处？

> 原文：[https://zwmst.com/683.html](https://zwmst.com/683.html)

mysql日志一般分为5种

错误日志：-log-err (记录启动，运行，停止mysql时出现的信息)

二进制日志：-log-bin （记录所有更改数据的语句，还用于复制，恢复数据库用）

查询日志：-log （记录建立的客户端连接和执行的语句）

慢查询日志: -log-slow-queries （记录所有执行超过long_query_time秒的所有查 询）

更新日志: -log-update （二进制日志已经代替了老的更新日志，更新日志在MySQL5.1 中不再使用）*

# 在哪些情况下会发生针对该列创建了索引但是在查询的时候并没有使用呢?

> 原文：[https://zwmst.com/685.html](https://zwmst.com/685.html)

*   使用不等于查询
*   列参与了数学运算或者函数
*   在字符串like时左边是通配符.类似于’%aaa’
*   当mysql分析全表扫描比使用索引快的时候不使用索引
*   当使用联合索引,前面一个条件为范围查询,后面的即使符合最左前缀原则,也无法使用索 引.*

# 为什么要尽量设定一个主键?

> 原文：[https://zwmst.com/687.html](https://zwmst.com/687.html)

主键是数据库确保数据行在整张表唯一性的保障,即使业务上本张表没有主键,也建议添加一个 自增长的ID列作为主键.设定了主键之后,在后续的删改查的时候可能更加快速以及确保操作数 据范围安全。*

# 主键使用自增ID还是UUID?

> 原文：[https://zwmst.com/689.html](https://zwmst.com/689.html)

推荐使用自增ID,不要使用UUID.

因为在InnoDB存储引擎中,主键索引是作为聚簇索引存在的,也就是说,主键索引的B+树叶子节 点上存储了主键索引以及全部的数据(按照顺序),如果主键索引是自增ID,那么只需要不断向后 排列即可,如果是UUID,由于到来的ID与原来的大小不确定,会造成非常多的数据插入,数据移动, 然后导致产生很多的内存碎片,进而造成插入性能的下降.

总之,在数据量大一些的情况下,用自增主键性能会好一些.

*图片来源于《高性能MySQL》: 其中默认后缀为使用自增ID,_uuid为使用UUID为主键的测 试,测试了插入100w行和300w行的性能

![image-20210813174937500](img/4db1267a4fb54b37c600e2ff7f290544.png)

关于主键是聚簇索引,如果没有主键,InnoDB会选择一个唯一键来作为聚簇索引,如果没有唯一 键,会生成一个隐式的主键。*

# 字段为什么要求定义为notnull?

> 原文：[https://zwmst.com/691.html](https://zwmst.com/691.html)

MySQL官网这样介绍:

> NULL columns require additional space in the rowto record whether their values are NULL. For MyISAM tables, each NULL columntakes one bit extra, rounded up to the nearest byte.

null值会占用更多的字节,且会在程序中造成很多与预期不符的情况。*

# 如果要存储用户的密码散列,应该使用什么字段进行存储?

> 原文：[https://zwmst.com/693.html](https://zwmst.com/693.html)

密码散列,盐,用户身份证号等固定长度的字符串应该使用char而不是varchar来存储,这样可以 节省空间且提高检索效率。*

# varchar(10)和int(10)代表什么含义?

> 原文：[https://zwmst.com/695.html](https://zwmst.com/695.html)

varchar的10代表了申请的空间长度,也是可以存储的数据的最大长度,而int的10只是代表了展示的长度,不足10位以0填充.也就是说,int(1)和int(10)所能存储的数字大小以及占用的空间都是相同的,只是在展示时按照长度展示。*

# MySQL的binlog有有几种录入格式?分别有什么区别?

> 原文：[https://zwmst.com/697.html](https://zwmst.com/697.html)

有三种格式,statement,row和mixed.

*   statement模式下,记录单元为语句.即每一个sql造成的影响会记录.由于sql的执行是有上 下文的,因此在保存的时候需要保存相关的信息,同时还有一些使用了函数之类的语句无法 被记录复制.
*   row级别下,记录单元为每一行的改动,基本是可以全部记下来但是由于很多操作,会导致大 量行的改动(比如alter table),因此这种模式的文件保存的信息太多,日志量太大.
*   mixed. 一种折中的方案,普通操作使用statement记录,当无法使用statement的时候使 用row.

此外,新版的MySQL中对row级别也做了一些优化,当表结构发生变化的时候,会记录语句而不是 逐行记录。*

# 超大分页怎么处理?

> 原文：[https://zwmst.com/699.html](https://zwmst.com/699.html)

超大的分页一般从两个方向上来解决.

*   数据库层面,这也是我们主要集中关注的(虽然收效没那么大),类似于select *from table where age > 20 limit 1000000,10这种查询其实也是有可以优化的余地 的. 这条语句需要load1000000数据然后基本上全部丢弃,只取10条当然比较慢. 当时我们 可以修改为select* from table where id in (select id from table where age > 20 limit 1000000,10).这样虽然也load了一百万的数据,但是由于索 引覆盖,要查询的所有字段都在索引中,所以速度会很快. 同时如果ID连续的好,我们还可以 select * from table where id > 1000000 limit 10,效率也是不错的,优化的 可能性有许多种,但是核心思想都一样,就是减少load的数据.
*   从需求的角度减少这种请求….主要是不做类似的需求(直接跳转到几百万页之后的具体某 一页.只允许逐页查看或者按照给定的路线走,这样可预测,可缓存)以及防止ID泄漏且连续 被人恶意攻击.

解决超大分页,其实主要是靠缓存,可预测性的提前查到内容,缓存至redis等k-V数据库中,直接 返回即可.

在阿里巴巴《Java开发手册》中,对超大分页的解决办法是类似于上面提到的第一种。

![image-20210813175148457](img/a8fcfd511c61758da797f2f695e461f1.png)*

# 关心过业务系统里面的sql耗时吗?统计过慢查询吗?对慢查询都怎么优化过?

> 原文：[https://zwmst.com/701.html](https://zwmst.com/701.html)

在业务系统中,除了使用主键进行的查询,其他的我都会在测试库上测试其耗时,慢查询的统计主 要由运维在做,会定期将业务中的慢查询反馈给我们。

慢查询的优化首先要搞明白慢的原因是什么? 是查询条件没有命中索引?是load了不需要的数据 列?还是数据量太大? 所以优化也是针对这三个方向来的

首先分析语句,看看是否load了额外的数据,可能是查询了多余的行并且抛弃掉了,可能是 加载了许多结果中并不需要的列,对语句进行分析以及重写。

分析语句的执行计划,然后获得其使用索引的情况,之后修改语句或者修改索引,使得语句 可以尽可能的命中索引。

如果对语句的优化已经无法进行,可以考虑表中的数据量是否太大,如果是的话可以进行横 向或者纵向的分表。*

# 什么是存储过程？有哪些优缺点？

> 原文：[https://zwmst.com/703.html](https://zwmst.com/703.html)

存储过程是一些预编译的SQL语句。

1、更加直白的理解：存储过程可以说是一个记录集，它是由一些T-SQL语句组成的代码块， 这些T-SQL语句代码像一个方法一样实现一些功能（对单表或多表的增删改查），然后再给这 个代码块取一个名字，在用到这个功能的时候调用他就行了。

2、存储过程是一个预编译的代码块，执行效率比较高,一个存储过程替代大量T_SQL语句 ， 可以降低网络通信量，提高通信速率,可以一定程度上确保数据安全

但是,在互联网项目中,其实是不太推荐存储过程的,比较出名的就是阿里的《Java开发手册》中 禁止使用存储过程,我个人的理解是,在互联网项目中,迭代太快,项目的生命周期也比较短,人员 流动相比于传统的项目也更加频繁,在这样的情况下,存储过程的管理确实是没有那么方便,同时, 复用性也没有写在服务层那么好。*

# 说一说三个范式

> 原文：[https://zwmst.com/705.html](https://zwmst.com/705.html)

第一范式: 每个列都不可以再拆分.

第二范式: 非主键列完全依赖于主键,而不能是依赖于主键的 一部分.

第三范式: 非主键列只依赖于主键,不依赖于其他非主键。

在设计数据库结构的时候,要尽量遵守三范式,如果不遵守,必须有足够的理由.比如性能. 事实上 我们经常会为了性能而妥协数据库的设计。*

# 什么情况下应不建或少建索引

> 原文：[https://zwmst.com/707.html](https://zwmst.com/707.html)

1、表记录太少

2、经常插入、删除、修改的表

3、数据重复且分布平均的表字段，假如一个表有10万行记录，有一个字段A只有T和F两种 值，且每个值的分布概率大约为50%，那么对这种表A字段建索引一般不会提高数据库的查询 速度。

4、经常和主字段一块查询但主字段索引值比较多的表字段*

# 什么是表分区？

> 原文：[https://zwmst.com/709.html](https://zwmst.com/709.html)

表分区，是指根据一定规则，将数据库中的一张表分解成多个更小的，容易管理的部分。从逻 辑上看，只有一张表，但是底层却是由多个物理分区组成。*

# 表分区与分表的区别

> 原文：[https://zwmst.com/711.html](https://zwmst.com/711.html)

分表：指的是通过一定规则，将一张表分解成多张不同的表。比如将用户订单记录根据时间成 多个表。

分表与分区的区别在于：分区从逻辑上来讲只有一张表，而分表则是将一张表分解成多张表。*

# 表分区有什么好处？

> 原文：[https://zwmst.com/713.html](https://zwmst.com/713.html)

1、存储更多数据。分区表的数据可以分布在不同的物理设备上，从而高效地利用多个硬件设 备。和单个磁盘或者文件系统相比，可以存储更多数据

2、优化查询。在where语句中包含分区条件时，可以只扫描一个或多个分区表来提高查询效 率；涉及sum和count语句时，也可以在多个分区上并行处理，最后汇总结果。

3、分区表更容易维护。例如：想批量删除大量数据可以清除整个分区。

4、避免某些特殊的瓶颈，例如InnoDB的单个索引的互斥访问，ext3问价你系统的inode锁竞 争等。*

# MVVC了解过吗

> 原文：[https://zwmst.com/715.html](https://zwmst.com/715.html)

MySQL InnoDB存储引擎，实现的是基于多版本的并发控制协议——MVCC (Multi-Version Concurrency Control)

注：与MVCC相对的，是基于锁的并发控制，Lock-Based Concurrency Control

MVCC最大的好处：读不加锁，读写不冲突。在读多写少的OLTP应用中，读写不冲突是非常 重要的，极大的增加了系统的并发性能，现阶段几乎所有的RDBMS，都支持了MVCC。

1.  LBCC：Lock-Based Concurrency Control，基于锁的并发控制

2.  MVCC：Multi-Version Concurrency Control

基于多版本的并发控制协议。纯粹基于锁的并发机制并发量低，MVCC是在基于锁的并 发控制上的改进，主要是在读操作上提高了并发量。*

# 在MVCC并发控制中，读操作可以分成哪几类？

> 原文：[https://zwmst.com/717.html](https://zwmst.com/717.html)

1.  快照读 (snapshot read)：读取的是记录的可见版本 (有可能是历史版本)，不用加锁 （共享读锁s锁也不加，所以不会阻塞其他事务的写）

2.  当前读 (current read)：读取的是记录的最新版本，并且，当前读返回的记录，都会加 上锁，保证其他事务不会再并发修改这条记录*

# 行级锁定的优点

> 原文：[https://zwmst.com/719.html](https://zwmst.com/719.html)

1、当在许多线程中访问不同的行时只存在少量锁定冲突。

2、回滚时只有少量的更改

3、可以长时间锁定单一的行。*

# 行级锁定的缺点

> 原文：[https://zwmst.com/721.html](https://zwmst.com/721.html)

1.  比页级或表级锁定占用更多的内存。

2.  当在表的大部分中使用时，比页级或表级锁定速度慢，因为你必须获取更多的锁。

3.  如果你在大部分数据上经常进行GROUP BY操作或者必须经常扫描整个表，比其它锁定 明显慢很多。

4.  用高级别锁定，通过支持不同的类型锁定，你也可以很容易地调节应用程序，因为其锁 成本小于行级锁定。*

# MySQL优化

> 原文：[https://zwmst.com/723.html](https://zwmst.com/723.html)

1.  开启查询缓存，优化查询

2.  explain你的select查询，这可以帮你分析你的查询语句或是表结构的性能瓶颈。 EXPLAIN 的查询结果还会告诉你你的索引主键被如何利用的，你的数据表是如何被搜索 和排序的

3.  当只要一行数据时使用limit 1，MySQL数据库引擎会在找到一条数据后停止搜索，而不 是继续往后查少下一条符合记录的数据

4.  为搜索字段建索引

5.  使用 ENUM 而不是 VARCHAR。如果你有一个字段，比如“性别”，“国家”，“民族”， “状态”或“部门”，你知道这些字段的取值是有限而且固定的，那么，你应该使用 ENUM 而不是VARCHAR

6.  Prepared StatementsPrepared Statements很像存储过程，是一种运行在后台的SQL 语句集合，我们可以从使用 prepared statements 获得很多好处，无论是性能问题还是 安全问题。Prepared Statements 可以检查一些你绑定好的变量，这样可以保护你的程序不会受到 “SQL注入式”攻击

7.  垂直分表

8.  选择正确的存储引擎*

# key和index的区别

> 原文：[https://zwmst.com/725.html](https://zwmst.com/725.html)

1.  key 是数据库的物理结构，它包含两层意义和作用，一是约束（偏重于约束和规范数据 库的结构完整性），二是索引（辅助查询用的）。包括primary key, unique key, foreign key 等

2.  index是数据库的物理结构，它只是辅助查询的，它创建时会在另外的表空间（mysql中 的innodb表空间）以一个类似目录的结构存储。索引要分类的话，分为前缀索引、全文 本索引等；*

# delete、truncate、drop区别

> 原文：[https://zwmst.com/727.html](https://zwmst.com/727.html)

*   truncate和delete只删除数据，不删除表结构 ,drop删除表结构，并且释放所占的空间。
*   删除数据的速度，drop> truncate > delete delete属于DML语言，需要事务管理，commit之后才能生效。
*   drop和truncate属于 DDL语言，操作立刻生效，不可回滚。
*   使用场合： 当你不再需要该表时， 用 drop; 当你 仍要保留该表，但要删除所有记录时， 用 truncate; 当你要删除部分记录时（always with a where clause), 用 delete。*

# MySQL主从复制原理流程

> 原文：[https://zwmst.com/729.html](https://zwmst.com/729.html)

*   主：binlog线程——记录下所有改变了数据库数据的语句，放进master上的binlog 中；
*   从：io线程——在使用start slave 之后，负责从master上拉取 binlog 内容，放进 自己 的relay log中；
*   从：sql执行线程——执行relay log中的语句；*

# 自增主键最大ID记录，MyISAM和InnoDB分别是如何存储的

> 原文：[https://zwmst.com/731.html](https://zwmst.com/731.html)

*   MyISAM表把自增主键的最大ID记录到数据文件里
*   InnoDB表把自增主键的最大ID记录到内存中*

# Mysql如何优化DISTINCT?

> 原文：[https://zwmst.com/733.html](https://zwmst.com/733.html)

DISTINCT在所有列上转换为GROUP BY，并与ORDER BY子句结合使用。*

# 解释MySQL外连接、内连接与自连接的区别

> 原文：[https://zwmst.com/735.html](https://zwmst.com/735.html)

先说什么是交叉连接: 交叉连接又叫笛卡尔积，它是指不使用任何条件，直接将一个表的所有记录和另一个表中的所有记录一一匹配。

内连接则是只有条件的交叉连接，根据某个条件筛选出符合条件的记录，不符合条件的记录不会出现在结果集中，即内连接只连接匹配的行。 外连接 其结果集中不仅包含符合连接条件的行，而且还会包括左表、右表或两个表中 的所有数据行，这三种情况依次称之为左外连接，右外连接，和全外连接。

左外连接，也称左连接，左表为主表，左表中的所有记录都会出现在结果集中，对于那些在右表中并没有匹配的记录，仍然要显示，右边对应的那些字段值以NULL来填充。右外连接，也 称右连接，右表为主表，右表中的所有记录都会出现在结果集中。左连接和右连接可以互换， MySQL目前还不支持全外连接。*

# 1120.一张表，里面有 ID 自增主键，当 insert 了 17 条记录之后，删除了第 15,16,17 条记录， 再把 Mysql 重启，再 insert 一条记录，这条记录的 ID 是 18 还是 15 ？

> 原文：[https://zwmst.com/5539.html](https://zwmst.com/5539.html)

1.  如果表的类型是 MyISAM，那么是 18因为 MyISAM 表会把自增主键的最大 ID 记录到数据文件里，重启 MySQL 自增主键的最大ID 也不会丢失
2.  如果表的类型是 InnoDB，那么是 15InnoDB 表只是把自增主键的最大 ID 记录到内存中，所以重启数据库或者是对表进行OPTIMIZE 操作，都会导致最大 ID 丢失*

# 1121.Mysql 的技术特点是什么？

> 原文：[https://zwmst.com/5541.html](https://zwmst.com/5541.html)

Mysql 数据库软件是一个客户端或服务器系统，其中包括：支持各种客户端程序和库的多线程 SQL 服务器、不同的后端、广泛的应用程序编程接口和管理工具。*

# 1122.Heap 表是什么？

> 原文：[https://zwmst.com/5543.html](https://zwmst.com/5543.html)

HEAP 表存在于内存中，用于临时高速存储。
BLOB 或 TEXT 字段是不允许的
只能使用比较运算符=，<，>，=>，= <
HEAP 表不支持 AUTO_INCREMENT
索引不可为 NULL*

# 1123.Mysql 服务器默认端口是什么？

> 原文：[https://zwmst.com/5545.html](https://zwmst.com/5545.html)

Mysql 服务器的默认端口是 3306。*

# 1124.与 Oracle 相比，Mysql 有什么优势？

> 原文：[https://zwmst.com/5547.html](https://zwmst.com/5547.html)

Mysql 是开源软件，随时可用，无需付费。
Mysql 是便携式的带有命令提示符的 GUI。
使用 Mysql 查询浏览器支持管理*

# 1125.如何区分 FLOAT 和 DOUBLE？

> 原文：[https://zwmst.com/5549.html](https://zwmst.com/5549.html)

以下是 FLOAT 和 DOUBLE 的区别：
浮点数以 8 位精度存储在 FLOAT 中，并且有四个字节。
浮点数存储在 DOUBLE 中，精度为 18 位，有八个字节。*

# 1126.区分 CHAR_LENGTH 和 LENGTH？

> 原文：[https://zwmst.com/5551.html](https://zwmst.com/5551.html)

CHAR_LENGTH 是字符数，而 LENGTH 是字节数。Latin 字符的这两个数据是相同的，但是对于 Unicode 和其他编码，它们是不同的。*

# 1127.请简洁描述 Mysql 中 InnoDB 支持的四种事务隔离级别名称，以及逐级之间的区别？

> 原文：[https://zwmst.com/5553.html](https://zwmst.com/5553.html)

SQL 标准定义的四个隔离级别为：
read uncommited ：读到未提交数据
read committed：脏读，不可重复读
repeatable read：可重读
serializable ：串行事物*

# 1128.在 Mysql 中 ENUM 的用法是什么？

> 原文：[https://zwmst.com/5555.html](https://zwmst.com/5555.html)

ENUM 是一个字符串对象，用于指定一组预定义的值，并可在创建表时使用。

```
Create table size(name ENUM('Smail,'Medium','Large');
```*

# 1129.如何定义 REGEXP？

> 原文：[https://zwmst.com/5557.html](https://zwmst.com/5557.html)

REGEXP 是模式匹配，其中匹配模式在搜索值的任何位置。*

# 1130.CHAR 和 VARCHAR 的区别？

> 原文：[https://zwmst.com/5559.html](https://zwmst.com/5559.html)

以下是 CHAR 和 VARCHAR 的区别：
CHAR 和 VARCHAR 类型在存储和检索方面有所不同
CHAR 列长度固定为创建表时声明的长度，长度值范围是 1 到 255
当 CHAR 值被存储时，它们被用空格填充到特定长度，检索 CHAR 值时需删除尾随空格。*

# 1131.列的字符串类型可以是什么？

> 原文：[https://zwmst.com/5561.html](https://zwmst.com/5561.html)

字符串类型是：
SET
BLOB
ENUM
CHAR
TEXT
VARCHAR*

# 1132.如何获取当前的 Mysql 版本？

> 原文：[https://zwmst.com/5563.html](https://zwmst.com/5563.html)

SELECT VERSION();用于获取当前 Mysql 的版本。*

# 1133.Mysql 中使用什么存储引擎？

> 原文：[https://zwmst.com/5565.html](https://zwmst.com/5565.html)

存储引擎称为表类型，数据使用各种技术存储在文件中。
技术涉及：
Storage mechanism
Locking levels
Indexing
Capabilities and functions.*

# 1134.Mysql 驱动程序是什么？

> 原文：[https://zwmst.com/5567.html](https://zwmst.com/5567.html)

以下是 Mysql 中可用的驱动程序：
PHP 驱动程序
JDBC 驱动程序
ODBC 驱动程序
CWRAPPER
PYTHON 驱动程序
PERL 驱动程序
RUBY 驱动程序
CAP11PHP 驱动程序
Ado.net5.mxj*

# 1135.TIMESTAMP 在 UPDATE CURRENT_TIMESTAMP 数据类型上做什么？

> 原文：[https://zwmst.com/5569.html](https://zwmst.com/5569.html)

创建表时 TIMESTAMP 列用 Zero 更新。只要表中的其他字段发生更改，UPDATE CURRENT_TIMESTAMP 修饰符就将时间戳字段更新为当前时间。*

# 1136.主键和候选键有什么区别？

> 原文：[https://zwmst.com/5571.html](https://zwmst.com/5571.html)

表格的每一行都由主键唯一标识,一个表只有一个主键。
主键也是候选键。按照惯例，候选键可以被指定为主键，并且可以用于任何外键引用。*

# 1137.如何使用 Unix shell 登录 Mysql？

> 原文：[https://zwmst.com/5573.html](https://zwmst.com/5573.html)

我们可以通过以下命令登录：
[mysql dir]/bin/mysql -h hostname -u*

# 1138.myisamchk 是用来做什么的？

> 原文：[https://zwmst.com/5575.html](https://zwmst.com/5575.html)

它用来压缩 MyISAM 表，这减少了磁盘或内存使用。*

# 1139.、如何控制 HEAP 表的最大尺寸？

> 原文：[https://zwmst.com/5577.html](https://zwmst.com/5577.html)

Heal 表的大小可通过称为 max_heap_table_size 的 Mysql 配置变量来控制。*

# 1140.MyISAM Static 和 MyISAM Dynamic 有什么区别？

> 原文：[https://zwmst.com/5579.html](https://zwmst.com/5579.html)

在 MyISAM Static 上的所有字段有固定宽度。动态 MyISAM 表将具有像 TEXT，BLOB 等字段，以适应不同长度的数据类型。点击这里有一套最全阿里面试题总结。
MyISAM Static 在受损情况下更容易恢复。*

# 1141.federated 表是什么？

> 原文：[https://zwmst.com/5581.html](https://zwmst.com/5581.html)

federated 表，允许访问位于其他服务器数据库上的表。*

# 1142.如果一个表有一列定义为 TIMESTAMP，将发生什么？

> 原文：[https://zwmst.com/5583.html](https://zwmst.com/5583.html)

每当行被更改时，时间戳字段将获取当前时间戳。*

# 1143.列设置为 AUTO INCREMENT 时，如果在表中达到最大值，会发生什么情况？

> 原文：[https://zwmst.com/5585.html](https://zwmst.com/5585.html)

它会停止递增，任何进一步的插入都将产生错误，因为密钥已被使用。*

# 1144.怎样才能找出最后一次插入时分配了哪个自动增量？

> 原文：[https://zwmst.com/5587.html](https://zwmst.com/5587.html)

LAST_INSERT_ID 将返回由 Auto_increment 分配的最后一个值，并且不需要指定表名称。*

# 1145.你怎么看到为表格定义的所有索引？

> 原文：[https://zwmst.com/5589.html](https://zwmst.com/5589.html)

索引是通过以下方式为表格定义的：
SHOW INDEX FROM*

# 1146.LIKE 声明中的％和_是什么意思？

> 原文：[https://zwmst.com/5591.html](https://zwmst.com/5591.html)

％对应于 0 个或更多字符，_只是 LIKE 语句中的一个字符。*

# 1147.如何在 Unix 和 Mysql 时间戳之间进行转换？

> 原文：[https://zwmst.com/5593.html](https://zwmst.com/5593.html)

UNIX_TIMESTAMP 是从 Mysql 时间戳转换为 Unix 时间戳的命令
FROM_UNIXTIME 是从 Unix 时间戳转换为 Mysql 时间戳的命令*

# 1148.列对比运算符是什么？

> 原文：[https://zwmst.com/5595.html](https://zwmst.com/5595.html)

在 SELECT 语句的列比较中使用=，<>，<=，<，> =，>，<<，>>，<=>，AND，OR 或 LIKE 运算符。*

# 1149.我们如何得到受查询影响的行数？

> 原文：[https://zwmst.com/5597.html](https://zwmst.com/5597.html)

行数可以通过以下代码获得：

```
SELECT COUNT(user_id)FROM users;
```*

# 1150.Mysql 查询是否区分大小写？

> 原文：[https://zwmst.com/5599.html](https://zwmst.com/5599.html)

不区分
SELECT VERSION(), CURRENT_DATE;
SeLect version(), current_date;
seleCt vErSiOn(), current_DATE;
所有这些例子都是一样的，Mysql 不区分大小写。*

# 1151.LIKE 和 REGEXP 操作有什么区别？

> 原文：[https://zwmst.com/5602.html](https://zwmst.com/5602.html)

LIKE 和 REGEXP 运算符用于表示^和％。

```
SELECT * FROM employee WHERE emp_name REGEXP "^b";
SELECT * FROM employee WHERE emp_name LIKE "%b";
```*

# 1152.BLOB 和 TEXT 有什么区别？

> 原文：[https://zwmst.com/5604.html](https://zwmst.com/5604.html)

BLOB 是一个二进制对象，可以容纳可变数量的数据。有四种类型的 BLOB –
TINYBLOB
BLOB
MEDIUMBLOB 和
LONGBLOB
它们只能在所能容纳价值的最大长度上有所不同。
TEXT 是一个不区分大小写的 BLOB。四种 TEXT 类型
TINYTEXT
TEXT
MEDIUMTEXT 和
LONGTEXT
它们对应于四种 BLOB 类型，并具有相同的最大长度和存储要求。
BLOB 和 TEXT 类型之间的唯一区别在于对 BLOB 值进行排序和比较时区分大小写，对 TEXT值不区分大小写。*

# 1153.mysql_fetch_array 和 mysql_fetch_object 的区别是什么？

> 原文：[https://zwmst.com/5606.html](https://zwmst.com/5606.html)

以下是 mysql_fetch_array 和 mysql_fetch_object 的区别：
mysql_fetch_array（） – 将结果行作为关联数组或来自数据库的常规数组返回。
mysql_fetch_object – 从数据库返回结果行作为对象。*

# 1154.我们如何在 mysql 中运行批处理模式？

> 原文：[https://zwmst.com/5608.html](https://zwmst.com/5608.html)

以下命令用于在批处理模式下运行：

```
mysql;
mysql mysql.out
```*

# 1155.MyISAM 表格将在哪里存储，并且还提供其存储格式？

> 原文：[https://zwmst.com/5610.html](https://zwmst.com/5610.html)

每个 MyISAM 表格以三种格式存储在磁盘上：

1.  “.frm”文件存储表定义

2.  数据文件具有“.MYD”（MYData）扩展名

索引文件具有“.MYI”（MYIndex）扩展名*

# 1156.Mysql 中有哪些不同的表格？

> 原文：[https://zwmst.com/5612.html](https://zwmst.com/5612.html)

共有 5 种类型的表格：
MyISAM
Heap
Merge
INNODB
ISAM
MyISAM 是 Mysql 的默认存储引擎。*

# 1157.ISAM 是什么？

> 原文：[https://zwmst.com/5614.html](https://zwmst.com/5614.html)

ISAM 简称为索引顺序访问方法。它是由 IBM 开发的，用于在磁带等辅助存储系统上存储和检索数据。*

# 1158.InnoDB 是什么？

> 原文：[https://zwmst.com/5616.html](https://zwmst.com/5616.html)

lnnoDB 是一个由 Oracle 公司开发的 Innobase Oy 事务安全存储引擎。*

# 1159.Mysql 如何优化 DISTINCT？

> 原文：[https://zwmst.com/5618.html](https://zwmst.com/5618.html)

DISTINCT 在所有列上转换为 GROUP BY，并与 ORDER BY 子句结合使用。

```
1
SELECT DISTINCT t1.a FROM t1,t2 where t1.a=t2.a;
```*

# 1160.如何输入字符为十六进制数字？

> 原文：[https://zwmst.com/5620.html](https://zwmst.com/5620.html)

如果想输入字符为十六进制数字，可以输入带有单引号的十六进制数字和前缀（X），或者只用（Ox）前缀输入十六进制数字。
如果表达式上下文是字符串，则十六进制数字串将自动转换为字符串。*

# 1161.如何显示前 50 行？

> 原文：[https://zwmst.com/5623.html](https://zwmst.com/5623.html)

在 Mysql 中，使用以下代码查询显示前 50 行：

```
SELECT*FROM
LIMIT 0,50;
```*

# 1162.可以使用多少列创建索引？

> 原文：[https://zwmst.com/5625.html](https://zwmst.com/5625.html)

任何标准表最多可以创建 16 个索引列。*

# 1163.NOW（）和 CURRENT_DATE（）有什么区别？

> 原文：[https://zwmst.com/5627.html](https://zwmst.com/5627.html)

NOW（）命令用于显示当前年份，月份，日期，小时，分钟和秒。
CURRENT_DATE（）仅显示当前年份，月份和日期。*

# 1164.什么样的对象可以使用 CREATE 语句创建？

> 原文：[https://zwmst.com/5629.html](https://zwmst.com/5629.html)

以下对象是使用 CREATE 语句创建的：
DATABASE
EVENT
FUNCTION
INDEX
PROCEDURE
TABLE
TRIGGER
USER
VIEW*

# 1165.Mysql 表中允许有多少个 TRIGGERS？

> 原文：[https://zwmst.com/5631.html](https://zwmst.com/5631.html)

在 Mysql 表中允许有六个触发器，如下：
BEFORE INSERT
AFTER INSERT
BEFORE UPDATE
AFTER UPDATE
BEFORE DELETE
AFTER DELETE*

# 1166.什么是非标准字符串类型？

> 原文：[https://zwmst.com/5633.html](https://zwmst.com/5633.html)

以下是非标准字符串类型：
TINYTEXT
TEXT
MEDIUMTEXT
LONGTEXT*

# 1167.什么是通用 SQL 函数？

> 原文：[https://zwmst.com/5635.html](https://zwmst.com/5635.html)

CONCAT(A, B) – 连接两个字符串值以创建单个字符串输出。通常用于将两个或多个字段合并为一个字段。
FORMAT(X, D)- 格式化数字 X 到 D 有效数字。
CURRDATE(), CURRTIME()- 返回当前日期或时间。
NOW（） – 将当前日期和时间作为一个值返回。
MONTH（），DAY（），YEAR（），WEEK（），WEEKDAY（） – 从日期值中提取给定数据。
HOUR（），MINUTE（），SECOND（） – 从时间值中提取给定数据。
DATEDIFF（A，B） – 确定两个日期之间的差异，通常用于计算年龄
SUBTIMES（A，B） – 确定两次之间的差异。
FROMDAYS（INT） – 将整数天数转换为日期值。*

# 1168.解释访问控制列表

> 原文：[https://zwmst.com/5637.html](https://zwmst.com/5637.html)

ACL（访问控制列表）是与对象关联的权限列表。这个列表是 Mysql 服务器安全模型的基础，它有助于排除用户无法连接的问题。
Mysql 将 ACL（也称为授权表）缓存在内存中。当用户尝试认证或运行命令时，Mysql 会按照预定的顺序检查 ACL 的认证信息和权限。*

# 1169.MYSQL 支持事务吗？

> 原文：[https://zwmst.com/5639.html](https://zwmst.com/5639.html)

在缺省模式下，MYSQL 是 autocommit 模式的，所有的数据库更新操作都会即时提交，所以在缺省情况下，mysql 是不支持事务的。
但是如果你的 MYSQL 表类型是使用 InnoDB Tables 或 BDB tables 的话，你的 MYSQL 就可以使用事务处理,使用 SET AUTOCOMMIT=0 就可以使 MYSQL 允许在非 autocommit 模式，在非autocommit 模式下，你必须使用 COMMIT 来提交你的更改，或者用 ROLLBACK 来回滚你的更改。
示例如下：

```
START TRANSACTION;
SELECT @A:=SUM(salary) FROM table1 WHERE type=1;
UPDATE table2 SET summmary=@A WHERE type=1;
COMMIT;
```*

# 1170.mysql 里记录货币用什么字段类型好

> 原文：[https://zwmst.com/5641.html](https://zwmst.com/5641.html)

NUMERIC 和 DECIMAL 类型被 Mysql 实现为同样的类型，这在 SQL92 标准允许。他们被用于保存值，该值的准确精度是极其重要的值，例如与金钱有关的数据。当声明一个类是这些类型之一时，精度和规模的能被(并且通常是)指定；
例如：

```
salary DECIMAL(9,2)
```

在这个例子中，9(precision)代表将被用于存储值的总的小数位数，而 2(scale)代表将被用于存储小数点后的位数。
因此，在这种情况下，能被存储在 salary 列中的值的范围是从-9999999.99 到 9999999.99。
在 ANSI/ISO SQL92 中，句法 DECIMAL(p)等价于 DECIMAL(p,0)。
同样，句法 DECIMAL 等价于 DECIMAL(p,0)，这里实现被允许决定值 p。Mysql 当前不支持DECIMAL/NUMERIC 数据类型的这些变种形式的任一种。
这一般说来不是一个严重的问题，因为这些类型的主要益处得自于明显地控制精度和规模的能力。
DECIMAL 和 NUMERIC 值作为字符串存储，而不是作为二进制浮点数，以便保存那些值的小数精度。
一个字符用于值的每一位、小数点(如果 scale>0)和“-”符号(对于负值)。如果 scale 是 0，DECIMAL 和 NUMERIC 值不包含小数点或小数部分。
DECIMAL 和 NUMERIC 值得最大的范围与 DOUBLE 一样，但是对于一个给定的 DECIMAL 或NUMERIC 列，实际的范围可由制由给定列的 precision 或 scale 限制。
当这样的列赋给了小数点后面的位超过指定 scale 所允许的位的值，该值根据 scale 四舍五入。
当一个 DECIMAL 或 NUMERIC 列被赋给了其大小超过指定(或缺省的）precision 和 scale 隐含的范围的值，Mysql 存储表示那个范围的相应的端点值。
我希望本文可以帮助你提升技术水平。那些，感觉学的好难，甚至会令你沮丧的人，别担心，我认为，如果你愿意试一试本文介绍的几点，会向前迈进，克服这种感觉。这些要点也许对你不适用，但你会明确一个重要的道理：接受自己觉得受困这个事实是摆脱这个困境的第一步。*

# 1171.MYSQL 数据表在什么情况下容易损坏？

> 原文：[https://zwmst.com/5643.html](https://zwmst.com/5643.html)

服务器突然断电导致数据文件损坏。
强制关机，没有先关闭 mysql 服务等。*

# 1172.mysql 有关权限的表都有哪几个？

> 原文：[https://zwmst.com/5645.html](https://zwmst.com/5645.html)

Mysql 服务器通过权限表来控制用户对数据库的访问，权限表存放在 mysql 数据库里，由mysql_install_db 脚本初始化。这些权限表分别 user，db，table_priv，columns_priv 和host。*

# 1173.Mysql 中有哪几种锁？

> 原文：[https://zwmst.com/5647.html](https://zwmst.com/5647.html)

MyISAM 支持表锁，InnoDB 支持表锁和行锁，默认为行锁
表级锁：开销小，加锁快，不会出现死锁。锁定粒度大，发生锁冲突的概率最高，并发量最低
行级锁：开销大，加锁慢，会出现死锁。锁力度小，发生锁冲突的概率小，并发度最高*

# 1174.数据库三范式是什么?

> 原文：[https://zwmst.com/5649.html](https://zwmst.com/5649.html)

1.  第一范式（1NF）：字段具有原子性,不可再分。(所有关系型数据库系统都满足第一范式数据库表中的字段都是单一属性的，不可再分)
2.  第二范式（2NF）是在第一范式（1NF）的基础上建立起来的，即满足第二范式（2NF）必须先满足第一范式（1NF）。要求数据库表中的每个实例或行必须可以被惟一地区分。通常需要为表加上一个列，以存储各个实例的惟一标识。这个惟一属性列被称为主关键字或主键。
3.  满足第三范式（3NF）必须先满足第二范式（2NF）。简而言之，第三范式（3NF）要求一个数据库表中不包含已在其它表中已包含的非主关键字信息。 >所以第三范式具有如下特征： >>1\. 每一列只有一个值 >>2\. 每一行都能区分。 >>3\. 每一个表都不包含其他表已经包含的非主关键字信息。*

# 1175.有哪些数据库优化方面的经验?

> 原文：[https://zwmst.com/5651.html](https://zwmst.com/5651.html)

1.  用 PreparedStatement， 一般来说比 Statement 性能高：一个 sql发给服务器去执行，涉及步骤：语法检查、语义分析， 编译，缓存。
2.  有外键约束会影响插入和删除性能，如果程序能够保证数据的完整性，那在设计数据库时就去掉外键。
3.  表中允许适当冗余，譬如，主题帖的回复数量和最后回复时间等
4.  UNION ALL 要比 UNION 快很多，所以，如果可以确认合并的两个结果集中不包含重复数据且不需要排序时的话，那么就使用 UNIONALL。 >>UNION 和 UNION ALL 关键字都是将两个结果集合并为一个，但这两者从使用和效率上来说都有所不同。

    > 1.  对重复结果的处理：UNION 在进行表链接后会筛选掉重复的记录，Union All 不会去除重复记录。
    > 2.  对排序的处理：Union 将会按照字段的顺序进行排序；UNION ALL 只是简单的将两个结果合并后就返回。*

# 1176.请简述常用的索引有哪些种类?

> 原文：[https://zwmst.com/5653.html](https://zwmst.com/5653.html)

1.  普通索引: 即针对数据库表创建索引
2.  唯一索引: 与普通索引类似，不同的就是：MySQL 数据库索引列的值必须唯一，但允许有空值
3.  主键索引: 它是一种特殊的唯一索引，不允许有空值。一般是在建表的时候同时创建主键索引
4.  组合索引: 为了进一步榨取 MySQL 的效率，就要考虑建立组合索引。即将数据库表中的多个字段联合起来作为一个组合索引。*

# 1177.以及在 mysql 数据库中索引的工作机制是什么？

> 原文：[https://zwmst.com/5655.html](https://zwmst.com/5655.html)

数据库索引，是数据库管理系统中一个排序的数据结构，以协助快速查询、更新数据库表中数据。索引的实现通常使用 B 树及其变种 B+树*

# 1178.MySQL 的基础操作命令:

> 原文：[https://zwmst.com/5657.html](https://zwmst.com/5657.html)

1.  MySQL 是否处于运行状态:Debian 上运行命令 service mysqlstatus，在 RedHat 上运行命令 service mysqld status
2.  开启或停止 MySQL 服务 :运行命令 service mysqld start 开启服务；运行命令 service mysqld stop 停止服务
3.  Shell 登入 MySQL: 运行命令 mysql -u root -p
4.  列出所有数据库:运行命令 show databases;
5.  切换到某个数据库并在上面工作:运行命令 use databasename; 进入名为 databasename 的数据库
6.  列出某个数据库内所有表: show tables;
7.  获取表内所有 Field 对象的名称和类型 :describe table_name;*

# 1179.mysql 的复制原理以及流程。

> 原文：[https://zwmst.com/5659.html](https://zwmst.com/5659.html)

Mysql 内建的复制功能是构建大型，高性能应用程序的基础。将 Mysql 的数据分布到多个系统上去，这种分布的机制，是通过将 Mysql 的某一台主机的数据复制到其它主机（slaves）上，并重新执行一遍来实现的。 * 复制过程中一个服务器充当主服务器，而一个或多个其它服务器充当从服务器。主服务器将更新写入二进制日志文件，并维护文件的一个索引以跟踪日志循环。这些日志可以记录发送到从服务器的更新。 当一个从服务器连接主服务器时，它通知主服务器在日志中读取的最后一次成功更新的位置。从服务器接收从那时起发生的任何更新，然后封锁并等待主服务器通知新的更新。 过程如下

1.  主服务器把更新记录到二进制日志文件中。
2.  从服务器把主服务器的二进制日志拷贝到自己的中继日志（replay log）中。
3.  从服务器重做中继日志中的时间，把更新应用到自己的数据库上。*

# 1180.mysql 支持的复制类型?

> 原文：[https://zwmst.com/5661.html](https://zwmst.com/5661.html)

1.  基于语句的复制： 在主服务器上执行的 SQL 语句，在从服务器上执行同样的语句。MySQL 默认采用基于语句的复制，效率比较高。 一旦发现没法精确复制时，会自动选着基于行的复制。
2.  基于行的复制：把改变的内容复制过去，而不是把命令在从服务器上执行一遍. 从 mysql5.0 开始支持
3.  混合类型的复制: 默认采用基于语句的复制，一旦发现基于语句的无法精确的复制时，就会采用基于行的复制。*

# 1181.mysql 中 myisam 与 innodb 的区别？

> 原文：[https://zwmst.com/5664.html](https://zwmst.com/5664.html)

1.  事务支持 > MyISAM：强调的是性能，每次查询具有原子性,其执行数度比 InnoDB 类型更快，但是不提供事务支持。 > InnoDB：提供事务支持事务，外部键等高级数据库功能。 具有事务(commit)、回滚(rollback)和崩溃修复能力(crash recovery capabilities)的事务安全(transaction-safe (ACID compliant))型表。
2.  InnoDB 支持行级锁，而 MyISAM 支持表级锁. >> 用户在操作myisam 表时，select，update，delete，insert 语句都会给表自动加锁，如果加锁以后的表满足 insert 并发的情况下，可以在表的尾部插入新的数据。
3.  InnoDB 支持 MVCC, 而 MyISAM 不支持
4.  InnoDB 支持外键，而 MyISAM 不支持
5.  表主键 > MyISAM：允许没有任何索引和主键的表存在，索引都是保存行的地址。 > InnoDB：如果没有设定主键或者非空唯一索引，就会自动生成一个 6 字节的主键(用户不可见)，数据是主索引的一部分，附加索引保存的是主索引的值。
6.  InnoDB 不支持全文索引，而 MyISAM 支持。
7.  可移植性、备份及恢复 > MyISAM：数据是以文件的形式存储，所以在跨平台的数据转移中会很方便。在备份和恢复时可单独针对某个表进行操作。 > InnoDB：免费的方案可以是拷贝数据文件、备份binlog，或者用 mysqldump，在数据量达到几十 G 的时候就相对痛苦了
8.  存储结构 > MyISAM：每个 MyISAM 在磁盘上存储成三个文件。第一个文件的名字以表的名字开始，扩展名指出文件类型。.frm 文件存储表定义。数据文件的扩展名为.MYD (MYData)。索引文件的扩展名是.MYI (MYIndex)。 > InnoDB：所有的表都保存在同一个数据文件中（也可能是多个文件，或者是独立的表空间文件），InnoDB 表的大小只受限于操作系统文件的大小，一般为 2GB。*

# 1182.mysql 中 varchar 与 char 的区别以及 varchar(50)中的 50 代表的涵 义？

> 原文：[https://zwmst.com/5666.html](https://zwmst.com/5666.html)

1.  varchar 与 char 的区别: char 是一种固定长度的类型，varchar 则是一种可变长度的类型.
2.  varchar(50)中 50 的涵义 : 最多存放 50 个字节
3.  int（20）中 20 的涵义: int(M)中的 M indicates the maximumdisplay width (最大显示宽度)for integer types. The maximumlegal display width is 255.*

# 1183.MySQL 中 InnoDB 支持的四种事务隔离级别名称，以及逐级之间的区 别？

> 原文：[https://zwmst.com/5668.html](https://zwmst.com/5668.html)

1.  Read Uncommitted（读取未提交内容） >> 在该隔离级别，所有事务都可以看到其他未提交事务的执行结果。本隔离级别很少用于实际应用，因为它的性能也不比其他级别好多少。读取未提交的数据，也被称之为脏读（Dirty Read）。
2.  Read Committed（读取提交内容） >> 这是大多数数据库系统的默认隔离级别（但不是 MySQL 默认的）。它满足了隔离的简单定义：一个事务只能看见已经提交事务所做的改变。这种隔离级别也支持所谓的不可重复读（Nonrepeatable Read），因为同一事务的其他实例在该实例处理其间可能会有新的 commit，所以同一 select 可能返回不同结果。
3.  Repeatable Read（可重读） >> 这是 MySQL 的默认事务隔离级别，它确保同一事务的多个实例在并发读取数据时，会看到同样的数据行。不过理论上，这会导致另一个棘手的问题：幻读（PhantomRead）。简单的说，幻读指当用户读取某一范围的数据行时，另一个事务又在该范围内插入了新行，当用户再读取该范围的数据行时，会发现有新的“幻影” 行。InnoDB 和 Falcon 存储引擎通过多版本并发控制（MVCC，Multiversion Concurrency Control 间隙锁）机制解决了该问题。注：其实多版本只是解决不可重复读问题，而加上间隙锁（也就是它这里所谓的并发控制）才解决了幻读问题。
4.  Serializable（可串行化） >> 这是最高的隔离级别，它通过强制事务排序，使之不可能相互冲突，从而解决幻读问题。简言之，它是在每个读的数据行上加上共享锁。在这个级别，可能导致大量的超时现象和锁竞争。*

# 1184.表中有大字段 X（例如：text 类型），且字段 X 不会经常更新，以读为 为主，将该字段拆成子表好处是什么？

> 原文：[https://zwmst.com/5670.html](https://zwmst.com/5670.html)

如果字段里面有大字段（text,blob)类型的，而且这些字段的访问并不多，这时候放在一起就变成缺点了。 MYSQL 数据库的记录存储是按行存储的，数据块大小又是固定的（16K），每条记录越小，相同的块存储的记录就越多。此时应该把大字段拆走，这样应付大部分小字段的查询时，就能提高效率。当需要查询大字段时，此时的关联查询是不可避免的，但也是值得的。拆分开后，对字段的 UPDAE 就要 UPDATE 多个表了*

# 1185.MySQL 中 InnoDB 引擎的行锁是通过加在什么上完成（或称实现） 的？

> 原文：[https://zwmst.com/5672.html](https://zwmst.com/5672.html)

InnoDB 行锁是通过给索引上的索引项加锁来实现的，这一点 MySQL 与Oracle 不同，后者是通过在数据块中对相应数据行加锁来实现的。InnoDB 这种行锁实现特点意味着：只有通过索引条件检索数据，InnoDB 才使用行级锁，否则，InnoDB 将使用表锁！*

# 1186.MySQL 中控制内存分配的全局参数，有哪些？

> 原文：[https://zwmst.com/5674.html](https://zwmst.com/5674.html)

1.  Keybuffersize： > *keybuffersize 指定索引缓冲区的大小，它决定索引处理的速度，尤其是索引读的速度。通过检查状态值Keyreadrequests 和 Keyreads，可以知道 keybuffersize 设置是否合理。比例 keyreads /keyreadrequests 应该尽可能的低，至少是1:100，1:1000 更好（上述状态值可以使用 SHOW STATUS LIKE‘keyread%’获得）。 >* keybuffersize 只对 MyISAM 表起作用。即使你不使用 MyISAM 表，但是内部的临时磁盘表是 MyISAM 表，也要使用该值。可以使用检查状态值 createdtmpdisktables 得知详情。对于 1G 内存的机器，如果不使用 MyISAM 表，推荐值是 16M（8-64M） > * keybuffersize 设置注意事项

    > > > 1.  单个 keybuffer 的大小不能超过 4G，如果设置超过 4G，就有可能遇到下面 3 个bug:
    > > >     
    > > >     
    > > >     > > [http://bugs.mysql.com/bug.php?id=29446](http://bugs.mysql.com/bug.php?id=29446) <br
    > > >     > > /> [http://bugs.mysql.com/bug.php?id=29419](http://bugs.mysql.com/bug.php?id=29419) <br
    > > >     > > /> [http://bugs.mysql.com/bug.php?id=5731](http://bugs.mysql.com/bug.php?id=5731) <br
    > > >     
    > > >     
    > > > 2.  建议 keybuffer 设置为物理内存的 1/4(针对 MyISAM 引擎)，甚至是物理内存的 30%~40%，如果 keybuffersize 设置太大，系统就会频繁的换页，降低系统性能。因为 MySQL 使用操作系统的缓存来缓存数据，所以我们得为系统留够足够的内存；在很多情况下数据要比索引大得多。 >>>3\. 如果机器性能优越，可以设置多个keybuffer,分别让不同的 keybuffer 来缓存专门的索引

2.  innodbbufferpool_size > 表示缓冲池字节大小，InnoDB 缓存表和索引数据的内存区域。mysql 默认的值是 128M。最大值与你的CPU 体系结构有关，在 32 位操作系统，最大值是 4294967295(2^32-1) ，在 64 位操作系统，最大值为
    18446744073709551615 (2^64-1)。 > 在 32 位操作系统中，CPU 和操作系统实用的最大大小低于设置的最大值。如果设定的缓冲池的大小大于 1G，设置 innodbbufferpoolinstances 的值大于 1\. > *数据读写在内存中非常快, innodbbufferpoolsize 减少了对磁盘的读写。 当数据提交或满足检查点条件后才一次性将内存数据刷新到磁盘中。然而内存还有操作系统或数据库其他进程使用, 一般设置 bufferpool 大小为总内存的 3/4 至 4/5。 若设置不当, 内存使用可能浪费或者使用过多。 对于繁忙的服务器, buffer pool 将划分为多个实例以提高系统并发性, 减少线程间读写缓存的争用。buffer pool 的大小首先受 innodbbufferpool_instances 影响, 当然影响较小。

3.  querycachesize > 当 mysql 接收到一条 select 类型的 query时，mysql 会对这条 query 进行 hash 计算而得到一个 hash 值，然后通过该 hash 值到 query cache 中去匹配，如果没有匹配中，则将这个hash 值存放在一个 hash 链表中，同时将 query 的结果集存放进cache 中，存放 hash 值的链表的每一个 hash 节点存放了相应 query结果集在 cache 中的地址，以及该 query 所涉及到的一些 table 的相关信息；如果通过 hash 值匹配到了一样的 query，则直接将 cache 中相应的 query 结果集返回给客户端。如果 mysql 任何一个表中的任何一条数据发生了变化，便会通知 query cache 需要与该 table 相关的query 的 cache 全部失效，并释放占用的内存地址。 > query cache
    优缺点

    > > 1.  query 语句的 hash 计算和 hash 查找带来的资源消耗。mysql 会对每条接收到的 select 类型的 query 进行 hash 计算然后查找该 query 的 cache 是否存在，虽然 hash 计算和查找的效率已经足够高了，一条 query 所带来的消耗可以忽略，但一旦涉及到高并发，有成千上万条 query 时，hash 计算和查找所带来的开销就的重视了；
    > > 2.  query cache 的失效问题。如果表变更比较频繁，则会造成 query cache 的失效率非常高。表变更不仅仅指表中的数据发生变化，还包括结构或者索引的任何变化；
    > > 3.  对于不同 sql 但同一结果集的 query 都会被缓存，这样便会造成内存资源的过渡消耗。sql 的字符大小写、空格或者注释的不同，缓存都是认为是不同的 sql（因为他们的 hash 值会不同）；
    > > 4.  相关参数设置不合理会造成大量内存碎片，相关的参数设置会稍后介绍。

4.  readbuffersize >是 MySQL 读入缓冲区大小。对表进行顺序扫描的请求将分配一个读入缓冲区，MySQL 会为它分配一段内存缓冲区。readbuffersize 变量控制这一缓冲区的大小。如果对表的顺序扫描请求非常频繁，并且你认为频繁扫描进行得太慢，可以通过增加该变量值以及内存缓冲区大小提高其性能。*

# 1187.若一张表中只有一个字段 VARCHAR(N)类型，utf8 编码，则 N 最大值 为多少(精确到数量级即可)?

> 原文：[https://zwmst.com/5676.html](https://zwmst.com/5676.html)

由于 utf8 的每个字符最多占用 3 个字节。而 MySQL 定义行的长度不能超过65535，因此 N 的最大值计算方法为：(65535-1-2)/3。减去 1 的原因是实际存储从第二个字节开始，减去 2 的原因是因为要在列表长度存储实际的字符长度，除以 3 是因为 utf8 限制：每个字符最多占用 3 个字节。*

# 1188\. [SELECT *] 和[SELECT 全部字段]的 2 种写法有何优缺点?

> 原文：[https://zwmst.com/5678.html](https://zwmst.com/5678.html)

1.  前者要解析数据字典，后者不需要
2.  结果输出顺序，前者与建表列顺序相同，后者按指定字段顺序。
3.  表字段改名，前者不需要修改，后者需要改
4.  后者可以建立索引进行优化，前者无法优化
5.  后者的可读性比前者要高*

# 1189.HAVNG 子句 和 WHERE 的异同点?

> 原文：[https://zwmst.com/5680.html](https://zwmst.com/5680.html)

1.  语法上：where 用表中列名，having 用 select 结果别名
2.  影响结果范围：where 从表读出数据的行数，having 返回客户端的行数
3.  索引：where 可以使用索引，having 不能使用索引，只能在临时结果集操作
4.  where 后面不能使用聚集函数，having 是专门使用聚集函数的。*

# 1190.MySQL 当记录不存在时 insert,当记录存在时 update，语句怎么写？

> 原文：[https://zwmst.com/5682.html](https://zwmst.com/5682.html)

```
INSERT INTO table (a,b,c) VALUES (1,2,3) ON DUPLICATE KEY UPDATE c=c+1;
```*

# 1191.MySQL 的 insert 和 update 的 select 语句语法

> 原文：[https://zwmst.com/5684.html](https://zwmst.com/5684.html)

```
SQL insert into student (stuid,stuname,deptid) select 10,'xzm',3
from student where stuid > 8;
update student a inner join student b on b.stuID=10 set
a.stuname=concat(b.stuname, b.stuID) where a.stuID=10 ;
```*
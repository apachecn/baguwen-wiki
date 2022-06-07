<!--yml
category: MongoDB
date: 0001-01-01 00:00:00
-->

# MongoDB 面试题（爪哇程序员）

# 什么是MongoDB？

> 原文：[https://zwmst.com/1537.html](https://zwmst.com/1537.html)

MongoDB是一个文档数据库，提供好的性能，领先的非关系型数据库。采用BSON存储文档 数据。

BSON（）是一种类json的一种二进制形式的存储格式，简称Binary JSON相对于json多了date类型和二进制数组。


# MongoDB的优势有哪些

> 原文：[https://zwmst.com/1539.html](https://zwmst.com/1539.html)

面向文档的存储：以 JSON 格式的文档保存数据。

任何属性都可以建立索引。

复制以及高可扩展性。

自动分片。

丰富的查询功能。

快速的即时更新。


# 什么是集合(表)？

> 原文：[https://zwmst.com/1541.html](https://zwmst.com/1541.html)

集合就是一组 MongoDB文档。它相当于关系型数据库（RDBMS）中的表这种概念。集合位 于单独的一个数据库中。

一个集合内的多个文档可以有多个不同的字段。一般来说，集合中的文档都有着相同或相关的 目的。


# 什么是文档(记录)

> 原文：[https://zwmst.com/1543.html](https://zwmst.com/1543.html)

文档由一组key value组成。文档是动态模式,这意味着同一集合里的文档不需要有相同的字段 和结构。在关系型数据库中table中的每一条记录相当于MongoDB中的一个文档。


# 在哪些场景使用MongoDB

> 原文：[https://zwmst.com/1545.html](https://zwmst.com/1545.html)

大数据

内容管理系统

移动端Apps

数据管理


# 为什么用MOngoDB？

> 原文：[https://zwmst.com/1547.html](https://zwmst.com/1547.html)

架构简单

没有复杂的连接

深度查询能力,MongoDB支持动态查询。

容易调试

容易扩展

不需要转化/映射应用对象到数据库对象

使用内部内存作为存储工作区,以便更快的存取数据。


# MongoDB中的命名空间是什么意思?

> 原文：[https://zwmst.com/1549.html](https://zwmst.com/1549.html)

mongodb存储bson对象在丛集(collection)中，数据库名字和丛集名字以句点连结起来叫做 名字空间(namespace)。

一个集合命名空间又有多个数据域(extent)，集合命名空间里存储着集合的元数据，比如集合 名称，集合的第一个数据域和最后一个数据域的位置等等。而一个数据域由若干条文档(document)组成，每个数据域都有一个头部，记录着第一条文档和最后一条文档的为知，以 及该数据域的一些元数据。extent之间，document之间通过双向链表连接。

索引的存储数据结构是B树，索引命名空间存储着对B树的根节点的指针。


# MongoDB中的分片什么意思

> 原文：[https://zwmst.com/1551.html](https://zwmst.com/1551.html)

分片是将数据水平切分到不同的物理节点。当应用数据越来越大的时候，数据量也会越来越 大。当数据量增长时，单台机器有可能无法存储数据或可接受的读取写入吞吐量。利用分片技 术可以添加更多的机器来应对数据量增加以及读写操作的要求。


# 为什么要在MongoDB中使用分析器

> 原文：[https://zwmst.com/1553.html](https://zwmst.com/1553.html)

mongodb中包括了一个可以显示数据库中每个操作性能特点的数据库分析器.通过这个分析器 你可以找到比预期慢的查询(或写操作);利用这一信息,比如,可以确定是否需要添加索引。


# MongoDB支持主键外键关系吗

> 原文：[https://zwmst.com/1555.html](https://zwmst.com/1555.html)

默认MongoDB不支持主键和外键关系。 用Mongodb本身的API需要硬编码才能实现外键关联，不够直观且难度较大。


# MongoDB支持哪些数据类型

> 原文：[https://zwmst.com/1557.html](https://zwmst.com/1557.html)

String

Integer

Double

Boolean

Object

Object ID

Arrays

Min/Max Keys

Datetime

Code

Regular Expression等


# 为什么要在MongoDB中用”Code”数据类型

> 原文：[https://zwmst.com/1559.html](https://zwmst.com/1559.html)

"Code"类型用于在文档中存储 JavaScript 代码。


# 为什么要在MongoDB中用”Regular Expression”数据类型

> 原文：[https://zwmst.com/1561.html](https://zwmst.com/1561.html)

"Regular Expression"类型用于在文档中存储正则表达式


# 为什么在MongoDB中使用”Object ID”数据类型

> 原文：[https://zwmst.com/1563.html](https://zwmst.com/1563.html)

"ObjectID"数据类型用于存储文档id


# “ObjectID”有哪些部分组成

> 原文：[https://zwmst.com/1565.html](https://zwmst.com/1565.html)

一共有四部分组成:时间戳、客户端ID、客户进程ID、三个字节的增量计数器


# 在MongoDb中什么是索引

> 原文：[https://zwmst.com/1567.html](https://zwmst.com/1567.html)

索引用于高效的执行查询,没有索引的MongoDB将扫描整个集合中的所有文档,这种扫描效率 很低,需要处理大量的数据。

索引是一种特殊的数据结构,将一小块数据集合保存为容易遍历的形式.索引能够存储某种特殊 字段或字段集的值,并按照索引指定的方式将字段值进行排序。


# MongoDB支持存储过程吗？如果支持的话，怎么用？

> 原文：[https://zwmst.com/1569.html](https://zwmst.com/1569.html)

MongoDB支持存储过程，它是javascript写的，保存在db.system.js表中。


# 在MongoDB中什么是副本集

> 原文：[https://zwmst.com/1571.html](https://zwmst.com/1571.html)

在MongoDB中副本集由一组MongoDB实例组成，包括一个主节点多个次节点，MongoDB客户端的所有数据都写入主节点(Primary),副节点从主节点同步写入数据，以保持所有复制集 内存储相同的数据，提高数据可用性。


# 如何理解MongoDB中的GridFS机制，MongoDB为何使用GridFS来存储文件？

> 原文：[https://zwmst.com/1573.html](https://zwmst.com/1573.html)

GridFS是一种将大型文件存储在MongoDB中的文件规范。使用GridFS可以将大文件分隔成 多个小文档存放，这样我们能够有效的保存大文档，而且解决了BSON对象有限制的问题。


# 为什么MongoDB的数据文件很大？

> 原文：[https://zwmst.com/1575.html](https://zwmst.com/1575.html)

MongoDB采用的预分配空间的方式来防止文件碎片。


# 410.MongoDB概念

> 原文：[https://zwmst.com/3869.html](https://zwmst.com/3869.html)

MongoDB 是由 C++语言编写的，是一个基于分布式文件存储的开源数据库系统。在高负载的情况下，添加更多的节点，可以保证服务器性能。MongoDB 旨在为 WEB 应用提供可扩展的高性能
数据存储解决方案。

MongoDB 将数据存储为一个文档，数据结构由键(key=>value)对组成。MongoDB 文档类似于 JSON 对象。字段值可以包含其他文档，数组及文档数组。


# 411.特点

> 原文：[https://zwmst.com/3871.html](https://zwmst.com/3871.html)

1.  MongoDB 是一个面向文档存储的数据库，操作起来比较简单和容易。
2.  你可以在 MongoDB 记录中设置任何属性的索引 (如：FirstName="Sameer",Address="8 Gandhi Road")来实现更快的排序。
3.  你可以通过本地或者网络创建数据镜像，这使得 MongoDB 有更强的扩展性。
4.  如果负载的增加（需要更多的存储空间和更强的处理能力） ，它可以分布在计算机网络中的其他节点上这就是所谓的分片。
5.  Mongo 支持丰富的查询表达式。查询指令使用 JSON 形式的标记，可轻易查询文档中内嵌的对象及数组。
6.  MongoDb 使用 update()命令可以实现替换完成的文档（数据）或者一些指定的数据字段 。
7.  Mongodb 中的 Map/reduce 主要是用来对数据进行批量处理和聚合操作。
8.  Map 和 Reduce。Map 函数调用 emit(key,value)遍历集合中所有的记录，将 key 与 value 传给 Reduce 函数进行处理。
9.  Map 函数和 Reduce 函数是使用 Javascript 编写的，并可以通过 db.runCommand 或 mapreduce 命令来执行 MapReduce 操作。
10.  GridFS 是 MongoDB 中的一个内置功能，可以用于存放大量小文件。
11.  MongoDB 允许在服务端执行脚本，可以用 Javascript 编写某个函数，直接在服务端执行，也可以把函数的定义存储在服务端，下次直接调用即可。


# 910.什么是 MongoDB。

> 原文：[https://zwmst.com/5088.html](https://zwmst.com/5088.html)

非关系型数据库 (NoSql),Mongo DB 很好的实现了面向对象的思想 (OO 思想), 在Mongo DB 中 每一条记录都是一个 Document 对象。Mongo DB 最大的优势在于所有的数据持久操作都无需开发人员手动编写 SQL 语句, 直接调用方法就可以轻松的实现 CRUD 操作.


# 911.MongoDB 特点。

> 原文：[https://zwmst.com/5091.html](https://zwmst.com/5091.html)

高性能、易部署、易使用，存储数据非常方便。主要功能特性有：
面向集合存储，易存储对象类型的数据。
模式自由。
支持动态查询。
支持完全索引，包含内部对象。
支持查询。
支持复制和故障恢复。
使用高效的二进制数据存储，包括大型对象（如视频等）。
自动处理碎片，以支持云计算层次的扩展性
支持 Python，PHP，Ruby，Java，C，C#，Javascript，Perl 及 C++ 语言的驱动程序，社区中也提供了对 Erlang 及. NET 等平台的驱动程序。
文件存储格式为 BSON（一种 JSON 的扩展）。
可通过网络访问。


# 912.MongoDB 的功能。

> 原文：[https://zwmst.com/5093.html](https://zwmst.com/5093.html)

面向集合的存储：适合存储对象及 JSON 形式的数据。
动态查询：Mongo 支持丰富的查询表达式。查询指令使用 JSON 形式的标记，可轻易查询文档中内嵌的对象及数组。
完整的索引支持：包括文档内嵌对象及数组。Mongo 的查询优化器会分析查询表达式，并生成一个高效的查询计划。
查询监视：Mongo 包含一个监视工具用于分析数据库操作的性能。
复制及自动故障转移：Mongo 数据库支持服务器之间的数据复制，支持主 – 从模式及服务器之间的相互复制。复制的主要目标是提供冗余及自动故障转移。
高效的传统存储方式：支持二进制数据及大型对象（如照片或图片）自动分片以支持云级别的伸缩性：自动分片功能支持水平的数据库集群，可动态添加额外的机器。


# 913.MongoDB 的适用场景。

> 原文：[https://zwmst.com/5097.html](https://zwmst.com/5097.html)

网站数据：Mongo 非常适合实时的插入，更新与查询，并具备网站实时数据存储所需的复制及高度伸缩性。
缓存：由于性能很高，Mongo 也适合作为信息基础设施的缓存层。在系统重启之后，由 Mongo 搭建的持久化缓存层可以避免下层的数据源 过载。
大尺寸，低价值的数据：使用传统的关系型数据库存储一些数据时可能会比较昂贵，在此之前，很多时候程序员往往会选择传统的文件进行存储。
高伸缩性的场景：Mongo 非常适合由数十或数百台服务器组成的数据库。Mongo的路线图中已经包含对 MapReduce 引擎的内置支持。
用于对象及 JSON 数据的存储：Mongo 的 BSON 数据格式非常适合文档化格式的存储及查询。


# 914.Redis、memcache、MongoDB 对比。

> 原文：[https://zwmst.com/5099.html](https://zwmst.com/5099.html)

mongodb 和 memcached 不是一个范畴内的东西。mongodb 是文档型的非关系型数据库，其优势在于查询功能比较强大，能存储海量数据。
和 memcached 更为接近的是 Redis。它们都是内存型数据库，数据保存在内存中，通过 tcp 直接存取，优势是速度快，并发高，缺点是数据类型有限，查询功能不强，一般用作缓存。

1.  性能
    Redis 和 memcache 差不多，要大于 mongodb。
2.  操作的便利性
    memcache 数据结构单一。
    Redis 丰富一些，数据操作方面，Redis 更好一些，较少的网络 IO 次数。
    mongodb 支持丰富的数据表达，索引，最类似关系型数据库，支持的查询语言非常丰富。
3.  内存空间的大小和数据量的大小
    Redis 在 2.0 版本后增加了自己的 VM 特性，突破物理内存的限制；可以对key value 设置过期时间（类似 memcache）。
    memcache 可以修改最大可用内存, 采用 LRU 算法。
    mongoDB 适合大数据量的存储，依赖操作系统 VM 做内存管理，吃内存也比较厉害，服务不要和别的服务在一起。
4.  可用性（单点问题）
    Redis 对于单点问题，依赖客户端来实现分布式读写；主从复制时，每次从节点重新连接主节点都要依赖整个快照, 无增量复制，因性能和效率问题，所以单点问题比较复杂；不支持自动 sharding, 需要依赖程序设定一致 hash 机制。一种替代方案是，不用 Redis 本身的复制机制，采用自己做主动复制（多份存储），或者改成增量复制的方式（需要自己实现），一致性问题和性能的权衡。
    Memcache 本身没有数据冗余机制，也没必要；对于故障预防，采用依赖成熟的 hash 或者环状的算法，解决单点故障引起的抖动问题。
    mongoDB 支持 master-slave,replicaset（内部采用 paxos 选举算法，自动故障恢复）,auto sharding 机制，对客户端屏蔽了故障转移和切分机制。
5.  可靠性（持久化）
    对于数据持久化和数据恢复，Redis 支持（快照、AOF）：依赖快照进行持久化，aof 增强了可靠性的同时，对性能有所影响。
    memcache 不支持，通常用在做缓存, 提升性能；
    MongoDB 从 1.8 版本开始采用 binlog 方式支持持久化的可靠性。
6.  数据一致性（事务支持）
    Memcache 在并发场景下，用 cas 保证一致性。
    Redis 事务支持比较弱，只能保证事务中的每个操作连续执行。
    mongoDB 不支持事务。
7.  数据分析
    mongoDB 内置了数据分析的功能 (mapreduce), 其他不支持。
8.  应用场景
    Redis：数据量较小的更性能操作和运算上。
    memcache：用于在动态系统中减少数据库负载，提升性能; 做缓存，提高性能（适合读多写少，对于数据量比较大，可以采用 sharding）。
    MongoDB: 主要解决海量数据的访问效率问题。


# 915.Redis 有什么用？只有了解了它有哪些特性，我们在用的时候才能扬长避短，为我们所 用。

> 原文：[https://zwmst.com/5101.html](https://zwmst.com/5101.html)

1.  速度快：使用标准 C 写，所有数据都在内存中完成，读写速度分别达到 10万 / 20 万。
2.  持久化：对数据的更新采用 Copy-on-write 技术，可以异步地保存到磁盘上，主要有两种策略，一是根据时间，更新次数的快照（save 300 10 ）二是基于语句追加方式 (Append-only file，aof) 。
3.  自动操作：对不同数据类型的操作都是自动的，很安全。
4.  快速的主 — 从复制，官方提供了一个数据，Slave 在 21 秒即完成了对Amazon 网站 10G key set 的复制。
5.  Sharding 技术： 很容易将数据分布到多个 Redis 实例中，数据库的扩展是个永恒的话题，在关系型数据库中，主要是以添加硬件、以分区为主要技术形式的纵向扩展解决了很多的应用场景，但随着 web2.0、移动互联网、云计等应用的兴起，这种扩展模式已经不太适合了，所以近年来，像采用主从配置、数据库复制形式的，Sharding 这种技术把负载分布到多个特理节点上去的横向扩展方式用处越来越多


# 1033.什么是 MongoDB？

> 原文：[https://zwmst.com/5355.html](https://zwmst.com/5355.html)

MongoDB 是一个文档数据库，提供好的性能，领先的非关系型数据库。采用BSON 存储文档数据。2007 年 10 月，MongoDB 由 10gen 团队所发展。2009年 2 月首度推出。获得安装包和查看详细的 API 可以访问官网网址
www.mongodb.com


# 1034\. MongoDB 是由哪种语言写的？

> 原文：[https://zwmst.com/5357.html](https://zwmst.com/5357.html)

MongoDB 用 c++编写的，流行的开源数据库 MySQL 也是用 C++开发的。
C++1983 年发行是一种使用广泛的计算机程序设计语言。它是一种通用程序设计语言，支持多重编程模式。


# 1035\. MongoDB 的优势有哪些？

> 原文：[https://zwmst.com/5359.html](https://zwmst.com/5359.html)

面向文档的存储：以 JSON 格式的文档保存数据。
任何属性都可以建立索引。
复制以及高可扩展性。
自动分片。
丰富的查询功能。
快速的即时更新。


# 1036.什么是数据库？

> 原文：[https://zwmst.com/5361.html](https://zwmst.com/5361.html)

数据库可以看成是一个电子化的文件柜,用户可以对文件中的数据运行新增、检索、更新、删除等操作。数据库是一个所有集合的容器，在文件系统中每一个数据库都有一个相关的物理文件


# 1037.什么是集合？

> 原文：[https://zwmst.com/5363.html](https://zwmst.com/5363.html)

集合就是一组 MongoDB 文档。它相当于关系型数据库（RDBMS）中的表这种概念。集合位于单独的一个数据库中。一个集合内的多个文档可以有多个不同的字段。一般来说，集合中的文档都有着相同或相关的目的。


# 1038.什么是文档？

> 原文：[https://zwmst.com/5366.html](https://zwmst.com/5366.html)

文档由一组 key value 组成。文档是动态模式,这意味着同一集合里的文档不需要有相同的字段和结构。在关系型数据库中table中的每一条记录相当于MongoDB中的一个文档


# 1039\. 什么是“mongod”？

> 原文：[https://zwmst.com/5368.html](https://zwmst.com/5368.html)

mongod 是处理 MongoDB 系统的主要进程。它处理数据请求，管理数据存储，和执行后台管理操作。当我们运行 mongod 命令意味着正在启动 MongoDB 进程,并且在后台运行。


# 1040.“mongod”参数有什么？

> 原文：[https://zwmst.com/5370.html](https://zwmst.com/5370.html)

传递数据库存储路径，默认是"/data/db" 端口号 默认是 "27017"


# 1041.什么是“mongo”？

> 原文：[https://zwmst.com/5372.html](https://zwmst.com/5372.html)

它是一个命令行工具用于连接一个特定的 mongod 实例。当我们没有带参数运行 mongo 命令它将使用默认的端口号和 localhost 连接。


# 1042.MongoDB 哪个命令可以切换数据库？

> 原文：[https://zwmst.com/5374.html](https://zwmst.com/5374.html)

MongoDB 用 use+数据库名称的方式来创建数据库。use 会创建一个新的数据库，如果该数据库存在，则返回这个数据库。


# 1043.什么是非关系型数据库？

> 原文：[https://zwmst.com/5376.html](https://zwmst.com/5376.html)

非关系型数据库是对不同于传统关系型数据库的统称。非关系型数据库的显著特点是不使用 SQL 作为查询语言，数据存储不需要特定的表格模式。由于简单的设计和非常好的性能所以被用于大数据和 Web Apps 等


# 1044.非关系型数据库有哪些类型？

> 原文：[https://zwmst.com/5378.html](https://zwmst.com/5378.html)

Key-Value 存储 Eg:Amazon S3
图表 Eg:Neo4J
文档存储 Eg:MongoDB
基于列存储 Eg:Cassandra


# 1045.为什么用 MOngoDB？

> 原文：[https://zwmst.com/5380.html](https://zwmst.com/5380.html)

架构简单
没有复杂的连接
深度查询能力,MongoDB 支持动态查询。
容易调试
容易扩展
不需要转化/映射应用对象到数据库对象
使用内部内存作为存储工作区,以便更快的存取数据。


# 1046.在哪些场景使用 MongoDB？

> 原文：[https://zwmst.com/5382.html](https://zwmst.com/5382.html)

大数据
内容管理系统
移动端 Apps
数据管理


# 1047.在 MongoDB 中如何创建一个新的数据库？

> 原文：[https://zwmst.com/5384.html](https://zwmst.com/5384.html)

MongoDB 用 use + 数据库名称 的方式来创建数据库。use 会创建一个新的数据库，如果该数据库存在，则返回这个数据库。


# 1048.在 MongoDB 中如何查看数据库列表？

> 原文：[https://zwmst.com/5386.html](https://zwmst.com/5386.html)

使用命令"show dbs"


# 1049.MongoDB 中的分片是什么意思？

> 原文：[https://zwmst.com/5388.html](https://zwmst.com/5388.html)

分片是将数据水平切分到不同的物理节点。当应用数据越来越大的时候，数据量也会越来越大。当数据量增长时，单台机器有可能无法存储数据或可接受的读取写入吞吐量。利用分片技术可以添加更多的机器来应对数据量增加以及读写操作的要求。
参考：[https://docs.mongodb.com/manual/sharding/](https://docs.mongodb.com/manual/sharding/)


# 1051.你说的 NoSQL 数据库是什么意思?NoSQL 与 RDBMS 直接有什么区别?为什么要使用和不使用 NoSQL 数据库?说一说 NoSQL 数据库的几个优点?

> 原文：[https://zwmst.com/5391.html](https://zwmst.com/5391.html)

NoSQL 是非关系型数据库，NoSQL = Not Only SQL。
关系型数据库采用的结构化的数据，NoSQL 采用的是键值对的方式存储数据。
在处理非结构化/半结构化的大数据时；在水平方向上进行扩展时；随时应对动态增加的数据项时可以优先考虑使用 NoSQL 数据库。
在考虑数据库的成熟度；支持；分析和商业智能；管理及专业性等问题时，应优先考虑关系型数据库。


# 1052.NoSQL 数据库有哪些类型?

> 原文：[https://zwmst.com/5393.html](https://zwmst.com/5393.html)

例如：MongoDB, Cassandra, CouchDB, Hypertable, Redis, Riak, Neo4j, HBASE, Couchbase,MemcacheDB, RevenDB and Voldemort are the examples of NoSQL databases


# 1053.MySQL 与 MongoDB 之间最基本的差别是什么

> 原文：[https://zwmst.com/5395.html](https://zwmst.com/5395.html)

MySQL 和 MongoDB 两者都是免费开源的数据库。MySQL 和 MongoDB 有许多基本差别包括数据的表示(data representation)，查询，关系，事务，schema 的设计和定义，标准化(normalization)，速度和性能。
通过比较 MySQL 和 MongoDB，实际上我们是在比较关系型和非关系型数据库，即数据存储结构不同。


# 1054.你怎么比较 MongoDB、CouchDB 及 CouchBase

> 原文：[https://zwmst.com/5397.html](https://zwmst.com/5397.html)

MongoDB 和 CouchDB 都是面向文档的数据库。MongoDB 和 CouchDB 都是开源 NoSQL 数据库的最典型代表。 除了都以文档形式存储外它们没有其他的共同点。MongoDB 和 CouchDB 在数据模型实现、接口、对象存储以及复制方法等方面有很多不同。


# 1055.MongoDB 成为最好 NoSQL 数据库的原因是什么?

> 原文：[https://zwmst.com/5399.html](https://zwmst.com/5399.html)

以下特点使得 MongoDB 成为最好的 NoSQL 数据库：

1.  面向文件的
2.  高性能
3.  高可用性
4.  易扩展性
5.  丰富的查询语言


# 1056.32 位系统上有什么细微差别?

> 原文：[https://zwmst.com/5401.html](https://zwmst.com/5401.html)

journaling 会激活额外的内存映射文件。这将进一步抑制 32 位版本上的数据库大小。因此，现在journaling 在 32 位系统上默认是禁用的。


# 1057.journal 回放在条目(entry)不完整时(比如恰巧有一个中途故障了)会遇到问题吗?

> 原文：[https://zwmst.com/5403.html](https://zwmst.com/5403.html)

每个 journal (group)的写操作都是一致的，除非它是完整的否则在恢复过程中它不会回放。


# 1058.分析器在 MongoDB 中的作用是什么?

> 原文：[https://zwmst.com/5405.html](https://zwmst.com/5405.html)

MongoDB 中包括了一个可以显示数据库中每个操作性能特点的数据库分析器。通过这个分析器你可以找到比预期慢的查询(或写操作);利用这一信息，比如，可以确定是否需要添加索引。


# 1059.名字空间(namespace)是什么?

> 原文：[https://zwmst.com/5409.html](https://zwmst.com/5409.html)

MongoDB 存储 BSON 对象在丛集(collection)中。数据库名字和丛集名字以句点连结起来叫做名字空间(namespace)。


# 1060\. 如果用户移除对象的属性，该属性是否从存储层中删除?

> 原文：[https://zwmst.com/5411.html](https://zwmst.com/5411.html)

是的，用户移除属性然后对象会重新保存(re-save())。


# 1061.能否使用日志特征进行安全备份?

> 原文：[https://zwmst.com/5413.html](https://zwmst.com/5413.html)

是的。


# 1062.允许空值 null 吗?

> 原文：[https://zwmst.com/5415.html](https://zwmst.com/5415.html)

对于对象成员而言，是的。然而用户不能够添加空值(null)到数据库丛集(collection)因为空值不是对象。然而用户能够添加空对象{}。


# 1063.更新操作立刻 fsync 到磁盘?

> 原文：[https://zwmst.com/5417.html](https://zwmst.com/5417.html)

不会，磁盘写操作默认是延迟执行的。写操作可能在两三秒(默认在 60 秒内)后到达磁盘。例如，如果一秒内数据库收到一千个对一个对象递增的操作，仅刷新磁盘一次。(注意，尽管 fsync 选项在命令行和经过 getLastError_old 是有效的)(译者：也许是坑人的面试题??)。


# 1064.如何执行事务/加锁?

> 原文：[https://zwmst.com/5419.html](https://zwmst.com/5419.html)

MongoDB 没有使用传统的锁或者复杂的带回滚的事务，因为它设计的宗旨是轻量，快速以及可预计的高性能。可以把它类比成 MySQL MylSAM 的自动提交模式。通过精简对事务的支持，性能得到了提升，特别是在一个可能会穿过多个服务器的系统里。


# 1065.为什么我的数据文件如此庞大?

> 原文：[https://zwmst.com/5421.html](https://zwmst.com/5421.html)

MongoDB 会积极的预分配预留空间来防止文件系统碎片。


# 1066.启用备份故障恢复需要多久

> 原文：[https://zwmst.com/5423.html](https://zwmst.com/5423.html)

从备份数据库声明主数据库宕机到选出一个备份数据库作为新的主数据库将花费 10 到 30 秒时间。这期间在主数据库上的操作将会失败–包括写入和强一致性读取(strong consistent read)操作。然而，你还能在第二数据库上执行最终一致性查询(eventually consistent query)(在 slaveOk 模式下)，即使在这段时间里。


# 1067.什么是 master 或 primary?

> 原文：[https://zwmst.com/5425.html](https://zwmst.com/5425.html)

它是当前备份集群(replica set)中负责处理所有写入操作的主要节点/成员。在一个备份集群中，当失效备援(failover)事件发生时，一个另外的成员会变成 primary。


# 1068.什么是 secondary 或 slave?

> 原文：[https://zwmst.com/5427.html](https://zwmst.com/5427.html)

Seconday 从当前的 primary 上复制相应的操作。它是通过跟踪复制 oplog(local.oplog.rs)做到的。


# 1069.我必须调用 getLastError 来确保写操作生效了么?

> 原文：[https://zwmst.com/5430.html](https://zwmst.com/5430.html)

不用。不管你有没有调用 getLastError(又叫"Safe Mode")服务器做的操作都一样。调用 getLastError 只是为了确认写操作成功提交了。当然，你经常想得到确认，但是写操作的安全性和是否生效不是由这个决定的。


# 1070.我应该启动一个集群分片(sharded)还是一个非集群分片的 MongoDB 环境?

> 原文：[https://zwmst.com/5432.html](https://zwmst.com/5432.html)

为开发便捷起见，我们建议以非集群分片(unsharded)方式开始一个 MongoDB 环境，除非一台服务器不足以存放你的初始数据集。从非集群分片升级到集群分片(sharding)是无缝的，所以在你的数据集还不是很大的时候没必要考虑集群分片(sharding)。


# 1071.分片(sharding)和复制(replication)是怎样工作的?

> 原文：[https://zwmst.com/5434.html](https://zwmst.com/5434.html)

每一个分片(shard)是一个分区数据的逻辑集合。分片可能由单一服务器或者集群组成，我们推荐为每一个分片(shard)使用集群。


# 1072.数据在什么时候才会扩展到多个分片(shard)里?

> 原文：[https://zwmst.com/5436.html](https://zwmst.com/5436.html)

MongoDB 分片是基于区域(range)的。所以一个集合(collection)中的所有的对象都被存放到一个块(chunk)中。只有当存在多余一个块的时候，才会有多个分片获取数据的选项。现在，每个默认块的大小是 64Mb，所以你需要至少 64 Mb 空间才可以实施一个迁移。


# 1073.当我试图更新一个正在被迁移的块(chunk)上的文档时会发生什么

> 原文：[https://zwmst.com/5438.html](https://zwmst.com/5438.html)

更新操作会立即发生在旧的分片(shard)上，然后更改才会在所有权转移(ownership transfers)前复制到新的分片上。


# 1074.如果在一个分片(shard)停止或者很慢的时候，我发起一个查询会怎样

> 原文：[https://zwmst.com/5440.html](https://zwmst.com/5440.html)

如果一个分片(shard)停止了，除非查询设置了“Partial”选项，否则查询会返回一个错误。如果一个分片(shard)响应很慢，MongoDB 则会等待它的响应。


# 1075.我可以把 moveChunk 目录里的旧文件删除吗

> 原文：[https://zwmst.com/5442.html](https://zwmst.com/5442.html)

没问题，这些文件是在分片(shard)进行均衡操作(balancing)的时候产生的临时文件。一旦这些操作已经完成，相关的临时文件也应该被删除掉。但目前清理工作是需要手动的，所以请小心地考虑再释放这些文件的空间。


# 1076.我怎么查看 Mongo 正在使用的链接

> 原文：[https://zwmst.com/5444.html](https://zwmst.com/5444.html)

```
db._adminCommand("connPoolStats");
```


# 1077.如果块移动操作(moveChunk)失败了，我需要手动清除部分转移的文档吗

> 原文：[https://zwmst.com/5446.html](https://zwmst.com/5446.html)

不需要，移动操作是一致(consistent)并且是确定性的(deterministic);一次失败后，移动操作会不断重试;当完成后，数据只会出现在新的分片里(shard)。


# 1078.如果我在使用复制技术(replication)，可以一部分使用日志(journaling)而其他部分则不使用吗

> 原文：[https://zwmst.com/5448.html](https://zwmst.com/5448.html)

可以。


# 1079.当更新一个正在被迁移的块（Chunk）上的文档时会发生什么

> 原文：[https://zwmst.com/5450.html](https://zwmst.com/5450.html)

更新操作会立即发生在旧的块（Chunk）上，然后更改才会在所有权转移前复制到新的分片上。


# 1080.MongoDB 在 A:{B,C}上建立索引，查询 A:{B,C}和 A:{C,B}都会使用索引吗

> 原文：[https://zwmst.com/5452.html](https://zwmst.com/5452.html)

不会，只会在 A:{B,C}上使用索引。


# 1081.如果一个分片（Shard）停止或很慢的时候，发起一个查询会怎样

> 原文：[https://zwmst.com/5454.html](https://zwmst.com/5454.html)

如果一个分片停止了，除非查询设置了“Partial”选项，否则查询会返回一个错误。如果一个分片响应很慢，MongoDB 会等待它的响应。


# 1082.MongoDB 支持存储过程吗？如果支持的话，怎么用

> 原文：[https://zwmst.com/5456.html](https://zwmst.com/5456.html)

MongoDB 支持存储过程，它是 javascript 写的，保存在 db.system.js 表中。


# 1083.如何理解 MongoDB 中的 GridFS 机制，MongoDB 为何使用 GridFS 来存储文件

> 原文：[https://zwmst.com/5458.html](https://zwmst.com/5458.html)

GridFS 是一种将大型文件存储在 MongoDB 中的文件规范。使用 GridFS 可以将大文件分隔成多个小文档存放，这样我们能够有效的保存大文档，而且解决了 BSON 对象有限制的问题
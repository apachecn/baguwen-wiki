<!--yml
category: 数据库
date: 2022-11-19 13:21:51
-->

# redis面试指南一（zthinker）

> 来源：[https://zthinker.com/archives/redis-interview-1](https://zthinker.com/archives/redis-interview-1)

1.  [Java内存管理面试指南一](https://zthinker.com/archives/java-memory-interview-1)
2.  [Java基础面试指南一](https://zthinker.com/archives/java-basic-interview-1)
3.  [Java基础面试指南二](https://zthinker.com/archives/java-basic-interview-2)
4.  [Java基础面试指南三](https://zthinker.com/archives/java-basic-interview-3)
5.  [Java基础面试指南四](https://zthinker.com/archives/java-basic-interview-4)
6.  [Java线程面试指南一](https://zthinker.com/archives/java-thread-interview-1)
7.  [Java线程面试指南二](https://zthinker.com/archives/java-thread-interview-2)
8.  [Redis面试指南一](https://zthinker.com/archives/redis-interview-1)
9.  [Kafka面试指南一](https://zthinker.com/archives/kafka-interview-1)
10.  [Spring面试指南一](https://zthinker.com/archives/spring-interview-1)
11.  [SpringBoot面试指南一](https://zthinker.com/archives/springboot-interview-1)
12.  [微服务面试指南一](https://zthinker.com/archives/microservice-interview-1)

名称Redis表示远程字典服务器。Redis的原始开发者Salvatore Sanfilippo，于2010年3月被VMware聘用。2013年5月，Redis由Pivotal Software(一家VMware分拆)赞助。2015年6月，开发由Redis Labs赞助。(维基百科说)

Redis(远程字典服务器)是一个开源键值数据库。它是网络化的，单线程，内存中的高级键值存储，具有可选的耐用性。它通常被称为数据结构服务器，因为键可以包含字符串，哈希，列表，集合和排序集合。它支持磁盘上的内存持久存储，复制以扩展读取性能，以及客户端分片以扩展写入性能。

Redis在数据库世界中创建了一个新类别。它结合了最佳的内存，无模式设计，优化的数据结构和可满足您数据需求的通用模块。结果就是最熟练的，高性能的多用途数据库，可以像简单的键/值数据存储一样轻松地进行扩展，但是以极其简单的方式提供了复杂的功能。除了完全内存化外，Redis还可以通过复制和备份实现数据持久性和高可用性。(重新分发)。它是为速度和语言而构建的。支持Redis的云服务器。媒体的内存中处理

*   Queue列
*   支持多语言
*   原子操作
*   排行榜/计数
*   Lua脚本
*   发布/订阅
*   事务
*   全页缓存(FPC)
*   主/从复制
*   集群(具有自动分片)*
*   自动故障转移(Redis Sentinel)
*   追加仅文件(AOF)持久性
*   快照(RDB文件)持久性
*   Redis最多可以处理232个Keys，并且经过实践测试，每个实例最多可以处理2.5亿个Keys。
*   它的加载速度高达110,000个SET /秒，可以在入门级Linux机器中检索81,000个GET /秒。每秒可以执行100000个查询
*   每个列表，集合和排序集合都可以容纳232个元素。

Redis支持具有Redis绑定的许多语言，包括：C，C ++，C＃，Clojure，Common Lisp，Dart，Erlang，Go，Haskell，Haxe，Io，Java，ActionScript，JavaScript(Node.js)，Lua，Objective- C，Perl，PHP，Pure Data，Python，R，Ruby，Scala，Smalltalk和Tcl。

Redis用ANSI C编写，主要用于缓存解决方案和会话管理。它为存储值创建唯一键。

使用Redis的知名公司列表：Twitter，GitHub，微博，Pinterest，Snapchat，Craigslist Digg，Stack Overflow，Flickr，Tumblr，Twilio。不包括Facebook和Google+

Redis不是简单的键值存储，实际上是一个数据结构服务器，支持不同类型的值。这是Redis支持的所有数据结构的列表。

**Redis支持以下数据结构：**

**二进制安全字符串：**字符串元素的列表或集合根据插入顺序进行排序。

**集和排序集：**唯一，未排序的字符串元素的集合，以及其中每个字符串元素都与一个称为得分的浮点值相关联的集合。

**哈希：**它映射由与值关联的字段组成的字段。字段和值都是字符串。

位数组**(位图)：**它使用特殊命令来处理字符串值，例如位数组。

**HyperLogLogs**：一种数据结构，可以估计集合中的项目数。

地理空间索引–以坐标对形式存储的数据。

有两种将数据持久保存到磁盘的方法。一种是称为快照的方法，它可以将某个时刻存在的数据取走并将其写入磁盘。另一种方法称为AOF，或仅附加文件，它通过将传入的写入命令复制到磁盘上而起作用。这些方法可以一起使用，也可以分开使用，或者在某些情况下根本不使用。选择哪种取决于您的数据和应用程序。

Redis提供了不同的持久性选项范围：

*   RDB持久性按指定的时间间隔执行数据集的时间点快照。
*   AOF持久性会记录服务器接收的每个写入操作，这些操作将在服务器启动时再次播放，从而重建原始数据集。使用与Redis协议本身相同的格式记录命令，并且仅采用追加方式。当日志太大时，Redis可以在后台重写日志。
*   如果希望，只要您的数据在服务器运行时就一直存在，则可以完全禁用持久性。
*   可以在同一实例中同时合并AOF和RDB。请注意，在这种情况下，当Redis重新启动时，AOF文件将用于重建原始数据集，因为它可以保证是最完整的。

Redis复制非常容易使用和配置主从复制，它允许从Redis服务器成为主服务器的精确副本。以下是有关Redis复制的一些重要事实：

Redis使用异步复制。

*   一个主站可以有多个从站。
*   从站能够接受其他从站的连接。从站也可以以类似图形的结构连接到其他从站。
*   Redis复制在主端无阻塞。
*   复制在从属端也是非阻塞的。
*   复制既可以用于可伸缩性，又可以具有多个从属来进行只读查询或仅用于数据冗余。
*   可以使用复制来避免将主数据库写入整个数据集的开销。

Redis可能会被Linux内核OOM杀手杀死，由于错误而崩溃，或者开始变慢。在现代操作系统中，malloc()返回NULL并不常见，通常服务器将开始交换并且Redis性能将下降，因此您可能会注意到问题所在。INFO命令将报告Redis正在使用的内存量，因此您可以编写脚本来监视Redis服务器以检查关键情况。

仅附加文件(AOF)记录通过将每个更改写入文件末尾而发生的数据更改。cache.t1.micro和cache.t2。*节点不支持AOF。对于这些类型的节点，appendonly参数值将被忽略。使用AOF Redis更加持久：您可以有不同的fsync策略：完全没有fsync，每秒fsync，每个查询fsync。使用默认策略fsync时，每秒的写入性能仍然很好(fsync是使用后台线程执行的，并且在没有进行fsync的情况下，主线程将尽力执行写入操作。)但是您只能损失一秒钟的写入时间。

使用SET命令设置的值将设置Keys的值。再次进行此操作将覆盖该值。但是，仅当键之前没有值时，使用append才具有set的作用，但是如果已经为键分配了值，则对键执行append会导致将值追加到现有的th值上。

**MemcacheD**：MemcacheD既简单又强大。其易于管理的设计促进了快速部署，易于夸张，并解决了与大数据缓存有关的许多问题。当缓存相对较小的静态数据(例如HTML代码片段)时，最好使用Memcached。Memcached内部内存管理在最简单的用例中效率更高，因为它消耗的元数据存储资源相对较少。当数据大小动态变化时，Memcached的内存管理效率会迅速降低，这时Memcached的内存可能会碎片化。同样，大型数据集通常涉及序列化数据，这总是需要更多空间来存储。如果您使用的是Memcached，则重新启动会丢失数据，并且重建缓存是一个代价高昂的过程。Memcached的读/写速度高于redis。         

**Redis：** Redis是一种开源的内存中数据结构存储，还可以用作数据库以及缓存。Redis有五种主要数据结构可供选择，通过智能缓存和缓存数据的操作为应用程序开发人员开辟了无限的可能性。由于其数据结构(以各种格式存储数据：列表，数组，集合和排序集合)，Redis作为缓存可为您提供大量功能和更高的整体效率。高速缓存采用一种称为数据逐出的机制，通过从内存中删除旧数据为新数据腾出空间。Memcached的数据驱逐机制采用了最近最少使用的算法，并在某种程度上任意驱逐了大小与新数据相似的数据。Redis的读/写速度很快，但这取决于正在开发的应用程序。

*   两者都归为NoSQL。
*   两者均以键值格式存储数据。
*   两者都可以将数据存储在内存中。

Redis和RDBMS之间有很多区别：

*   Redis是NoSQL数据库，而RDBMS是SQL数据库。
*   Redis遵循键值结构，而RDBMS遵循表结构。
*   Redis非常快，而RDBMS比较慢。
*   Redis将所有数据集存储在主内存中，而RDBMS将其数据集存储在辅助内存中。
*   Redis通常用于存储经常使用的小文件，而RDBMS用于存储大文件。
*   Redis仅提供对Linux，BSD，Mac OS X和Solaris的官方支持。目前，它不提供对Windows的官方支持，而RDBMS提供了对两者的支持。

为了提高Redis的持久性，可以使用磁盘上的fsync数据来配置"仅添加文件"。

*   每次将新命令添加到附加日志文件时，均使用Fsync()：这是安全的，但速度很慢。
*   每秒一次Fysnc()：速度很快，但是如果系统出现故障，您可能会丢失1秒的数据。
*   从不fsync()：这是一种不安全的方法，并且您的数据已在操作系统中。

使用BGSAVE命令将数据库的快照保存到dump.rdb中

将此dump.rdb文件复制到另一台服务器

KEYS / SCAN仅列出当前服务器上的Keys；不是更广泛的逻辑数据库

FLUSHDB / FLUSHALL仅删除当前服务器上的Keys；不是更广泛的逻辑数据库

RANDOMKEY仅选择当前服务器上的Keys。不是更广泛的逻辑数据库

*   TYPE key
*   TTL key
*   KEYS pattern
*   EXPIRE key seconds
*   EXPIREAT key timestamp
*   EXISTS key
*   DEL key

MongoDB是一种非结构化(至少在定义上)的分布式文档存储。出于清除目的，您可以将其视为高可伸缩性而不是高性能的JSON存储(尽管实际上它使用BSON)。它具有简单但有效的多类型索引系统，复制和分片以及许多更出色的功能。Redis是最简单的键/值存储，具有临时数据缓存。它可以作为高效的队列系统。

在查找更多特定信息时，您会发现很多同时使用它们的场景，Mongo是真正的持久规范存储，Redis是瞬态/缓存存储。

要检查Redis是否正在运行，请尝试以下代码：

```
try

{

    $redis = new Redis ();

    $redis->connect ('127.0.0.1', 6379);

    echo "Redis is running.";

    echo "Server is running: " . $redis->ping();

}

catch (Exception $e)

{

    echo $e->getMessage();

} 
```

要在Redis中设置多个值，请使用以下命令：

*   $ redis-> lpush("tutorials"，"PHP");
*   $ redis-> lpush("tutorials"，"MySQL");
*   $ redis-> lpush("tutorials，" Redis");
*   $ redis-> lpush("tutorials"，"Mongodb");

SAVE命令用于创建当前Redis数据库的备份。该命令将通过执行同步保存在您的Redis目录中创建dump.rdb文件。

句法"

save

返回值：成功执行后，SAVE命令返回OK。

使用BGSAVE命令将数据库的快照保存到dump.rdb中

将此dump.rdb文件复制到另一台服务器。

二进制安全意味着它具有已知的长度，但不受任何特殊字符的限制。您可以将任何值存储为给定大小。字符串值的长度可以为512 MB。

您可以使用以下路径停止Redis：

/etc/init.d/redis-server停止

**优点：**

*   速度快
*   稳定性高
*   Redis是内存中的数据结构存储，用作数据库，缓存和消息代理。
*   易于设置，使用和维护
*   数据方案免费
*   可通过LUA脚本扩展
*   Redis使用分片进行分区。
*   Redis遵循专有协议。
*   乐观锁定，命令块和脚本的原子执行。
*   客户端库多
*   服务器端锁定

**缺点：**

*   Redis内存中
*   它是单线程的
*   客户端对一致性哈希的支持有限
*   它没有广泛部署
*   使用RDB时，持久性会消耗大量I / O
*   您的所有数据都必须容纳在内存中
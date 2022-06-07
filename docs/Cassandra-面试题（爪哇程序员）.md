<!--yml
category: Cassandra
date: 0001-01-01 00:00:00
-->

# Cassandra 面试题（爪哇程序员）

# 412.Cassandra概念

> 原文：[https://zwmst.com/3873.html](https://zwmst.com/3873.html)

Apache Cassandra 是高度可扩展的，高性能的分布式 NoSQL 数据库。 Cassandra 旨在处理许多商品服务器上的大量数据，提供高可用性而无需担心单点故障。
Cassandra 具有能够处理大量数据的分布式架构。 数据放置在具有多个复制因子的不同机器上，以获得高可用性，而无需担心单点故障。


# 413.数据模型

> 原文：[https://zwmst.com/3875.html](https://zwmst.com/3875.html)

### Key Space（对应 SQL 数据库中的 database）

1.  一个 Key Space 中可包含若干个 CF，如同 SQL 数据库中一个 database 可包含多个 table

### Key（对应 SQL 数据库中的主键）

2.  在 Cassandra 中，每一行数据记录是以 key/value 的形式存储的，其中 key 是唯一标识。

### column（对应 SQL 数据库中的列）

3.  Cassandra 中每个 key/value 对中的 value 又称为 column，它是一个三元组，即：name，value 和 timestamp，其中 name 需要是唯一的。

### super column（SQL 数据库不支持）

4.  cassandra 允许 key/value 中的 value 是一个 map(key/value_list)，即某个 column 有多个子列。

### Standard Column Family（相对应 SQL 数据库中的 table）

5.  每个 CF 由一系列 row 组成，每个 row 包含一个 key 以及其对应的若干 column。

### Super Column Family（SQL 数据库不支持）

6.  每个 SCF 由一系列 row 组成，每个 row 包含一个 key 以及其对应的若干 super column。


# 414.一致性 Hash（多米诺 down 机）

> 原文：[https://zwmst.com/3877.html](https://zwmst.com/3877.html)

为每个节点分配一个 token，根据这个 token 值来决定节点在集群中的位置以及这个节点所存储的数据范围。


# 415.虚拟节点（down 机多节点托管）

> 原文：[https://zwmst.com/3880.html](https://zwmst.com/3880.html)

由于这种方式会造成数据分布不均的问题，**在 Cassandra1.2 以后采用了虚拟节点的思想：不需要为每个节点分配 token，把圆环分成更多部分，让每个节点负责多个部分的数据，这样一个节点移除后，它所负责的多个 token 会托管给多个节点处理，这种思想解决了数据分布不均的问题。**![](img/0eb331d96687f7827d8ee6f4e97c353b.png)
如图所示，上面部分是标准一致性哈希，每个节点负责圆环中连续的一段，如果 Node2 突然down 掉，Node2 负责的数据托管给 Node1，即 Node1 负责 EFAB 四段，如果 Node1 里面有很多热点用户产生的数据导致 Node1 已经有点撑不住了，恰巧 B 也是热点用户产生的数据，这样一来 Node1 可能会接着 down 机，Node1down 机，Node6 还 hold 住吗？

**下面部分是虚拟节点实现，每个节点不再负责连续部分，且圆环被分为更多的部分。如果 Node2突然 down 掉，Node2 负责的数据不全是托管给 Node1，而是托管给多个节点。而且也保持了一致性哈希的特点。


# 416.Gossip 协议

> 原文：[https://zwmst.com/3883.html](https://zwmst.com/3883.html)

Gossip 算法如其名，灵感来自办公室八卦，只要一个人八卦一下，在有限的时间内所有的人都会知道该八卦的信息，这种方式也与病毒传播类似，因此 Gossip 有众多的别名“闲话算法”、“疫情传播算法”、“病毒感染算法”、“谣言传播算法”。 Gossip 的特点：在一个有界网络中，每个节点都随机地与其他节点通信，经过一番杂乱无章的通信，最终所有节点的状态都会达成一致。因为 Gossip 不要求节点知道所有其他节点，因此又具有去中心化的特点，节点之间完全对等，不需要任何的中心节点。实际上 Gossip 可以用于众多能接受“最终一致性”的领域：失败检测、路由同步、Pub/Sub、动态负载均衡。


# 417.Gossip 两个节点（A、B）之间存在三种通信方式（push、pull、push&pull）

> 原文：[https://zwmst.com/3885.html](https://zwmst.com/3885.html)

1.  push: A 节点将数据(key,value,version)及对应的版本号推送给 B 节点，B 节点更新 A 中比自己新的数据。
2.  pull：A 仅将数据 key,version 推送给 B，B 将本地比 A 新的数据（Key,value,version）推送给 A，A 更新本地。
3.  push/pull：与 pull 类似，只是多了一步，A 再将本地比 B 新的数据推送给 B，B 更新本地。

如果把两个节点数据同步一次定义为一个周期，则在一个周期内，push 需通信 1 次，pull 需 2 次，push/pull 则需 3 次，从效果上来讲，push/pull 最好，理论上一个周期内可以使两个节点完全一致。直观上也感觉，push/pull 的收敛速度是最快的。


# 418.gossip 的协议和 seed list（防止集群分列）

> 原文：[https://zwmst.com/3887.html](https://zwmst.com/3887.html)

cassandra 使用称为 gossip 的协议来发现加入 C 集群中的其他节点的位置和状态信息。**gossip 进程每秒都在进行，并与至多三个节点交换状态信息**。节点交换他们自己和所知道的信息，于是所有的节点很快就能学习到整个集群中的其他节点的信息。gossip 信息有一个相关的版本号，于是在一次 gossip 信息交换中，旧的信息会被新的信息覆盖重写。要阻止分区进行 gossip 交流，那么在集群中的所有节点中使用相同的 seed list，种子节点的指定除了启动起 gossip 进程外，没有其他的目的。种子节点不是一个单点故障，他们在集群操作中也没有其他的特殊目的，除了引导节点以外


# 419.Partitioners（计算 primary key token 的 hash 函数）

> 原文：[https://zwmst.com/3889.html](https://zwmst.com/3889.html)

在 Cassandra 中，table 的每行由唯一的 primarykey 标识，partitioner 实际上为一 hash 函数用以计算 primary key 的 token。Cassandra 依据这个 token 值在集群中放置对应的行


# 420.两种可用的复制策略

> 原文：[https://zwmst.com/3892.html](https://zwmst.com/3892.html)

### SimpleStrategy：仅用于单数据中心，

将第一个 replica 放在由 partitioner 确定的节点中，其余的 replicas 放在上述节点顺时针方向的后续节点中。

### NetworkTopologyStrategy：可用于较复杂的多数据中心。

可以指定在每个数据中心分别存储多少份 replicas。复制策略在创建 keyspace 时指定，如

```
CREATE KEYSPACE Excelsior WITH REPLICATION = { 'class' :
'SimpleStrategy','replication_factor' : 3 };
CREATE KEYSPACE Excalibur WITH REPLICATION = {'class' :'NetworkTopologyStrategy',
'dc1' : 3, 'dc2' : 2};
```


# 421.协调者(coordinator)

> 原文：[https://zwmst.com/3894.html](https://zwmst.com/3894.html)

**协调者(coordinator)将 write 请求发送到拥有对应 row 的所有 replica 节点**，只要节点可用便获取并执行写请求。**写一致性级别(write consistency level)确定要有多少个 replica 节点必须返回成功的确认信息。成功意味着数据被正确写入了 commit log 和 memtable**。![](img/03476a950b6af1d92f66eba25b7171c4.png)
其中 dc1、dc2 这些数据中心名称要与 snitch 中配置的名称一致.上面的拓扑策略表示在 dc1 配置3 个副本,在 dc2 配置 2 个副本


# 422.数据读请求和后台修复

> 原文：[https://zwmst.com/3897.html](https://zwmst.com/3897.html)

1.  协调者首先与一致性级别确定的所有 replica 联系，被联系的节点返回请求的数据。
2.  若多个节点被联系，则来自各 replica 的 row 会在内存中作比较，若不一致，则协调者使用含最新数据的 replica 向 client 返回结果。那么比较操作过程中只需要传递时间戳就可以,因为要比较的只是哪个副本数据是最新的。
3.  协调者在后台联系和比较来自其余拥有对应 row 的 replica 的数据，若不一致，会向过时的replica 发写请求用最新的数据进行更新 read repair。


# 423.数据存储（CommitLog、MemTable、SSTable）

> 原文：[https://zwmst.com/3899.html](https://zwmst.com/3899.html)

写请求分别到 CommitLog 和 MemTable, 并且 MemTable 的数据会刷写到磁盘 SSTable 上. 除了写数据,还有索引也会保存到磁盘上.
先将数据写到磁盘中的 commitlog，同时追加到中内存中的数据结构 memtable 。这个时候就会返回客户端状态 ， memtable 内 容 超 出 指 定 容 量 后 会 被 放 进 将 被 刷 入 磁 盘 的 队 列(memtable_flush_queue_size 配置队列长度)。若将被刷入磁盘的数据超出了队列长度，将内存数据刷进磁盘中的 SSTable,之后 commit log 被清空。


# 424.SSTable 文件构成（BloomFilter、index、data、static）

> 原文：[https://zwmst.com/3902.html](https://zwmst.com/3902.html)

SSTable 文件有 fileer（判断数据 key 是否存在，这里使用了 BloomFilter 提高效率），index（寻找对应 column 值所在 data 文件位置）文件，data（存储真实数据）文件，static（存储和统计column 和 row 大小）文件。


# 425.二级索引（对要索引的 value 摘要，生成 RowKey）

> 原文：[https://zwmst.com/3904.html](https://zwmst.com/3904.html)

在 Cassandra 中，数据都是以 Key-value 的形式保存的。

KeysIndex 所创建的二级索引也被保存在一张 ColumnFamily 中。在插入数据时，对需要进行索引的 value进行摘要，生成独一无二的key，将其作为 RowKey保存在索引的 ColumnFamily 中；同时在 RowKey 上添加一个 Column，将插入数据的 RowKey 作为 name 域的值，value 域则赋空值，timestamp 域则赋为插入数据的时间戳。

如果有相同的 value 被索引了，则会在索引 ColumnFamily 中相同的 RowKey 后再添加新的Column。如果有新的 value 被索引，则会在索引 ColumnFamily 中添加新的 RowKey 以及对应新的 Column。

当对 value 进行查询时，只需计算该 value 的 RowKey，在索引 ColumnFamily 中的查找该RowKey，对其 Columns 进行遍历就能得到该 value 所有数据的 RowKey。


# 426.数据写入和更新（数据追加）

> 原文：[https://zwmst.com/3906.html](https://zwmst.com/3906.html)

Cassandra 的设计思路与这些系统不同，无论是 insert 还是 remove 操作，都是在已有的数据后面进行追加，而不修改已有的数据。这种设计称为 Log structured 存储，顾名思义就是系统中的数据是以日志的形式存在的，所以只会将新的数据追加到已有数据的后面。Log structured 存储系统有两个主要优点：

### 数据的写和删除效率极高

1.  传统的存储系统需要更新元信息和数据，因此磁盘的磁头需要反复移动，这是一个比较耗时的操作，而 Log structured 的系统则是顺序写，可以充分利用文件系统的 cache，所以效率很高。

### 错误恢复简单

2.  由于数据本身就是以日志形式保存，老的数据不会被覆盖，所以在设计 journal 的时候不需要考虑 undo，简化了错误恢复。

### 读的复杂度高

3.  但是，Log structured 的存储系统也引入了一个重要的问题：读的复杂度和性能。理论上说，读操作需要从后往前扫描数据，以找到某个记录的最新版本。相比传统的存储系统，这是比较耗时的。


# 427.数据删除（column 的墓碑）

> 原文：[https://zwmst.com/3908.html](https://zwmst.com/3908.html)

如果一次删除操作在一个节点上失败了（总共 3 个节点，副本为 3， RF=3).整个删除操作仍然被认为成功的（因为有两个节点应答成功，使用 CL.QUORUM 一致性）。接下来如果读发生在该节点上就会变的不明确，因为结果返回是空，还是返回数据，没有办法确定哪一种是正确的。
Cassandra 总是认为返回数据是对的，那就会发生删除的数据又出现了的事情，这些数据可以叫”僵尸”，并且他们的表现是不可预见的。


# 428.墓碑

> 原文：[https://zwmst.com/3910.html](https://zwmst.com/3910.html)

**删除一个 column 其实只是插入一个关于这个 column 的墓碑（tombstone），并不直接删除原有的 column。**该墓碑被作为对该 CF 的一次修改记录在 Memtable 和 SSTable 中。墓碑的内容是删除请求被执行的时间，该时间是接受客户端请求的存储节点在执行该请求时的本地时间（local delete time），称为本地删除时间。需要注意区分本地删除时间和时间戳，每个 CF 修改记录都有一个时间戳，这个时间戳可以理解为该 column 的修改时间，是由客户端给定的。


# 429.垃圾回收 compaction

> 原文：[https://zwmst.com/3912.html](https://zwmst.com/3912.html)

由于被删除的 column 并不会立即被从磁盘中删除，所以系统占用的磁盘空间会越来越大，这就需要有一种垃圾回收的机制，定期删除被标记了墓碑的 column。垃圾回收是在 compaction 的过程中完成的。


# 430.数据读取（memtable+SStables）

> 原文：[https://zwmst.com/3914.html](https://zwmst.com/3914.html)

为了满足读 cassandra 读取的数据是 memtable 中的数据和 SStables 中数据的合并结果。读取SSTables 中的数据就是查找到具体的哪些的 SSTables 以及数据在这些 SSTables 中的偏移量(SSTables 是按主键排序后的数据块)。首先如果 row cache enable 了话，会检测缓存。缓存命中直接返回数据，没有则查找 Bloom filter，查找可能的 SSTable。然后有一层 Partition key cache，找 partition key 的位置。如果有根据找到的 partition 去压缩偏移量映射表找具体的数据块。如果缓存没有，则要经过 Partition summary,Partition index 去找 partition key。然后经过压缩偏移量映射表找具体的数据块。

1.  检查 memtable
2.  如果 enabled 了,检查 row cache
3.  检查 Bloom filter
4.  如果 enable 了,检查 partition key 缓存
5.  如果在 partition key 缓存中找到了 partition key,直接去 compression offset 命中，如果没有，检查partition summary
6.  根据 compression offset map 找到数据位置
7.  从磁盘的 SSTable 中取出数据


# 431.行缓存和键缓存请求流程图

> 原文：[https://zwmst.com/3917.html](https://zwmst.com/3917.html)

![](img/baad668944a518972f33b980983637c8.png)

**MemTable**：如果 memtable 有目标分区数据，这个数据会被读出来并且和从 SSTables 中读出来的数据进行合并。SSTable 的数据访问如下面所示的步骤。

### Row Cache（SSTables 中频繁被访问的数据）

1.  在 Cassandra2.2+，它们被存储在堆外内存，使用全新的实现避免造成垃圾回收对 JVM 造成压力。存在在 row cache 的子集数据可以在特定的一段时间内配置一定大小的内存。row cache 使用LRU(least-recently-userd)进行回收在申请内存。存储在 row cache 中的数据是SSTables 中频繁被访问的数据。存储到row cache中后，数据就可以被后续的查询访问。row cache不是写更新。如果写某行了，这行的缓存就会失效，并且不会被继续缓存，直到这行被读到。类似的，如果一个partition更新了，整个partition的cache都会被移除，但目标的数据在row cache中找不到，就会去检查 Bloom filter。

### Bloom Filter（查找数据可能对应的 SSTable）

2.  首先，Cassandra 检查 Bloom filter 去发现哪个 SSTables 中有可能有请求的分区数据。Bloom filter 是存储在堆外内存。每个 SSTable 都有一个关联的 Bloom filter。一个 Bloom filter 可以建立一个 SSTable 没有包含的特定的分区数据。同样也可以找到分区数据存在 SSTable 中的可能性。它可以加速查找 partition key 的查找过程。然而，因为 Bloom filter 是一个概率函数，所以可能会得到错误的结果，并不是所有的 SSTables 都可以被 Bloom filter 识别出是否有数据。如果Bloom filter 不能够查找到 SSTable，Cassandra 会检查 partition key cache。Bloom filter 大小增长很适宜，每 10 亿数据 1~2GB。在极端情况下，可以一个分区一行。都可以很轻松的将数十亿的 entries 存储在单个机器上。Bloom filter 是可以调节的，如果你愿意用内存来换取性能。

### Partition Key Cache（查找数据可能对应的 Partition key）

3.  partition key 缓存如果开启了，将 partition index 存储在堆外内存。key cache 使用一小块可配置大小的内存。在读的过程中，每个”hit”保存一个检索。如果在 key cache 中找到了 partition key。就直接到 compression offset map 中招对应的块。partition key cache 热启动后工作的更好，相比较冷启动，有很大的性能提升。如果一个节点上的内存非常受限制，可能的话，需要限制保存在 key cache 中的 partition key 数目。如果一个在 key cache 中没有找到 partition key。就会去partition summary中去找。partition key cache 大小是可以配置的，意义就是存储在key cache 中的 partition keys 数目。

### Partition Summary（内存中存储一些 partition index 的样本）

4.  partition summary 是存储在堆外内存的结构，存储一些 partition index 的样本。如果一个partition index 包含所有的 partition keys。鉴于一个 partition summary 从每 X 个 keys 中取样，然后将每 X 个 key map 到 index 文件中。例如，如果一个 partition summary 设置了 20keys进行取样。它就会存储 SSTable file 开始的一个 key,20th 个 key，以此类推。尽管并不知道partition key 的具体位置，partition summary 可以缩短找到 partition 数据位置。当找到了partition key 值可能的范围后，就会去找 partition index。通过配置取样频率，你可以用内存来换取性能，当 partition summary 包含的数据越多，使用的内存越多。可以通过表定义的 index interval 属性来改变样本频率。固定大小的内存可以通过 index_summary_capacity_in_mb 属性来设置，默认是堆大小的 5%。

### Partition Index（磁盘中）

5.  partition index 驻扎在磁盘中，索引所有 partition keys 和偏移量的映射。如果 partition summary 已经查到 partition keys 的范围，现在的检索就是根据这个范围值来检索目标 partition key。需要进行单次检索和顺序读。根据找到的信息。然后去 compression offset map 中去找磁盘中有这个数据的块。如果 partition index 必须要被检索，则需要检索两次磁盘去找到目标数据。

### Compression offset map（磁盘中）

6.  compression offset map 存储磁盘数据准确位置的指针。存储在堆外内存，可以被 partition key cache 或者 partition index 访问。一旦 compression offset map 识别出来磁盘中的数据位置，就会从正确的 SStable(s)中取出数据。查询就会收到结果集。
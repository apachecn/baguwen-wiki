<!--yml
category: Redis
date: 0001-01-01 00:00:00
-->

# Redis 面试题（爪哇程序员）

# 什么是Redis？简述它的优缺点？

> 原文：[https://zwmst.com/765.html](https://zwmst.com/765.html)

Redis本质上是一个Key-Value类型的内存数据库，很像memcached，整个数据库统统加载 在内存当中进行操作，定期通过异步操作把数据库数据flush到硬盘上进行保存。

因为是纯内存操作，Redis的性能非常出色，每秒可以处理超过 10万次读写操作，是已知性能 最快的Key-Value DB。

Redis的出色之处不仅仅是性能，Redis最大的魅力是支持保存多种数据结构，此外单个value 的最大限制是1GB，不像 memcached只能保存1MB的数据，因此Redis可以用来实现很多有 用的功能。

比方说用他的List来做FIFO双向链表，实现一个轻量级的高性 能消息队列服务，用他的Set可 以做高性能的tag系统等等。

另外Redis也可以对存入的Key-Value设置expire时间，因此也可以被当作一 个功能加强版的 memcached来用。 Redis的主要缺点是数据库容量受到物理内存的限制，不能用作海量数据 的高性能读写，因此Redis适合的场景主要局限在较小数据量的高性能操作和运算上。


# Redis相比memcached有哪些优势？

> 原文：[https://zwmst.com/767.html](https://zwmst.com/767.html)

(1) memcached所有的值均是简单的字符串，redis作为其替代者，支持更为丰富的数据类型

(2) redis的速度比memcached快很多

(3) redis可以持久化其数据


# Redis有哪些数据结构？

> 原文：[https://zwmst.com/769.html](https://zwmst.com/769.html)

Redis 有 5 种基础数据结构，它们分别是：string(字符串)、list(列表)、hash(字典)、set(集 合) 和 zset(有序集合)。

这 5 种是 Redis 相关知识中最基础、最重要的部分。


# Redis主要消耗什么物理资源？

> 原文：[https://zwmst.com/771.html](https://zwmst.com/771.html)

内存。


# Redis的全称是什么？

> 原文：[https://zwmst.com/773.html](https://zwmst.com/773.html)

Remote Dictionary Server。


# 一个字符串类型的值能存储最大容量是多少？

> 原文：[https://zwmst.com/775.html](https://zwmst.com/775.html)

512M


# Redis为什么那么快？

> 原文：[https://zwmst.com/777.html](https://zwmst.com/777.html)

1、内存操作；

2、单线程，省去线程切换、锁竞争的开销；

3、非阻塞IO模型，epoll。


# Redis是单线程还是多线程？

> 原文：[https://zwmst.com/780.html](https://zwmst.com/780.html)

Redis6.0采用多线程IO，不过命令的执行还是单线程的。

Redis6.0之前，IO线程和执行线程都是单线程的。


# Redis 官方为什么不提供 Windows 版本？

> 原文：[https://zwmst.com/782.html](https://zwmst.com/782.html)

因为目前 Linux 版本已经相当稳定，而且用户量很大，无需开发 windows 版本，反而会带来 兼容性等问题。


# 为什么 Redis 需要把所有数据放到内存中？

> 原文：[https://zwmst.com/784.html](https://zwmst.com/784.html)

Redis 为了达到最快的读写速度将数据都读到内存中，并通过异步的方式将数据写入磁盘。

所以 redis 具有快速和数据持久化的特征，如果不将数据放在内存中，磁盘 I/O 速度为严重影 响 redis 的性能。

在内存越来越便宜的今天，redis 将会越来越受欢迎， 如果设置了最大使用的内存，则数据已 有记录数达到内存限值后不能继续插入新值。


# Redis如何设置密码及验证密码？

> 原文：[https://zwmst.com/786.html](https://zwmst.com/786.html)

设置密码：config set requirepass 123456

授权密码：auth 123456


# Redis集群如何选择数据库？

> 原文：[https://zwmst.com/788.html](https://zwmst.com/788.html)

Redis集群目前无法做数据库选择，默认在0数据库。


# 缓存失效？缓存穿透？缓存雪崩？缓存并发？

> 原文：[https://zwmst.com/790.html](https://zwmst.com/790.html)

1.  缓存失效 缓存失效指的是大量的缓存在同一时间失效，到时DB的瞬间压力飙升。造成这种现象的 原因是，key的过期时间都设置成一样了。解决方案是，key的过期时间引入随机因素， 比如5分钟+随机秒这种方式。

2.  缓存穿透 缓存穿透是指查询一条数据库和缓存都没有的一条数据，就会一直查询数据库，对数据 库的访问压力就会增大，缓存穿透的解决方案，有以下2种： 缓存空对象：代码维护较简单，但是效果不好。 布隆过滤器：代码维护复杂，效果很好。

3.  缓存雪崩 缓存雪崩 是指在某一个时间段，缓存集中过期失效。此刻无数的请求直接绕开缓存，直 接请求数据库。 造成缓存雪崩的原因，有以下2种： reids宕机。 大部分数据失效。

对于缓存雪崩的解决方案有以下2种：

搭建高可用的集群，防止单机的redis宕机。

设置不同的过期时间，防止同意之间内大量的key失效。

4.  缓存并发 有时候如果网站并发访问高，一个缓存如果失效，可能出现多个进程同时查询DB，同时 设置缓存的情况，如果并发确实很大，这也可能造成DB压力过大，还有缓存频繁更新的 问题。 一般处理方案是在查DB的时候进行加锁，如果KEY不存在，就加锁，然后查DB入缓存， 然后解锁；其他进程如果发现有锁就等待，然后等解锁后再查缓存或者进入DB查询。


# Redis中的热key怎么处理？

> 原文：[https://zwmst.com/792.html](https://zwmst.com/792.html)

1、对热key进行分散处理。比如：在key上加上不同的前后缀，缓存多个key，使得各个key分 散到不同的节点上。

2、采用多级缓存。


# Redis中的大key怎么处理？

> 原文：[https://zwmst.com/794.html](https://zwmst.com/794.html)

大key指的是value特别大的key。比如很长的字符串，或者很大的set等等。 大key会造成2个问题：

1、数据倾斜，比如某些节点内存占用过高。

2、当删除大key或者大 key自动过期的时候，会造成QPS突降，因为Redis是单线程的缘故。

处理方案：可以将一个大key进行分片处理，比如：将一个大set分成多个小的set。


# 使用Redis统计网站的UV，应该怎么做？

> 原文：[https://zwmst.com/796.html](https://zwmst.com/796.html)

UV与PV不同，UV需要去重。一般有2种方案：

1、用BitMap。存的是用户的uid，计算UV的时候，做下bitcount就行了。

2、用布隆过滤器。将每次访问的用户uid都放到布隆过滤器中。优点是省内存，缺点是无法得 到精确的UV。但是对于不需要精确知道具体UV，只需要大概的数量级的场景，是个不错的选 择。


# Redis事务机制了解过吗？

> 原文：[https://zwmst.com/798.html](https://zwmst.com/798.html)

Redis事务的概念：

Redis 事务的本质是一组命令的集合。事务支持一次执行多个命令，一个事务中所有命令都会 被序列化。在事务执行过程，会按照顺序串行化执行队列中的命令，其他客户端提交的命令请 求不会插入到事务执行命令序列中。

Redis事务就是一次性、顺序性、排他性的执行一个队列中的一系列命令。

Redis事务没有隔离级别的概念：

批量操作在发送 EXEC 命令前被放入队列缓存，并不会被实际执行，也就不存在事务内的查询 要看到事务里的更新，事务外查询不能看到。

Redis不保证原子性：

Redis中，单条命令是原子性执行的，但事务不保证原子性，且没有回滚。事务中任意命令执 行失败，其余的命令仍会被执行。

Redis事务的三个阶段：

开始事务

命令入队

执行事务

Redis事务相关命令：

watch key1 key2 … : 监视一或多个key,如果在事务执行之前，被监视的key被其他命令改动， 则事务被打断 （ 类似乐观锁 ）

multi : 标记一个事务块的开始（ queued ）

exec : 执行所有事务块的命令 （ 一旦执行exec后，之前加的监控锁都会被取消掉 ）

discard : 取消事务，放弃事务块中的所有命令

unwatch : 取消watch对所有key的监控


# Redis key的淘汰策略有哪些？

> 原文：[https://zwmst.com/800.html](https://zwmst.com/800.html)

8种：noeviction，volatile-lru，volatile-lfu，volatile-ttl，volatile-random，allkeylru，allkeys-lfu，allkeys-random


# Redis在什么情况下会触发key的回收？

> 原文：[https://zwmst.com/802.html](https://zwmst.com/802.html)

2种情况：1、定时（抽样）清理；2、执行命令时，判断内存是否超过maxmemory。


# Redis的持久化了解过吗？

> 原文：[https://zwmst.com/804.html](https://zwmst.com/804.html)

Redis持久化有RDB和AOF这2种方式。

RDB：将数据库快照以二进制的方式保存到磁盘中。

AOF：以协议文本方式，将所有对数据库进行过写入的命令和参数记录到AOF文件，从而记录 数据库状态。


# Redis在集群种查找key的时候，是怎么定位到具体节点的？

> 原文：[https://zwmst.com/806.html](https://zwmst.com/806.html)

使用crc16算法对key进行hash 将hash值对16384取模，得到具体的槽位根据节点和槽位的映射信息（与集群建立连接后，客户端可以取得槽位映射信息），找到具体的节点地址 去具体的节点找key如果key不在这个节点上，则redis集群会返回moved指令，加上新的节点地址给客户端，同时，客户端会刷新本地的节点槽位映射关系如果槽位正在迁移中，那么redis集群会返回asking指令给客户端，这是临时纠正，客户端不会刷新本地的节点槽位映射关系


# 用Redis做延时队列，具体应该怎么实现？

> 原文：[https://zwmst.com/808.html](https://zwmst.com/808.html)

可以使用Zset实现。member是任务描述，score是执行时间，然后用定时器定时去扫描，一 旦有执行时间小于或等于当前时间的任务，就立即执行。


# Redis String的内部编码有哪些？

> 原文：[https://zwmst.com/810.html](https://zwmst.com/810.html)

int、embstr、raw

10000以下的整数会使用缓存里的int常量。

长度小于等于44字节：embstr编码

长度大于44字节：raw编码


# Redis 集群方案应该怎么做？都有哪些方案？

> 原文：[https://zwmst.com/812.html](https://zwmst.com/812.html)

codis

目前用的最多的集群方案，基本和 twemproxy 一致的效果，但它支持在节点数量改变情况下，旧节点数据可恢复到新 hash 节点。

redis cluster

3.0 自带的集群，特点在于他的分布式算法不是一致性 hash，而是 hash 槽的概念，以及自身支持节点设置从节点。具体看官方文档介绍。 在业务代码层实现，起几个毫无关联的 redis 实例，在代码层，对 key 进行 hash 计算， 然后去对应的redis 实例操作数据。这种方式对 hash 层代码要求比较高，考虑部分包 括，节点失效后的替代算法方案，数据震荡后的自动脚本恢复，实例的监控，等等。


# Redis 集群方案什么情况下会导致整个集群不可用？

> 原文：[https://zwmst.com/814.html](https://zwmst.com/814.html)

有 A，B，C 三个节点的集群,在没有复制模型的情况下,如果节点 B 失败了，那么整个集群就会 以为缺少5501-11000 这个范围的槽而不可用。


# MySQL 里有 2000w 数据，redis 中只存 20w 的数据，如何保证 redis 中的数据都 是热点数据？

> 原文：[https://zwmst.com/816.html](https://zwmst.com/816.html)

redis 内存数据集大小上升到一定大小的时候，就会施行数据淘汰策略。

其实面试除了考察 Redis，不少公司都很重视高并发高可用的技术，特别是一线互联网公司， 分布式、

JVM、spring 源码分析、微服务等知识点已是面试的必考题。


# Redis有哪些适合的场景？

> 原文：[https://zwmst.com/818.html](https://zwmst.com/818.html)

（1）会话缓存（Session Cache）

最常用的一种使用Redis的情景是会话缓存（session cache）。用Redis缓存会话比其他存储 （如Memcached）的优势在于：Redis提供持久化。当维护一个不是严格要求一致性的缓存 时，如果用户的购物车信息全部丢失，大部分人都会不高兴的，现在，他们还会这样吗？

幸运的是，随着 Redis 这些年的改进，很容易找到怎么恰当的使用Redis来缓存会话的文档。 甚至广为人知的商业平台Magento也提供Redis的插件。

（2）全页缓存（FPC）

除基本的会话token之外，Redis还提供很简便的FPC平台。回到一致性问题，即使重启了 Redis实例，因为有磁盘的持久化，用户也不会看到页面加载速度的下降，这是一个极大改 进，类似PHP本地FPC。

再次以Magento为例，Magento提供一个插件来使用Redis作为全页缓存后端。

此外，对WordPress的用户来说，Pantheon有一个非常好的插件 wp-redis，这个插件能帮 助你以最快速度加载你曾浏览过的页面。

（3）队列

Reids在内存存储引擎领域的一大优点是提供 list 和 set 操作，这使得Redis能作为一个很好的 消息队列平台来使用。Redis作为队列使用的操作，就类似于本地程序语言（如Python）对 list 的 push/pop 操作。

如果你快速的在Google中搜索“Redis queues”，你马上就能找到大量的开源项目，这些项目 的目的就是利用Redis创建非常好的后端工具，以满足各种队列需求。例如，Celery有一个后 台就是使用Redis作为broker，你可以从这里去查看。

（4）排行榜/计数器

Redis在内存中对数字进行递增或递减的操作实现的非常好。集合（Set）和有序集合（Sorted Set）也使得我们在执行这些操作的时候变的非常简单，Redis只是正好提供了这两种数据结 构。

所以，我们要从排序集合中获取到排名最靠前的10个用户–我们称之为“user_scores”，我们 只需要像下面一样执行即可： 当然，这是假定你是根据你用户的分数做递增的排序。如果你想返回用户及用户的分数，你需 要这样执行：

ZRANGE user_scores 0 10 WITHSCORES

Agora Games就是一个很好的例子，用Ruby实现的，它的排行榜就是使用Redis来存储数据 的，你可以在这里看到。

（5）发布/订阅

最后（但肯定不是最不重要的）是Redis的发布/订阅功能。发布/订阅的使用场景确实非常 多。我已看见人们在社交网络连接中使用，还可作为基于发布/订阅的脚本触发器，甚至用 Redis的发布/订阅功能来建立聊天系统！


# Redis和Redisson有什么关系？

> 原文：[https://zwmst.com/820.html](https://zwmst.com/820.html)

Redisson是一个高级的分布式协调Redis客服端，能帮助用户在分布式环境中轻松实现一些 Java的对象 (Bloom filter, BitSet, Set, SetMultimap, ScoredSortedSet, SortedSet, Map, ConcurrentMap, List, ListMultimap, Queue, BlockingQueue, Deque, BlockingDeque, Semaphore, Lock, ReadWriteLock, AtomicLong, CountDownLatch, Publish / Subscribe, HyperLogLog)。


# Redis中的管道有什么用？

> 原文：[https://zwmst.com/822.html](https://zwmst.com/822.html)

一次请求/响应服务器能实现处理新的请求即使旧的请求还未被响应。这样就可以将多个命令发 送到服务器，而不用等待回复，最后在一个步骤中读取该答复。

这就是管道（pipelining），是一种几十年来广泛使用的技术。例如许多POP3协议已经实现 支持这个功能，大大加快了从服务器下载新邮件的过程。


# Redis如何做内存优化？

> 原文：[https://zwmst.com/824.html](https://zwmst.com/824.html)

尽可能使用散列表（hashes），散列表（是说散列表里面存储的数少）使用的内存非常小，所 以你应该尽可能的将你的数据模型抽象到一个散列表里面。

比如你的web系统中有一个用户对象，不要为这个用户的名称，姓氏，邮箱，密码设置单独的 key,而是应该把这个用户的所有信息存储到一张散列表里面。


# 什么是 Redis

> 原文：[https://zwmst.com/2299.html](https://zwmst.com/2299.html)

**Redis 是完全开源免费的，遵守 BSD 协议，是一个高性能的 key-value 数据库**。

## Redis 与其他 key – value 缓存产品有以下三个特点：

*   （1） Redis 支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。
*   （2） Redis 不仅仅支持简单的 key-value 类型的数据，同时还提供 list， set，zset，hash 等数据结构的存储。
*   （3） Redis 支持数据的备份，即 master-slave 模式的数据备份。

## Redis 优势

*   （1） 性能极高 – Redis 能读的速度是 110000 次/s,写的速度是 81000 次 /s 。
*   （2） 丰富的数据类型 – Redis 支持二进制案例的 Strings, Lists, Hashes, Sets 及 Ordered Sets 数据类型操作。
*   （3） 原子 – Redis 的所有操作都是原子性的，意思就是要么成功执行要么失败完全不执行。单个操作是原子性的。多个操作也支持事务，即原子性，通过MULTI 和 EXEC 指令包起来。
*   （4） 丰富的特性 – Redis 还支持 publish/subscribe, 通知, key 过期等等特性。

## Redis 与其他 key-value 存储有什么不同？

*   （1） Redis 有着更为复杂的数据结构并且提供对他们的原子性操作，这是一个不同于其他数据库的进化路径。Redis 的数据类型都是基于基本数据结构的同时对程序员透明，无需进行额外的抽象。
*   （2） Redis 运行在内存中但是可以持久化到磁盘，所以在对不同数据集进行高速读写时需要权衡内存，因为数据量不能大于硬件内存。在内存数据库方面的另一个优点是，相比在磁盘上相同的复杂的数据结构，在内存中操作起来非常简单，这样 Redis 可以做很多内部复杂性很强的事情。同时，在磁盘格式方面他们是紧凑的以追加的方式产生的，因为他们并不需要进行随机访问。


# Redis 的数据类型

> 原文：[https://zwmst.com/2301.html](https://zwmst.com/2301.html)

答：Redis 支持五种数据类型：**string（字符串），hash（哈希），list（列表），set（集合）及 zsetsorted set：有序集合)。
我们实际项目中比较常用的是 string，hash 如果你是 Redis 中高级用户，还需要加上下面几种数据结构 HyperLogLog、Geo、Pub/Sub。
如果你说还玩过 Redis Module，像 BloomFilter，RedisSearch，Redis-ML，面试官得眼睛就开始发亮了。


# 使用 Redis 有哪些好处？

> 原文：[https://zwmst.com/2303.html](https://zwmst.com/2303.html)

*   （1） 速度快，因为数据存在内存中，类似于 HashMap，HashMap 的优势就是查找和操作的时间复杂度都是 O1)
*   （2） 支持丰富数据类型，支持 string，list，set，Zset，hash 等
*   （3） 支持事务，操作都是原子性，所谓的原子性就是对数据的更改要么全部执行，要么全部不执行
*   （4） 丰富的特性：可用于缓存，消息，按 key 设置过期时间，过期后将会自动删除


# Redis 相比 Memcached 有哪些优势？

> 原文：[https://zwmst.com/2305.html](https://zwmst.com/2305.html)

*   （1） Memcached 所有的值均是简单的字符串，redis 作为其替代者，支持更为丰富的数据类
*   （2） Redis 的速度比 Memcached 快很
*   （3） Redis 可以持久化其数据


# Memcache 与 Redis 的区别都有哪些？

> 原文：[https://zwmst.com/2307.html](https://zwmst.com/2307.html)

*   （1） 存储方式 Memecache 把数据全部存在内存之中，断电后会挂掉，数据不能超过内存大小。 Redis 有部份存在硬盘上，这样能保证数据的持久性。
*   （2） 数据支持类型 Memcache 对数据类型支持相对简单。 Redis 有复杂的数据类型。
*   （3） 使用底层模型不同 它们之间底层实现方式 以及与客户端之间通信的应用协议不一样。 Redis 直接自己构建了 VM 机制 ，因为一般的系统调用系统函数的话，会浪费一定的时间去移动和请求。


# Redis 是单进程单线程的

> 原文：[https://zwmst.com/2309.html](https://zwmst.com/2309.html)

答：Redis 是单进程单线程的，redis 利用队列技术将并发访问变为串行访问，消除了传统数据库串行控制的开销。


# 一个字符串类型的值能存储最大容量是多少？

> 原文：[https://zwmst.com/2314.html](https://zwmst.com/2314.html)

答：512M


# Redis 的持久化机制是什么？各自的优缺点？

> 原文：[https://zwmst.com/2320.html](https://zwmst.com/2320.html)

**Redis 提供两种持久化机制 RDB 和 AOF 机制:

## 1、RDBRedis DataBase)持久化方式：

是指用数据集快照的方式半持久化模式)记录 redis 数据库的所有键值对,在某个时间点将数据写入一个临时文件，持久化结束后，用这个临时文件替换上次持久化的文件，达到数据恢复。
**优点：

*   （1） 只有一个文件 dump.rdb，方便持久化。
*   （2） 容灾性好，一个文件可以保存到安全的磁盘。
*   （3） 性能最大化，fork 子进程来完成写操作，让主进程继续处理命令，所以是 IO 最大化。使用单独子进程来进行持久化，主进程不会进行任何 IO 操 作，保证了 redis 的高性能)
*   （4） 相对于数据集大时，比 AOF 的启动效率更高。

**缺点：
数据安全性低。RDB 是间隔一段时间进行持久化，如果持久化之间 redis 发生故障，会发生数据丢失。所以这种方式更适合数据要求不严谨的时候

## 2、AOFAppend-only file)持久化方式：

是指所有的命令行记录以 redis 命令请求协议的格式完全持久化存储)保存为 aof 文件。
**优点：

*   （1） 数据安全，aof 持久化可以配置 appendfsync 属性，有 always，每进行一次命令操作就记录到 aof 文件中一次。
*   （2） 通过 append 模式写文件，即使中途服务器宕机，可以通过 redis- check-aof 工具解决数据一致性问题。
*   （3） AOF 机制的 rewrite 模式。AOF 文件没被 rewrite 之前（文件过大时会对命令进行合并重写），可以删除其中的某些命令（比如误操作的 flushall）)
    **缺点：
*   （1） AOF 文件比 RDB 文件大，且恢复速度慢。
*   （2） 数据集大的时候，比 rdb 启动效率低。


# Redis 常见性能问题和解决方案

> 原文：[https://zwmst.com/2323.html](https://zwmst.com/2323.html)

*   （1） Master 最好不要写内存快照，如果 Master 写内存快照，save 命令调度rdbSave 函数，会阻塞主线程的工作，当快照比较大时对性能影响是非常大的，会间断性暂停服务
*   （2） 如果数据比较重要，某个 Slave 开启 AOF 备份数据，策略设置为每秒同步一
*   （3） 为了主从复制的速度和连接的稳定性，Master 和 Slave 最好在同一个局域网
*   （4） 尽量避免在压力很大的主库上增加从
*   （5） 主从复制不要用图状结构，用单向链表结构更为稳定，即：Master <- Slave1<- Slave2 <- Slave3…这样的结构方便解决单点故障问题，实现 Slave 对 Master 的替换。如果 Master 挂了，可以立刻启用 Slave1 做 Master，其他不变。


# redis 过期键的删除策略？

> 原文：[https://zwmst.com/2325.html](https://zwmst.com/2325.html)

*   （1） 定时删除:在设置键的过期时间的同时，创建一个定时器 timer). 让定时器在键的过期时间来临时，立即执行对键的删除操作。
*   （2） 惰性删除:放任键过期不管，但是每次从键空间中获取键时，都检查取得的键是否过期，如果过期的话，就删除该键;如果没有过期，就返回该键。
*   （3） 定期删除:每隔一段时间程序就对数据库进行一次检查，删除里面的过期键。至于要删除多少过期键，以及要检查多少个数据库，则由算法决定。


# Redis 的回收策略(淘汰策略)

> 原文：[https://zwmst.com/2327.html](https://zwmst.com/2327.html)

*   volatile-lru：从已设置过期时间的数据集（server.db[i].expires）中挑选最近最少使用的数据淘汰
*   volatile-ttl：从已设置过期时间的数据集（server.db[i].expires）中挑选将要过期的数据淘汰
*   volatile-random：从已设置过期时间的数据集（server.db[i].expires）中任意选择数据淘汰
*   allkeys-lru：从数据集（server.db[i].dict）中挑选最近最少使用的数据淘汰
*   allkeys-random：从数据集（server.db[i].dict）中任意选择数据淘汰
*   no-enviction（驱逐）：禁止驱逐数据
    注意这里的 6 种机制，volatile 和 allkeys 规定了是对已设置过期时间的数据集淘汰数据还是从全部数据集淘汰数据，后面的 lru、ttl 以及 random 是三种不同的淘汰策略，再加上一种 no-enviction 永不回收的策略。
    **使用策略规则：
*   （1） 如果数据呈现幂律分布，也就是一部分数据访问频率高，一部分数据访问频率低，则使用 allkeys-lru
*   （2） 如果数据呈现平等分布，也就是所有的数据访问频率都相同，则使用 allkeys-random


# 为什么 redis 需要把所有数据放到内存中？

> 原文：[https://zwmst.com/2329.html](https://zwmst.com/2329.html)

答 ：Redis 为了达到最快的读写速度将数据都读到内存中，并通过异步的方式将数据写入磁盘。所以 redis 具有快速和数据持久化的特征。
如果不将数据放在内存中，磁盘 I/O 速度为严重影响 redis 的性能。在内存越来越便宜的今天，redis 将会越来越受欢迎。如果设置了最大使用的内存，则数据已有记录数达到内存限值后不能继续插入新值。


# Redis 的同步机制了解么？

> 原文：[https://zwmst.com/2331.html](https://zwmst.com/2331.html)

答：Redis 可以使用主从同步，从从同步。
第一次同步时，主节点做一次bgsave，并同时将后续修改操作记录到内存 buffer，待完成后将 rdb 文件全量同步到复制节点，复制节点接受完成后将 rdb 镜像加载到内存。加载完成后，再通知主节点将期间修改的操作记录同步到复制节点进行重放就完成了同步过程。


# Pipeline 有什么好处，为什么要用 pipeline

> 原文：[https://zwmst.com/2333.html](https://zwmst.com/2333.html)

答：可以将多次 IO 往返的时间缩减为一次，前提是 pipeline 执行的指令之间没有因果相关性。
使用 redis-benchmark 进行压测的时候可以发现影响 redis 的 QPS 峰值的一个重要因素是 pipeline 批次指令的数目。


# 是否使用过 Redis 集群，集群的原理是什么？

> 原文：[https://zwmst.com/2335.html](https://zwmst.com/2335.html)

*   （1） Redis Sentinal 着眼于高可用，在 master 宕机时会自动将 slave 提升为 master，继续提供服务。
*   （2） Redis Cluster 着眼于扩展性，在单个 redis 内存不足时，使用Cluster 进行分片存储。


# Redis 集群方案什么情况下会导致整个集群不可用？

> 原文：[https://zwmst.com/2337.html](https://zwmst.com/2337.html)

答：有 A，B，C 三个节点的集群,在没有复制模型的情况下,如果节点 B 失败了，那么整个集群就会以为缺少 5501-11000 这个范围的槽而不可用。


# Redis 支持的 Java 客户端都有哪些？官方推荐用哪个？

> 原文：[https://zwmst.com/2339.html](https://zwmst.com/2339.html)

答：**Redisson、Jedis、lettuce** 等等，官方推荐使用 Redisson。


# Jedis 与 Redisson 对比有什么优缺点？

> 原文：[https://zwmst.com/2341.html](https://zwmst.com/2341.html)

答：Jedis 是 Redis 的 Java 实现的客户端，其 API 提供了比较全面的Redis 命令的支持；
Redisson 实现了分布式和可扩展的 Java 数据结构，和 Jedis 相比，功能较为简单，不支持字符串操作，不支持排序、事务、管道、分区等 Redis 特性。
Redisson 的宗旨是促进使用者对 Redis 的关注分离，从而让使用者能够将精力更集中地放在处理业务逻辑上。


# Redis 如何设置密码及验证密码？

> 原文：[https://zwmst.com/2343.html](https://zwmst.com/2343.html)

设置密码：config set requirepass 123456 授权密码：auth 123456


# 说说 Redis 哈希槽的概念？

> 原文：[https://zwmst.com/2345.html](https://zwmst.com/2345.html)

答：Redis 集群没有使用一致性 hash,而是引入了哈希槽的概念，Redis 集群有 16384 个哈希槽，每个 key 通过 CRC16 校验后对 16384 取模来决定放置哪个槽，集群的每个节点负责一部分 hash 槽。


# Redis 集群的主从复制模型是怎样的？

> 原文：[https://zwmst.com/2347.html](https://zwmst.com/2347.html)

答：为了使在部分节点失败或者大部分节点无法通信的情况下集群仍然可用，所以集群使用了主从复制模型,每个节点都会有 N-1 个复制品.


# Redis 集群会有写操作丢失吗？为什么？

> 原文：[https://zwmst.com/2349.html](https://zwmst.com/2349.html)

答 ：Redis 并不能保证数据的强一致性，这意味这在实际中集群在特定的条件下可能会丢失写操作。


# Redis 集群之间是如何复制的

> 原文：[https://zwmst.com/2351.html](https://zwmst.com/2351.html)

答：异步复制


# Redis 集群最大节点个数是多少？

> 原文：[https://zwmst.com/2353.html](https://zwmst.com/2353.html)

答：16384 个。


# Redis 集群如何选择数据库？

> 原文：[https://zwmst.com/2355.html](https://zwmst.com/2355.html)

答：Redis 集群目前无法做数据库选择，默认在 0 数据库。


# 怎么测试 Redis 的连通性？

> 原文：[https://zwmst.com/2357.html](https://zwmst.com/2357.html)

答：使用 ping 命令。


# 怎么理解 Redis 事务？

> 原文：[https://zwmst.com/2361.html](https://zwmst.com/2361.html)

答：

*   （1） 事务是一个单独的隔离操作：事务中的所有命令都会序列化、按顺序地执行。事务在执行的过程中，不会被其他客户端发送来的命令请求所打断。
*   （2） 事务是一个原子操作：事务中的命令要么全部被执行，要么全部都不执行。


# Redis 事务相关的命令有哪几个？

> 原文：[https://zwmst.com/2363.html](https://zwmst.com/2363.html)

答：**MULTI、EXEC、DISCARD、WATCH


# Redis key 的过期时间和永久有效分别怎么设置

> 原文：[https://zwmst.com/2365.html](https://zwmst.com/2365.html)

答：**EXPIRE 和 PERSIST** 命令。


# Redis 如何做内存优化？

> 原文：[https://zwmst.com/2367.html](https://zwmst.com/2367.html)

答：尽可能使用**散列表（hashes）**，散列表（是说散列表里面存储的数少）使用的内存非常小，所以你应该尽可能的将你的数据模型抽象到一个散列表里面。
比如你的 web 系统中有一个用户对象，不要为这个用户的名称，姓氏，邮箱，密码设置单独的 key,而是应该把这个用户的所有信息存储到一张散列表里面。


# Redis 回收进程如何工作的？

> 原文：[https://zwmst.com/2369.html](https://zwmst.com/2369.html)

答：
一个客户端运行了新的命令，添加了新的数据。
Redi 检查内存使用情况,如果大于 maxmemory 的限制, 则根据设定好的策略进行回收。
一个新的命令被执行，等等。
所以我们不断地穿越内存限制的边界，通过不断达到边界然后不断地回收回到边界以下。
如果一个命令的结果导致大量内存被使用（例如很大的集合的交集保存到一个新的键），不用多久内存限制就会被这个内存使用量超越。


# 都有哪些办法可以降低 Redis 的内存使用情况呢？

> 原文：[https://zwmst.com/2371.html](https://zwmst.com/2371.html)

答：如果你使用的是 32 位的 Redis 实例，可以好好利用 Hash,list,sorted set,set 等集合类型数据，因为通常情况下很多小的 Key-Value 可以用更紧凑的方式存放到一起。


# Redis 的内存用完了会发生什么

> 原文：[https://zwmst.com/2373.html](https://zwmst.com/2373.html)

答：如果达到设置的上限，Redis 的写命令会返回错误信息（但是读命令还可以正常返回。）或者你可以将 Redis 当缓存来使用配置淘汰机制，当 Redis 达到内存上限时会冲刷掉旧的内容。


# 一个 Redis 实例最多能存放多少的 keys？ List、Set、Sorted Set 他们最多能存放多少元素？

> 原文：[https://zwmst.com/2375.html](https://zwmst.com/2375.html)

答：理论上 Redis 可以处理多达 2的32次方 的 keys，并且在实际中进行了测试，每个实例至少存放了 2 亿 5 千万的 keys。我们正在测试一些较大的值。
任何list、set、和 sorted set 都可以放 232 个元素。换句话说，Redis 的存储极限是系统中的可用内存值。


# MySQL 里有 2000w 数据，redis 中只存 20w 的数据，如何保证 redis 中的数据都是热点数据

> 原文：[https://zwmst.com/2377.html](https://zwmst.com/2377.html)

答：Redis 内存数据集大小上升到一定大小的时候，就会施行数据淘汰策略。
相关知识：Redis 提供 6 种数据淘汰策略：

*   volatile-lru：从已设置过期时间的数据集（server.db[i].expires）中挑选最近最少使用的数据淘汰
*   volatile-ttl：从已设置过期时间的数据集（server.db[i].expires）中挑选将要过期的数据淘汰
*   volatile-random：从已设置过期时间的数据集（server.db[i].expires）中任意选择数据淘汰
*   allkeys-lru：从数据集（server.db[i].dict）中挑选最近最少使用的数据淘汰
*   allkeys-random：从数据集（server.db[i].dict）中任意选择数据淘汰
*   no-enviction（驱逐）：禁止驱逐数据


# Redis 最适合的场景

> 原文：[https://zwmst.com/2379.html](https://zwmst.com/2379.html)

## 1、 会话缓存（Session Cache）

最常用的一种使用 Redis 的情景是会话缓存（session cache）。用 Redis 缓存会话比其他存储（如 Memcached）的优势在于：Redis 提供持久化。
当维护一个不是严格要求一致性的缓存时，如果用户的购物车信息全部丢失，大部分人都会不高兴的，现在，他们还会这样吗？ 幸运的是，随着 Redis 这些年的改进，很容易找到怎么恰当的使用 Redis 来缓存会话的文档。甚至广为人知的商业平台 Magento 也提供 Redis 的插件。

## 2、 全页缓存（FPC）

除基本的会话 token 之外，Redis 还提供很简便的 FPC 平台。回到一致性问题，即使重启了 Redis 实例，因为有磁盘的持久化，用户也不会看到页面加载速度的下降，这是一个极大改进，类似 PHP 本地 FPC。 再次以 Magento 为例，Magento 提供一个插件来使用 Redis 作为全页缓存后端。
此外，对WordPress 的用户来说，Pantheon 有一个非常好的插件 wp-redis，这个插件能帮助你以最快速度加载你曾浏览过的页面。

## 3、 队列

Reids 在内存存储引擎领域的一大优点是提供 list 和 set 操作，这使得Redis 能作为一个很好的消息队列平台来使用。Redis 作为队列使用的操作，就类似于本地程序语言（如 Python）对 list 的 push/pop 操作。
如果你快速的在 Google 中搜索“Redis queues”，你马上就能找到大量的开源项目， 这些项目的目的就是利用 Redis 创建非常好的后端工具，以满足各种队列需求。
例如，Celery 有一个后台就是使用 Redis 作为 broker，你可以从这里去查看。

## 4，排行榜/计数器

Redis 在内存中对数字进行递增或递减的操作实现的非常好。集合（Set）和有序集合（Sorted Set）也使得我们在执行这些操作的时候变的非常简单，Redis 只是正好提供了这两种数据结构。所以，我们要从排序集合中获取到排名最靠前的 10 个用户–我们称之为“user_scores”，我们只需要像下面一样执行即可： 当然，这是假定你是根据你用户的分数做递增的排序。
如果你想返回用户及用户的分数，你需要这样执行： ZRANGE user_scores 0 10 WITHSCORES Agora Games 就是一个很好的例子，用 Ruby 实现的，它的排行榜就是使用
Redis 来存储数据的，你可以在这里看到。

## 5、发布/订阅

最后（但肯定不是最不重要的）是 Redis 的发布/订阅功能。发布/订阅的使用场景确实非常多。我已看见人们在社交网络连接中使用，还可作为基于发布/订阅的脚本触发器，甚至用 Redis 的发布/订阅功能来建立聊天系统！


# 假如 Redis 里面有 1 亿个 key，其中有 10w 个 key 是以某个固定的已知的前缀开头的，如果将它们全部找出来？

> 原文：[https://zwmst.com/2381.html](https://zwmst.com/2381.html)

答：使用 keys 指令可以扫出指定模式的 key 列表。
对方接着追问：如果这个 redis 正在给线上的业务提供服务，那使用 keys 指令会有什么问题？
这个时候你要回答 redis 关键的一个特性：**redis 的单线程的**。keys 指令会导致线程阻塞一段时间，线上服务会停顿，直到指令执行完毕，服务才能恢复。
这个时候可以使用 scan 指令，scan 指令可以无阻塞的提取出指定模式的 key 列表，但是会有一定的重复概率，在客户端做一次去重就可以了，但是整体所花费的时间会比直接用 keys 指令长。


# 如果有大量的 key 需要设置同一时间过期，一般需要注意什么

> 原文：[https://zwmst.com/2383.html](https://zwmst.com/2383.html)

答：如果大量的 key 过期时间设置的过于集中，到过期的那个时间点，redis 可能会出现短暂的卡顿现象。一般需要在时间上加一个随机值，使得过期时间分散一些。


# 使用过 Redis 做异步队列么，你是怎么用的

> 原文：[https://zwmst.com/2385.html](https://zwmst.com/2385.html)

答：一般使用 list 结构作为队列，rpush 生产消息，lpop 消费消息。当 lpop 没有消息的时候，要适当 sleep 一会再重试。
如果对方追问可不可以不用 sleep 呢？list 还有个指令叫 blpop，在没有消息的时候，它会阻塞住直到消息到来。如果对方追问能不能生产一次消费多次呢？使用 pub/sub 主题订阅者模式，可以实现 1:N 的消息队列。
如果对方追问 pub/sub 有什么缺点？
在消费者下线的情况下，生产的消息会丢失，得使用专业的消息队列如RabbitMQ 等。
如果对方追问 redis 如何实现延时队列？
我估计现在你很想把面试官一棒打死如果你手上有一根棒球棍的话，怎么问的这么详细。但是你很克制，然后神态自若的回答道：使用 sortedset，拿时间戳作为 score，消息内容作为 key 调用 zadd 来生产消息，消费者用zrangebyscore 指令获取 N 秒之前的数据轮询进行处理。
到这里，面试官暗地里已经对你竖起了大拇指。但是他不知道的是此刻你却竖起了中指，在椅子背后。


# 使用过 Redis 分布式锁么，它是什么回事？

> 原文：[https://zwmst.com/2387.html](https://zwmst.com/2387.html)

先拿 setnx 来争抢锁，抢到之后，再用 expire 给锁加一个过期时间防止锁忘记了释放。
这时候对方会告诉你说你回答得不错，然后接着问如果在 setnx 之后执行expire 之前进程意外 crash 或者要重启维护了，那会怎么样？
这时候你要给予惊讶的反馈：唉，是喔，这个锁就永远得不到释放了。
紧接着你需要抓一抓自己得脑袋，故作思考片刻，好像接下来的结果是你主动思考出来的，然后回答：我记得 set 指令有非常复杂的参数，这个应该是可以同时把 setnx 和 expire 合成一条指令来用的！
对方这时会显露笑容，心里开始默念：摁，这小子还不错。


# 1241.redis 和 memcached 什么区别？为什么高并发下有时单线程的 redis 比多线程的 memcached 效率要高？

> 原文：[https://zwmst.com/5791.html](https://zwmst.com/5791.html)

## 区别：

1.  mc 可缓存图片和视频。rd 支持除 k/v 更多的数据结构;
2.  rd 可以使用虚拟内存，rd 可持久化和 aof 灾难恢复，rd 通过主从支持数据备份;
3.  rd 可以做消息队列。

## 原因：

mc 多线程模型引入了缓存一致性和锁，加锁带来了性能损耗。


# 1242.redis 主从复制如何实现的？redis 的集群模式如何实现？redis 的 key 是如何寻址的？

> 原文：[https://zwmst.com/5793.html](https://zwmst.com/5793.html)

主从复制实现：主节点将自己内存中的数据做一份快照，将快照发给从节点，从节点将数据恢复到内存中。之后再每次增加新数据的时候，主节点以类似于 mysql 的二进制日志方式将语句发送给从节点，从节点拿到主节点发送过来的语句进行重放。
分片方式：

1.  客户端分片
2.  基于代理的分片
    1.  Twemproxy
    2.  codis
        3.路由查询分片
    3.  Redis-cluster（本身提供了自动将数据分散到 Redis Cluster 不同节点的能力，整个数据集合的某个数据子集存储在哪个节点对于用户来说是透明的）redis-cluster 分片原理：Cluster 中有一个 16384 长度的槽(虚拟槽)，编号分别为 0-16383。每个 Master 节点都会负责一部分的槽，当有某个 key 被映射到某个 Master 负责的槽，那么这个 Master 负责为这个 key 提供服务，至于哪个 Master 节点负责哪个槽，可以由用户指定，也可以在初始化的时候自动生成，只有 Master 才拥有槽的所有权。Master 节点维护着一个 16384/8 字节的位序列，Master 节点用 bit 来标识对于某个槽自己是否拥有。比如对于编号为 1 的槽，Master 只要判断序列的第二位（索引从 0 开始）是不是为 1 即可。这种结构很容易添加或者删除节点。比如如果我想新添加个节点 D, 我需要从节点 A、B、C 中得部分槽到 D 上。


# 1243.使用 redis 如何设计分布式锁？说一下实现思路？使用 zk 可以吗？如何实现？这两种有什 么区别？

> 原文：[https://zwmst.com/5795.html](https://zwmst.com/5795.html)

## redis:

1.  线程 A setnx(上锁的对象,超时时的时间戳 t1)，如果返回 true，获得锁。
2.  线程 B 用 get 获取 t1,与当前时间戳比较,判断是是否超时,没超时 false,若超时执行第 3 步;
3.  计算新的超时时间 t2,使用 getset 命令返回 t3(该值可能其他线程已经修改过),如果t1==t3，获得锁，如果 t1!=t3 说明锁被其他线程获取了。
4.  获取锁后，处理完业务逻辑，再去判断锁是否超时，如果没超时删除锁，如果已超时，不用处理（防止删除其他线程的锁）。

## zk:

1.  客户端对某个方法加锁时，在 zk 上的与该方法对应的指定节点的目录下，生成一个唯一的瞬时有序节点 node1;
2.  客户端获取该路径下所有已经创建的子节点，如果发现自己创建的 node1 的序号是最小的，就认为这个客户端获得了锁。
3.  如果发现 node1 不是最小的，则监听比自己创建节点序号小的最大的节点，进入等待。
4.  获取锁后，处理完逻辑，删除自己创建的 node1 即可。

## 区别:

zk 性能差一些，开销大，实现简单。


# 1244.知道 redis 的持久化吗？底层如何实现的？有什么优点缺点？

> 原文：[https://zwmst.com/5797.html](https://zwmst.com/5797.html)

RDB(Redis DataBase:在不同的时间点将 redis 的数据生成的快照同步到磁盘等介质上):内存到硬盘的快照，定期更新。缺点：耗时，耗性能(fork+io 操作)，易丢失数据。

AOF(Append Only File：将 redis 所执行过的所有指令都记录下来，在下次 redis 重启时，只需要执行指令就可以了):写日志。缺点：体积大，恢复速度慢。

bgsave 做镜像全量持久化，aof 做增量持久化。因为 bgsave 会消耗比较长的时间，不够实时，在停机的时候会导致大量的数据丢失，需要 aof 来配合，在 redis 实例重启时，优先使用 aof 来恢复内存的状态，如果没有 aof 日志，就会使用 rdb 文件来恢复。Redis 会定期做aof 重写，压缩 aof 文件日志大小。Redis4.0 之后有了混合持久化的功能，将 bgsave 的全量和 aof 的增量做了融合处理，这样既保证了恢复的效率又兼顾了数据的安全性。bgsave 的原理，fork 和 cow, fork 是指 redis 通过创建子进程来进行 bgsave 操作，cow 指的是 copy onwrite，子进程创建后，父子进程共享数据段，父进程继续提供读写服务，写脏的页面数据会逐渐和子进程分离开来。


# 1245.redis 过期策略都有哪些？LRU 算法知道吗？写一下 java 代码实现？

> 原文：[https://zwmst.com/5799.html](https://zwmst.com/5799.html)

过期策略:
定时过期(一 key 一定时器)，惰性过期：只有使用 key 时才判断 key 是否已过期，过期则清除。定期过期：前两者折中。

LRU:new LinkedHashMap<K, V>(capacity, DEFAULT_LOAD_FACTORY, true);

//第三个参数置为 true，代表 linkedlist 按访问顺序排序，可作为 LRU 缓存；设为 false 代表按插入顺序排序，可作为 FIFO 缓存

LRU 算法实现：1.通过双向链表来实现，新数据插入到链表头部；2.每当缓存命中（即缓存数据被访问），则将数据移到链表头部；3.当链表满的时候，将链表尾部的数据丢弃。

LinkedHashMap：HashMap 和双向链表合二为一即是 LinkedHashMap。HashMap 是无序的，LinkedHashMap 通过维护一个额外的双向链表保证了迭代顺序。该迭代顺序可以是插入顺序（默认），也可以是访问顺序。


# 1246.缓存穿透、缓存击穿、缓存雪崩解决方案？

> 原文：[https://zwmst.com/5801.html](https://zwmst.com/5801.html)

## 缓存穿透：

指查询一个一定不存在的数据，如果从存储层查不到数据则不写入缓存，这将导致这个不存在的数据每次请求都要到 DB 去查询，可能导致 DB 挂掉。

## 解决方案：

1.  查询返回的数据为空，仍把这个空结果进行缓存，但过期时间会比较短；
2.  布隆过滤器：将所有可能存在的数据哈希到一个足够大的 bitmap 中，一个一定不存在的数据会被这个 bitmap 拦截掉，从而避免了对 DB 的查询。

## 缓存击穿：

对于设置了过期时间的 key，缓存在某个时间点过期的时候，恰好这时间点对这个 Key 有大量的并发请求过来，这些请求发现缓存过期一般都会从后端 DB 加载数据并回设到缓存，这个时候大并发的请求可能会瞬间把 DB 压垮。

## 解决方案：

1.  使用互斥锁：当缓存失效时，不立即去 load db，先使用如 Redis 的 setnx 去设置一个互斥锁，当操作成功返回时再进行 load db 的操作并回设缓存，否则重试 get 缓存的方法。
2.  永远不过期：物理不过期，但逻辑过期（后台异步线程去刷新）。

## 缓存雪崩：

设置缓存时采用了相同的过期时间，导致缓存在某一时刻同时失效，请求全部转发到 DB，DB 瞬时压力过重雪崩。与缓存击穿的区别：雪崩是很多 key，击穿是某一个key 缓存。

## 解决方案：

将缓存失效时间分散开，比如可以在原有的失效时间基础上增加一个随机值，比如 1-5 分钟随机，这样每一个缓存的过期时间的重复率就会降低，就很难引发集体失效的事件。


# 1247.在选择缓存时，什么时候选择 redis，什么时候选择 memcached

> 原文：[https://zwmst.com/5803.html](https://zwmst.com/5803.html)

选择 redis 的情况：

1.  复杂数据结构，value 的数据是哈希，列表，集合，有序集合等这种情况下，会选择redis, 因为 memcache 无法满足这些数据结构，最典型的的使用场景是，用户订单列表，用户消息，帖子评论等。
2.  需要进行数据的持久化功能，但是注意，不要把 redis 当成数据库使用，如果 redis挂了，内存能够快速恢复热数据，不会将压力瞬间压在数据库上，没有 cache 预热的过程。对于只读和数据一致性要求不高的场景可以采用持久化存储
3.  高可用，redis 支持集群，可以实现主动复制，读写分离，而对于 memcache 如果想要实现高可用，需要进行二次开发。
4.  存储的内容比较大，memcache 存储的 value 最大为 1M。

选择 memcache 的场景：

1.  纯 KV,数据量非常大的业务，使用 memcache 更合适，原因是，
    1.  memcache 的内存分配采用的是预分配内存池的管理方式，能够省去内存分配的时间，redis 是临时申请空间，可能导致碎片化。
    2.  虚拟内存使用，memcache 将所有的数据存储在物理内存里，redis 有自己的 vm 机制，理论上能够存储比物理内存更多的数据，当数据超量时，引发 swap,把冷数据刷新到磁盘上，从这点上，数据量大时，memcache 更快
    3.  网络模型，memcache 使用非阻塞的 IO 复用模型，redis 也是使用非阻塞的 IO 复用模型，但是 redis 还提供了一些非 KV 存储之外的排序，聚合功能，复杂的 CPU 计算，会阻塞整个 IO 调度，从这点上由于 redis 提供的功能较多，memcache 更快些
    4.  线程模型，memcache 使用多线程，主线程监听，worker 子线程接受请求，执行读写，这个过程可能存在锁冲突。redis 使用的单线程，虽然无锁冲突，但是难以利用多核的特性提升吞吐量。


# 1248.缓存与数据库不一致怎么办

> 原文：[https://zwmst.com/5805.html](https://zwmst.com/5805.html)

假设采用的主存分离，读写分离的数据库，

如果一个线程 A 先删除缓存数据，然后将数据写入到主库当中，这个时候，主库和从库同步没有完成，线程 B 从缓存当中读取数据失败，从从库当中读取到旧数据，然后更新至缓存，这个时候，缓存当中的就是旧的数据。

发生上述不一致的原因在于，主从库数据不一致问题，加入了缓存之后，主从不一致的时间被拉长了

处理思路：
在从库有数据更新之后，将缓存当中的数据也同时进行更新，即当从库发生了数据更新之后，向缓存发出删除，淘汰这段时间写入的旧数据。


# 1249.主从数据库不一致如何解决

> 原文：[https://zwmst.com/5807.html](https://zwmst.com/5807.html)

场景描述，对于主从库，读写分离，如果主从库更新同步有时差，就会导致主从库数据的不一致

1.  忽略这个数据不一致，在数据一致性要求不高的业务下，未必需要时时一致性
2.  强制读主库，使用一个高可用的主库，数据库读写都在主库，添加一个缓存，提升数据读取的性能。
3.  选择性读主库，添加一个缓存，用来记录必须读主库的数据，将哪个库，哪个表，哪个主键，作为缓存的 key,设置缓存失效的时间为主从库同步的时间，如果缓存当中有这个数据，直接读取主库，如果缓存当中没有这个主键，就到对应的从库中读取。


# 1250.Redis 常见的性能问题和解决方案

> 原文：[https://zwmst.com/5811.html](https://zwmst.com/5811.html)

1.  master 最好不要做持久化工作，如 RDB 内存快照和 AOF 日志文件
2.  如果数据比较重要，某个 slave 开启 AOF 备份，策略设置成每秒同步一次
3.  为了主从复制的速度和连接的稳定性，master 和 Slave 最好在一个局域网内
4.  尽量避免在压力大得主库上增加从库
5.  主从复制不要采用网状结构，尽量是线性结构，Master<–Slave1<—-Slave2 ….


# 1251.Redis 的数据淘汰策略有哪些

> 原文：[https://zwmst.com/5813.html](https://zwmst.com/5813.html)

voltile-lru 从已经设置过期时间的数据集中挑选最近最少使用的数据淘汰
voltile-ttl 从已经设置过期时间的数据库集当中挑选将要过期的数据
voltile-random 从已经设置过期时间的数据集任意选择淘汰数据
allkeys-lru 从数据集中挑选最近最少使用的数据淘汰
allkeys-random 从数据集中任意选择淘汰的数据
no-eviction 禁止驱逐数据


# 1252.Redis 当中有哪些数据结构

> 原文：[https://zwmst.com/5815.html](https://zwmst.com/5815.html)

字符串 String、字典 Hash、列表 List、集合 Set、有序集合 SortedSet。如果是高级用户，那么还会有，如果你是 Redis 中高级用户，还需要加上下面几种数据结构 HyperLogLog、Geo、Pub/Sub。


# 1253.假如 Redis 里面有 1 亿个 key，其中有 10w 个 key 是以某个固定的已知的前缀开头的，如 果将它们全部找出来？

> 原文：[https://zwmst.com/5817.html](https://zwmst.com/5817.html)

使用 keys 指令可以扫出指定模式的 key 列表。
对方接着追问：如果这个 redis 正在给线上的业务提供服务，那使用 keys 指令会有什么问题？
这个时候你要回答 redis 关键的一个特性：redis 的单线程的。keys 指令会导致线程阻塞一段时间，线上服务会停顿，直到指令执行完毕，服务才能恢复。这个时候可以使用 scan 指令，scan 指令可以无阻塞的提取出指定模式的 key 列表，但是会有一定的重复概率，在客户端做一次去重就可以了，但是整体所花费的时间会比直接用 keys 指令长。


# 1254.使用 Redis 做过异步队列吗，是如何实现的

> 原文：[https://zwmst.com/5819.html](https://zwmst.com/5819.html)

使用 list 类型保存数据信息，rpush 生产消息，lpop 消费消息，当 lpop 没有消息时，可以 sleep 一段时间，然后再检查有没有信息，如果不想 sleep 的话，可以使用 blpop, 在没有信息的时候，会一直阻塞，直到信息的到来。redis 可以通过 pub/sub 主题订阅模式实现一个生产者，多个消费者，当然也存在一定的缺点，当消费者下线时，生产的消息会丢失。


# 1255.Redis 如何实现延时队列

> 原文：[https://zwmst.com/5821.html](https://zwmst.com/5821.html)

使用 sortedset，使用时间戳做 score, 消息内容作为 key,调用 zadd 来生产消息，消费者使用 zrangbyscore 获取 n 秒之前的数据做轮询处理


# 1256.什么是 Redis？简述它的优缺点？

> 原文：[https://zwmst.com/5823.html](https://zwmst.com/5823.html)

Redis 本质上是一个 Key-Value 类型的内存数据库，很像 memcached，整个数据库统统加载在内存当中进行操作，定期通过异步操作把数据库数据 flush 到硬盘上进行保存。
因为是纯内存操作，Redis 的性能非常出色，每秒可以处理超过 10 万次读写操作，是已知性能最快的 Key-Value DB。
Redis 的出色之处不仅仅是性能，Redis 最大的魅力是支持保存多种数据结构，此外单个 value 的最大限制是 1GB，不像 memcached 只能保存 1MB 的数据，因此 Redis 可以用来实现很多有用的功能。
比方说用他的 List 来做 FIFO 双向链表，实现一个轻量级的高性 能消息队列服务，用他的 Set 可以做高性能的 tag 系统等等。
另外 Redis 也可以对存入的 Key-Value 设置 expire 时间，因此也可以被当作一 个功能加强版的 memcached 来用。 Redis 的主要缺点是数据库容量受到物理内存的限制，不能用作海量数据的高性能读写，因此 Redis 适合的场景主要局限在较小数据量的高性能操作和运算上。


# 1257.Redis 相比 memcached 有哪些优势？

> 原文：[https://zwmst.com/5825.html](https://zwmst.com/5825.html)

1.  memcached 所有的值均是简单的字符串，redis 作为其替代者，支持更为丰富的数据类型
2.  redis 的速度比 memcached 快很多
3.  redis 可以持久化其数据


# 1258.Redis 支持哪几种数据类型？

> 原文：[https://zwmst.com/5827.html](https://zwmst.com/5827.html)

String、List、Set、Sorted Set、hashes


# 1259.Redis 主要消耗什么物理资源？

> 原文：[https://zwmst.com/5829.html](https://zwmst.com/5829.html)

内存。


# 1260.Redis 的全称是什么？

> 原文：[https://zwmst.com/5831.html](https://zwmst.com/5831.html)

Remote Dictionary Server。


# 1261.Redis 有哪几种数据淘汰策略？

> 原文：[https://zwmst.com/5833.html](https://zwmst.com/5833.html)

noeviction:返回错误当内存限制达到并且客户端尝试执行会让更多内存被使用的命令（大部分的写入指令，但 DEL 和几个例外）
allkeys-lru: 尝试回收最少使用的键（LRU），使得新添加的数据有空间存放。
volatile-lru: 尝试回收最少使用的键（LRU），但仅限于在过期集合的键,使得新添加的数据有空间存放。
allkeys-random: 回收随机的键使得新添加的数据有空间存放。
volatile-random: 回收随机的键使得新添加的数据有空间存放，但仅限于在过期集合的键。
volatile-ttl: 回收在过期集合的键，并且优先回收存活时间（TTL）较短的键,使得新添加的数据有空间存放。


# 1262.Redis 官方为什么不提供 Windows 版本？

> 原文：[https://zwmst.com/5835.html](https://zwmst.com/5835.html)

因为目前 Linux 版本已经相当稳定，而且用户量很大，无需开发 windows 版本，反而会带来兼容性等问题。


# 1263.一个字符串类型的值能存储最大容量是多少？

> 原文：[https://zwmst.com/5837.html](https://zwmst.com/5837.html)

512M


# 1264.为什么 Redis 需要把所有数据放到内存中？

> 原文：[https://zwmst.com/5839.html](https://zwmst.com/5839.html)

Redis 为了达到最快的读写速度将数据都读到内存中，并通过异步的方式将数据写入磁盘。
所以 redis 具有快速和数据持久化的特征。如果不将数据放在内存中，磁盘 I/O 速度为严重影响 redis 的性能。
在内存越来越便宜的今天，redis 将会越来越受欢迎。 如果设置了最大使用的内存，则数据已有记录数达到内存限值后不能继续插入新值。


# 1265.Redis 集群方案应该怎么做？都有哪些方案？

> 原文：[https://zwmst.com/5841.html](https://zwmst.com/5841.html)

1.  codis。
    目前用的最多的集群方案，基本和 twemproxy 一致的效果，但它支持在 节点数量改变情况下，旧节点数
    据可恢复到新 hash 节点。
2.  redis cluster3.0 自带的集群，特点在于他的分布式算法不是一致性 hash，而是 hash 槽的概念，以及自身支持节点设置从节点。具体看官方文档介绍。
3.  在业务代码层实现，起几个毫无关联的 redis 实例，在代码层，对 key 进行 hash 计算，然后去对应的 redis 实例操作数据。 这种方式对 hash 层代码要求比较高，考虑部分包括，节点失效后的替代算法方案，数据震荡后的自动脚本恢复，实例的监控，等等。


# 1266.Redis 集群方案什么情况下会导致整个集群不可用？

> 原文：[https://zwmst.com/5843.html](https://zwmst.com/5843.html)

有 A，B，C 三个节点的集群,在没有复制模型的情况下,如果节点 B 失败了，那么整个集群就会以为缺少 5501-11000 这个范围的槽而不可用。


# 1267.MySQL 里有 2000w 数据，redis 中只存 20w 的数据，如何保证 redis 中的数据都是热点数据？

> 原文：[https://zwmst.com/5845.html](https://zwmst.com/5845.html)

redis 内存数据集大小上升到一定大小的时候，就会施行数据淘汰策略。


# 1268.Redis 有哪些适合的场景？

> 原文：[https://zwmst.com/5847.html](https://zwmst.com/5847.html)

1.  会话缓存（Session Cache）
    最常用的一种使用 Redis 的情景是会话缓存（session cache）。用 Redis 缓存会话比其他存储（如 Memcached）的优势在于：Redis 提供持久化。当维护一个不是严格要求一致性的缓存时，如果用户的购物车信息全部丢失，大部分人都会不高兴的，现在，他们还会这样吗？幸运的是，随着 Redis 这些年的改进，很容易找到怎么恰当的使用 Redis 来缓存会话的文档。甚至广为人知的商业平台 Magento 也提供 Redis 的插件。
2.  全页缓存（FPC）
    除基本的会话 token 之外，Redis 还提供很简便的 FPC 平台。回到一致性问题，即使重启了 Redis 实例，因为有磁盘的持久化，用户也不会看到页面加载速度的下降，这是一个极大改进，类似 PHP 本地 FPC。
    再次以 Magento 为例，Magento 提供一个插件来使用 Redis 作为全页缓存后端。
    此外，对 WordPress 的用户来说，Pantheon 有一个非常好的插件 wp-redis，这个插件能帮助你以最快速度加载你曾浏览过的页面。
3.  队列
    Reids 在内存存储引擎领域的一大优点是提供 list 和 set 操作，这使得 Redis 能作为一个很好的消息队列平台来使用。Redis 作为队列使用的操作，就类似于本地程序语言（如 Python）对 list 的 push/pop操作。
    如果你快速的在 Google 中搜索“Redis queues”，你马上就能找到大量的开源项目，这些项目的目的就是利用 Redis 创建非常好的后端工具，以满足各种队列需求。例如，Celery 有一个后台就是使用 Redis 作为 broker，你可以从这里去查看。
4.  排行榜/计数器
    Redis 在内存中对数字进行递增或递减的操作实现的非常好。集合（Set）和有序集合（Sorted Set）也使得我们在执行这些操作的时候变的非常简单，Redis 只是正好提供了这两种数据结构。
    所以，我们要从排序集合中获取到排名最靠前的 10 个用户–我们称之为“user_scores”，我们只需要像下面一样执行即可：
    当然，这是假定你是根据你用户的分数做递增的排序。如果你想返回用户及用户的分数，你需要这样执行：
    ZRANGE user_scores 0 10 WITHSCORES Agora Games 就是一个很好的例子，用 Ruby 实现的，它的排行榜就是使用 Redis 来存储数据的，你可以在这里看到。
5.  发布/订阅
    最后（但肯定不是最不重要的）是 Redis 的发布/订阅功能。发布/订阅的使用场景确实非常多。我已看见人们在社交网络连接中使用，还可作为基于发布/订阅的脚本触发器，甚至用 Redis 的发布/订阅功能来建立聊天系统！


# 1269.Redis 支持的 Java 客户端都有哪些？官方推荐用哪个？

> 原文：[https://zwmst.com/5849.html](https://zwmst.com/5849.html)

Redisson、Jedis、lettuce 等等，官方推荐使用 Redisson。


# 1270.Redis 和 Redisson 有什么关系？

> 原文：[https://zwmst.com/5851.html](https://zwmst.com/5851.html)

Redisson 是一个高级的分布式协调 Redis 客服端，能帮助用户在分布式环境中轻松实现一些 Java 的对象
(Bloom filter, BitSet, Set, SetMultimap, ScoredSortedSet, SortedSet, Map, ConcurrentMap, List, ListMultimap, Queue, BlockingQueue, Deque, BlockingDeque, Semaphore, Lock, ReadWriteLock, AtomicLong, CountDownLatch, Publish / Subscribe, HyperLogLog)。


# 1271.Jedis 与 Redisson 对比有什么优缺点？

> 原文：[https://zwmst.com/5853.html](https://zwmst.com/5853.html)

Jedis 是 Redis 的 Java 实现的客户端，其 API 提供了比较全面的 Redis 命令的支持；
Redisson 实现了分布式和可扩展的 Java 数据结构，和 Jedis 相比，功能较为简单，不支持字符串操作，不支持排序、事务、管道、分区等 Redis 特性。Redisson 的宗旨是促进使用者对 Redis 的关注分离，从而让使用者能够将精力更集中地放在处理业务逻辑上。


# 1272.、Redis 如何设置密码及验证密码？

> 原文：[https://zwmst.com/5855.html](https://zwmst.com/5855.html)

设置密码：config set requirepass 123456
授权密码：auth 123456


# 1273.说说 Redis 哈希槽的概念？

> 原文：[https://zwmst.com/5857.html](https://zwmst.com/5857.html)

Redis 集群没有使用一致性 hash,而是引入了哈希槽的概念，Redis 集群有 16384 个哈希槽，每个 key 通过 CRC16 校验后对 16384 取模来决定放置哪个槽，集群的每个节点负责一部分 hash 槽。


# 1274.Redis 集群的主从复制模型是怎样的？

> 原文：[https://zwmst.com/5859.html](https://zwmst.com/5859.html)

为了使在部分节点失败或者大部分节点无法通信的情况下集群仍然可用，所以集群使用了主从复制模型,每个节点都会有 N-1 个复制品.


# 1275.Redis 集群会有写操作丢失吗？为什么？

> 原文：[https://zwmst.com/5861.html](https://zwmst.com/5861.html)

Redis 并不能保证数据的强一致性，这意味这在实际中集群在特定的条件下可能会丢失写操作。


# 1276.Redis 集群之间是如何复制的？

> 原文：[https://zwmst.com/5863.html](https://zwmst.com/5863.html)

异步复制


# 1277.Redis 集群最大节点个数是多少？

> 原文：[https://zwmst.com/5865.html](https://zwmst.com/5865.html)

16384 个。


# 1278.Redis 集群如何选择数据库？

> 原文：[https://zwmst.com/5867.html](https://zwmst.com/5867.html)

Redis 集群目前无法做数据库选择，默认在 0 数据库。


# 1279.怎么测试 Redis 的连通性？

> 原文：[https://zwmst.com/5869.html](https://zwmst.com/5869.html)

ping


# 1280.Redis 中的管道有什么用？

> 原文：[https://zwmst.com/5871.html](https://zwmst.com/5871.html)

一次请求/响应服务器能实现处理新的请求即使旧的请求还未被响应。这样就可以将多个命令发送到服务器，而不用等待回复，最后在一个步骤中读取该答复。
这就是管道（pipelining），是一种几十年来广泛使用的技术。例如许多 POP3 协议已经实现支持这个功能，大大加快了从服务器下载新邮件的过程。
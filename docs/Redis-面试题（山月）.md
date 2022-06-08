# redis

# 如何实现一个分布式锁

> 原文：[https://q.shanyue.tech/server/redis/21.html](https://q.shanyue.tech/server/redis/21.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 21(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/21)

Author

回答者: [zhangxiaokun(opens new window)](https://github.com/zhangxiaokun)

mysql,redis,zk redis 效率较高

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

多节点部署就会产生分布式问题，分布式锁由两个词组成，**分布式**和**锁**

1.  分布式: 解决分布式问题就要找一个大家都能够访问到的中介，比如 `Redis`，`Consul`，`Zookeeper`
2.  锁: 解决原子问题，当不存在时便加锁，**不存在** 和 **加锁** 要作为原子进行操作

以下是一个 `redis` 实现的操作

```
# EX 100：100s 的过期时间
# NX: 如果不存在 User:10086，设置成功返回 OK，否则返回 nil，也就是说 100s 之内只有第一次操作返回 OK
set User:10086 Random:shanyue EX 100 NX 
```

# redis 的持久化方案有哪些

> 原文：[https://q.shanyue.tech/server/redis/40.html](https://q.shanyue.tech/server/redis/40.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 40(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/40)

Author

回答者: [Carrie999(opens new window)](https://github.com/Carrie999)

rdb aof 主从复制+哨兵 rdb 是全量 aof 是增量

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

两种方案

*   RDB，备份数据本身。因此粒度不够细，数据完整性也不是能够很好的保证。但是简单粗暴，适合大量数据
*   AOF，备份命令本身。当恢复数据时，把所有写命令执行一遍即可恢复，粒度细，完整性好。正因为是命令，所以恢复速度慢

如果需要持久化时，两种方案全开。

PS：一般 redis 只用到缓存功能，无重要数据，如不涉及消息队列，则持久化可以关掉

# redis 中 zset 是什么，用作什么应用场景

> 原文：[https://q.shanyue.tech/server/redis/151.html](https://q.shanyue.tech/server/redis/151.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 151(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/151)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

`SortedSet`，有序集合，一般可以有两种用途

1.  排行榜，TOP N 之类
2.  优先级消息队列

# 在 redis 中如何查看版本号

> 原文：[https://q.shanyue.tech/server/redis/289.html](https://q.shanyue.tech/server/redis/289.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 289(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/289)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

```
$ redis-server -v
Redis server v=5.0.7 sha=00000000:0 malloc=jemalloc-5.1.0 bits=64 build=fbc6fab733127977 
```

# 如何发现 redis 中的 bigkey

> 原文：[https://q.shanyue.tech/server/redis/329.html](https://q.shanyue.tech/server/redis/329.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 329(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/329)

# 如何保存数据库与缓存的双写一致性

> 原文：[https://q.shanyue.tech/server/redis/371.html](https://q.shanyue.tech/server/redis/371.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 371(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/371)

# redis 是如何删掉过期数据的

> 原文：[https://q.shanyue.tech/server/redis/377.html](https://q.shanyue.tech/server/redis/377.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 377(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/377)

Author

回答者: [shay-an(opens new window)](https://github.com/shay-an)

懒删除：查询时删除 定时删除：通过定时任务删除

# 什么是缓存穿透，如何解决

> 原文：[https://q.shanyue.tech/server/redis/390.html](https://q.shanyue.tech/server/redis/390.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 390(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/390)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

**当访问数据库中不存在的数据时，此时由于不恰当的缓存策略，每次查询都会穿透缓存打在数据库上，这样在高并发下可能造成缓存穿透**，此时的解决方案：

1.  当应用访问缓存不存在时，应用继续去访问数据库，即便数据库中不存在数据，此时应用再在缓存中把该值设为空，过期时间以短时间为主
2.  使用过滤器做进一步的过滤，如 redis 中的 bitmap 或 set，当不存在该值时，直接返回

Author

回答者: [manondidi(opens new window)](https://github.com/manondidi)

缓存穿透是指 在 redis 缓存中 不存在, 同时数据库也不存在的情况, 一旦被黑客利用了, 通过频繁请求 击垮数据库 做法是加 redis 和 mysql 之间加过滤器 在应用启动的时候 用布隆过滤器 将数据库中的值(如 id)加载起来放在布隆过滤器中 布隆过滤器 有一定的误差 能判断出这个数据 一定在数据库中, 不能 判断这个数据一定不在数据库中, 他比 set 好处是 节约更多内存 以为他不是将数据完整的存下, 而是通过多次 hash 标志某个位为 1,有更高的效率

# 在你们的后端应用中，redis 用在哪些场景

> 原文：[https://q.shanyue.tech/server/redis/413.html](https://q.shanyue.tech/server/redis/413.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 413(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/413)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

1.  缓存
2.  限流
3.  队列
4.  分布式锁
5.  并发数控制
6.  bitmap

# 如何使用 redis 计算 wordcount，并计算出现频率最高的词

> 原文：[https://q.shanyue.tech/server/redis/491.html](https://q.shanyue.tech/server/redis/491.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 491(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/491)

# redis 中的哨兵与集群模式各是什么

> 原文：[https://q.shanyue.tech/server/redis/659.html](https://q.shanyue.tech/server/redis/659.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 659(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/659)
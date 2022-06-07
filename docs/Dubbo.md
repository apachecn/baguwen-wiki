<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo是什么？

> 原文：[https://zwmst.com/1141.html](https://zwmst.com/1141.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:35:20+08:00"> 2021-08-15 </time> ](https://zwmst.com/1141.html)  Dubbo是阿里巴巴开源的基于 Java 的高性能 RPC 分布式服务框架，现已成为 Apache 基金会 孵化项目。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 为什么要用Dubbo？

> 原文：[https://zwmst.com/1143.html](https://zwmst.com/1143.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:35:31+08:00"> 2021-08-15 </time> ](https://zwmst.com/1143.html)  因为是阿里开源项目，国内很多互联网公司都在用，已经经过很多线上考验。内部使用了 Netty、Zookeeper，保证了高性能高可用性。

使用 Dubbo 可以将核心业务抽取出来，作为独立的服务，逐渐形成稳定的服务中心，可用于 提高业务复用灵活扩展，使前端应用能更快速的响应多变的市场需求。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo 和 Dubbox 有什么区别？

> 原文：[https://zwmst.com/1145.html](https://zwmst.com/1145.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:35:43+08:00"> 2021-08-15 </time> ](https://zwmst.com/1145.html)  Dubbox 是继 Dubbo 停止维护后，当当网基于 Dubbo 做的一个扩展项目，如加了服务可 Restful 调用，更新了开源组件等。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# dubbo都支持什么协议，推荐用哪种？

> 原文：[https://zwmst.com/1147.html](https://zwmst.com/1147.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:35:56+08:00"> 2021-08-15 </time> ](https://zwmst.com/1147.html)  dubbo://（推荐）

rmi://

hessian://

http://

webservice://

thrift://

memcached://

redis://

rest://*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo需要 Web 容器吗？

> 原文：[https://zwmst.com/1149.html](https://zwmst.com/1149.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:36:07+08:00"> 2021-08-15 </time> ](https://zwmst.com/1149.html)  不需要，如果硬要用 Web 容器，只会增加复杂性，也浪费资源。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo内置了哪几种服务容器？

> 原文：[https://zwmst.com/1151.html](https://zwmst.com/1151.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:36:19+08:00"> 2021-08-15 </time> ](https://zwmst.com/1151.html)  Spring Container

Jetty Container

Log4j Container*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo默认使用什么注册中心，还有别的选择吗？

> 原文：[https://zwmst.com/1153.html](https://zwmst.com/1153.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:36:33+08:00"> 2021-08-15 </time> ](https://zwmst.com/1153.html)  推荐使用 Zookeeper 作为注册中心，还有 Redis、Multicast、Simple 注册中心，但不推 荐。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo有哪几种配置方式？

> 原文：[https://zwmst.com/1155.html](https://zwmst.com/1155.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:37:09+08:00"> 2021-08-15 </time> ](https://zwmst.com/1155.html)  1）Spring 配置方式

2）Java API 配置方式*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 在 Provider 上可以配置的 Consumer 端的属性有哪些？

> 原文：[https://zwmst.com/1157.html](https://zwmst.com/1157.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:37:54+08:00"> 2021-08-15 </time> ](https://zwmst.com/1157.html)  1）timeout：方法调用超时

2）retries：失败重试次数，默认重试 2 次

3）loadbalance：负载均衡算法，默认随机

4）actives 消费者端，最大并发调用限制*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo启动时如果依赖的服务不可用会怎样？

> 原文：[https://zwmst.com/1159.html](https://zwmst.com/1159.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:38:08+08:00"> 2021-08-15 </time> ](https://zwmst.com/1159.html)  Dubbo 缺省会在启动时检查依赖的服务是否可用，不可用时会抛出异常，阻止 Spring 初始化 完成，默认 check="true"，可以通过 check="false" 关闭检查。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo推荐使用什么序列化框架，你知道的还有哪些？

> 原文：[https://zwmst.com/1161.html](https://zwmst.com/1161.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:38:24+08:00"> 2021-08-15 </time> ](https://zwmst.com/1161.html)  推荐使用Hessian序列化，还有Duddo、FastJson、Java自带序列化。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo默认使用的是什么通信框架，还有别的选择吗？

> 原文：[https://zwmst.com/1163.html](https://zwmst.com/1163.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:38:35+08:00"> 2021-08-15 </time> ](https://zwmst.com/1163.html)  Dubbo 默认使用 Netty 框架，也是推荐的选择，另外内容还集成有Mina、Grizzly。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 注册了多个同一样的服务，如果测试指定的某一个服务呢？

> 原文：[https://zwmst.com/1165.html](https://zwmst.com/1165.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:38:58+08:00"> 2021-08-15 </time> ](https://zwmst.com/1165.html)  可以配置环境点对点直连，绕过注册中心，将以服务接口为单位，忽略注册中心的提供者列 表。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo支持服务多协议吗？

> 原文：[https://zwmst.com/1167.html](https://zwmst.com/1167.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:39:10+08:00"> 2021-08-15 </time> ](https://zwmst.com/1167.html)  Dubbo 允许配置多协议，在不同服务上支持不同协议或者同一服务上同时支持多种协议。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 当一个服务接口有多种实现时怎么做？

> 原文：[https://zwmst.com/1169.html](https://zwmst.com/1169.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:39:22+08:00"> 2021-08-15 </time> ](https://zwmst.com/1169.html)  当一个接口有多种实现时，可以用 group 属性来分组，服务提供方和消费方都指定同一个 group 即可。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 服务上线怎么兼容旧版本？

> 原文：[https://zwmst.com/1171.html](https://zwmst.com/1171.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:39:33+08:00"> 2021-08-15 </time> ](https://zwmst.com/1171.html)  可以用版本号（version）过渡，多个不同版本的服务注册到注册中心，版本号不同的服务相 互间不引用。这个和服务分组的概念有一点类似。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo可以对结果进行缓存吗？

> 原文：[https://zwmst.com/1173.html](https://zwmst.com/1173.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:39:47+08:00"> 2021-08-15 </time> ](https://zwmst.com/1173.html)  可以，Dubbo 提供了声明式缓存，用于加速热门数据的访问速度，以减少用户加缓存的工作 量。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo服务之间的调用是阻塞的吗？

> 原文：[https://zwmst.com/1175.html](https://zwmst.com/1175.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:39:58+08:00"> 2021-08-15 </time> ](https://zwmst.com/1175.html)  默认是同步等待结果阻塞的，支持异步调用。

Dubbo 是基于 NIO 的非阻塞实现并行调用，客户端不需要启动多线程即可完成并行调用多个 远程服务，相对多线程开销较小，异步调用会返回一个 Future 对象。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo支持分布式事务吗？

> 原文：[https://zwmst.com/1177.html](https://zwmst.com/1177.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:40:12+08:00"> 2021-08-15 </time> ](https://zwmst.com/1177.html)  目前暂时不支持，后续可能采用基于 JTA/XA 规范实现。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo支持服务降级吗？

> 原文：[https://zwmst.com/1179.html](https://zwmst.com/1179.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:40:23+08:00"> 2021-08-15 </time> ](https://zwmst.com/1179.html)  Dubbo 2.2.0 以上版本支持。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo如何优雅停机？

> 原文：[https://zwmst.com/1181.html](https://zwmst.com/1181.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:40:36+08:00"> 2021-08-15 </time> ](https://zwmst.com/1181.html)  Dubbo 是通过 JDK 的 ShutdownHook 来完成优雅停机的，所以如果使用 kill -9 PID 等强制 关闭指令，是不会执行优雅停机的，只有通过 kill PID 时，才会执行。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 服务提供者能实现失效踢出是什么原理？

> 原文：[https://zwmst.com/1183.html](https://zwmst.com/1183.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:40:49+08:00"> 2021-08-15 </time> ](https://zwmst.com/1183.html)  服务失效踢出基于 Zookeeper 的临时节点原理。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 如何解决服务调用链过长的问题？

> 原文：[https://zwmst.com/1185.html](https://zwmst.com/1185.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:41:01+08:00"> 2021-08-15 </time> ](https://zwmst.com/1185.html)  Dubbo 可以使用 Pinpoint 和 Apache Skywalking(Incubator) 实现分布式服务追踪，当然 还有其他很多方案。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 服务读写推荐的容错策略是怎样的？

> 原文：[https://zwmst.com/1187.html](https://zwmst.com/1187.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:41:13+08:00"> 2021-08-15 </time> ](https://zwmst.com/1187.html)  读操作建议使用 Failover 失败自动切换，默认重试两次其他服务器。

写操作建议使用 Failfast 快速失败，发一次调用失败就立即报错。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo必须依赖的包有哪些？

> 原文：[https://zwmst.com/1189.html](https://zwmst.com/1189.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:41:24+08:00"> 2021-08-15 </time> ](https://zwmst.com/1189.html)  Dubbo 必须依赖 JDK，其他为可选。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Dubbo的管理控制台能做什么？

> 原文：[https://zwmst.com/1191.html](https://zwmst.com/1191.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:41:35+08:00"> 2021-08-15 </time> ](https://zwmst.com/1191.html)  管理控制台主要包含：路由规则，动态配置，服务降级，访问控制，权重调整，负载均衡，等 管理功能。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 说说 Dubbo 服务暴露的过程。

> 原文：[https://zwmst.com/1193.html](https://zwmst.com/1193.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-08-15T10:41:45+08:00"> 2021-08-15 </time> ](https://zwmst.com/1193.html)  Dubbo 会在 Spring 实例化完 bean 之后，在刷新容器最后一步发布ContextRefreshEvent 事件的时候，通知实现了 ApplicationListener 的 ServiceBean 类进行回调 onApplicationEvent 事件方法，Dubbo 会在这个方法中调用 ServiceBean 父类 ServiceConfig 的 export 方法，而该方法真正实现了服务的（异步或者非异步）发布。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 923.Dubbo 支持哪些协议，每种协议的应用场景，优缺点？

> 原文：[https://zwmst.com/5119.html](https://zwmst.com/5119.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)* [ *设计模式* ](https://zwmst.com/%e8%ae%be%e8%ae%a1%e6%a8%a1%e5%bc%8f)***[ <time datetime="2021-10-19T00:42:12+08:00"> 2021-10-18 </time> ](https://zwmst.com/5119.html)  1.  dubbo： 单一长连接和 NIO 异步通讯，适合大并发小数据量的服务调用，以及消费者远大于提供者。传输协议 TCP，异步，Hessian 序列化；
2.  rmi： 采用 JDK 标准的 rmi 协议实现，传输参数和返回参数对象需要实现Serializable 接口，使用 java 标准序列化机制，使用阻塞式短连接，传输数据包大小混合，消费者和提供者个数差不多，可传文件，传输协议 TCP。多个短连接，TCP 协议传输，同步传输，适用常规的远程服务调用和 rmi 互操作。在依赖低版本的 Common-Collections 包，java 序列化存在安全漏洞；
3.  webservice： 基于 WebService 的远程调用协议，集成 CXF 实现，提供和原生 WebService 的互操作。多个短连接，基于 HTTP 传输，同步传输，适用系统集成和跨语言调用；
4.  http： 基于 Http 表单提交的远程调用协议，使用 Spring 的 HttpInvoke 实现。多个短连接，传输协议 HTTP，传入参数大小混合，提供者个数多于消费者，需要给应用程序和浏览器 JS 调用；
5.  hessian： 集成 Hessian 服务，基于 HTTP 通讯，采用 Servlet 暴露服务，Dubbo 内嵌 Jetty 作为服务器时默认实现，提供与 Hession 服务互操作。多个短连接，同步 HTTP 传输，Hessian 序列化，传入参数较大，提供者大于消费者，提供者压力较大，可传文件；
6.  memcache： 基于 memcached 实现的 RPC 协议
7.  redis： 基于 redis 实现的 RPC 协议**
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 924.Dubbo 超时时间怎样设置？

> 原文：[https://zwmst.com/5121.html](https://zwmst.com/5121.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T00:50:14+08:00"> 2021-10-18 </time> ](https://zwmst.com/5121.html)  ## Dubbo 超时时间设置有两种方式：

1.  服务提供者端设置超时时间，在 Dubbo 的用户文档中，推荐如果能在服务端多配置就尽量多配置，因为服务提供者比消费者更清楚自己提供的服务特性。
2.  服务消费者端设置超时时间，如果在消费者端设置了超时时间，以消费者端为主，即优先级更高。因为服务调用方设置超时时间控制性更灵活。如果消费方超时，服务端线程不会定制，会产生警告。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 925.Dubbo 有些哪些注册中心？

> 原文：[https://zwmst.com/5123.html](https://zwmst.com/5123.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T00:52:46+08:00"> 2021-10-18 </time> ](https://zwmst.com/5123.html)  1.  Multicast 注册中心： Multicast 注册中心不需要任何中心节点，只要广播地址，就能进行服务注册和发现。基于网络中组播传输实现；
2.  Zookeeper 注册中心： 基于分布式协调系统 Zookeeper 实现，采用Zookeeper 的 watch 机制实现数据变更；
3.  redis 注册中心： 基于 redis 实现，采用 key/Map 存储，住 key 存储服务名和类型，Map 中 key 存储服务 URL，value 服务过期时间。基于 redis 的发布/订阅模式通知数据变更；
4.  Simple 注册中心*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 927.Dubbo 是什么？

> 原文：[https://zwmst.com/5127.html](https://zwmst.com/5127.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T00:55:39+08:00"> 2021-10-18 </time> ](https://zwmst.com/5127.html)  Dubbo 是一个分布式、高性能、透明化的 RPC 服务框架，提供服务自动注册、自动发现等高效服务治理方案， 可以和Spring 框架无缝集成。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 928.Dubbo 的主要应用场景？

> 原文：[https://zwmst.com/5129.html](https://zwmst.com/5129.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T00:56:33+08:00"> 2021-10-18 </time> ](https://zwmst.com/5129.html)  透明化的远程方法调用，就像调用本地方法一样调用远程方法，只需简单配置，没有任何 API 侵入。

1.  软负载均衡及容错机制，可在内网替代 F5 等硬件负载均衡器，降低成本，减少单点。
2.  服务自动注册与发现，不再需要写死服务提供方地址，注册中心基于接口名查询服务提供者的 IP 地址，并且能够平滑添加或删除服务提供者。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 929.Dubbo 的核心功能

> 原文：[https://zwmst.com/5131.html](https://zwmst.com/5131.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T00:57:31+08:00"> 2021-10-18 </time> ](https://zwmst.com/5131.html)  主要就是如下 3 个核心功能：

1.  Remoting：网络通信框架，提供对多种 NIO 框架抽象封装，包括“同步转异步”和“请求-响应”模式的信息交换方式。
2.  Cluster：服务框架，提供基于接口方法的透明远程过程调用，包括多协议支持，以及软负载均衡，失败容错，地址路由，动态配置等集群支持。
3.  Registry：服务注册，基于注册中心目录服务，使服务消费方能动态的查找服务提供方，使地址透明，使服务提供方可以平滑增加或减少机器。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 930.Dubbo 的核心组件？

> 原文：[https://zwmst.com/5133.html](https://zwmst.com/5133.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T00:58:21+08:00"> 2021-10-18 </time> ](https://zwmst.com/5133.html)  ![](img/7e1397f23112b4ff11443515b2534b88.png)*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 931.Dubbo 服务注册与发现的流程？

> 原文：[https://zwmst.com/5136.html](https://zwmst.com/5136.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:01:08+08:00"> 2021-10-18 </time> ](https://zwmst.com/5136.html)  ![](img/e80fb316573f142d0c2a5f4d1f17516b.png)

## 流程说明：

1.  Provider(提供者)绑定指定端口并启动服务
2.  指供者连接注册中心，并发本机 IP、端口、应用信息和提供服务信息发送至注册中心存储
3.  Consumer(消费者），连接注册中心 ，并发送应用信息、所求服务信息至注册中心
4.  注册中心根据 消费 者所求服务信息匹配对应的提供者列表发送至Consumer 应用缓存。
5.  Consumer 在发起远程调用时基于缓存的消费者列表择其一发起调用。
6.  Provider 状态变更会实时通知注册中心、在由注册中心实时推送至Consumer

    ## 设计的原因：

7.  Consumer 与 Provider 解偶，双方都可以横向增减节点数。
8.  注册中心对本身可做对等集群，可动态增减节点，并且任意一台宕掉后，将自动切换到另一台
9.  去中心化，双方不直接依懒注册中心，即使注册中心全部宕机短时间内也不会影响服务的调用
10.  服务提供者无状态，任意一台宕掉后，不影响使用*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 932.Dubbo 的架构设计？

> 原文：[https://zwmst.com/5139.html](https://zwmst.com/5139.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:03:04+08:00"> 2021-10-18 </time> ](https://zwmst.com/5139.html)  ![](img/79130e114c62f682c4d868e9b419f5c4.png)

## Dubbo 框架设计一共划分了 10 个层：

1.  服务接口层（Service）：该层是与实际业务逻辑相关的，根据服务提供方和服务消费方的业务设计对应的接口和实现。
2.  配置层（Config）：对外配置接口，以 ServiceConfig 和ReferenceConfig 为中心。
3.  服务代理层（Proxy）：服务接口透明代理，生成服务的客户端 Stub和服务器端 Skeleton。
4.  服务注册层（Registry）：封装服务地址的注册与发现，以服务 URL为中心。
5.  集群层（Cluster）：封装多个提供者的路由及负载均衡，并桥接注册中心，以 Invoker 为中心。
6.  监控层（Monitor）：RPC 调用次数和调用时间监控。
7.  远程调用层（Protocol）：封将 RPC 调用，以 Invocation 和 Result为中心，扩展接口为 Protocol、Invoker 和 Exporter。
8.  信息交换层（Exchange）：封装请求响应模式，同步转异步，以Request 和 Response 为中心。
9.  网络传输层（Transport）：抽象 mina 和 netty 为统一接口，以Message 为中心。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 933.Dubbo 的服务调用流程？

> 原文：[https://zwmst.com/5142.html](https://zwmst.com/5142.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:04:02+08:00"> 2021-10-18 </time> ](https://zwmst.com/5142.html)  ![](img/fb9f3cf26600d6bc6cc2eef766125e08.png)*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 934.Dubbo 支持哪些协议，每种协议的应用场景，优缺点？

> 原文：[https://zwmst.com/5145.html](https://zwmst.com/5145.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:06:31+08:00"> 2021-10-18 </time> ](https://zwmst.com/5145.html)  1.  dubbo： 单一长连接和 NIO 异步通讯，适合大并发小数据量的服务调用，以及消费者远大于提供者。传输协议 TCP，异步，Hessian 序列化；
2.  rmi： 采用 JDK 标准的 rmi 协议实现，传输参数和返回参数对象需要实现 Serializable 接口，使用 java 标准序列化机制，使用阻塞式短连接，传输数据包大小混合，消费者和提供者个数差不多，可传文件，传输协议 TCP。 多个短连接，TCP 协议传输，同步传输，适用常规的远程服务调用和 rmi 互操作。在依赖低版本的 Common-Collections包，java 序列化存在安全漏洞；
3.  webservice： 基于 WebService 的远程调用协议，集成 CXF 实现，提供和原生 WebService 的互操作。多个短连接，基于 HTTP 传输，同步传输，适用系统集成和跨语言调用；
4.  http： 基于 Http 表单提交的远程调用协议，使用 Spring 的HttpInvoke 实现。多个短连接，传输协议 HTTP，传入参数大小混合，提供者个数多于消费者，需要给应用程序和浏览器 JS 调用；
5.  hessian： 集成 Hessian 服务，基于 HTTP 通讯，采用 Servlet 暴露服务，Dubbo 内嵌 Jetty 作为服务器时默认实现，提供与 Hession 服务互操作。多个短连接，同步 HTTP 传输，Hessian 序列化，传入参数较大，提供者大于消费者，提供者压力较大，可传文件；
6.  memcache： 基于 memcached 实现的 RPC 协议
7.  redis： 基于 redis 实现的 RPC 协议*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 935.dubbo 推荐用什么协议？

> 原文：[https://zwmst.com/5147.html](https://zwmst.com/5147.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:07:17+08:00"> 2021-10-18 </time> ](https://zwmst.com/5147.html)  默认使用 dubbo 协议*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 936.Dubbo 有些哪些注册中心？

> 原文：[https://zwmst.com/5149.html](https://zwmst.com/5149.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:08:20+08:00"> 2021-10-18 </time> ](https://zwmst.com/5149.html)  1.  Multicast 注册中心： Multicast 注册中心不需要任何中心节点，只要广播地址，就能进行服务注册和发现。基于网络中组播传输实现；
2.  Zookeeper 注册中心： 基于分布式协调系统 Zookeeper 实现，采用Zookeeper 的 watch 机制实现数据变更；
3.  redis 注册中心： 基于 redis 实现，采用 key/Map 存储，住 key 存储服务名和类型，Map 中 key 存储服务 URL，value 服务过期时间。基于 redis 的发布/订阅模式通知数据变更；
4.  Simple 注册中心*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 937.Dubbo 默认采用注册中心？

> 原文：[https://zwmst.com/5151.html](https://zwmst.com/5151.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:08:53+08:00"> 2021-10-18 </time> ](https://zwmst.com/5151.html)  采用 Zookeeper*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 938.为什么需要服务治理？

> 原文：[https://zwmst.com/5153.html](https://zwmst.com/5153.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:09:46+08:00"> 2021-10-18 </time> ](https://zwmst.com/5153.html)  1.  过多的服务 URL 配置困难
2.  负载均衡分配节点压力过大的情况下也需要部署集群
3.  服务依赖混乱，启动顺序不清晰
4.  过多服务导致性能指标分析难度较大，需要监控*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 939.Dubbo 的注册中心集群挂掉，发布者和订阅者之间还能通信么？

> 原文：[https://zwmst.com/5155.html](https://zwmst.com/5155.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:10:25+08:00"> 2021-10-18 </time> ](https://zwmst.com/5155.html)  可以的，启动 dubbo 时，消费者会从 zookeeper 拉取注册的生产者的地址接口等数据，缓存在本地。
每次调用时，按照本地存储的地址进行调用。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 940.Dubbo 与 Spring 的关系？

> 原文：[https://zwmst.com/5157.html](https://zwmst.com/5157.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:11:05+08:00"> 2021-10-18 </time> ](https://zwmst.com/5157.html)  Dubbo 采用全 Spring 配置方式，透明化接入应用，对应用没有任何API 侵入，只需用 Spring 加载 Dubbo 的配置即可，Dubbo 基于Spring 的 Schema 扩展进行加载。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 941.Dubbo 使用的是什么通信框架?

> 原文：[https://zwmst.com/5159.html](https://zwmst.com/5159.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:11:44+08:00"> 2021-10-18 </time> ](https://zwmst.com/5159.html)  默认使用 NIO Netty 框架*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 942.Dubbo 集群提供了哪些负载均衡策略？

> 原文：[https://zwmst.com/5161.html](https://zwmst.com/5161.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:17:32+08:00"> 2021-10-18 </time> ](https://zwmst.com/5161.html)  Random LoadBalance: 随机选取提供者策略，有利于动态调整提供者权重。截面碰撞率高，调用次数越多，分布越均匀；

1.  RoundRobin LoadBalance: 轮循选取提供者策略，平均分布，但是存在请求累积的问题；
2.  LeastActive LoadBalance: 最少活跃调用策略，解决慢提供者接收更少的请求；
3.  ConstantHash LoadBalance: 一致性 Hash 策略，使相同参数请求总是发到同一提供者，一台机器宕机，可以基于虚拟节点，分摊至其他提供者，避免引起提供者的剧烈变动；缺省时为 Random 随机调用*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 943.Dubbo 的集群容错方案有哪些？

> 原文：[https://zwmst.com/5163.html](https://zwmst.com/5163.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:19:17+08:00"> 2021-10-18 </time> ](https://zwmst.com/5163.html)  ## Failover Cluster

1.  失败自动切换，当出现失败，重试其它服务器。通常用于读操作，但重试会带来更长延迟。

## Failfast Cluster

2.  快速失败，只发起一次调用，失败立即报错。通常用于非幂等性的写操作，比如新增记录。

## Failsafe Cluster

3.  失败安全，出现异常时，直接忽略。通常用于写入审计日志等操作。

## Failback Cluster

4.  失败自动恢复，后台记录失败请求，定时重发。通常用于消息通知操作。

## Forking Cluster

5.  并行调用多个服务器，只要一个成功即返回。通常用于实时性要求较高的读操作，但需要浪费更多服务资源。可通过 forks="2" 来设置最大并行数。

## Broadcast Cluster

6.  广播调用所有提供者，逐个调用，任意一台报错则报错 。通常用于通知所有提供者更新缓存或日志等本地资源信息。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 944.Dubbo 的默认集群容错方案？

> 原文：[https://zwmst.com/5165.html](https://zwmst.com/5165.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:20:23+08:00"> 2021-10-18 </time> ](https://zwmst.com/5165.html)  Failover Cluster*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 945.Dubbo 支持哪些序列化方式？

> 原文：[https://zwmst.com/5167.html](https://zwmst.com/5167.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:20:58+08:00"> 2021-10-18 </time> ](https://zwmst.com/5167.html)  默认使用 Hessian 序列化，还有 Duddo、FastJson、Java 自带序列化。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 946.Dubbo 超时时间怎样设置？

> 原文：[https://zwmst.com/5169.html](https://zwmst.com/5169.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:21:53+08:00"> 2021-10-18 </time> ](https://zwmst.com/5169.html)  Dubbo 超时时间设置有两种方式：

1.  服务提供者端设置超时时间，在 Dubbo 的用户文档中，推荐如果能在服务端多配置就尽量多配置，因为服务提供者比消费者更清楚自己提供的服务特性。
2.  服务消费者端设置超时时间，如果在消费者端设置了超时时间，以消费者端为主，即优先级更高。因为服务调用方设置超时时间控制性更灵活。如果消费方超时，服务端线程不会定制，会产生警告。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 947.服务调用超时问题怎么解决？

> 原文：[https://zwmst.com/5171.html](https://zwmst.com/5171.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:22:50+08:00"> 2021-10-18 </time> ](https://zwmst.com/5171.html)  dubbo 在调用服务不成功时，默认是会重试两次的。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 948.Dubbo 在安全机制方面是如何解决？

> 原文：[https://zwmst.com/5173.html](https://zwmst.com/5173.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:23:40+08:00"> 2021-10-18 </time> ](https://zwmst.com/5173.html)  Dubbo 通过 Token 令牌防止用户绕过注册中心直连，然后在注册中心上管理授权。Dubbo 还提供服务黑白名单，来控制服务所允许的调用方。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 949.Dubbo 和 Dubbox 之间的区别？

> 原文：[https://zwmst.com/5175.html](https://zwmst.com/5175.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:24:20+08:00"> 2021-10-18 </time> ](https://zwmst.com/5175.html)  dubbox 基于 dubbo 上做了一些扩展，如加了服务可 restful 调用，更新了开源组件等。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 950.Dubbo 和 Spring Cloud 的关系？

> 原文：[https://zwmst.com/5177.html](https://zwmst.com/5177.html)

   [ *Dubbo* ](https://zwmst.com/dubbo)*[ <time datetime="2021-10-19T01:25:05+08:00"> 2021-10-18 </time> ](https://zwmst.com/5177.html)  Dubbo 是 SOA 时代的产物，它的关注点主要在于服务的调用，流量分发、流量监控和熔断。而 Spring Cloud 诞生于微服务架构时代，考虑的是微服务治理的方方面面，另外由于依托了 Spirng、Spirng Boot 的优势之上，两个框架在开始目标就不一致，Dubbo定位服务治理、Spirng Cloud 是一个生态。*
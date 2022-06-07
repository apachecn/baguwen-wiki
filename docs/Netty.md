<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是Reactor模型？Reactor的3种版本都知道吗？

> 原文：[https://zwmst.com/738.html](https://zwmst.com/738.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-08-14T08:01:47+08:00"> 2021-08-14 </time> ](https://zwmst.com/738.html)  Reactor模式究竟是个什么东西呢？这要从事件驱动的开发方式说起。我们知道，对于应用服 务器，一个主要规律就是，CPU的处理速度是要远远快于IO速度的，如果CPU为了IO操作（例 如从Socket读取一段数据）而阻塞显然是不划算的。好一点的方法是分为多进程或者线程去进 行处理，但是这样会带来一些进程切换的开销，试想一个进程一个数据读了500ms，期间进程 切换到它3次，但是CPU却什么都不能干，就这么切换走了，是不是也不划算？

这时先驱们找到了事件驱动，或者叫回调的方式，来完成这件事情。这种方式就是，应用业务 向一个中间人注册一个回调（event handler），当IO就绪后，就这个中间人产生一个事件， 并通知此handler进行处理。这种回调的方式，也体现了“好莱坞原则”（Hollywood principle）-“Don’t call us, we’ll call you”，在我们熟悉的IoC中也有用到。看来软件开发 真是互通的！

好了，我们现在来看Reactor模式。在前面事件驱动的例子里有个问题：我们如何知道IO就绪 这个事件，谁来充当这个中间人？Reactor模式的答案是：由一个不断等待和循环的单独进程 （线程）来做这件事，它接受所有handler的注册，并负责先操作系统查询IO是否就绪，在就 绪后就调用指定handler进行处理，这个角色的名字就叫做Reactor。

Reactor的3种版本：单线程模式、多线程模式、主从多线程模式*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 了解过粘包拆包吗？为什么会出现粘包拆包？怎么处理粘包拆包？

> 原文：[https://zwmst.com/740.html](https://zwmst.com/740.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-08-14T08:01:59+08:00"> 2021-08-14 </time> ](https://zwmst.com/740.html)  粘包的主要原因：发送方写入数据套接字缓冲区大小；发送方发送的数据大于协议的 MTU（最大传输单元），不得已必须拆包。

如何处理：1、消息长度固定；2、消息之间用分隔符分隔；3、在消息头保留一个字段，用于 描述消息的长度。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# UDP协议会有粘包拆包的问题吗？为什么？

> 原文：[https://zwmst.com/742.html](https://zwmst.com/742.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-08-14T08:02:11+08:00"> 2021-08-14 </time> ](https://zwmst.com/742.html)  UDP不会有这个问题。

因为TCP是“数据流”协议，UDP是“数据报”协议。

UDP协议的数据包之间是没有联系，而且有明确边界的。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Netty 是什么？

> 原文：[https://zwmst.com/744.html](https://zwmst.com/744.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-08-14T08:02:23+08:00"> 2021-08-14 </time> ](https://zwmst.com/744.html)  Netty 是一个 基于 NIO 的 client-server(客户端服务器)框架，使用它可以快速简单地开发网 络应用程序。

它极大地简化并优化了 TCP 和 UDP 套接字服务器等网络编程,并且性能以及安全性等很多方面 甚至都要更好。

支持多种协议 如 FTP，SMTP，HTTP 以及各种二进制和基于文本的传统协议。 用官方的总结就是：Netty 成功地找到了一种在不妥协可维护性和性能的情况下实现易于开 发，性能，稳定性和灵活性的方法。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 为什么要用 Netty？

> 原文：[https://zwmst.com/746.html](https://zwmst.com/746.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-08-14T08:02:33+08:00"> 2021-08-14 </time> ](https://zwmst.com/746.html)  统一的 API，支持多种传输类型，阻塞和非阻塞的。

简单而强大的线程模型。

自带编解码器解决 TCP 粘包/拆包问题。

自带各种协议栈。

真正的无连接数据包套接字支持。

比直接使用 Java 核心 API 有更高的吞吐量、更低的延迟、更低的资源消耗和更少的内存复 制。

安全性不错，有完整的 SSL/TLS 以及 StartTLS 支持。

社区活跃 成熟稳定，经历了大型项目的使用和考验，而且很多开源项目都使用到了 Netty， 比如我们经 常接触的 Dubbo、RocketMQ 等等。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Netty 的应用场景了解么？

> 原文：[https://zwmst.com/748.html](https://zwmst.com/748.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-08-14T08:02:44+08:00"> 2021-08-14 </time> ](https://zwmst.com/748.html)  Netty 主要用来做网络通信 :

作为 RPC 框架的网络通信工具 ：我们在分布式系统中，不同服务节点之间经常需要相互调 用，这个时候就需要 RPC 框架了。不同服务节点之间的通信是如何做的呢？可以使用 Netty 来做。比如我调用另外一个节点的方法的话，至少是要让对方知道我调用的是哪个类中的哪个方法以及相关参数吧！

实现一个自己的 HTTP 服务器 ：通过 Netty 我们可以自己实现一个简单的 HTTP 服务器，这 个大家应该不陌生。说到 HTTP 服务器的话，作为 Java 后端开发，我们一般使用 Tomcat 比 较多。一个最基本的 HTTP 服务器可要以处理常见的 HTTP Method 的请求，比如 POST 请 求、GET 请求等等。

实现一个即时通讯系统 ：使用 Netty 我们可以实现一个可以聊天类似微信的即时通讯系统，这 方面的开源项目还蛮多的，可以自行去 Github 找一找。 实现消息推送系统 ：市面上有很多消息推送系统都是基于 Netty 来做的。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Netty 的零拷贝了解么？

> 原文：[https://zwmst.com/750.html](https://zwmst.com/750.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-08-14T08:02:57+08:00"> 2021-08-14 </time> ](https://zwmst.com/750.html)  维基百科是这样介绍零拷贝的：“零复制（英语：Zero-copy；也译零拷贝）技术是指计算机 执行操作时，CPU 不需要先将数据从某处内存复制到另一个特定区域。这种技术通常用于通过 网络传输文件时节省 CPU 周期和内存带宽。

在 OS 层面上的 Zero-copy 通常指避免在 用户态(User-space) 与 内核态(Kernel-space) 之 间来回拷贝数据。而在 Netty 层面 ，零拷贝主要体现在对于数据操作的优化。

Netty 中的零拷贝体现在以下几个方面： 使用 Netty 提供的 CompositeByteBuf 类, 可以将多个ByteBuf 合并为一个逻辑上的 ByteBuf, 避免了各个 ByteBuf 之间的拷贝。

ByteBuf 支持 slice 操作, 因此可以将 ByteBuf 分解为多个共享同一个存储区域的 ByteBuf, 避免了内存的拷贝。

通过 FileRegion 包装的FileChannel.tranferTo 实现文件传输, 可以直接将文件缓冲区的数据 发送到目标 Channel, 避免了传统通过循环 write 方式导致的内存拷贝问题。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Netty 的心跳机制了解么？

> 原文：[https://zwmst.com/752.html](https://zwmst.com/752.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-08-14T08:03:07+08:00"> 2021-08-14 </time> ](https://zwmst.com/752.html)  在 TCP 保持长连接的过程中，可能会出现断网等网络异常出现，异常发生的时候， client 与 server 之间如果没有交互的话，它们是无法发现对方已经掉线的。为了解决这个问题, 我们就 需要引入 心跳机制。

心跳机制的工作原理是: 在 client 与 server 之间在一定时间内没有数据交互时, 即处于 idle 状 态时, 客户端或服务器就会发送一个特殊的数据包给对方, 当接收方收到这个数据报文后, 也立 即发送一个特殊的数据报文, 回应发送方, 此即一个 PING-PONG 交互。所以, 当某一端收到心 跳消息后, 就知道了对方仍然在线, 这就确保 TCP 连接的有效性.

TCP 实际上自带的就有长连接选项，本身是也有心跳包机制，也就是 TCP 的选项： SO_KEEPALIVE。但是，TCP 协议层面的长连接灵活性不够。所以，一般情况下我们都是在 应用层协议上实现自定义心跳机制的，也就是在 Netty 层面通过编码实现。通过 Netty 实现心 跳机制的话，核心类是 IdleStateHandler 。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Netty 中有哪些重要组件？

> 原文：[https://zwmst.com/754.html](https://zwmst.com/754.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-08-14T08:03:19+08:00"> 2021-08-14 </time> ](https://zwmst.com/754.html)  Channel：Netty 网络操作抽象类，它除了包括基本的 I/O 操作，如 bind、connect、 read、write 等。

EventLoop：主要是配合 Channel 处理 I/O 操作，用来处理连接的生命周期中所发生的事 情。

ChannelFuture：Netty 框架中所有的 I/O 操作都为异步的，因此我们需要 ChannelFuture 的 addListener()注册一个 ChannelFutureListener 监听事件，当操作执行成功或者失败 时，监听就会自动触发返回结果。

ChannelHandler：充当了所有处理入站和出站数据的逻辑容器。ChannelHandler 主要用来 处理各种事件，这里的事件很广泛，比如可以是连接、数据接收、异常、数据转换等。

ChannelPipeline：为 ChannelHandler 链提供了容器，当 channel 创建时，就会被自动分 配到它专属的 ChannelPipeline，这个关联是永久性的。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Netty 发送消息有几种方式？

> 原文：[https://zwmst.com/756.html](https://zwmst.com/756.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-08-14T08:03:29+08:00"> 2021-08-14 </time> ](https://zwmst.com/756.html)  Netty 有两种发送消息的方式：

直接写入 Channel 中，消息从 ChannelPipeline 当中尾部开始移动； 写入和 ChannelHandler 绑定的 ChannelHandlerContext 中，消息从 ChannelPipeline 中 的下一个 ChannelHandler 中移动。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Netty 支持哪些心跳类型设置？

> 原文：[https://zwmst.com/758.html](https://zwmst.com/758.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-08-14T08:03:39+08:00"> 2021-08-14 </time> ](https://zwmst.com/758.html)  readerIdleTime：为读超时时间（即测试端一定时间内未接受到被测试端消息）。writerIdleTime：为写超时时间（即测试端一定时间内向被测试端发送消息）。allIdleTime：所有类型的超时时间。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 说说Netty的执行流程？

> 原文：[https://zwmst.com/760.html](https://zwmst.com/760.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-08-14T08:03:50+08:00"> 2021-08-14 </time> ](https://zwmst.com/760.html)  创建ServerBootStrap实例

设置并绑定Reactor线程池：EventLoopGroup，EventLoop就是处理所有注册到本线程的 Selector上面的Channel

设置并绑定服务端的channel

创建处理网络事件的ChannelPipeline和handler，网络时间以流的形式在其中流转， handler完成多数的功能定制：比如编解码 SSl安全认证

绑定并启动监听端口

当轮训到准备就绪的channel后，由Reactor线程：NioEventLoop执行pipline中的方法，最 终调度并执行channelHandler*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Netty高性能体现在哪些方面？

> 原文：[https://zwmst.com/762.html](https://zwmst.com/762.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-08-14T08:03:59+08:00"> 2021-08-14 </time> ](https://zwmst.com/762.html)  1）传输：IO模型在很大程度上决定了框架的性能，相比于bio，netty建议采用异步通信模 式，因为nio一个线程可以并发处理N个客户端连接和读写操作，这从根本上解决了传统同步阻 塞IO一连接一线程模型，架构的性能、弹性伸缩能力和可靠性都得到了极大的提升。正如代码 中所示，使用的是NioEventLoopGroup和NioSocketChannel来提升传输效率。

2）协议：采用什么样的通信协议，对系统的性能极其重要，netty默认提供了对Google Protobuf的支持，也可以通过扩展Netty的编解码接口，用户可以实现其它的高性能序列化框 架。

3）线程：netty使用了Reactor线程模型，但Reactor模型不同，对性能的影响也非常大，下 面介绍常用的Reactor线程模型有三种，分别如下：

Reactor单线程模型：单线程模型的线程即作为NIO服务端接收客户端的TCP连接，又作为 NIO客户端向服务端发起TCP连接，即读取通信对端的请求或者应答消息，又向通信对端发送 消息请求或者应答消息。理论上一个线程可以独立处理所有IO相关的操作，但一个NIO线程同时处理成百上千的链路，性能上无法支撑，即便NIO线程的CPU负荷达到100%，也无法满足 海量消息的编码、解码、读取和发送，又因为当NIO线程负载过重之后，处理速度将变慢，这 会导致大量客户端连接超时，超时之后往往会进行重发，这更加重了NIO线程的负载，最终会 导致大量消息积压和处理超时，NIO线程会成为系统的性能瓶颈。

Reactor多线程模型：有专门一个NIO线程用于监听服务端，接收客户端的TCP连接请求；网 络IO操作(读写)由一个NIO线程池负责，线程池可以采用标准的JDK线程池实现。但百万客户 端并发连接时，一个nio线程用来监听和接受明显不够，因此有了主从多线程模型。 主从Reactor多线程模型：利用主从NIO线程模型，可以解决1个服务端监听线程无法有效处理 所有客户端连接的性能不足问题，即把监听服务端，接收客户端的TCP连接请求分给一个线程 池。因此，在代码中可以看到，我们在server端选择的就是这种方式，并且也推荐使用该线程 模型。在启动类中创建不同的EventLoopGroup实例并通过适当的参数配置，就可以支持上述 三种Reactor线程模型。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 292.Netty 原理

> 原文：[https://zwmst.com/3583.html](https://zwmst.com/3583.html)

   [ *Netty* ](https://zwmst.com/netty)* [ *微服务* ](https://zwmst.com/%e5%be%ae%e6%9c%8d%e5%8a%a1)***[ <time datetime="2021-09-21T02:24:58+08:00"> 2021-09-20 </time> ](https://zwmst.com/3583.html)  Netty 是一个高性能、异步事件驱动的 NIO 框架，基于 JAVA NIO 提供的 API 实现。它提供了对TCP、UDP 和文件传输的支持，作为一个异步 NIO 框架，Netty 的所有 IO 操作都是异步非阻塞的，通过 Future-Listener 机制，用户可以方便的主动获取或者通过通知机制获得 IO 操作结果。**
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 293.Netty 高性能

> 原文：[https://zwmst.com/3586.html](https://zwmst.com/3586.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T03:26:44+08:00"> 2021-09-20 </time> ](https://zwmst.com/3586.html)  在 IO 编程过程中，当需要同时处理多个客户端接入请求时，可以利用多线程或者 IO 多路复用技术进行处理。IO 多路复用技术通过把多个 IO 的阻塞复用到同一个 select 的阻塞上，从而使得系统在单线程的情况下可以同时处理多个客户端请求。与传统的多线程/多进程模型比，I/O 多路复用的最大优势是系统开销小，系统不需要创建新的额外进程或者线程，也不需要维护这些进程和线程的运行，降低了系统的维护工作量，节省了系统资源。

与 Socket 类和 ServerSocket 类相对应，NIO 也提供了SocketChannel 和 ServerSocketChannel两种不同的套接字通道实现。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 294.多路复用通讯方式

> 原文：[https://zwmst.com/3590.html](https://zwmst.com/3590.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:10:01+08:00"> 2021-09-20 </time> ](https://zwmst.com/3590.html)  Netty 架构按照 Reactor 模式设计和实现，它的服务端通信序列图如下：![](img/9e4163f2bf7aded4cd32a06997f4e572.png)

客户端通信序列图如下：
![](img/fa14d35d459f9a4b98d64b31b70142b4.png)

Netty 的 IO 线程 NioEventLoop 由于聚合了多路复用器Selector，可以同时并发处理成百上千个客户端 Channel，由于读写操作都是非阻塞的，这就可以充分提升 IO 线程的运行效率，避免由于频繁 IO 阻塞导致的线程挂起。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 295.异步通讯 NIO

> 原文：[https://zwmst.com/3594.html](https://zwmst.com/3594.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:11:05+08:00"> 2021-09-20 </time> ](https://zwmst.com/3594.html)  **由于 Netty 采用了异步通信模式，一个 IO 线程可以并发处理 N 个客户端连接和读写操作**，这从根本上解决了传统同步阻塞 IO 一连接一线程模型，架构的性能、弹性伸缩能力和可靠性都得到了极
大的提升。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 296.零拷贝（DIRECT BUFFERS 使用堆外直接内存）

> 原文：[https://zwmst.com/3596.html](https://zwmst.com/3596.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:11:49+08:00"> 2021-09-20 </time> ](https://zwmst.com/3596.html)  1.  Netty 的接收和发送 ByteBuffer 采用 DIRECT BUFFERS，使用堆外直接内存进行 Socket 读写，不需要进行字节缓冲区的二次拷贝。如果使用传统的堆内存（HEAP BUFFERS）进行 Socket 读写，JVM 会将堆内存 Buffer 拷贝一份到直接内存中，然后才写入 Socket 中。相比于堆外直接内存，消息在发送过程中多了一次缓冲区的内存拷贝。
2.  Netty 提供了组合 Buffer 对象，可以聚合多个 ByteBuffer 对象，用户可以像操作一个 Buffer 那样方便的对组合 Buffer 进行操作，避免了传统通过内存拷贝的方式将几个小 Buffer 合并成一个大的Buffer。
3.  Netty的文件传输采用了transferTo方法，它可以直接将文件缓冲区的数据发送到目标Channel，避免了传统通过循环 write 方式导致的内存拷贝问题*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 297.内存池（基于内存池的缓冲区重用机制）

> 原文：[https://zwmst.com/3598.html](https://zwmst.com/3598.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:12:32+08:00"> 2021-09-20 </time> ](https://zwmst.com/3598.html)  随着 JVM 虚拟机和 JIT 即时编译技术的发展，对象的分配和回收是个非常轻量级的工作。但是对于缓冲区 Buffer，情况却稍有不同，特别是对于堆外直接内存的分配和回收，是一件耗时的操作。为了尽量重用缓冲区，Netty 提供了基于内存池的缓冲区重用机制。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 298.高效的 Reactor 线程模型

> 原文：[https://zwmst.com/3600.html](https://zwmst.com/3600.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:13:15+08:00"> 2021-09-20 </time> ](https://zwmst.com/3600.html)  常用的 Reactor 线程模型有三种，Reactor 单线程模型, Reactor 多线程模型, 主从 Reactor 多线程模型。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 299.Reactor 单线程模

> 原文：[https://zwmst.com/3602.html](https://zwmst.com/3602.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:14:17+08:00"> 2021-09-20 </time> ](https://zwmst.com/3602.html)  Reactor 单线程模型，指的是所有的 IO 操作都在同一个 NIO 线程上面完成，NIO 线程的职责如下：

1.  作为 NIO 服务端，接收客户端的 TCP 连接；
2.  作为 NIO 客户端，向服务端发起 TCP 连接；
3.  读取通信对端的请求或者应答消息；
4.  向通信对端发送消息请求或者应答消息。

由于 Reactor 模式使用的是异步非阻塞 IO，所有的 IO 操作都不会导致阻塞，理论上一个线程可以独立处理所有 IO 相关的操作。从架构层面看，一个 NIO 线程确实可以完成其承担的职责。例如，通过Acceptor 接收客户端的 TCP 连接请求消息，链路建立成功之后，通过 Dispatch 将对应的 ByteBuffer派发到指定的 Handler 上进行消息解码。用户 Handler 可以通过 NIO 线程将消息发送给客户端。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 300.Reactor 多线程模型

> 原文：[https://zwmst.com/3607.html](https://zwmst.com/3607.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:16:14+08:00"> 2021-09-20 </time> ](https://zwmst.com/3607.html)  Rector 多线程模型与单线程模型最大的区别就是有一组 NIO 线程处理 IO 操作。 有专门一个NIO 线程-Acceptor 线程用于监听服务端，接收客户端的 TCP 连接请求； 网络 IO 操作-读、写等由一个 NIO 线程池负责，线程池可以采用标准的 JDK 线程池实现，它包含一个任务队列和 N个可用的线程，由这些 NIO 线程负责消息的读取、解码、编码和发送；*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 302.无锁设计、线程绑定

> 原文：[https://zwmst.com/3611.html](https://zwmst.com/3611.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:21:53+08:00"> 2021-09-20 </time> ](https://zwmst.com/3611.html)  Netty 采用了串行无锁化设计，在 IO 线程内部进行串行操作，避免多线程竞争导致的性能下降。表面上看，串行化设计似乎 CPU 利用率不高，并发程度不够。但是，通过调整 NIO 线程池的线程参数，可以同时启动多个串行化的线程并行运行，这种局部无锁化的串行线程设计相比一个队列-多个工作线程模型性能更优。

Netty 的 NioEventLoop 读取到消息之后，直接调用ChannelPipeline 的fireChannelRead(Object msg)，只要用户不主动切换线程，一直会由 NioEventLoop 调用到用户的 Handler，期间不进行线程切换，这种串行化处理方式避免了多线程操作导致的锁的竞争，从性能角度看是最优的。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 303.高性能的序列化框架

> 原文：[https://zwmst.com/3613.html](https://zwmst.com/3613.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:24:28+08:00"> 2021-09-20 </time> ](https://zwmst.com/3613.html)  Netty 默认提供了对 Google Protobuf 的支持，通过扩展 Netty 的编解码接口，用户可以实现其它的高性能序列化框架，例如 Thrift 的压缩二进制编解码框架。

1.  SO_RCVBUF 和 SO_SNDBUF：通常建议值为 128K 或者 256K。

### 小包封大包，防止网络阻塞

2.  SO_TCPNODELAY：NAGLE 算法通过将缓冲区内的小封包自动相连，组成较大的封包，阻止大量小封包的发送阻塞网络，从而提高网络应用效率。但是对于时延敏感的应用场景需要关闭该优化算法。

### 软中断 Hash 值和 CPU 绑定

3.  软中断：开启 RPS 后可以实现软中断，提升网络吞吐量。RPS 根据数据包的源地址，目的地址以及目的和源端口，计算出一个 hash 值，然后根据这个 hash 值来选择软中断运行的 cpu，从上层来看，也就是说将每个连接和 cpu 绑定，并通过这个 hash 值，来均衡软中断在多个 cpu 上，提升网络并行处理性能。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 304.Netty RPC 实现

> 原文：[https://zwmst.com/3615.html](https://zwmst.com/3615.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:26:31+08:00"> 2021-09-20 </time> ](https://zwmst.com/3615.html)  RPC，即 Remote Procedure Call（远程过程调用），调用远程计算机上的服务，就像调用本地服务一样。RPC 可以很好的解耦系统，如 WebService 就是一种基于 Http 协议的 RPC。这个 RPC 整体框架如下：![](img/2b859664dc59dc4ed4a1a7dbb89310df.png)*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 305.关键技术

> 原文：[https://zwmst.com/3618.html](https://zwmst.com/3618.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:27:30+08:00"> 2021-09-20 </time> ](https://zwmst.com/3618.html)  1.  服务发布与订阅：服务端使用 Zookeeper 注册服务地址，客户端从 Zookeeper 获取可用的服务地址。
2.  通信：使用 Netty 作为通信框架。
3.  Spring：使用 Spring 配置服务，加载 Bean，扫描注解。
4.  动态代理：客户端使用代理模式透明化服务调用。
5.  消息编解码：使用 Protostuff 序列化和反序列化消息。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 306.核心流程

> 原文：[https://zwmst.com/3620.html](https://zwmst.com/3620.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:29:02+08:00"> 2021-09-20 </time> ](https://zwmst.com/3620.html)  1.  服务消费方（client）调用以本地调用方式调用服务；
2.  client stub 接收到调用后负责将方法、参数等组装成能够进行网络传输的消息体；
3.  client stub 找到服务地址，并将消息发送到服务端；
4.  server stub 收到消息后进行解码；
5.  server stub 根据解码结果调用本地的服务；
6.  本地服务执行并将结果返回给 server stub；
7.  server stub 将返回结果打包成消息并发送至消费方；
8.  client stub 接收到消息，并进行解码；
9.  服务消费方得到最终结果。

RPC 的目标就是要 2~8 这些步骤都封装起来，让用户对这些细节透明。JAVA 一般使用动态代理方式实现远程调用。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 307.消息编解码

> 原文：[https://zwmst.com/3622.html](https://zwmst.com/3622.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:30:32+08:00"> 2021-09-20 </time> ](https://zwmst.com/3622.html)  ### 息数据结构（接口名称+方法名+参数类型和参数值+超时时间+ requestID）

客户端的请求消息结构一般需要包括以下内容：

1.  接口名称：在我们的例子里接口名是“HelloWorldService”，如果不传，服务端就不知道调用哪个接口了；
2.  方法名：一个接口内可能有很多方法，如果不传方法名服务端也就不知道调用哪个方法；
3.  参数类型和参数值：参数类型有很多，比如有 bool、int、long、double、string、map、list，甚至如 struct（class）；以及相应的参数值；
4.  超时时间：
5.  requestID，标识唯一请求 id，在下面一节会详细描述 requestID 的用处。
6.  服务端返回的消息 ： 一般包括以下内容。返回值+状态 code+requestID*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 308.序列化

> 原文：[https://zwmst.com/3625.html](https://zwmst.com/3625.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:31:38+08:00"> 2021-09-20 </time> ](https://zwmst.com/3625.html)  目前互联网公司广泛使用 Protobuf、Thrift、Avro 等成熟的序列化解决方案来搭建 RPC 框架，这些都是久经考验的解决方案。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 309.通讯过程

> 原文：[https://zwmst.com/3628.html](https://zwmst.com/3628.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:33:37+08:00"> 2021-09-20 </time> ](https://zwmst.com/3628.html)  ### 核心问题(线程暂停、消息乱序)

如果使用 netty 的话，一般会用 channel.writeAndFlush()方法来发送消息二进制串，这个方法调用后对于整个远程调用(从发出请求到接收到结果)来说是一个异步的，即对于当前线程来说，将请求发送出来后，线程就可以往后执行了，至于服务端的结果，是服务端处理完成后，再以消息的形式发送给客户端的。于是这里出现以下两个问题：

1.  怎么让当前线程“暂停”，等结果回来后，再向后执行？
2.  如果有多个线程同时进行远程方法调用，这时建立在 client server 之间的 socket 连接上会有很多双方发送的消息传递，前后顺序也可能是随机的，server 处理完结果后，将结果消息发送给 client，client 收到很多消息，怎么知道哪个消息结果是原先哪个线程调用的？如下图所示，线程 A 和线程 B 同时向 client socket 发送请求 requestA 和 requestB，socket 先后将 requestB 和 requestA 发送至 server，而 server 可能将 responseB 先返回，尽管 requestB 请求到达时间更晚。我们需要一种机制保证 responseA 丢给ThreadA，responseB 丢给 ThreadB。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 310.通讯流程

> 原文：[https://zwmst.com/3630.html](https://zwmst.com/3630.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:34:47+08:00"> 2021-09-20 </time> ](https://zwmst.com/3630.html)  ### requestID 生成-AtomicLong

1.  client 线程每次通过 socket 调用一次远程接口前，生成一个唯一的 ID，即 requestID（requestID 必需保证在一个 Socket 连接里面是唯一的），一般常常使用 AtomicLong从 0 开始累计数字生成唯一 ID；*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 311.存放回调对象 callback 到全局 ConcurrentHashMap

> 原文：[https://zwmst.com/3632.html](https://zwmst.com/3632.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:35:40+08:00"> 2021-09-20 </time> ](https://zwmst.com/3632.html)  2.  将 处 理 结 果 的 回 调 对 象 callback ， 存 放 到 全 局 ConcurrentHashMap 里 面put(requestID, callback)；*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 312.synchronized 获取回调对象 callback 的锁并自旋 wait

> 原文：[https://zwmst.com/3635.html](https://zwmst.com/3635.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:36:59+08:00"> 2021-09-20 </time> ](https://zwmst.com/3635.html)  3.  当线程调用 channel.writeAndFlush()发送消息后，紧接着执行 callback 的 get()方法试图获取远程返回的结果。在 get()内部，则使用 synchronized 获取回调对象 callback 的锁，再先检测是否已经获取到结果，如果没有，然后调用 callback 的 wait()方法，释放callback 上的锁，让当前线程处于等待状态。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 313.监听消息的线程收到消息，找到 callback 上的锁并唤醒

> 原文：[https://zwmst.com/3637.html](https://zwmst.com/3637.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:37:50+08:00"> 2021-09-20 </time> ](https://zwmst.com/3637.html)  4.  服务端接收到请求并处理后，将 response 结果（此结果中包含了前面的 requestID）发送给客户端，客户端 socket 连接上专门监听消息的线程收到消息，分析结果，取到requestID ， 再 从 前 面 的 ConcurrentHashMap 里 面 get(requestID) ， 从 而 找 到callback 对象，再用 synchronized 获取 callback 上的锁，将方法调用结果设置到callback 对象里，再调用 callback.notifyAll()唤醒前面处于等待状态的线程。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 314.RMI 实现方式

> 原文：[https://zwmst.com/3641.html](https://zwmst.com/3641.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:39:47+08:00"> 2021-09-20 </time> ](https://zwmst.com/3641.html)  Java 远程方法调用，即 Java RMI（Java Remote Method Invocation）是 Java 编程语言里，一种用于实现远程过程调用的应用程序编程接口。它使客户机上运行的程序可以调用远程服务器上的对象。远程方法调用特性使 Java 编程人员能够在网络环境中分布操作。RMI 全部的宗旨就是尽可能简化远程接口对象的使用。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 315.实现步骤

> 原文：[https://zwmst.com/3643.html](https://zwmst.com/3643.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-21T04:41:26+08:00"> 2021-09-20 </time> ](https://zwmst.com/3643.html)  1.  编写远程服务接口，该接口必须继承 java.rmi.Remote 接口，方法必须抛出java.rmi.RemoteException 异常；
2.  编写远程接口实现类，该实现类必须继承 java.rmi.server.UnicastRemoteObject 类；
3.  运行 RMI 编译器（rmic），创建客户端 stub 类和服务端 skeleton 类;
4.  启动一个 RMI 注册表，以便驻留这些服务;
5.  在 RMI 注册表中注册服务；
6.  客户端查找远程对象，并调用远程方法；

```
 1：创建远程接口，继承 java.rmi.Remote 接口
public interface GreetService extends java.rmi.Remote {
 String sayHello(String name) throws RemoteException;
}
2：实现远程接口，继承 java.rmi.server.UnicastRemoteObject 类
public class GreetServiceImpl extends java.rmi.server.UnicastRemoteObject
implements GreetService {
 private static final long serialVersionUID = 3434060152387200042L;
 public GreetServiceImpl() throws RemoteException {
 super();
 }
 @Override
 public String sayHello(String name) throws RemoteException {
 return "Hello " + name;
 }
}
 3：生成 Stub 和 Skeleton;
4：执行 rmiregistry 命令注册服务
5：启动服务
LocateRegistry.createRegistry(1098);
Naming.bind("rmi://10.108.1.138:1098/GreetService", new GreetServiceImpl());
6.客户端调用
GreetService greetService = (GreetService) 
Naming.lookup("rmi://10.108.1.138:1098/GreetService");
System.out.println(greetService.sayHello("Jobs"));~~~
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 316.Protoclol Buffer

> 原文：[https://zwmst.com/3646.html](https://zwmst.com/3646.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-22T00:10:32+08:00"> 2021-09-21 </time> ](https://zwmst.com/3646.html)  protocol buffer 是 google 的一个开源项目,它是用于结构化数据串行化的灵活、高效、自动的方法，例如 XML，不过它比 xml 更小、更快、也更简单。你可以定义自己的数据结构，然后使用代码生成器生成的代码来读写这个数据结构。你甚至可以在无需重新部署程序的情况下更新数据结构。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 317.特点

> 原文：[https://zwmst.com/3648.html](https://zwmst.com/3648.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-22T00:11:53+08:00"> 2021-09-21 </time> ](https://zwmst.com/3648.html)  Protocol Buffer 的序列化 & 反序列化简单 & 速度快的原因是：

1.  编码 / 解码 方式简单（只需要简单的数学运算 = 位移等等）
2.  采用 Protocol Buffer 自身的框架代码 和 编译器 共同完成

Protocol Buffer 的数据压缩效果好（即序列化后的数据量体积小）的原因是：

1.  a. 采用了独特的编码方式，如 Varint、Zigzag 编码方式等等
2.  b. 采用 T – L – V 的数据存储方式：减少了分隔符的使用 & 数据存储得紧凑*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 318.Thrift

> 原文：[https://zwmst.com/3650.html](https://zwmst.com/3650.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-22T00:17:19+08:00"> 2021-09-21 </time> ](https://zwmst.com/3650.html)  Apache Thrift 是 Facebook 实现的一种高效的、支持多种编程语言的远程服务调用的框架。本文将从Java 开发人员角度详细介绍 Apache Thrift 的架构、开发和部署，并且针对不同的传输协议和服务类型给出相应的 Java 实例，同时详细介绍 Thrift 异步客户端的实现，最后提出使用 Thrift 需要注意的事项。

目前流行的服务调用方式有很多种，例如基于 SOAP 消息格式的 Web Service，基于 JSON 消息格式的 RESTful 服务等。其中所用到的数据传输方式包括 XML，JSON 等，然而 XML 相对体积太大，传输效率低，JSON 体积较小，新颖，但还不够完善。本文将介绍由 Facebook 开发的远程服务调用框架Apache Thrift，它采用接口描述语言定义并创建服务，支持可扩展的跨语言服务开发，所包含的代码生成引擎可以在多种语言中，如 C++, Java, Python, PHP, Ruby, Erlang, Perl, Haskell, C#, Cocoa, Smalltalk 等创建高效的、无缝的服务，其传输数据采用二进制格式，相对 XML 和 JSON 体积更小，对于高并发、大数据量和多语言的环境更有优势。

本文将详细介绍 Thrift 的使用，并且提供丰富的实例代码加以解释说明，帮助使用者快速构建服务。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 319.为什么要 Thrift

> 原文：[https://zwmst.com/3652.html](https://zwmst.com/3652.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-09-22T00:28:20+08:00"> 2021-09-21 </time> ](https://zwmst.com/3652.html)  1.  多语言开发的需要
2.  性能问题*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1192.BIO、NIO 和 AIO 的区别？

> 原文：[https://zwmst.com/5686.html](https://zwmst.com/5686.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-10-28T23:47:28+08:00"> 2021-10-28 </time> ](https://zwmst.com/5686.html)  BIO：一个连接一个线程，客户端有连接请求时服务器端就需要启动一个线程进行处理。线程开销大。
伪异步 IO：将请求连接放入线程池，一对多，但线程还是很宝贵的资源。

NIO：一个请求一个线程，但客户端发送的连接请求都会注册到多路复用器上，多路复用器轮询到连接有 I/O 请求时才启动个线程进行处理。

AIO：一个有效请求一个线程，客户端的 I/O 请求都是由 OS 先完成了再通知服务器应用去启动线程进行处理，
BIO 是面向流的，NIO 是面向缓冲区的；BIO 的各种流是阻塞的。而 NIO 是非阻塞的；BIO的 Stream 是单向的，而 NIO 的 channel 是双向的。

NIO 的特点：事件驱动模型、单线程处理多任务、非阻塞 I/O，I/O 读写不再阻塞，而是返回 0、基于 block 的传输比基于流的传输更高效、更高级的 IO 函数 zero-copy、IO 多路复用大大提高了 Java 网络应用的可伸缩性和实用性。基于 Reactor 线程模型。

在 Reactor 模式中，事件分发器等待某个事件或者可应用或个操作的状态发生，事件分发器就把这个事件传给事先注册的事件处理函数或者回调函数，由后者来做实际的读写操作。如在 Reactor 中实现读：注册读就绪事件和相应的事件处理器、事件分发器等待事件、事件到来，激活分发器，分发器调用事件对应的处理器、事件处理器完成实际的读操作，处理读到的数据，注册新的事件，然后返还控制权。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1193.NIO 的组成？

> 原文：[https://zwmst.com/5688.html](https://zwmst.com/5688.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-10-28T23:51:30+08:00"> 2021-10-28 </time> ](https://zwmst.com/5688.html)  Buffer：与 Channel 进行交互，数据是从 Channel 读入缓冲区，从缓冲区写入 Channel 中的

flip 方法 ： 反转此缓冲区，将 position 给 limit，然后将 position 置为 0，其实就是切换读写模式

clear 方法 ：清除此缓冲区，将 position 置为 0，把 capacity 的值给 limit。

rewind 方法 ： 重绕此缓冲区，将 position 置为 0

DirectByteBuffer 可减少一次系统空间到用户空间的拷贝。但 Buffer 创建和销毁的成本更高，不可控，通常会用内存池来提高性能。直接缓冲区主要分配给那些易受基础系统的本机 I/O 操作影响的大型、持久的缓冲区。如果数据量比较小的中小应用情况下，可以考虑使用 heapBuffer，由 JVM 进行管理。

Channel：表示 IO 源与目标打开的连接，是双向的，但不能直接访问数据，只能与 Buffer进行交互。通过源码可知，FileChannel 的 read 方法和 write 方法都导致数据复制了两次！

Selector 可使一个单独的线程管理多个 Channel，open 方法可创建 Selector，register 方法向多路复用器器注册通道，可以监听的事件类型：读、写、连接、accept。注册事件后会产生一个 SelectionKey：它表示 SelectableChannel 和 Selector 之间的注册关系，wakeup 方法：使尚未返回的第一个选择操作立即返回，唤醒的原因是：注册了新的 channel 或者事件；channel 关闭，取消注册；优先级更高的事件触发（如定时器事件），希望及时处理。

Selector 在 Linux 的实现类是 EPollSelectorImpl，委托给 EPollArrayWrapper 实现，其中三个native 方法是对 epoll 的封装，而 EPollSelectorImpl. implRegister 方法，通过调用 epoll_ctl向 epoll 实例中注册事件，还将注册的文件描述符(fd)与 SelectionKey 的对应关系添加到fdToKey 中，这个 map 维护了文件描述符与 SelectionKey 的映射。

fdToKey 有时会变得非常大，因为注册到 Selector 上的 Channel 非常多（百万连接）；过期或失效的 Channel 没有及时关闭。fdToKey 总是串行读取的，而读取是在 select 方法中进行的，该方法是非线程安全的。

Pipe：两个线程之间的单向数据连接，数据会被写到 sink 通道，从 source 通道读取NIO 的服务端建立过程：Selector.open()：打开一个 Selector；ServerSocketChannel.open()：创建服务端的 Channel；bind()：绑定到某个端口上。并配置非阻塞模式；register()：注册Channel 和关注的事件到 Selector 上；select()轮询拿到已经就绪的事件*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1194.Netty 的特点？

> 原文：[https://zwmst.com/5690.html](https://zwmst.com/5690.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-10-28T23:52:32+08:00"> 2021-10-28 </time> ](https://zwmst.com/5690.html)  一个高性能、异步事件驱动的 NIO 框架，它提供了对 TCP、UDP 和文件传输的支持使用更高效的 socket 底层，对 epoll 空轮询引起的 cpu 占用飙升在内部进行了处理，避免了直接使用 NIO 的陷阱，简化了 NIO 的处理方式。
采用多种 decoder/encoder 支持，对 TCP 粘包/分包进行自动化处理可使用接受/处理线程池，提高连接效率，对重连、心跳检测的简单支持可配置 IO 线程数、TCP 参数， TCP 接收和发送缓冲区使用直接内存代替堆内存，通过内存池的方式循环利用 ByteBuf通过引用计数器及时申请释放不再引用的对象，降低了 GC 频率使用单线程串行化的方式，高效的 Reactor 线程模型大量使用了 volitale、使用了 CAS 和原子类、线程安全类的使用、读写锁的使用*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1195.Netty 的线程模型？

> 原文：[https://zwmst.com/5692.html](https://zwmst.com/5692.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-10-28T23:53:39+08:00"> 2021-10-28 </time> ](https://zwmst.com/5692.html)  Netty 通过 Reactor 模型基于多路复用器接收并处理用户请求，内部实现了两个线程池，boss 线程池和 work 线程池，其中 boss 线程池的线程负责处理请求的 accept 事件，当接收到 accept 事件的请求时，把对应的 socket 封装到一个 NioSocketChannel 中，并交给 work线程池，其中 work 线程池负责请求的 read 和 write 事件，由对应的 Handler 处理。
单线程模型：所有 I/O 操作都由一个线程完成，即多路复用、事件分发和处理都是在一个Reactor 线程上完成的。既要接收客户端的连接请求,向服务端发起连接，又要发送/读取请求或应答/响应消息。一个 NIO 线程同时处理成百上千的链路，性能上无法支撑，速度慢，若线程进入死循环，整个程序不可用，对于高负载、大并发的应用场景不合适。
多线程模型：有一个 NIO 线程（Acceptor） 只负责监听服务端，接收客户端的 TCP 连接请求；NIO 线程池负责网络 IO 的操作，即消息的读取、解码、编码和发送；1 个 NIO 线程可以同时处理 N 条链路，但是 1 个链路只对应 1 个 NIO 线程，这是为了防止发生并发操作问题。但在并发百万客户端连接或需要安全认证时，一个 Acceptor 线程可能会存在性
能不足问题。
主从多线程模型：Acceptor 线程用于绑定监听端口，接收客户端连接，将 SocketChannel从主线程池的 Reactor 线程的多路复用器上移除，重新注册到 Sub 线程池的线程上，用于处理 I/O 的读写等操作，从而保证 mainReactor 只负责接入认证、握手等操作；*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1196.TCP 粘包/拆包的原因及解决方法？

> 原文：[https://zwmst.com/5694.html](https://zwmst.com/5694.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-10-28T23:54:51+08:00"> 2021-10-28 </time> ](https://zwmst.com/5694.html)  TCP 是以流的方式来处理数据，一个完整的包可能会被 TCP 拆分成多个包进行发送，也可能把小的封装成一个大的数据包发送。
TCP 粘包/分包的原因：
应用程序写入的字节大小大于套接字发送缓冲区的大小，会发生拆包现象，而应用程序写入数据小于套接字缓冲区大小，网卡将应用多次写入的数据发送到网络上，这将会发生粘包现象；
进行 MSS 大小的 TCP 分段，当 TCP 报文长度-TCP 头部长度>MSS 的时候将发生拆包以太网帧的 payload（净荷）大于 MTU（1500 字节）进行 ip 分片。
解决方法
消息定长：FixedLengthFrameDecoder 类
包尾增加特殊字符分割：行分隔符类：LineBasedFrameDecoder 或自定义分隔符类 ：
DelimiterBasedFrameDecoder
将消息分为消息头和消息体：LengthFieldBasedFrameDecoder 类。分为有头部的拆包与粘包、长度字段在前且有头部的拆包与粘包、多扩展头部的拆包与粘包。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1197.了解哪几种序列化协议？

> 原文：[https://zwmst.com/5696.html](https://zwmst.com/5696.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-10-28T23:57:25+08:00"> 2021-10-28 </time> ](https://zwmst.com/5696.html)  序列化（编码）是将对象序列化为二进制形式（字节数组），主要用于网络传输、数据持久化等；而反序列化（解码）则是将从网络、磁盘等读取的字节数组还原成原始对象，主要用于网络传输对象的解码，以便完成远程调用。

影响序列化性能的关键因素：序列化后的码流大小（网络带宽的占用）、序列化的性能（CPU 资源占用）；是否支持跨语言（异构系统的对接和开发语言切换）。

Java 默认提供的序列化：无法跨语言、序列化后的码流太大、序列化的性能差

XML，优点：人机可读性好，可指定元素或特性的名称。缺点：序列化数据只包含数据本身以及类的结构，不包括类型标识和程序集信息；只能序列化公共属性和字段；不能序列化方法；文件庞大，文件格式复杂，传输占带宽。适用场景：当做配置文件存储数据，实时数据转换。

JSON，是一种轻量级的数据交换格式，优点：兼容性高、数据格式比较简单，易于读写、序列化后数据较小，可扩展性好，兼容性好、与 XML 相比，其协议比较简单，解析速度比较快。缺点：数据的描述性比 XML 差、不适合性能要求为 ms 级别的情况、额外空间开销比较大。适用场景（可替代ＸＭＬ）：跨防火墙访问、可调式性要求高、基于 Web browser 的 Ajax 请求、传输数据量相对小，实时性要求相对低（例如秒级别）的服务。

Fastjson，采用一种“假定有序快速匹配”的算法。优点：接口简单易用、目前 java 语言中最快的 json 库。缺点：过于注重快，而偏离了“标准”及功能性、代码质量不高，文档不全。适用场景：协议交互、Web 输出、Android 客户端

Thrift，不仅是序列化协议，还是一个 RPC 框架。优点：序列化后的体积小, 速度快、支持多种语言和丰富的数据类型、对于数据字段的增删具有较强的兼容性、支持二进制压缩编码。缺点：使用者较少、跨防火墙访问时，不安全、不具有可读性，调试代码时相对困难、不能与其他传输层协议共同使用（例如 HTTP）、无法支持向持久层直接读写数据，即不适合做数据持久化序列化协议。适用场景：分布式系统的 RPC 解决方案

Avro，Hadoop 的一个子项目，解决了 JSON 的冗长和没有 IDL 的问题。优点：支持丰富的数据类型、简单的动态语言结合功能、具有自我描述属性、提高了数据解析速度、快速可压缩的二进制数据形式、可以实现远程过程调用 RPC、支持跨编程语言实现。缺点：对于习惯于静态类型语言的用户不直观。适用场景：在 Hadoop 中做 Hive、Pig 和 MapReduce的持久化数据格式。

Protobuf，将数据结构以.proto 文件进行描述，通过代码生成工具可以生成对应数据结构的POJO 对象和 Protobuf 相关的方法和属性。优点：序列化后码流小，性能高、结构化数据存储格式（XML JSON 等）、通过标识字段的顺序，可以实现协议的前向兼容、结构化的文档更容易管理和维护。缺点：需要依赖于工具生成代码、支持的语言相对较少，官方只支持Java 、C++ 、python。适用场景：对性能要求高的 RPC 调用、具有良好的跨防火墙的访问属性、适合应用层对象的持久化

其它

protostuff 基于 protobuf 协议，但不需要配置 proto 文件，直接导包即可Jboss marshaling 可以直接序列化 java 类， 无须实 java.io.Serializable 接口Message pack 一个高效的二进制序列化格式

Hessian 采用二进制协议的轻量级 remoting onhttp 工具

kryo 基于 protobuf 协议，只支持 java 语言,需要注册（Registration），然后序列化（Output），反序列化（Input）*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1198.如何选择序列化协议？

> 原文：[https://zwmst.com/5698.html](https://zwmst.com/5698.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-10-29T00:00:02+08:00"> 2021-10-28 </time> ](https://zwmst.com/5698.html)  具体场景
对于公司间的系统调用，如果性能要求在 100ms 以上的服务，基于 XML 的 SOAP 协议是一个值得考虑的方案。

基于 Web browser 的 Ajax，以及 Mobile app 与服务端之间的通讯，JSON 协议是首选。对于性能要求不太高，或者以动态类型语言为主，或者传输数据载荷很小的的运用场景，JSON也是非常不错的选择。

对于调试环境比较恶劣的场景，采用 JSON 或 XML 能够极大的提高调试效率，降低系统开发成本。

当对性能和简洁性有极高要求的场景，Protobuf，Thrift，Avro 之间具有一定的竞争关系。

对于 T 级别的数据的持久化应用场景，Protobuf 和 Avro 是首要选择。如果持久化后的数据存储在 hadoop 子项目里，Avro 会是更好的选择。

对于持久层非 Hadoop 项目，以静态类型语言为主的应用场景，Protobuf 会更符合静态类型语言工程师的开发习惯。由于 Avro 的设计理念偏向于动态类型语言，对于动态语言为主的应用场景，Avro 是更好的选择。

如果需要提供一个完整的 RPC 解决方案，Thrift 是一个好的选择。

如果序列化之后需要支持不同的传输层协议，或者需要跨防火墙访问的高性能场景，Protobuf 可以优先考虑。

protobuf 的数据类型有多种：bool、double、float、int32、int64、string、bytes、enum、message。protobuf 的限定符：required: 必须赋值，不能为空、optional:字段可以赋值，也可以不赋值、repeated: 该字段可以重复任意次数（包括 0 次）、枚举；只能用指定的常量集中的一个值作为其值；

protobuf 的基本规则：每个消息中必须至少留有一个 required 类型的字段、包含 0 个或多个 optional 类型的字段；repeated 表示的字段可以包含 0 个或多个数据；[1,15]之内的标识号在编码的时候会占用一个字节（常用），[16,2047]之内的标识号则占用 2 个字节，标识号一定不能重复、使用消息类型，也可以将消息嵌套任意多层，可用嵌套消息类型来代替组。

protobuf 的消息升级原则：不要更改任何已有的字段的数值标识；不能移除已经存在的required 字段，optional 和 repeated 类型的字段可以被移除，但要保留标号不能被重用。新添加的字段必须是 optional 或 repeated。因为旧版本程序无法读取或写入新增的required 限定符的字段。

编译器为每一个消息类型生成了一个.java 文件，以及一个特殊的 Builder 类（该类是用来创建消息类接口的）。如：

```
UserProto.User.Builder builder =
UserProto.User.newBuilder();builder.build()；
```

Netty 中的使用：ProtobufVarint32FrameDecoder 是用于处理半包消息的解码类；
ProtobufDecoder(UserProto.User.getDefaultInstance())这是创建的 UserProto.java 文件中的解码类；ProtobufVarint32LengthFieldPrepender 对 protobuf 协议的消息头上加上一个长度为32 的整形字段，用于标志这个消息的长度的类；ProtobufEncoder 是编码类将 StringBuilder 转换为 ByteBuf 类型：copiedBuffer()方法*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1199.Netty 的零拷贝实现？

> 原文：[https://zwmst.com/5700.html](https://zwmst.com/5700.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-10-29T00:27:45+08:00"> 2021-10-28 </time> ](https://zwmst.com/5700.html)  Netty 的接收和发送 ByteBuffer 采用 DIRECT BUFFERS，使用堆外直接内存进行 Socket 读写，不需要进行字节缓冲区的二次拷贝。堆内存多了一次内存拷贝，JVM 会将堆内存Buffer 拷贝一份到直接内存中，然后才写入 Socket 中。ByteBuffer 由 ChannelConfig 分配，而 ChannelConfig 创建 ByteBufAllocator 默认使用 Direct Buffer

CompositeByteBuf 类可以将多个 ByteBuf 合并为一个逻辑上的 ByteBuf, 避免了传统通过内存拷贝的方式将几个小 Buffer 合并成一个大的 Buffer。addComponents 方法将 header与 body 合并为一个逻辑上的 ByteBuf, 这两个 ByteBuf 在 CompositeByteBuf 内部都是单独存在的, CompositeByteBuf 只是逻辑上是一个整体

通过 FileRegion 包装的 FileChannel.tranferTo 方法 实现文件传输, 可以直接将文件缓冲区的数据发送到目标 Channel，避免了传统通过循环 write 方式导致的内存拷贝问题。

通过 wrap 方法, 我们可以将 byte[] 数组、ByteBuf、ByteBuffer 等包装成一个 NettyByteBuf 对象, 进而避免了拷贝操作。

Selector BUG：若 Selector 的轮询结果为空，也没有 wakeup 或新消息处理，则发生空轮询，CPU 使用率 100%，

Netty 的解决办法：对 Selector 的 select 操作周期进行统计，每完成一次空的 select 操作进行一次计数，若在某个周期内连续发生 N 次空轮询，则触发了 epoll 死循环 bug。重建Selector，判断是否是其他线程发起的重建请求，若不是则将原 SocketChannel 从旧的Selector 上去除注册，重新注册到新的 Selector 上，并将原来的 Selector 关闭。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1200.Netty 的高性能表现在哪些方面？

> 原文：[https://zwmst.com/5702.html](https://zwmst.com/5702.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-10-29T00:29:24+08:00"> 2021-10-28 </time> ](https://zwmst.com/5702.html)  心跳，对服务端：会定时清除闲置会话 inactive(netty5)，对客户端:用来检测会话是否断开，是否重来，检测网络延迟，其中 idleStateHandler 类 用来检测会话状态串行无锁化设计，即消息的处理尽可能在同一个线程内完成，期间不进行线程切换，这样就避免了多线程竞争和同步锁。表面上看，串行化设计似乎 CPU 利用率不高，并发程度不够。但是，通过调整 NIO 线程池的线程参数，可以同时启动多个串行化的线程并行运行，这种局部无锁化的串行线程设计相比一个队列-多个工作线程模型性能更优。

可靠性，链路有效性检测：链路空闲检测机制，读/写空闲超时机制；内存保护机制：通过内存池重用 ByteBuf;ByteBuf 的解码保护；优雅停机：不再接收新消息、退出前的预处理操作、资源的释放操作。

Netty 安全性：支持的安全协议：SSL V2 和 V3，TLS，SSL 单向认证、双向认证和第三方 CA认证。

高效并发编程的体现：volatile 的大量、正确使用；CAS 和原子类的广泛使用；线程安全容器的使用；通过读写锁提升并发性能。IO 通信性能三原则：传输（AIO）、协议（Http）、线程（主从多线程）

流量整型的作用（变压器）：防止由于上下游网元性能不均衡导致下游网元被压垮，业务流中断；防止由于通信模块接受消息过快，后端业务线程处理不及时导致撑死问题。

TCP 参数配置：SO_RCVBUF 和 SO_SNDBUF：通常建议值为 128K 或者 256K；

SO_TCPNODELAY：NAGLE 算法通过将缓冲区内的小封包自动相连，组成较大的封包，阻止大量小封包的发送阻塞网络，从而提高网络应用效率。但是对于时延敏感的应用场景需要关闭该优化算法；*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1201.NIOEventLoopGroup 源码？

> 原文：[https://zwmst.com/5704.html](https://zwmst.com/5704.html)

   [ *Netty* ](https://zwmst.com/netty)*[ <time datetime="2021-10-29T00:31:20+08:00"> 2021-10-28 </time> ](https://zwmst.com/5704.html)  NioEventLoopGroup(其实是 MultithreadEventExecutorGroup) 内部维护一个类型为EventExecutor children [], 默认大小是处理器核数 * 2, 这样就构成了一个线程池，初始化EventExecutor 时 NioEventLoopGroup 重载 newChild 方法，所以 children 元素的实际类型为NioEventLoop。

线程启动时调用 SingleThreadEventExecutor 的构造方法，执行 NioEventLoop 类的 run 方法，首先会调用 hasTasks()方法判断当前 taskQueue 是否有元素。如果 taskQueue 中有元素，执行 selectNow() 方法，最终执行 selector.selectNow()，该方法会立即返回。如果taskQueue 没有元素，执行 select(oldWakenUp) 方法select ( oldWakenUp) 方法解决了 Nio 中的 bug，selectCnt 用来记录 selector.select 方法的执行次数和标识是否执行过 selector.selectNow()，若触发了 epoll 的空轮询 bug，则会反复执行 selector.select(timeoutMillis)，变量 selectCnt 会逐渐变大，当 selectCnt 达到阈值（默认 512），则执行 rebuildSelector 方法，进行 selector 重建，解决 cpu 占用 100%的 bug。

rebuildSelector 方法先通过 openSelector 方法创建一个新的 selector。然后将 old selector 的selectionKey 执行 cancel。最后将 old selector 的 channel 重新注册到新的 selector 中。

rebuild 后，需要重新执行方法 selectNow，检查是否有已 ready 的 selectionKey。

接下来调用 processSelectedKeys 方法（处理 I/O 任务），当 selectedKeys != null 时，调用processSelectedKeysOptimized 方法，迭代 selectedKeys 获取就绪的 IO 事件的 selectkey 存放在数组 selectedKeys 中, 然后为每个事件都调用 processSelectedKey 来处理它，processSelectedKey 中分别处理 OP_READ；OP_WRITE；OP_CONNECT 事件。

最后调用 runAllTasks 方法（非 IO 任务），该方法首先会调用 fetchFromScheduledTaskQueue方法，把 scheduledTaskQueue 中已经超过延迟执行时间的任务移到 taskQueue 中等待被执行，然后依次从 taskQueue 中取任务执行，每执行 64 个任务，进行耗时检查，如果已执行时间超过预先设定的执行时间，则停止执行非 IO 任务，避免非 IO 任务太多，影响 IO 任务的执行。

每个 NioEventLoop 对应一个线程和一个 Selector，NioServerSocketChannel 会主动注册到某一个 NioEventLoop 的 Selector 上，NioEventLoop 负责事件轮询。

Outbound 事件都是请求事件, 发起者是 Channel，处理者是 unsafe，通过 Outbound 事件进行通知，传播方向是 tail 到 head。Inbound 事件发起者是 unsafe，事件的处理者是Channel, 是通知事件，传播方向是从头到尾。

内存管理机制，首先会预申请一大块内存 Arena，Arena 由许多 Chunk 组成，而每个 Chunk默认由 2048 个 page 组成。Chunk 通过 AVL 树的形式组织 Page，每个叶子节点表示一个Page，而中间节点表示内存区域，节点自己记录它在整个 Arena 中的偏移地址。当区域被分配出去后，中间节点上的标记位会被标记，这样就表示这个中间节点以下的所有节点都已被分配了。大于 8k 的内存分配在 poolChunkList 中，而 PoolSubpage 用于分配小于 8k 的内存，它会把一个 page 分割成多段，进行内存分配。

ByteBuf 的特点：支持自动扩容（4M），保证 put 方法不会抛出异常、通过内置的复合缓冲类型，实现零拷贝（zero-copy）；不需要调用 flip()来切换读/写模式，读取和写入索引分开；方法链；引用计数基于 AtomicIntegerFieldUpdater 用于内存回收；PooledByteBuf 采用二叉树来实现一个内存池，集中管理内存的分配和释放，不用每次使用都新建一个缓冲区对象。UnpooledHeapByteBuf 每次都会新建一个缓冲区对象*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1207.请列举 Nginx 服务器的最佳用途。

> 原文：[https://zwmst.com/5720.html](https://zwmst.com/5720.html)

   [ *Netty* ](https://zwmst.com/netty)* [ *Nginx* ](https://zwmst.com/nginx)***[ <time datetime="2021-10-30T05:14:04+08:00"> 2021-10-29 </time> ](https://zwmst.com/5720.html)  Nginx 服务器的最佳用法是在网络上部署动态 HTTP 内容，使用 SCGI、WSGI 应用程序服务器、用于脚本的 FastCGI 处理程序。它还可以作为负载均衡器。**
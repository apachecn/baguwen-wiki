<!--yml
category: Java
date: 0001-01-01 00:00:00
-->

# Java 多线程面试题（爪哇程序员）

# 什么是进程

> 原文：[https://zwmst.com/1671.html](https://zwmst.com/1671.html)

进程是指运行中的应用程序，每个进程都有自己独立的地址空间（内存空间）。 比如用户点击桌面的IE浏览器，就启动了一个进程，操作系统就会为该进程分配独立的地址空 间。当用户再次点击左边的IE浏览器，又启动了一个进程，操作系统将为新的进程分配新的独 立的地址空间。目前操作系统都支持多进程。


# 什么是线程

> 原文：[https://zwmst.com/1673.html](https://zwmst.com/1673.html)

进程是表示自愿分配的基本单位。而线程则是进程中执行运算的最小单位，即执行处理机调度 的基本单位。通俗来讲：一个程序有一个进程，而一个进程可以有多个线程。


# 进程间如何通讯

> 原文：[https://zwmst.com/1675.html](https://zwmst.com/1675.html)

管道(pipe)

管道是一种半双工的通信方式，数据只能单向流动，而且只能在具有亲缘关系的进程间使用。 进程的亲缘关系通常是指父子进程关系 有名管道(namedpipe)

有名管道也是半双工的通信方式，但是它云溪无亲缘关系进程间的通信。 信号量(semaphore)

信号量是一个计数器，可以用来控制多个进程对共享资源的访问。它常作为一种锁机制，防止 某进程正在访问共享资源时，其他进程也访问该资源。因此，主要作为进程间以及同一进程内 不同线程之间的同步手段。

消息队列（messagequeue）

消息队列里有消息的链表，存放在内核中并由消息队列标识符标识。消息队列克服了信号传递 消息少、管道只能承载无格式字节流以及缓冲区大小受限等缺点

信号（signal）

信号是一种比较复杂的通信方式，用于通知接收进程某个事件已经发生

共享内存（shared memory）

共享内存就是映射一段能被其他进程所访问的内存，这段共享内存由一个进程创建，但多个进 程都可以访问。共享内存是最快的IPC方式，它是针对其他进程间通信方式运行效率低而专门 设计的。它往往与其他通信机制，如信号量配合使用，来实现进程间的同步和通信。

套接字（socket）

套接口也是一种进程间通信机制，以其他通信机制不同的是，它可用于不同进程间的通信


# 线程间如何通讯

> 原文：[https://zwmst.com/1677.html](https://zwmst.com/1677.html)

锁机制：包括互斥锁、条件变量、读写锁

互斥锁提供了以排他方式防止数据结构被并发修改的方法 读写锁允许多个线程同时读共享数据，而对写操作是互斥的 条件变量可以以原子的方式阻塞进程，直到某个特定条件为真为止。对条件的测试是在互斥锁 的保护下进行的。条件变量始终与互斥锁一起使用。 信号量机制：包括无名线程信号量和命名线程信号量

信号机制：类似进程间的信号处理

线程间的通信目的只要是用于新城同步，所以线程没有像进程通信中的用于数据交换的通信机 制。


# 同步和异步有何不同，在什么情况下分别使用它们？举例说明

> 原文：[https://zwmst.com/1679.html](https://zwmst.com/1679.html)

如果数据将在线程间共享。例如：正在写的数据以后可能会被另一个线程读到，或者正在读的 数据可能已经被另一个线程写过了，那么这些数据就是共享数据，必须进行同步存取 当应用程序在对象上调用了一个需要花费很长时间来执行的方法，并且不希望让程序等待方法 的返回时，就应该使用异步编程，在很多情况下采用异步途径往往更有效。

同步交互：指发送一个请求，需要等待返回，然后才能发送下一个请求，有个等待的过程

异步交互：指发送一个请求，不需要等待返回，随时可以再发送下一个请求，即不需要等待。 区别：一个需要等待，一个不需要等待


# 进程调度算法

> 原文：[https://zwmst.com/1681.html](https://zwmst.com/1681.html)

实时系统：

FIFO(First Input First Output，先进先出算法)，

SJF(Shortest Job First，最短 作业优先算法)，

SRTF(Shortest Remaining Time First，最短剩余时间优先算法）。

交互式系统：

RR(Round Robin，时间片轮转算法)，

HPF(Highest Priority First，最高优先级算法)，多级队列，最短进程优先，保证调度，彩票调度，公平分享调度。


# Java中Unsafe类详解

> 原文：[https://zwmst.com/1683.html](https://zwmst.com/1683.html)

1.  通过Unsafe类可以分配内存，可以释放内存；类中提供的3个本地方法 allocateMemory、reallocateMemory、freeMemory分别用于分配内存，扩充内存和 释放内存，与C语言中的3个方法对应。
2.  可以定位对象某字段的内存位置，也可以修改对象的字段值，即使它是私有的；
3.  挂起与恢复:将一个线程进行挂起是通过park方法实现的，调用 park后，线程将一直阻 塞直到超时或者中断等条件出现。unpark可以终止一个挂起的线程，使其恢复正常。整 个并发框架中对线程的挂起操作被封装在 LockSupport类中，LockSupport类中有各种 版本pack方法，但最终都调用了Unsafe.park()方法。
4.  [Java中Unsafe类详解](https://blog.csdn.net/bluetjs/article/details/52758095)


# 如何测试并发量？

> 原文：[https://zwmst.com/1685.html](https://zwmst.com/1685.html)

可以使用apache提供的ab工具测试。


# 有三个线程T1，T2，T3，怎么确保它们按顺序执行？

> 原文：[https://zwmst.com/1687.html](https://zwmst.com/1687.html)

在多线程中有多种方法让线程按特定顺序执行，你可以用线程类的join()方法在一个线程中启 动另一个线程，另外一个线程完成该线程继续执行。为了确保三个线程的顺序你应该先启动最 后一个(T3调用T2，T2调用T1)，这样T1就会先完成而T3最后完成。


# 什么是线程调度器(Thread Scheduler)和时间分片(Time Slicing)？

> 原文：[https://zwmst.com/1689.html](https://zwmst.com/1689.html)

线程调度器是一个操作系统服务，它负责为Runnable状态的线程分配CPU时间。一旦我们 创建一个线程并启动它，它的执行便依赖于线程调度器的实现。

时间分片是指将可用的CPU时间分配给可用的Runnable线程的过程。分配CPU时间可以 基于线程优先级或者线程等待的时间。线程调度并不受到Java虚拟机控制，所以由应用程序来 控制它是更好的选择（即最好不要让你的程序依赖于线程的优先级）。


# 数据库死锁？

> 原文：[https://zwmst.com/1691.html](https://zwmst.com/1691.html)

在执行一个事务时可能要获取多个锁，一直持有锁到事务提交，如果A事务需要获取的锁在另 一个事务B中，且B事务也在等待A事务所持有的锁，那么两个事务之间就会发生死锁。但数据 库死锁比较少见，数据库会加以干涉死锁问题，牺牲一个事务使得其他事务正常执行。


# 什么是锁顺序死锁？

> 原文：[https://zwmst.com/1693.html](https://zwmst.com/1693.html)

两个线程试图以不同的顺序获得相同的锁，那么可能发发生死锁。比如转账问题，由from账户 向to账户转账，假设每次我们先同步from对象，再同步to账户，然后执行转账操作，貌似没什 么问题。如果这时候to账户同时向from账户转账，那么两个线程可能要永久等待了。


# 死锁的避免与诊断？

> 原文：[https://zwmst.com/1695.html](https://zwmst.com/1695.html)

如果一个线程最多只能获取一个锁，那么就不会发生锁顺序死锁了。如果确实需要获取多个 锁，锁的顺序可以按照某种规约，比如两个资源的id值，程序按规约保证获取锁的顺序一致。 或者可以使用显式的锁Lock，获取锁的时候设置超时时间，超时后可以重新发起，以避免发生 死锁。


# 常见的并发容器？

> 原文：[https://zwmst.com/1697.html](https://zwmst.com/1697.html)

ConcurrentHashMap：使用了分段锁，锁的粒度变得更小，多线程访问时，可能都不存在锁 的竞争，所以大大提高了吞吐量。简单对比来看，就好比数据库上用行锁来取代表锁，行锁无 疑带来更大的并发。

CopyOnWriteArrayList：写入时复制，多线程访问时，彼此不会互相干扰或被修改的线程所 干扰，当然copy时有开销的，尤其时列表元素庞大，且写入操作频繁时，所以仅当迭代操作远 远大于修改操作时，才应该考虑使用。

BlockingQueue：阻塞队列提供了可阻塞的put和take方法，当队列已经满了，那么put操作

将阻塞到队列可用，当队列为空时，take操作会阻塞到队列里有数据。有界的队列是一种强大 的资源管理器，可以在程序负荷过载时保护应用，可作为一种服务降级的策略。阻塞队列还提 供offer操作，当数据无法加入队列时，返回失败状态，给应用主动处理负荷过载带来更多灵活 性。


# 常见的同步工具类？

> 原文：[https://zwmst.com/1699.html](https://zwmst.com/1699.html)

CountDownLatch：递减计数器闭锁，直到达到某个条件时才放行，多线程可以调用await方 法一直阻塞，直到计数器递减为零。比如我们连接zookeeper，由于连接操作是异步的，所以 可以使用countDownLatch创建一个计数器为1的锁，连接挂起，当异步连接成功时，调用countDown通知挂起线程；再比如5V5游戏竞技，只有房间人满了才可以开始游戏。

FutureTask：带有计算结果的任务，在计算完成时才能获取结果，如果计算尚未完成，则阻 塞 get方法。FutureTask将计算结果从执行线程传递到获取这个结果的线程。

Semaphore：信号量，用来控制同时访问某个特定资源的数量，只有获取到许可acquire，才 能够正常执行，并在完成后释放许可，acquire会一致阻塞到有许可或中断超时。使用信号量可以轻松实现一个阻塞队列。

CyclicBarrier：类似于闭锁，它可以阻塞一组线程，只有所有线程全部到达以后，才能够继续 执行，so线程必须相互等待。这在并行计算中是很有用的，将一个问题拆分为多个独立的子问 题，当线程到达栅栏时，调用await等待，一直阻塞到所有参与线程全部到达，再执行下一步 任务。


# Nginx多进程模型是如何实现高并发的？

> 原文：[https://zwmst.com/1701.html](https://zwmst.com/1701.html)

进程数与并发数不存在很直接的关系。这取决取server采用的工作方式。如果一个server采用 一个进程负责一个request的方式，那么进程数就是并发数。那么显而易见的，就是会有很多 进程在等待中。等什么？最多的应该是等待网络传输。

Nginx的异步非阻塞工作方式正是利用了这点等待的时间。在需要等待的时候，这些进程就空 闲出来待命了。因此表现为少数几个进程就解决了大量的并发问题。apache是如何利用的呢， 简单来说：同样的4个进程，如果采用一个进程负责一个request的方式，那么，同时进来4个 request之后，每个进程就负责其中一个，直至会话关闭。期间，如果有第5个request进来了。就无法及时反应了，因为4个进程都没干完活呢，因此，一般有个调度进程，每当新进来了一个request，就新开个进程来处理。nginx不这样，每进来一个request，会有一个worker进程去处理。但不是全程的处理，处理到什么程度呢？处理到可能发生阻塞的地方，比 如向上游（后端）服务器转发request，并等待请求返回。那么，这个处理的worker不会这么 傻等着，他会在发送完请求后，注册一个事件：“如果upstream返回了，告诉我一声，我再接 着干”。于是他就休息去了。此时，如果再有request进来，他就可以很快再按这种方式处理。 而一旦上游服务器返回了，就会触发这个事件，worker才会来接手，这个request才会接着往 下走。由于web server的工作性质决定了每个request的大部份生命都是在网络传输中，实际 上花费在server机器上的时间片不多。这是几个进程就解决高并发的秘密所在。webserver刚 好属于网络io密集型应用，不算是计算密集型。异步，非阻塞，使用epoll，和大量细节处的优 化。也正是nginx之所以然的技术基石。


# CopyOnWriteArrayList

> 原文：[https://zwmst.com/1703.html](https://zwmst.com/1703.html)

CopyOnWriteArrayList : 写时加锁，当添加一个元素的时候，将原来的容器进行copy，复制 出一个新的容器，然后在新的容器里面写，写完之后再将原容器的引用指向新的容器，而读的 时候是读旧容器的数据，所以可以进行并发的读，但这是一种弱一致性的策略。

使用场景：CopyOnWriteArrayList适合使用在读操作远远大于写操作的场景里，比如缓存。


# AQS

> 原文：[https://zwmst.com/1705.html](https://zwmst.com/1705.html)

1.  AQS使用一个int成员变量来表示同步状态，通过内置的FIFO队列来完成获取资源线程的排队工作。

```
private volatile int state;//共享变量，使用volatile修饰保证线程可见性
```

1.  2种同步方式：独占式，共享式。独占式如ReentrantLock，共享式如Semaphore，

    CountDownLatch，组合式的如ReentrantReadWriteLock

2.  节点的状态

    CANCELLED，值为1，表示当前的线程被取消；

    SIGNAL，值为-1，表示当前节点的后继节点包含的线程需要运行，也就是unpark；

    CONDITION，值为-2，表示当前节点在等待condition，也就是在condition队列中；

    PROPAGATE，值为-3，表示当前场景下后续的acquireShared能够得以执行； 值为0，表示当前节点在sync队列中，等待着获取锁。

3.  模板方法模式

protected boolean tryAcquire(int arg) : 独占式获取同步状态，试着获取，成功返回 true，反之为false

protected boolean tryRelease(int arg) ：独占式释放同步状态，等待中的其他线 程此时将有机会获取到同步状态；

protected int tryAcquireShared(int arg) ：共享式获取同步状态，返回值大于等 于0，代表获取成功；反之获取失败；

protected boolean tryReleaseShared(int arg) ：共享式释放同步状态，成功为 true，失败为false

AQS维护一个共享资源state，通过内置的FIFO来完成获取资源线程的排队工作。该队列 由一个一个的Node结点组成，每个Node结点维护一个prev引用和next引用，分别指向 自己的前驱和后继结点。双端双向链表。

*   独占式:乐观的并发策略

    **acquire

    a.首先tryAcquire获取同步状态，成功则直接返回；否则，进入下一环节；

    b.线程获取同步状态失败，就构造一个结点，加入同步队列中，这个过程要保证线

    程安全；

    c.加入队列中的结点线程进入自旋状态，若是老二结点（即前驱结点为头结点），才有机会尝试去获取同步状态；否则，当其前驱结点的状态为SIGNAL，线程便可安心休息，进入阻塞状态，直到被中断或者被前驱结点唤醒。

    **release

    release的同步状态相对简单，需要找到头结点的后继结点进行唤醒，若后继结点为空或处于CANCEL状态，从后向前遍历找寻一个正常的结点，唤醒其对应线程。

4.  共享式:

共享式地获取同步状态.同步状态的方法tryAcquireShared返回值为int。

a.当返回值大于0时，表示获取同步状态成功，同时还有剩余同步状态可供其他线程获 取；

b.当返回值等于0时，表示获取同步状态成功，但没有可用同步状态了；

c.当返回值小于0时，表示获取同步状态失败。

5.  AQS实现公平锁和非公平锁

    非公平锁中，那些尝试获取锁且尚未进入等待队列的线程会和等待队列head结点的线程

    发生竞争。公平锁中，在获取锁时，增加了isFirst(current)判断，当且仅当，等待队列

    为空或当前线程是等待队列的头结点时，才可尝试获取锁。


# Java里的阻塞队列

> 原文：[https://zwmst.com/1707.html](https://zwmst.com/1707.html)

**7个阻塞队列。分别是

ArrayBlockingQueue ：一个由数组结构组成的有界阻塞队列。

LinkedBlockingQueue ：一个由链表结构组成的有界阻塞队列。

PriorityBlockingQueue ：一个支持优先级排序的无界阻塞队列。

DelayQueue：一个使用优先级队列实现的无界阻塞队列。

SynchronousQueue：一个不存储元素的阻塞队列。

LinkedTransferQueue：一个由链表结构组成的无界阻塞队列。

LinkedBlockingDeque：一个由链表结构组成的双向阻塞队列。

**添加元素

Java中的阻塞队列接口BlockingQueue继承自Queue接口。BlockingQueue接口提供了3个添加元素方法。

add：添加元素到队列里，添加成功返回true，由于容量满了添加失败会抛出IllegalStateException异常

offer：添加元素到队列里，添加成功返回true，添加失败返回false

put：添加元素到队列里，如果容量满了会阻塞直到容量不满

**删除方法

3个删除方法

poll：删除队列头部元素，如果队列为空，返回null。否则返回元素。

remove：基于对象找到对应的元素，并删除。删除成功返回true，否则返回false

take：删除队列头部元素，如果队列为空，一直阻塞到队列有元素并删除


# ForkJoin框架

> 原文：[https://zwmst.com/1709.html](https://zwmst.com/1709.html)

Fork/Join框架是Java 7提供的一个用于并行执行任务的框架，是一个把大任务分割成若干个 小任务，最终汇总每个小任务结果后得到大任务结果的框架。Fork/Join框架要完成两件事情：

1.任务分割：首先Fork/Join框架需要把大的任务分割成足够小的子任务，如果子任务比较 大的话还要对子任务进行继续分割

2.执行任务并合并结果：分割的子任务分别放到双端队列里，然后几个启动线程分别从双 端队列里获取任务执行。子任务执行完的结果都放在另外一个队列里，启动一个线程从队列里 取数据，然后合并这些数据。

在Java的Fork/Join框架中，使用两个类完成上述操作

1.ForkJoinTask:我们要使用Fork/Join框架，首先需要创建一个ForkJoin任务。该类提供 了在任务中执行fork和join的机制。通常情况下我们不需要直接集成ForkJoinTask类，只需要 继承它的子类，Fork/Join框架提供了两个子类：

a.RecursiveAction：用于没有返回结果的任务

b.RecursiveTask:用于有返回结果的任务

2.ForkJoinPool:ForkJoinTask需要通过ForkJoinPool来执行 任务分割出的子任务会添加到当前工作线程所维护的双端队列中，进入队列的头部。当一 个工作线程的队列里暂时没有任务时，它会随机从其他工作线程的队列的尾部获取一个任务(工 作窃取算法)。

Fork/Join框架的实现原理

ForkJoinPool由ForkJoinTask数组和ForkJoinWorkerThread数组组成，ForkJoinTask数组负责将存放程序提交给ForkJoinPool，而ForkJoinWorkerThread负责执 行这


# 在 java 中守护线程和本地线程区别？

> 原文：[https://zwmst.com/2088.html](https://zwmst.com/2088.html)

java 中的线程分为两种：**守护线程（Daemon）和用户线程（User）**。任何线程都可以设置为守护线程和用户线程，通过方法Thread.setDaemon(boolon)；true 则把该线程设置为守护线程，反之则为用户线程。
Thread.setDaemon()必须在 Thread.start()之前调用，否则运行时会抛出异常。

## 两者的区别：

唯一的区别是判断虚拟机(JVM)何时离开，Daemon 是为其他线程提供服务，如果全部的 User Thread 已经撤离，Daemon 没有可服务的线程，JVM 撤离。
也可以理解为守护线程是 JVM 自动创建的线程（但不一定），用户线程是程序创建的线程；比如 JVM 的垃圾回收线程是一个守护线程，当所有线程已经撤离， 不再产生垃圾，守护线程自然就没事可干了，当垃圾回收线程是 Java 虚拟机上仅剩的线程时，Java 虚拟机会自动离开。

## 扩展：

Thread Dump 打印出来的线程信息，含有 daemon 字样的线程即为守护进程，可能会有：服务守护进程、编译守护进程、windows 下的监听Ctrl+break 的守护进程、Finalizer 守护进程、引用处理守护进程、GC 守护进程。


# 线程与进程的区别？

> 原文：[https://zwmst.com/2090.html](https://zwmst.com/2090.html)

进程是操作系统分配资源的最小单元，线程是操作系统调度的最小单元。
一个程序至少有一个进程,一个进程至少有一个线程。


# 什么是多线程中的上下文切换？

> 原文：[https://zwmst.com/2092.html](https://zwmst.com/2092.html)

多线程会共同使用一组计算机上的 CPU，而线程数大于给程序分配的CPU 数量时，为了让各个线程都有执行的机会，就需要轮转使用CPU。**不同的线程切换使用CPU 发生的切换数据等就是上下文切换**。


# 死锁与活锁的区别，死锁与饥饿的区别？

> 原文：[https://zwmst.com/2094.html](https://zwmst.com/2094.html)

## 死锁：

是指两个或两个以上的进程（或线程）在执行过程中，因争夺资源而造成的一种互相等待的现象，若无外力作用，它们都将无法推进下去。

## 产生死锁的必要条件：

*   1、互斥条件：所谓互斥就是进程在某一时间内独占资源。
*   2、请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不 放。
*   3、不剥夺条件:进程已获得资源，在末使用完之前，不能强行剥夺。
*   4、循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。活锁：任务或者执行者没有被阻塞，由于某些条件没有满足，导致一直重复尝试，失败，尝试，失败。

活锁和死锁的区别在于，处于活锁的实体是在不断的改变状态，所谓的
“活”， 而处于死锁的实体表现为等待；活锁有可能自行解开，死锁则不能。饥饿：一个或者多个线程因为种种原因无法获得所需要的资源，导致一直无法执行的状态。

## Java 中导致饥饿的原因：

*   1、高优先级线程吞噬所有的低优先级线程的 CPU 时间。
*   2、线程被永久堵塞在一个等待进入同步块的状态，因为其他线程总是能在它之 前持续地对该同步块进行访问。
*   3、线程在等待一个本身也处于永久等待完成的对象(比如调用这个对象的 wait 方法)，因为其他线程总是被持续地获得唤醒。


# Java 中用到的线程调度算法是什么？

> 原文：[https://zwmst.com/2096.html](https://zwmst.com/2096.html)

采用时间片轮转的方式。可以设置线程的优先级，会映射到下层的系统上面的优先级上，如非特别需要，尽量不要用，防止线程饥饿。


# 什么是线程组，为什么在 Java 中不推荐使用？

> 原文：[https://zwmst.com/2098.html](https://zwmst.com/2098.html)

**ThreadGroup 类**，可以把线程归属到某一个线程组中，线程组中可以有线程对象，也可以有线程组，组中还可以有线程，这样的组织结构有点类似于树的形式。
为什么不推荐使用？因为使用有很多的安全隐患吧，没有具体追究，如果需要使用，推荐使用线程池。


# 为什么使用 Executor 框架？

> 原文：[https://zwmst.com/2100.html](https://zwmst.com/2100.html)

每次执行任务创建线程 new Thread()比较消耗性能，创建一个线程是比较耗时、耗资源的。
调用 new Thread()创建的线程缺乏管理，被称为**野线程**，而且可以无限制的创建，线程之间的相互竞争会导致过多占用系统资源而导致系统瘫痪，还有线程之间的频繁交替也会消耗很多系统资源。
接使用 new Thread() 启动的线程不利于扩展，比如定时执行、定期执行、定时定期执行、线程中断等都不便实现。


# 在 Java 中 Executor 和 Executors 的区别？

> 原文：[https://zwmst.com/2102.html](https://zwmst.com/2102.html)

Executors 工具类的不同方法按照我们的需求创建了不同的线程池，来满足业务的需求。
Executor 接口对象能执行我们的线程任务。
ExecutorService 接口继承了 Executor 接口并进行了扩展，提供了更多的方法我们能获得任务执行的状态并且可以获取任务的返回值。
使用 ThreadPoolExecutor 可以创建自定义线程池。
Future表示异步计算的结果，他提供了检查计算是否完成的方法，以等待计算的完成，并可以使用 get()方法获取计算的结果。


# 什么是原子操作？在 Java Concurrency API 中有哪些原子类(atomic classes)？

> 原文：[https://zwmst.com/2104.html](https://zwmst.com/2104.html)

**原子操作（atomic operation）** 意为”不可被中断的一个或一系列操作” 。处理器使用基于对缓存加锁或总线加锁的方式来实现多处理器之间的原子操 作。
在 Java 中可以通过锁和循环 CAS 的方式来实现原子操作。 CAS 操作—
—Compare & Set，或是 Compare & Swap，现在几乎所有的 CPU 指令都支持CAS 的原子操作。
原子操作是指一个不受其他操作影响的操作任务单元。原子操作是在多线程环境下避免数据不一致必须的手段。
int++并不是一个原子操作，所以当一个线程读取它的值并加 1 时，另外一个线程有可能会读到之前的值，这就会引发错误。
为了解决这个问题，必须保证增加操作是原子的，在 JDK1.5 之前我们可以使用同步技术来做到这一点。到 JDK1.5，java.util.concurrent.atomic 包提供了 int 和 long 类型的原子包装类，它们可以自动的保证对于他们的操作是原子的并且不需要使用同步。
java.util.concurrent 这个包里面提供了一组原子类。其基本的特性就是在多线程环境下，当有多个线程同时执行这些类的实例包含的方法时，具有排他性，即当某个线程进入方法，执行其中的指令时，不会被其他线程打断，而别的线程就像自旋锁一样，一直等到该方法执行完成，才由 JVM 从等待队列中选择一个另一个线程进入，这只是一种逻辑上的理解。

## 原子类：

AtomicBoolean，AtomicInteger，AtomicLong，AtomicReference

## 原子数组：

AtomicIntegerArray，AtomicLongArray，AtomicReferenceArray

## 原子属性更新器：

AtomicLongFieldUpdater，AtomicIntegerFieldUpdater， AtomicReferenceFieldUpdater

## 解决 ABA 问题的原子类：

AtomicMarkableReference（通过引入一个 boolean 来反映中间有没有变过），AtomicStampedReference（通过引入一个 int 来累加来反映中间有没有变过）


# Java Concurrency API 中的 Lock 接口(Lock interface) 是什么？

> 原文：[https://zwmst.com/2106.html](https://zwmst.com/2106.html)

**Lock 接口比同步方法和同步块提供了更具扩展性的锁操作。
他们允许更灵活的结构，可以具有完全不同的性质，并且可以支持多个相关类的条件对象。

## 它的优势有：

*   可以使锁更公平可以使线程在等待锁的时候响应中断
*   可以让线程尝试获取锁，并在无法获取锁的时候立即返回或者等待一段时间可以在不同的范围，以不同的顺序获取和释放锁

整体上来说 Lock 是 synchronized 的扩展版，Lock 提供了无条件的、可轮询的
(tryLock 方法)、定时的(tryLock 带参方法)、可中断的(lockInterruptibly)、可多条件队列的(newCondition 方法)锁操作。
另外Lock 的实现类基本都支持非公平锁(默认)和公平锁，synchronized 只支持非公平锁，当然，在大部分情况下，非公平锁是高效的选择。


# 什么是 Executors 框架？

> 原文：[https://zwmst.com/2108.html](https://zwmst.com/2108.html)

**Executor** 框架是一个根据一组执行策略调用，调度，执行和控制的异步任务的框架。
无限制的创建线程会引起应用程序内存溢出。所以创建一个线程池是个更好的的解决方案，因为可以限制线程的数量并且可以回收再利用这些线程。利用Executors 框架可以非常方便的创建一个线程池。


# 什么是阻塞队列？阻塞队列的实现原理是什 么？如何使用阻塞队列来实现生产者-消费者模型？

> 原文：[https://zwmst.com/2110.html](https://zwmst.com/2110.html)

**阻塞队列（BlockingQueue）** 是一个支持两个附加操作的队列。

## 这两个附加的操作是：

*   在队列为空时，获取元素的线程会等待队列变为非空。
*   当队列满时，存储元素的线程会等待队列可用。
    阻塞队列常用于生产者和消费者的场景，生产者是往队列里添加元素的线程，消费者是从队列里拿元素的线程。阻塞队列就是生产者存放元素的容器，而消费者也只从容器里拿元素。

    ## JDK7 提供了 7 个阻塞队列。分别是：

*   ArrayBlockingQueue ：一个由数组结构组成的有界阻塞队列。
*   LinkedBlockingQueue ：一个由链表结构组成的有界阻塞队列。
*   PriorityBlockingQueue ：一个支持优先级排序的无界阻塞队列。
*   DelayQueue：一个使用优先级队列实现的无界阻塞队列。
*   SynchronousQueue：一个不存储元素的阻塞队列。
*   LinkedTransferQueue：一个由链表结构组成的无界阻塞队列。
*   LinkedBlockingDeque：一个由链表结构组成的双向阻塞队列。
    Java 5 之前实现同步存取时，可以使用普通的一个集合，然后在使用线程的协作和线程同步可以实现生产者，消费者模式，主要的技术就是用好， wait ,notify,notifyAll,sychronized 这些关键字。而在 java 5 之后，可以使用阻塞队列来实现，此方式大大简少了代码量，使得多线程编程更加容易，安全方面也有保障。
    **BlockingQueue** 接口是 Queue 的子接口，它的主要用途并不是作为容器，而是作为线程同步的的工具，因此他具有一个很明显的特性，当生产者线程试图向 BlockingQueue 放入元素时，如果队列已满，则线程被阻塞，当消费者线程试图从中取出一个元素时，如果队列为空，则该线程会被阻塞，正是因为它所具有这个特性，所以在程序中多个线程交替向 BlockingQueue 中放入元素，取出元素，它可以很好的控制线程之间的通信。
    阻塞队列使用最经典的场景就是 socket 客户端数据的读取和解析，读取数据的线程不断将数据放入队列，然后解析线程不断从队列取数据解析。


# 什么是callable和future

> 原文：[https://zwmst.com/2112.html](https://zwmst.com/2112.html)

Callable 接口类似于 Runnable，从名字就可以看出来了，但是 Runnable 不会返回结果，并且无法抛出返回结果的异常，而 Callable 功能更强大一些， 被线程执行后，可以返回值，这个返回值可以被 Future 拿到，也就是说， Future 可以拿到异步执行任务的返回值。
可以认为是带有回调的 Runnable。
Future 接口表示异步任务，是还没有完成的任务给出的未来结果。所以说Callable 用于产生结果，Future 用于获取结果。


# 什么是 FutureTask

> 原文：[https://zwmst.com/2114.html](https://zwmst.com/2114.html)

在 Java 并发程序中 FutureTask 表示一个可以取消的异步运算。它有启动和取消运算、查询运算是否完成和取回运算结果等方法。只有当运算完成的时候结果才能取回，如果运算尚未完成 get 方法将会阻塞。一个 FutureTask 对象可以对调用了 Callable 和 Runnable 的对象进行包装，由于 FutureTask 也是调用了Runnable 接口所以它可以提交给 Executor 来执行。


# 什么是并发容器的实现

> 原文：[https://zwmst.com/2116.html](https://zwmst.com/2116.html)

## 何为同步容器：

可以简单地理解为通过 synchronized 来实现同步的容器，如果有多个线程调用同步容器的方法，它们将会串行执行。比如 Vector， Hashtable，以及 Collections.synchronizedSet，synchronizedList 等方法返回的容器。可以通过查看 Vector，Hashtable 等这些同步容器的实现代码， 可以看到这些容器实现线程安全的方式就是将它们的状态封装起来，并在需要同步的方法上加上关键字 synchronized。
并发容器使用了与同步容器完全不同的加锁策略来提供更高的并发性和伸缩性，例如在 ConcurrentHashMap 中采用了一种粒度更细的加锁机制，可以称为分段锁，在这种锁机制下，允许任意数量的读线程并发地访问 map，并且执行读操作的线程和写操作的线程也可以并发的访问map，同时允许一定数量的写操作线程并发地修改 map，所以它可以在并发环境下实现更高的吞吐量。


# 多线程同步和互斥有几种实现方法，都是什么？

> 原文：[https://zwmst.com/2118.html](https://zwmst.com/2118.html)

**线程同步** 是指线程之间所具有的一种制约关系，一个线程的执行依赖另一个线程的消息，当它没有得到另一个线程的消息时应等待，直到消息到达时才被唤醒。
**线程互斥** 是指对于共享的进程系统资源，在各单个线程访问时的排它性。当有若干个线程都要使用某一共享资源时，任何时刻最多只允许一个线程去使用，其它要使用该资源的线程必须等待，直到占用资源者释放该资源。
**线程互斥可以看成是一种特殊的线程同步。
线程间的同步方法大体可分为两类：用户模式和内核模式。
顾名思义，内核模式就是指利用系统内核对象的单一性来进行同步，使用时需要切换内核态与用户态，而用户模式就是不需要切换到内核态，只在用户态完成操作。
用户模式下的方法有：
原子操作（例如一个单一的全局变量），临界区。
内核模式下的方法有：
事件，信号量，互斥量。


# 什么是竞争条件？你怎样发现和解决竞争？

> 原文：[https://zwmst.com/2120.html](https://zwmst.com/2120.html)

当多个进程都企图对共享数据进行某种处理，而最后的结果又取决于进程运行的顺序时，则我们认为这发生了竞争条件（race condition）。


# 你将如何使用 thread dump？你将如何分析Thread dump？

> 原文：[https://zwmst.com/2122.html](https://zwmst.com/2122.html)

## 新建状态（New）

用 new 语句创建的线程处于新建状态，此时它和其他 Java 对象一样，仅仅在堆区中被分配了内存。

## 就绪状态（Runnable）

当一个线程对象创建后，其他线程调用它的 start()方法，该线程就进入就绪状态，Java虚拟机会为它创建方法调用栈和程序计数器。处于这个状态的线程位于可运行池中，等待获得 CPU 的使用权。

## 运行状态（Running）

处于这个状态的线程占用 CPU，执行程序代码。只有处于就绪状态的线程才有机会转到运行状态。

## 阻塞状态（Blocked）

阻塞状态是指线程因为某些原因放弃 CPU，暂时停止运行。当线程处于阻塞状态时，Java 虚拟机不会给线程分配 CPU。直到线程重新进入就绪状态，它才有机会转到运行状态。

## 阻塞状态可分为以下 3 种：

### 位于对象等待池中的阻塞状态（Blocked in object’s wait pool）：

当线程处于运行状态时，如果执行了某个对象的 wait()方法，Java 虚拟机就会
把线程放到这个对象的等待池中，这涉及到“线程通信”的内容。

### 位于对象锁池中的阻塞状态（Blocked in object’s lock pool）：

当线程处于运行状态时，试图获得某个对象的同步锁时，如果该对象的同步锁已经被其他线程占用，Java 虚拟机就会把这个线程放到这个对象的锁池中，这涉及到“线程同步”的内容。

### 其他阻塞状态（Otherwise Blocked）：

当前线程执行了 sleep()方法，或者调用了其他线程的 join()方法，或者发出了
I/O 请求时，就会进入这个状态。

## 死亡状态（Dead）

当线程退出 run()方法时，就进入死亡状态，该线程结束生命周期。


# 为什么我们调用 start()方法时会执行 run() 方法，为什么我们不能直接调用 run()方法？

> 原文：[https://zwmst.com/2124.html](https://zwmst.com/2124.html)

当你调用 start()方法时你将创建新的线程，并且执行在 run()方法里的代码。
但是如果你直接调用 run()方法，它不会创建新的线程也不会执行调用线程的代码，只会把 run 方法当作普通方法去执行。


# Java 中你怎样唤醒一个阻塞的线程？

> 原文：[https://zwmst.com/2126.html](https://zwmst.com/2126.html)

在 Java 发展史上曾经使用 suspend()、resume()方法对于线程进行阻塞唤醒，但随之出现很多问题，比较典型的还是死锁问题。
解决方案可以使用以对象为目标的阻塞，即利用 Object 类的 wait()和 notify()方法实现线程阻塞。
首 先 ，wait、notify 方法是针对对象的，调用任意对象的 wait()方法都将导致线程阻塞，阻塞的同时也将释放该对象的锁，相应地，调用任意对象的notify() 方法则将随机解除该对象阻塞的线程，但它需要重新获取改对象的 锁，直到获取成功才能往下执行；其次，wait、notify 方法必须在synchronized 块或方法中被调用，并且要保证同步块或方法的锁对象与调用wait、notify 方法的对象是同一个，如此一来在调用 wait 之前当前线程就已经成功获取某对象的锁，执行 wait 阻塞后当前线程就将之前获取的对象锁释放。


# 在 Java 中 CycliBarriar 和 CountdownLatch 有什么区别？

> 原文：[https://zwmst.com/2131.html](https://zwmst.com/2131.html)

CyclicBarrier 可以重复使用，而 CountdownLatch 不能重复使用。
Java 的 concurrent 包里面的 CountDownLatch 其实可以把它看作一个计数器，只不过这个计数器的操作是原子操作，同时只能有一个线程去操作这个计数器，也就是同时只能有一个线程去减这个计数器里面的值。
你可以向CountDownLatch 对象设置一个初始的数字作为计数值，任何调用这个对象上的await()方法都会阻塞，直到这个计数器的计数值被其他的线程减为 0 为止。所以在当前计数到达零之前，await 方法会一直受阻塞。之后，会释放所有等待的线程，await 的所有后续调用都将立即返回。这种现象只出现一次——计数无法被重置。如果需要重置计数，请考虑使用 CyclicBarrier。
CountDownLatch 的一个非常典型的应用场景是：有一个任务想要往下执行，但必须要等到其他的任务执行完毕后才可以继续往下执行。假如我们这个想要继续往下执行的任务调用一个 CountDownLatch 对象的 await()方法，其他的任务执行完自己的任务后调用同一个 CountDownLatch 对象上的 countDown()方法，这个调用 await()方法的任务将一直阻塞等待，直到这个 CountDownLatch 对象的计数值减到 0 为止。
CyclicBarrier 一个同步辅助类，它允许一组线程互相等待，直到到达某个公共屏障点 (common barrier point)。在涉及一组固定大小的线程的程序中，这些线程必须不时地互相等待，此时 CyclicBarrier 很有用。因为该 barrier 在释放等待线程后可以重用，所以称它为循环 的 barrier。


# 什么是不可变对象，它对写并发应用有什么帮助？

> 原文：[https://zwmst.com/2133.html](https://zwmst.com/2133.html)

**不可变对象(Immutable Objects)** 即对象一旦被创建它的状态（对象的数据，也即对象属性值）就不能改变，反之即为可变对象(Mutable Objects)。
**不可变对象的类即为不可变类(Immutable Class)。** Java 平台类库中包含许多不可变类，如 String、基本类型的包装类、BigInteger 和 BigDecimal 等。不可变对象天生是线程安全的。它们的常量（域）是在构造函数中创建的。既然它们的状态无法修改，这些常量永远不会变。
**不可变对象永远是线程安全的。
只有满足如下状态，一个对象才是不可变的；
它的状态不能在创建后再被修改；
所有域都是 final 类型；并且，它被正确创建（创建期间没有发生 this 引用的逸出）。


# 什么是多线程中的上下文切换

> 原文：[https://zwmst.com/2135.html](https://zwmst.com/2135.html)

在上下文切换过程中，CPU 会停止处理当前运行的程序，并保存当前程序运行的具体位置以便之后继续运行。从这个角度来看，上下文切换有点像我们同时阅读几本书，在来回切换书本的同时我们需要记住每本书当前读到的页码。在程序中，上下文切换过程中的“页码”信息是保存在进程控制块（PCB）中的。
PCB 还经常被称作“切换桢”（switchframe）。“页码”信息会一直保存到 CPU 的内存中，直到他们被再次使用。
上下文切换是存储和恢复 CPU 状态的过程，它使得线程执行能够从中断点恢复执行。上下文切换是多任务操作系统和多线程环境的基本特征。


# Java中用到的线程调度算法是什么？

> 原文：[https://zwmst.com/2137.html](https://zwmst.com/2137.html)

计算机通常只有一个 CPU,在任意时刻只能执行一条机器指令,每个线程只有获得 CPU 的使用权才能执行指令.所谓多线程的并发运行,其实是指从宏观上看, 各个线程轮流获得 CPU 的使用权,分别执行各自的任务.在运行池中,会有多个处于就绪状态的线程在等待 CPU,JAVA 虚拟机的一项任务就是负责线程的调度, 线程调度是指按照特定机制为多个线程分配 CPU 的使用权. 有两种调度模型：分时调度模型和抢占式调度模型。
分时调度模型是指让所有的线程轮流获得 cpu 的使用权,并且平均分配每个线程占用的 CPU 的时间片这个也比较好理解。
Java 虚拟机采用抢占式调度模型，是指优先让可运行池中优先级高的线程占用CPU，如果可运行池中的线程优先级相同，那么就随机选择一个线程，使其占用CPU。处于运行状态的线程会一直运行，直至它不得不放弃 CPU。


# 什么是线程组，为什么在 Java 中不推荐使用？

> 原文：[https://zwmst.com/2139.html](https://zwmst.com/2139.html)

线程组和线程池是两个不同的概念，他们的作用完全不同，前者是为了方便线程的管理，后者是为了管理线程的生命周期，复用线程，减少创建销毁线程的开销。


# 为什么使用 Executor 框架比使用应用创建和管理线程好？

> 原文：[https://zwmst.com/2141.html](https://zwmst.com/2141.html)

## 为什么要使用 Executor 线程池框架

*   1、 每次执行任务创建线程 new Thread()比较消耗性能，创建一个线程是比较耗时、耗资源的。
*   2、 调用 new Thread()创建的线程缺乏管理，被称为野线程，而且可以无限制的创建，线程之间的相互竞争会导致过多占用系统资源而导致系统瘫痪，还有线程之间的频繁交替也会消耗很多系统资源。
*   3、 直接使用 new Thread() 启动的线程不利于扩展，比如定时执行、定期执行、定时定期执行、线程中断等都不便实现。

    ## 使用 Executor 线程池框架的优点

*   1、 能复用已存在并空闲的线程从而减少线程对象的创建从而减少了消亡线程的 开销。
*   2、 可有效控制最大并发线程数，提高系统资源使用率，同时避免过多资源竞争。
*   3、 框架中已经有定时、定期、单线程、并发数控制等功能。
    综上所述使用线程池框架 Executor 能更好的管理线程、提供系统资源使用率。


# java 中有几种方法可以实现一个线程？

> 原文：[https://zwmst.com/2143.html](https://zwmst.com/2143.html)

*   继 承 Thread 类
*   实现 Runnable 接口
*   实现 Callable 接口，需要实现的是 call() 方法


# 如何停止一个正在运行的线程？

> 原文：[https://zwmst.com/2145.html](https://zwmst.com/2145.html)

## 使用共享变量的方式

在这种方式中，之所以引入共享变量，是因为该变量可以被多个执行相同任务的线程用来作为是否中断的信号，通知中断线程的执行。

## 使用 interrupt 方法终止线程

如果一个线程由于等待某些事件的发生而被阻塞，又该怎样停止该线程呢？这种情况经常会发生，比如当一个线程由于需要等候键盘输入而被阻塞，或者调用 Thread.join()方法，或者 Thread.sleep()方法，在网络中调用ServerSocket.accept()方法，或者调用了 DatagramSocket.receive()方法时，都有可能导致线程阻塞，使线程处于处于不可运行状态时，即使主程序中将该线程的共享变量设置为 true，但该线程此时根本无法检查循环标志，当然也就无法立即中断。这里我们给出的建议是，不要使用 stop()方法，而是使用 Thread 提供的 interrupt()方法，因为该方法虽然不会中断一个正在运行的线程，但是它可以使一个被阻塞的线程抛出一个中断异常，从而使线程提前结束阻塞状态，退出堵塞代码。


# notify()和 notifyAll()有什么区别？

> 原文：[https://zwmst.com/2147.html](https://zwmst.com/2147.html)

当一个线程进入 wait 之后，就必须等其他线程 notify/notifyall,使用notifyall, 可以唤醒所有处于 wait 状态的线程，使其重新进入锁的争夺队列中，而 notify 只能唤醒一个。
如果没把握，建议 notifyAll，防止 notigy 因为信号丢失而造成程序异常。


# 什么是 Daemon 线程？它有什么意义？

> 原文：[https://zwmst.com/2149.html](https://zwmst.com/2149.html)

所谓后台(daemon)线程，是指在程序运行的时候在后台提供一种通用服务的线程，并且这个线程并不属于程序中不可或缺的部分。因此，当所有的非后台线程结束时，程序也就终止了，同时会杀死进程中的所有后台线程。反过来说， 只要有任何非后台线程还在运行，程序就不会终止。必须在线程启动之前调用setDaemon()方法，才能把它设置为后台线程。
**注意**：后台进程在不执行finally 子句的情况下就会终止其 run()方法。
比如：JVM 的垃圾回收线程就是 Daemon 线程，Finalizer 也是守护线程。


# java 如何实现多线程之间的通讯和协作？

> 原文：[https://zwmst.com/2151.html](https://zwmst.com/2151.html)

中断 和 共享变量


# 什么是可重入锁（ReentrantLock）？

> 原文：[https://zwmst.com/2153.html](https://zwmst.com/2153.html)

## 举例来说明锁的可重入性

```
public class UnReentrant{ 
Lock lock = new Lock(); public void outer(){ lock.lock(); 
inner(); lock.unlock(); 
} 
public void inner(){ 
lock.lock(); 
//do something lock.unlock(); 
} }
```

outer 中调用了 inner，outer 先锁住了 lock，这样 inner 就不能再获取lock。其实调用 outer 的线程已经获取了 lock 锁，但是不能在 inner 中重复利用已经获取的锁资源，这种锁即称之为 不可重入可重入就意味着：**线程可以进入任何一个它已经拥有的锁所同步着的代码块。
synchronized、ReentrantLock 都是可重入的锁，可重入锁相对来说简化了并发编程的开发。


# 当一个线程进入某个对象的一个 synchronized 的实例方法后，其它线程是否可进入此对象的其它方法？

> 原文：[https://zwmst.com/2155.html](https://zwmst.com/2155.html)

如果其他方法没有 synchronized 的话，其他线程是可以进入的。
所以要开放一个线程安全的对象时，得保证每个方法都是线程安全的。


# 乐观锁和悲观锁的理解及如何实现，有哪些实现方式？

> 原文：[https://zwmst.com/2157.html](https://zwmst.com/2157.html)

## 悲观锁：

总是假设最坏的情况，每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会阻塞直到它拿到锁。
传统的关系型数据库里边就用到了很多这种锁机制，比如行锁，表锁等， 读锁，写锁等，都是在做操作之前先上锁。
再比如 Java 里面的同步原语 synchronized 关键字的实现也是悲观锁。

## 乐观锁：

顾名思义，就是很乐观，每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据，可以使用版本号等机制。
乐观锁适用于多读的应用类型，这样可以提高吞吐量，像数据库提供的类似于 write_condition 机制，其实都是提供的乐观锁。
在 Java 中 java.util.concurrent.atomic 包下面的原子变量类就是使用了乐观锁的一种实现方式 CAS 实现的。

## 乐观锁的实现方式：

*   1、 使用版本标识来确定读到的数据与提交时的数据是否一致。提交后修改版本标识，不一致时可以采取丢弃和再次尝试的策略。
*   2、 java 中的 Compare and Swap 即 CAS ，当多个线程尝试使用 CAS 同时更新同一个变量时，只有其中一个线程能更新变量的值，而其它线程都失败，失败的线程并不会被挂起，而是被告知这次竞争中失败，并可以再次尝试。 CAS 操作中包含三个操作数 —— 需要读写的内存位置（V）、进行比较的预期原值 （A）和拟写入的新值(B)。如果内存位置 V 的值与预期原值 A 相匹配，那么处理器会自动将该位置值更新为新值 B。否则处理器不做任何操作。

    ## CAS 缺点：

*   1、 ABA 问题：
    比如说一个线程 one 从内存位置 V 中取出 A，这时候另一个线程 two 也从内存中取出 A，并且 two 进行了一些操作变成了 B，然后 two 又将 V 位置的数据变成
    A，这时候线程 one 进行 CAS 操作发现内存中仍然是 A，然后 one 操作成功。尽
    管线程 one 的 CAS 操作成功，但可能存在潜藏的问题。
    从Java1.5 开始 JDK 的 atomic 包里提供了一个类 AtomicStampedReference 来解决 ABA 问题。
*   2、 循环时间长开销大：
    对于资源竞争严重（线程冲突严重）的情况，CAS 自旋的概率会比较大，从而浪费更多的 CPU 资源，效率低于 synchronized。
*   3、 只能保证一个共享变量的原子操作：
    当对一个共享变量执行操作时，我们可以使用循环 CAS 的方式来保证原子操作，但是对多个共享变量操作时，循环 CAS 就无法保证操作的原子性，这个时候就可以用锁。


# SynchronizedMap 和 ConcurrentHashMap 有什么区别？

> 原文：[https://zwmst.com/2159.html](https://zwmst.com/2159.html)

**SynchronizedMap** 一次锁住整张表来保证线程安全，所以每次只能有一个线程来访为 map。
**ConcurrentHashMap** 使用分段锁来保证在多线程下的性能。
ConcurrentHashMap 中则是一次锁住一个桶。ConcurrentHashMap 默认将 hash 表分为 16 个桶，诸如 get,put,remove 等常用操作只锁当前需要用到的桶。这样，原来只能一个线程进入，现在却能同时有 16 个写线程执行，并发性能的提升是显而易见的。
另外 ConcurrentHashMap 使用了一种不同的迭代方式。在这种迭代方式中，当
iterator 被创建后集合再发生改变就不再是抛出ConcurrentModificationException，取而代之的是在改变时 new 新的数据从而不影响原有的数据 ，iterator 完成后再将头指针替换为新的数据 ，这样iterator 线程可以使用原来老的数据，而写线程也可以并发的完成改变。


# CopyOnWriteArrayList 可以用于什么应用场景？

> 原文：[https://zwmst.com/2161.html](https://zwmst.com/2161.html)

**CopyOnWriteArrayList(免锁容器)** 的好处之一是当多个迭代器同时遍历和修改这个列表时，不会抛出 ConcurrentModificationException。
在 CopyOnWriteArrayList 中，写入将导致创建整个底层数组的副本，而源数组将保留在原地，使得复制的数组在被修改时，读取操作可以安全地执行。

*   1、 由于写操作的时候，需要拷贝数组，会消耗内存，如果原数组的内容比较多 的情况下，可能导致 young gc 或者 full gc；
*   2、 不能用于实时读的场景，像拷贝数组、新增元素都需要时间，所以调用一个set 操作后，读取到数据可能还是旧的,虽然 CopyOnWriteArrayList 能做到最终一致性,但是还是没法满足实时性要求；

    ## CopyOnWriteArrayList 透露的思想

*   1、 读写分离，读和写分开
*   2、 最终一致性
*   3、 使用另外开辟空间的思路，来解决并发冲突


# 什么叫线程安全？servlet 是线程安全吗

> 原文：[https://zwmst.com/2163.html](https://zwmst.com/2163.html)

线程安全是编程中的术语，指某个函数、函数库在多线程环境中被调用时，能够正确地处理多个线程之间的共享变量，使程序功能正确完成。
Servlet 不是线程安全的，servlet 是单实例多线程的，当多个线程同时访问同一个方法，是不能保证共享变量的线程安全性的。
Struts2 的 action 是多实例多线程的，是线程安全的，每个请求过来都会new 一个新的 action 分配给这个请求，请求完成后销毁。
SpringMVC 的 Controller 是线程安全的吗？不是的，和 Servlet 类似的处理流程。
Struts2 好处是不用考虑线程安全问题；Servlet 和 SpringMVC 需要考虑线程安全问题，但是性能可以提升不用处理太多的 gc，可以使用 ThreadLocal 来处理多线程的问题。


# volatile 有什么用？能否用一句话说明下 volatile 的应用场景？

> 原文：[https://zwmst.com/2165.html](https://zwmst.com/2165.html)

volatile 保证内存可见性和禁止指令重排。
volatile 用于多线程环境下的单次操作(单次读或者单次写)。


# 为什么代码会重排序？

> 原文：[https://zwmst.com/2167.html](https://zwmst.com/2167.html)

在执行程序时，为了提供性能，处理器和编译器常常会对指令进行重排序，但是不能随意重排序，不是你想怎么排序就怎么排序，它需要满足以下两个条件：

*   在单线程环境下不能改变程序运行的结果；
*   存在数据依赖关系的不允许重排序

    ## 需要注意的是：

    重排序不会影响单线程环境的执行结果，但是会破坏多线程的执行语义。


# 在 java 中 wait 和 sleep 方法的不同？

> 原文：[https://zwmst.com/2169.html](https://zwmst.com/2169.html)

最大的不同是在等待时 wait 会释放锁，而 sleep 一直持有锁。
Wait 通常被用于线程间交互，sleep 通常被用于暂停执行。


# 一个线程运行时发生异常会怎样

> 原文：[https://zwmst.com/2171.html](https://zwmst.com/2171.html)

如果异常没有被捕获该线程将会停止执行。
Thread.UncaughtExceptionHandler 是用于处理未捕获异常造成线程突然中断情况的一个内嵌接口。
当一个未捕获异常将造成线程中断的时候 JVM 会使用Thread.getUncaughtExceptionHandler()来查询线程的UncaughtExceptionHandler 并将线程和异常作为参数传递给 handler 的 uncaughtException()方法进行处理。


# 如何在两个线程间共享数据

> 原文：[https://zwmst.com/2173.html](https://zwmst.com/2173.html)

在两个线程间共享变量即可实现共享。
一般来说，共享变量要求变量本身是线程安全的，然后在线程内使用的时候，如果有对共享变量的复合操作，那么也得保证复合操作的线程安全性。


# Java 中 notify 和 notifyAll 有什么区别？

> 原文：[https://zwmst.com/2175.html](https://zwmst.com/2175.html)

notify() 方法不能唤醒某个具体的线程，所以只有一个线程在等待的时候它才有用武之地。而 notifyAll()唤醒所有线程并允许他们争夺锁确保了至少有一个线程能继续运行。


# 为什么 wait, notify 和 notifyAll 这些方法不在 thread 类里面？

> 原文：[https://zwmst.com/2177.html](https://zwmst.com/2177.html)

一个很明显的原因是 JAVA 提供的锁是对象级的而不是线程级的，每个对象都有锁，通过线程获得。
由于 wait，notify 和 notifyAll 都是锁级别的操作， 所以把他们定义在 Object 类中因为锁属于对象。


# 什么是 ThreadLocal 变量？

> 原文：[https://zwmst.com/2179.html](https://zwmst.com/2179.html)

**ThreadLocal 是 Java 里一种特殊的变量。** 每个线程都有一个 ThreadLocal 就是每个线程都拥有了自己独立的一个变量，竞争条件被彻底消除了。
它是为创建代价高昂的对象获取线程安全的好方法，比如你可以用 ThreadLocal 让SimpleDateFormat 变成线程安全的，因为那个类创建代价高昂且每次调用都需要创建不同的实例所以不值得在局部范围使用它，如果为每个线程提供一个自己独有的变量拷贝，将大大提高效率。
首先，通过复用减少了代价高昂的对象的创建个数。
其次，你在没有使用高代价的同步或者不变性的情况下获得了线程安全。


# Java 中 interrupted 和 isInterrupted 方 法 的区别？

> 原文：[https://zwmst.com/2185.html](https://zwmst.com/2185.html)

## interrupt

interrupt 方法用于中断线程。调用该方法的线程的状态为将被置为”中断” 状态。
**注意：** 线程中断仅仅是置线程的中断状态位，不会停止线程。需要用户自己去监视线程的状态为并做处理。
支持线程中断的方法（也就是线程中断后会抛出 interruptedException 的方法）就是在监视线程的中断状态，一旦线程的中断状态被置为“中断状态”，就会抛出中断异常。

## interrupted

查询当前线程的中断状态，并且清除原状态。
如果一个线程被中断了，第一次调用 interrupted 则返回 true，第二次和后面的就返回 false 了。
isInterrupted 仅仅是查询当前线程的中断状态


# 为什么 wait 和 notify 方法要在同步块中调用？

> 原文：[https://zwmst.com/2187.html](https://zwmst.com/2187.html)

Java API 强制要求这样做，如果你不这么做，你的代码会抛出IllegalMonitorStateException 异常。还有一个原因是为了避免 wait 和notify 之间产生竞态条件。


# 为什么你应该在循环中检查等待条件

> 原文：[https://zwmst.com/2189.html](https://zwmst.com/2189.html)

处于等待状态的线程可能会收到错误警报和伪唤醒，如果不在循环中检查等待条件，程序就会在没有满足结束条件的情况下退出。


# Java 中的同步集合与并发集合有什么区别

> 原文：[https://zwmst.com/2191.html](https://zwmst.com/2191.html)

同步集合与并发集合都为多线程和并发提供了合适的线程安全的集合，不过并发集合的可扩展性更高。
在 Java1.5 之前程序员们只有同步集合来用且在多线程并发的时候会导致争用，阻碍了系统的扩展性。
Java5 介绍了并发集合像ConcurrentHashMap，不仅提供线程安全还用锁分离和内部分区等现代技术提高了可扩展性。


# 什么是线程池？ 为什么要使用它？

> 原文：[https://zwmst.com/2193.html](https://zwmst.com/2193.html)

创建线程要花费昂贵的资源和时间，如果任务来了才创建线程那么响应时间会变长，而且一个进程能创建的线程数有限。
为了避免这些问题，在程序启动的时候就创建若干线程来响应处理，它们被称为线程池，里面的线程叫工作线程。
从 JDK1.5 开始，Java API 提供了 Executor 框架让你可以创建不同的线程池。


# 怎么检测一个线程是否拥有锁？

> 原文：[https://zwmst.com/2195.html](https://zwmst.com/2195.html)

在 java.lang.Thread 中有一个方法叫 holdsLock()，它返回 true 如果当且仅当当前线程拥有某个具体对象的锁。


# JVM 中哪个参数是用来控制线程的栈堆栈小的

> 原文：[https://zwmst.com/2197.html](https://zwmst.com/2197.html)

**-Xss** 每个线程的栈大小


# Thread 类中的 yield 方法有什么作用

> 原文：[https://zwmst.com/2199.html](https://zwmst.com/2199.html)

使当前线程从执行状态（运行状态）变为可执行态（就绪状态）。
当前线程到了就绪状态，那么接下来哪个线程会从就绪状态变成执行状态呢？可能是当前线程，也可能是其他线程，看系统的分配了。


# Java 中 ConcurrentHashMap 的并发度是什么？

> 原文：[https://zwmst.com/2201.html](https://zwmst.com/2201.html)

ConcurrentHashMap 把实际 map 划分成若干部分来实现它的可扩展性和线程安全。这种划分是使用并发度获得的，它是 ConcurrentHashMap 类构造函数的一个可选参数，默认值为 16，这样在多线程情况下就能避免争用。
在 JDK8 后，它摒弃了 Segment（锁段）的概念，而是启用了一种全新的方式实现, 利用 CAS 算法。同时加入了更多的辅助变量来提高并发度，具体内容还是查看源码吧


# Java 中 Semaphore 是什么？

> 原文：[https://zwmst.com/2203.html](https://zwmst.com/2203.html)

Java 中的 Semaphore 是一种新的同步类，它是一个计数信号。
从概念上讲，信号量维护了一个许可集合。
如有必要，在许可可用前会阻塞每一个 acquire()，然后再获取该许可。
每个 release()添加一个许可，从而可能释放一个正在阻塞的获取者。
但是，不使用实际的许可对象，Semaphore 只对可用许可的号码进行计数，并采取相应的行动。
信号量常常用于多线程的代码中，比如数据库连接池。


# Java 线程池中 submit() 和 execute()方法有什么区别？

> 原文：[https://zwmst.com/2205.html](https://zwmst.com/2205.html)

两个方法都可以向线程池提交任务，execute()方法的返回类型是 void，它定义在 Executor 接口中。
而 submit()方法可以返回持有计算结果的 Future 对象，它定义在ExecutorService 接口中，它扩展了 Executor 接口，其它线程池类像ThreadPoolExecutor 和 ScheduledThreadPoolExecutor 都有这些方法。


# 什么是阻塞式方法？

> 原文：[https://zwmst.com/2207.html](https://zwmst.com/2207.html)

阻塞式方法是指程序会一直等待该方法完成期间不做其他事情，ServerSocket 的 accept()方法就是一直等待客户端连接。
这里的阻塞是指调用结果返回之前，当前线程会被挂起，直到得到结果之后才会返回。 此外，还有异步和非阻塞式方法在任务完成前就返回。


# Java 中的 ReadWriteLock 是什么？

> 原文：[https://zwmst.com/2209.html](https://zwmst.com/2209.html)

读写锁是用来提升并发程序性能的锁分离技术的成果。


# volatile 变量和 atomic 变量有什么不同？

> 原文：[https://zwmst.com/2211.html](https://zwmst.com/2211.html)

Volatile 变量可以确保先行关系，即写操作会发生在后续的读操作之前, 但它并不能保证原子性。例如用 volatile 修饰 count 变量那么 count++ 操作就不是原子性的。
而 AtomicInteger 类提供的 atomic 方法可以让这种操作具有原子性如getAndIncrement()方法会原子性的进行增量操作把当前值加一，其它数据类型和引用变量也可以进行相似操作。


# 可以直接调用 Thread 类的 run ()方法么？

> 原文：[https://zwmst.com/2213.html](https://zwmst.com/2213.html)

当然可以。但是如果我们调用了 Thread 的 run()方法，它的行为就会和普通的方法一样，会在当前线程中执行。
为了在新的线程中执行我们的代码，必须使用 Thread.start()方法。


# 如何让正在运行的线程暂停一段时间？

> 原文：[https://zwmst.com/2215.html](https://zwmst.com/2215.html)

我们可以使用 Thread 类的 Sleep()方法让线程暂停一段时间。
需要注意的是，这并不会让线程终止，一旦从休眠中唤醒线程，线程的状态将会被改变为Runnable，并且根据线程调度，它将得到执行。


# 你对线程优先级的理解是什么？

> 原文：[https://zwmst.com/2217.html](https://zwmst.com/2217.html)

每一个线程都是有优先级的，一般来说，高优先级的线程在运行时会具有优先权，但这依赖于线程调度的实现，这个实现是和操作系统相关的(OS dependent)。
我们可以定义线程的优先级，但是这并不能保证高优先级的线程会在低优先级的线程前执行。
线程优先级是一个 int 变量(从 1-10)，1 代表最低优先级，10 代表最高优先级。
java 的线程优先级调度会委托给操作系统去处理，所以与具体的操作系统优先级有关，如非特别需要，一般无需设置线程优先级。


# 什么是线程调度器(Thread Scheduler)和时间分片 (Time Slicing )？

> 原文：[https://zwmst.com/2219.html](https://zwmst.com/2219.html)

线程调度器是一个操作系统服务，它负责为 Runnable 状态的线程分配 CPU 时间。
一旦我们创建一个线程并启动它，它的执行便依赖于线程调度器的实现。
同上一个问题，线程调度并不受到 Java 虚拟机控制，所以由应用程序来控制它是更
好的选择（也就是说不要让你的程序依赖于线程的优先级）。
时间分片是指将可用的 CPU 时间分配给可用的 Runnable 线程的过程。
分配CPU 时间可以基于线程优先级或者线程等待的时间。


# 你如何确保 main()方法所在的线程是 Java 程 序最后结束的线程？

> 原文：[https://zwmst.com/2221.html](https://zwmst.com/2221.html)

我们可以使用 Thread 类的 join()方法来确保所有程序创建的线程在 main() 方法退出前结束。


# 线程之间是如何通信的？

> 原文：[https://zwmst.com/2225.html](https://zwmst.com/2225.html)

当线程间是可以共享资源时，线程间通信是协调它们的重要的手段。
Object 类中 **wait()\notify()\notifyAll()方法**可以用于线程间通信关于资源的锁的状态。


# 为什么线程通信的方法 wait(), notify()和 notifyAll()被定义在 Object 类里

> 原文：[https://zwmst.com/2227.html](https://zwmst.com/2227.html)

Java 的每个对象中都有一个锁(monitor，也可以成为监视器) 并且 wait()， notify()等方法用于等待对象的锁或者通知其他线程对象的监视器可用。
**在Java的线程中并没有可供任何对象使用的锁和同步器。
这就是为什么这些方法是 Object 类的一部分，这样 Java 的每一个类都有用于线程间通信的基本方法。


# 为什么 wait(), notify()和 notifyAll ()必须在同步方法或者同步块中被调用？

> 原文：[https://zwmst.com/2229.html](https://zwmst.com/2229.html)

当一个线程需要调用对象的 wait()方法的时候，这个线程必须拥有该对象的锁，接着它就会释放这个对象锁并进入等待状态直到其他线程调用这个对象上的 notify()方法。
同样的，当一个线程需要调用对象的 notify()方法时，它会释放这个对象的锁，以便其他在等待的线程就可以得到这个对象锁。
由于所有的这些方法都需要线程持有对象的锁，这样就只能通过同步来实现，所以他们只能在同步方法或者同步块中被调用。


# 为什么 Thread 类的 sleep()和 yield ()方法是静态的？

> 原文：[https://zwmst.com/2231.html](https://zwmst.com/2231.html)

**Thread 类的 sleep()和 yield()方法将在当前正在执行的线程上运行。
所以在其他处于等待状态的线程上调用这些方法是没有意义的.这就是为什么这些方法是静态的。
它们可以在当前正在执行的线程中工作，并避免程序员错误的认为可以在其他非运行线程调用这些方法。


# 如何确保线程安全？

> 原文：[https://zwmst.com/2233.html](https://zwmst.com/2233.html)

在 Java 中可以有很多方法来保证线程安全——同步，使用原子类(atomic concurrent classes)，实现并发锁，使用 volatile 关键字，使用不变类和线程安全类。


# 同步方法和同步块，哪个是更好的选择？

> 原文：[https://zwmst.com/2235.html](https://zwmst.com/2235.html)

同步块是更好的选择，因为它不会锁住整个对象（当然你也可以让它锁住整个对象）。
同步方法会锁住整个对象，哪怕这个类中有多个不相关联的同步块，这通常会导致他们停止执行并需要等待获得这个对象上的锁。
同步块更要符合开放调用的原则，只在需要锁住的代码块锁住相应的对象，这样从侧面来说也可以避免死锁。


# 如何创建守护线程？

> 原文：[https://zwmst.com/2237.html](https://zwmst.com/2237.html)

使用 Thread 类的 setDaemon(true)方法可以将线程设置为守护线程，需要注意的是，需要在调用 start()方法前调用这个方法，否则会抛出IllegalThreadStateException 异常。


# 什么是 Java Timer 类？如何创建一个有特定时间间隔的任务？

> 原文：[https://zwmst.com/2239.html](https://zwmst.com/2239.html)

**java.util.Timer** 是一个工具类，可以用于安排一个线程在未来的某个特定时间
执行。
**Timer** 类可以用安排一次性任务或者周期任务。
**java.util.TimerTask** 是一个实现了 Runnable 接口的抽象类，我们需要去继承这个类来创建我们自己的定时任务并使用 Timer 去安排它的执行。


# 673.现在有 T1、T2、T3 三个线程，你怎样保证 T2 在 T1 执行完后执行，T3 在 T2 执行完后执行？

> 原文：[https://zwmst.com/4515.html](https://zwmst.com/4515.html)

这个线程问题通常会在第一轮或电话面试阶段被问到，目的是检测你对”join”方法是否熟悉。这个多线程问题比较简单，可以用 join 方法实现。


# 674.在 Java 中 Lock 接口比 synchronized 块的优势是什么？你需要实现一个高效的缓存，它允 许多个用户读，但只允许一个用户写，以此来保持它的完整性，你会怎样去实现它？

> 原文：[https://zwmst.com/4517.html](https://zwmst.com/4517.html)

lock 接口在多线程和并发编程中最大的优势是它们为读和写分别提供了锁，它能满足你写像 ConcurrentHashMap 这样的高性能数据结构和有条件的阻塞。Java 线程面试的问题越来越会根据面试者的回答来提问。我强烈建议在你去参加多线程的面试之前认真读一下Locks，因为当前其大量用于构建电子交易终统的客户端缓存和交易连接空间。


# 675.在 java 中 wait 和 sleep 方法的不同？

> 原文：[https://zwmst.com/4519.html](https://zwmst.com/4519.html)

通常会在电话面试中经常被问到的 Java 线程面试问题。最大的不同是在等待时 wait 会释放锁，而 sleep 一直持有锁。Wait 通常被用于线程间交互，sleep 通常被用于暂停执行。


# 676.用 Java 实现阻塞队列

> 原文：[https://zwmst.com/4521.html](https://zwmst.com/4521.html)

这是一个相对艰难的多线程面试问题，它能达到很多的目的。第一，它可以检测侯选者是否能实际的用 Java 线程写程序；第二，可以检测侯选者对并发场景的理解，并且你可以根据这个问很多问题。如果他用 wait()和 notify()方法来实现阻塞队列，你可以要求他用最新的 Java 5 中的并发类来再写一次。


# 677.用 Java 写代码来解决生产者——消费者问题。

> 原文：[https://zwmst.com/4523.html](https://zwmst.com/4523.html)

与上面的问题很类似，但这个问题更经典，有些时候面试都会问下面的问题。在 Java 中怎么解决生产者——消费者问题，当然有很多解决方法，我已经分享了一种用阻塞队列实现的方法。有些时候他们甚至会问怎么实现哲学家进餐问题。


# 678.用 Java 编程一个会导致死锁的程序，你将怎么解决

> 原文：[https://zwmst.com/4525.html](https://zwmst.com/4525.html)

这是我最喜欢的 Java 线程面试问题，因为即使死锁问题在写多线程并发程序时非常普遍，但是很多侯选者并不能写 deadlock free code（无死锁代码？），他们很挣扎。只要告诉他们，你有 N 个资源和 N 个线程，并且你需要所有的资源来完成一个操作。为了简单这里的n 可以替换为 2，越大的数据会使问题看起来更复杂。通过避免 Java 中的死锁来得到关于死锁的更多信息。


# 679.什么是原子操作，Java 中的原子操作是什么？

> 原文：[https://zwmst.com/4527.html](https://zwmst.com/4527.html)

非常简单的 java 线程面试问题，接下来的问题是你需要同步一个原子操作。


# 680.Java 中的 volatile 关键是什么作用？怎样使用它？在 Java 中它跟 synchronized 方法有什 么不同？

> 原文：[https://zwmst.com/4529.html](https://zwmst.com/4529.html)

自从 Java 5 和 Java 内存模型改变以后，基于 volatile 关键字的线程问题越来越流行。应该准备好回答关于 volatile 变量怎样在并发环境中确保可见性。


# 681.什么是竞争条件？你怎样发现和解决竞争？

> 原文：[https://zwmst.com/4531.html](https://zwmst.com/4531.html)

这是一道出现在多线程面试的高级阶段的问题。大多数的面试官会问最近你遇到的竞争条件，以及你是怎么解决的。有些时间他们会写简单的代码，然后让你检测出代码的竞争条件。可以参考我之前发布的关于 Java 竞争条件的文章。在我看来这是最好的 java 线程面试问题之一，它可以确切的检测候选者解决竞争条件的经验，or writing code which is free ofdata race or anyother race condition。关于这方面最好的书是《Concurrency practices in Java》。


# 682.你将如何使用 threaddump？你将如何分析 Thread dump？

> 原文：[https://zwmst.com/4533.html](https://zwmst.com/4533.html)

在 UNIX 中你可以使用 kill -3，然后 thread dump 将会打印日志，在 windows 中你可以使用”CTRL+Break”。非常简单和专业的线程面试问题，但是如果他问你怎样分析它，就会很棘手。


# 683.为什么我们调用 start()方法时会执行 run()方法，为什么我们不能直接调用 run()方法？

> 原文：[https://zwmst.com/4535.html](https://zwmst.com/4535.html)

这是另一个非常经典的 java 多线程面试问题。这也是我刚开始写线程程序时候的困惑。现在这个问题通常在电话面试或者是在初中级 Java 面试的第一轮被问到。这个问题的回答应该是这样的，当你调用 start()方法时你将创建新的线程，并且执行在 run()方法里的代码。但是如果你直接调用 run()方法，它不会创建新的线程也不会执行调用线程的代码。阅读我之前写的《start 与 run 方法的区别》这篇文章来获得更多信息。


# 684.Java 中你怎样唤醒一个阻塞的线程？

> 原文：[https://zwmst.com/4537.html](https://zwmst.com/4537.html)

这是个关于线程和阻塞的棘手的问题，它有很多解决方法。如果线程遇到了 IO 阻塞，我并且不认为有一种方法可以中止线程。如果线程因为调用 wait()、sleep()、或者 join()方法而导致的阻塞，你可以中断线程，并且通过抛出 InterruptedException 来唤醒它。我之前写的《How to deal with blocking methods in java》有很多关于处理线程阻塞的信息。


# 685.在 Java 中 CycliBarriar 和 CountdownLatch 有什么区别？

> 原文：[https://zwmst.com/4539.html](https://zwmst.com/4539.html)

这个线程问题主要用来检测你是否熟悉 JDK5 中的并发包。这两个的区别是 CyclicBarrier 可以重复使用已经通过的障碍，而 CountdownLatch 不能重复使用。


# 686.什么是不可变对象，它对写并发应用有什么帮助？

> 原文：[https://zwmst.com/4541.html](https://zwmst.com/4541.html)

另一个多线程经典面试问题，并不直接跟线程有关，但间接帮助很多。这个 java 面试问题可以变的非常棘手，如果他要求你写一个不可变对象，或者问你为什么 String 是不可变的。


# 687.你在多线程环境中遇到的常见的问题是什么？你是怎么解决它的？

> 原文：[https://zwmst.com/4543.html](https://zwmst.com/4543.html)

多线程和并发程序中常遇到的有 Memory-interface、竞争条件、死锁、活锁和饥饿。问题是没有止境的，如果你弄错了，将很难发现和调试。这是大多数基于面试的，而不是基于实际应用的 Java 线程问题


# 688.Synchronized 用 过 吗 ， 其 原 理 是 什 么 ？

> 原文：[https://zwmst.com/4545.html](https://zwmst.com/4545.html)

这 是 一 道 Java 面 试 中 几 乎 百 分 百 会 问 到 的 问 题 ， 因 为 没 有 任 何 写 过 并 发 程 序 的 开 发 者 会 没 听 说 或 者 没 接 触 过 Synchronized。
Synchronized 是 由 JVM 实 现 的 一 种 实 现 互 斥 同 步 的 一 种 方 式 ， 如 果 你 查 看 被 Synchronized 修 饰 过 的 程 序 块 编 译 后 的 字 节 码 ， 会 发 现 ，被 Synchronized 修 饰 过 的 程 序 块 ， 在 编 译 前 后 被 编 译 器 生 成 了 monitorenter 和 monitorexit 两 个 字 节 码 指 令 。

这 两 个 指 令 是 什 么 意 思 呢 ？

在 虚 拟 机 执 行 到 monitorenter 指 令 时 ， 首 先 要 尝 试 获 取 对 象 的 锁 ：
如 果 这 个 对 象 没 有 锁 定 ， 或 者 当 前 线 程 已 经 拥 有 了 这 个 对 象 的 锁 ， 把 锁 的 计 数 器 +1； 当 执 行 monitorexit 指 令 时 将 锁 计 数 器 -1； 当 计 数 器 为 0 时 ， 锁 就 被 释 放 了 。
如 果 获 取 对 象 失 败 了 ， 那 当 前 线 程 就 要 阻 塞 等 待 ， 直 到 对 象 锁 被 另 外 一 个 线 程 释 放 为 止 。
Java 中 Synchronize 通 过 在 对 象 头 设 置 标 记 ， 达 到 了 获 取 锁 和 释 放 锁 的 目 的 。


# 689.你 刚 才 提 到 获 取 对 象 的 锁 ， 这 个 “ 锁 ” 到 底 是 什 么 ？ 如 何 确 定 对 象 的 锁

> 原文：[https://zwmst.com/4547.html](https://zwmst.com/4547.html)

“ 锁 ” 的 本 质 其 实 是 monitorenter 和 monitorexit 字 节 码 指 令 的 一 个 Reference 类 型 的 参 数 ， 即 要 锁 定 和 解 锁 的 对 象 。 我 们 知 道 ， 使 用 Synchronized 可 以 修 饰 不 同 的 对 象 ， 因 此 ， 对 应 的 对 象 锁 可 以 这 么 确 定 。

1.  如 果 Synchronized 明 确 指 定 了 锁 对 象 ， 比 如 Synchronized（ 变 量 名 ） 、 Synchronized(this) 等 ， 说 明 加 解 锁 对 象 为 该 对 象 。
2.  如 果 没 有 明 确 指 定 ：
    若 Synchronized 修 饰 的 方 法 为 非 静 态 方 法 ， 表 示 此 方 法 对 应 的 对 象 为 锁 对 象 ；
    若 Synchronized 修 饰 的 方 法 为 静 态 方 法 ， 则 表 示 此 方 法 对 应 的 类 对 象 为 锁 对 象 。

注 意 ， 当 一 个 对 象 被 锁 住 时 ， 对 象 里 面 所 有 用 Synchronized 修 饰 的 方 法 都 将 产 生 堵 塞 ， 而 对 象 里 非 Synchronized 修 饰 的 方 法 可 正 常 被 调 用 ， 不 受 锁 影 响 。


# 690.什 么 是 可 重 入 性 ， 为 什 么 说 Synchronized 是 可 重 入 锁 ？

> 原文：[https://zwmst.com/4549.html](https://zwmst.com/4549.html)

可 重 入 性 是 锁 的 一 个 基 本 要 求 ， 是 为 了 解 决 自 己 锁 死 自 己 的 情 况 。比 如 下 面 的 伪 代 码 ， 一 个 类 中 的 同 步 方 法 调 用 另 一 个 同 步 方 法 ， 假 如 Synchronized 不 支 持 重 入 ， 进 入 method2 方 法 时 当 前 线 程 获 得 锁 ，method2 方 法 里 面 执 行 method1 时 当 前 线 程 又 要 去 尝 试 获 取 锁 ， 这 时 如 果 不 支 持 重 入 ， 它 就 要 等 释 放 ， 把 自 己 阻 塞 ， 导 致 自 己 锁 死 自 己 。

对 Synchronized 来 说 ， 可 重 入 性 是 显 而 易 见 的 ， 刚 才 提 到 ， 在 执 行 monitorenter 指 令 时 ， 如 果 这 个 对 象 没 有 锁 定 ， 或 者 当 前 线 程 已 经 拥 有 了 这 个 对 象 的 锁 （ 而 不 是 已 拥 有 了 锁 则 不 能 继 续 获 取 ） ， 就 把 锁 的 计 数 器 +1， 其 实 本 质 上 就 通 过 这 种 方 式 实 现 了 可 重 入 性 。


# 691.JVM 对 Java 的 原 生 锁 做 了 哪 些 优 化 ？

> 原文：[https://zwmst.com/4551.html](https://zwmst.com/4551.html)

在 Java 6 之 前 ， Monitor 的 实 现 完 全 依 赖 底 层 操 作 系 统 的 互 斥 锁 来 实 现 ， 也 就 是 我 们 刚 才 在 问 题 二 中 所 阐 述 的 获 取 /释 放 锁 的 逻 辑 。

由 于 Java 层 面 的 线 程 与 操 作 系 统 的 原 生 线 程 有 映 射 关 系 ， 如 果 要 将 一 个 线 程 进 行 阻 塞 或 唤 起 都 需 要 操 作 系 统 的 协 助 ， 这 就 需 要 从 用 户 态 切 换 到 内 核 态 来 执 行 ， 这 种 切 换 代 价 十 分 昂 贵 ， 很 耗 处 理 器 时 间 ， 现 代 JDK 中 做 了 大 量 的 优 化 。

一 种 优 化 是 使 用 自 旋 锁 ， 即 在 把 线 程 进 行 阻 塞 操 作 之 前 先 让 线 程 自 旋 等 待 一 段 时 间 ， 可 能 在 等 待 期 间 其 他 线 程 已 经 解 锁 ， 这 时 就 无 需 再 让 线 程 执 行 阻 塞 操 作 ， 避 免 了 用 户 态 到 内 核 态 的 切 换 。现 代 JDK 中 还 提 供 了 三 种 不 同 的 Monitor 实 现 ， 也 就 是 三 种 不 同 的 锁 ：

1.  偏 向 锁 （ Biased Locking）
2.  轻 量 级 锁
3.  重 量 级 锁

这 三 种 锁 使 得 JDK 得 以 优 化 Synchronized 的 运 行 ， 当 JVM 检 测 到 不 同 的 竞 争 状 况 时 ， 会 自 动 切 换 到 适 合 的 锁 实 现 ， 这 就 是 锁 的 升 级 、降 级 。

1.  当 没 有 竞 争 出 现 时 ， 默 认 会 使 用 偏 向 锁 。
    JVM 会 利 用 CAS 操 作 ， 在 对 象 头 上 的 Mark Word 部 分 设 置 线 程 ID， 以 表 示 这 个 对 象 偏 向 于 当 前 线 程 ， 所 以 并 不 涉 及 真 正 的 互 斥 锁 ， 因 为 在 很 多 应 用 场 景 中 ， 大 部 分 对 象 生 命 周 期 中 最 多 会 被 一 个 线 程 锁 定 ，使 用 偏 斜 锁 可 以 降 低 无 竞 争 开 销 。

2.  如 果 有 另 一 线 程 试 图 锁 定 某 个 被 偏 斜 过 的 对 象 ， JVM 就 撤 销 偏 斜 锁 ，切 换 到 轻 量 级 锁 实 现 。

3.  轻 量 级 锁 依 赖 CAS 操 作 Mark Word 来 试 图 获 取 锁 ， 如 果 重 试 成 功 ，就 使 用 普 通 的 轻 量 级 锁 ； 否 则 ， 进 一 步 升 级 为 重 量 级 锁 。


# 692\. 为 什 么 说 Synchronized 是 非 公 平 锁 ？

> 原文：[https://zwmst.com/4553.html](https://zwmst.com/4553.html)

非 公 平 主 要 表 现 在 获 取 锁 的 行 为 上 ， 并 非 是 按 照 申 请 锁 的 时 间 前 后 给 等待 线 程 分 配 锁 的 ， 每 当 锁 被 释 放 后 ， 任 何 一 个 线 程 都 有 机 会 竞 争 到 锁 ，这 样 做 的 目 的 是 为 了 提 高 执 行 性 能 ， 缺 点 是 可 能 会 产 生 线 程 饥 饿 现 象 。


# 693.什 么 是 锁 消 除 和 锁 粗 化 ？

> 原文：[https://zwmst.com/4555.html](https://zwmst.com/4555.html)

1.  锁 消 除 ： 指 虚 拟 机 即 时 编 译 器 在 运 行 时 ， 对 一 些 代 码 上 要 求 同 步 ， 但 被 检 测 到 不 可 能 存 在 共 享 数 据 竞 争 的 锁 进 行 消 除 。 主 要 根 据 逃 逸 分 析 。程 序 员 怎 么 会 在 明 知 道 不 存 在 数 据 竞 争 的 情 况 下 使 用 同 步 呢 ？ 很 多 不 是程 序 员 自 己 加 入 的 。
2.  锁 粗 化 ： 原 则 上 ， 同 步 块 的 作 用 范 围 要 尽 量 小 。 但 是 如 果 一 系 列 的 连 续 操 作 都 对 同 一 个 对 象 反 复 加 锁 和 解 锁 ， 甚 至 加 锁 操 作 在 循 环 体 内 ， 频 繁 地 进 行 互 斥 同 步 操 作 也 会 导 致 不 必 要 的 性 能 损 耗 。 锁 粗 化 就 是 增 大 锁 的 作 用 域


# 694.为 什 么 说 Synchronized 是 一 个 悲 观 锁 ？ 乐 观 锁 的 实 现 原 理 又 是 什 么 ？ 什 么 是 CAS， 它 有 什 么 特 性 ？

> 原文：[https://zwmst.com/4557.html](https://zwmst.com/4557.html)

Synchronized 显 然 是 一 个 悲 观 锁 ， 因 为 它 的 并 发 策 略 是 悲 观 的 ：

不 管 是 否 会 产 生 竞 争 ， 任 何 的 数 据 操 作 都 必 须 要 加 锁 、 用 户 态 核 心 态 转换 、 维 护 锁 计 数 器 和 检 查 是 否 有 被 阻 塞 的 线 程 需 要 被 唤 醒 等 操 作 。随 着 硬 件 指 令 集 的 发 展 ， 我 们 可 以 使 用 基 于 冲 突 检 测 的 乐 观 并 发 策 略 。

先 进 行 操 作 ， 如 果 没 有 其 他 线 程 征 用 数 据 ， 那 操 作 就 成 功 了 ；

如 果 共 享 数 据 有 征 用 ， 产 生 了 冲 突 ， 那 就 再 进 行 其 他 的 补 偿 措 施 。 这 种乐 观 的 并 发 策 略 的 许 多 实 现 不 需 要 线 程 挂 起 ， 所 以 被 称 为 非 阻 塞 同 步 。乐 观 锁 的 核 心 算 法 是 CAS（ Compareand Swap， 比 较 并 交 换 ） ， 它 涉 及 到 三 个 操 作 数 ： 内 存 值 、 预 期 值 、 新 值 。 当 且 仅 当 预 期 值 和 内 存 值 相 等 时 才 将 内 存 值 修 改 为 新 值 。

这 样 处 理 的 逻 辑 是 ， 首 先 检 查 某 块 内 存 的 值 是 否 跟 之 前 我 读 取 时 的 一 样 ， 如 不 一 样 则 表 示 期 间 此 内 存 值 已 经 被 别 的 线 程 更 改 过 ， 舍 弃 本 次 操 作 ， 否 则 说 明 期 间 没 有 其 他 线 程 对 此 内 存 值 操 作 ， 可 以 把 新 值 设 置 给 此 块 内 存 。

CAS 具 有 原 子 性 ， 它 的 原 子 性 由 CPU 硬 件 指 令 实 现 保 证 ， 即 使 用 JNI 调 用 Native 方 法 调 用 由 C++ 编 写 的 硬 件 级 别 指 令 ， JDK 中 提 供 了 Unsafe 类 执 行 这 些 操 作 。


# 695\. 乐 观 锁 一 定 就 是 好 的 吗 ？

> 原文：[https://zwmst.com/4559.html](https://zwmst.com/4559.html)

乐 观 锁 避 免 了 悲 观 锁 独 占 对 象 的 现 象 ， 同 时 也 提 高 了 并 发 性 能 ， 但 它 也有 缺 点 ：

1.  乐 观 锁 只 能 保 证 一 个 共 享 变 量 的 原 子 操 作 。 如 果 多 一 个 或 几 个 变 量 ， 乐观 锁 将 变 得 力 不 从 心 ， 但 互 斥 锁 能 轻 易 解 决 ， 不 管 对 象 数 量 多 少 及 对 象颗 粒 度 大 小 。
2.  长 时 间 自 旋 可 能 导 致 开 销 大 。 假 如 CAS 长 时 间 不 成 功 而 一 直 自 旋 ， 会给 CPU 带 来 很 大 的 开 销 。
3.  ABA 问 题 。 CAS 的 核 心 思 想 是 通 过 比 对 内 存 值 与 预 期 值 是 否 一 样 而 判断 内 存 值 是 否 被 改 过 ， 但 这 个 判 断 逻 辑 不 严 谨 ， 假 如 内 存 值 原 来 是 A，后 来 被 一 条 线 程 改 为 B， 最 后 又 被 改 成 了 A， 则 CAS 认 为 此 内 存 值 并 没 有 发 生 改 变 ， 但 实 际 上 是 有 被 其 他 线 程 改 过 的 ， 这 种 情 况 对 依 赖 过 程 值 的 情 景 的 运 算 结 果 影 响 很 大 。 解 决 的 思 路 是 引 入 版 本 号 ， 每 次 变 量 更 新 都 把 版 本 号 加 一 。


# 696.跟 Synchronized 相 比 ， 可 重 入 锁 ReentrantLock 其 实 现 原 理 有 什 么 不 同

> 原文：[https://zwmst.com/4561.html](https://zwmst.com/4561.html)

其 实 ， 锁 的 实 现 原 理 基 本 是 为 了 达 到 一 个 目 的 ：
让 所 有 的 线 程 都 能 看 到 某 种 标 记 。
Synchronized 通 过 在 对 象 头 中 设 置 标 记 实 现 了 这 一 目 的 ， 是 一 种 JVM 原 生 的 锁 实 现 方 式 ， 而 ReentrantLock 以 及 所 有 的 基 于 Lock 接 口 的 实 现 类 ， 都 是 通 过 用 一 个 volitile 修 饰 的 int 型 变 量 ， 并 保 证 每 个 线 程 都 能 拥 有 对 该 int 的 可 见 性 和 原 子 修 改 ， 其 本 质 是 基 于 所 谓 的 AQS 框 架 。


# 697.那 么 请 谈 谈 AQS 框 架 是 怎 么 回 事 儿 ？

> 原文：[https://zwmst.com/4563.html](https://zwmst.com/4563.html)

AQS（ AbstractQueuedSynchronizer 类 ） 是 一 个 用 来 构 建 锁 和 同 步 器 的 框 架 ， 各 种 Lock 包 中 的 锁 （ 常 用 的 有 ReentrantLock、ReadWriteLock） ， 以 及 其 他 如Semaphore、 CountDownLatch， 甚至 是 早 期 的 FutureTask 等 ， 都 是 基 于 AQS 来 构 建 。

1.  AQS 在 内 部 定 义 了 一 个 volatile int state 变 量 ， 表 示 同 步 状 态 ： 当 线 程 调 用 lock 方 法 时 ， 如 果 state=0， 说 明 没 有 任 何 线 程 占 有 共 享 资 源 的 锁 ， 可 以 获 得 锁 并 将 state=1； 如 果 state=1， 则 说 明 有 线 程 目 前 正 在 使 用 共 享 变 量 ， 其 他 线 程 必 须 加 入 同 步 队 列 进 行 等 待 。
2.  AQS 通 过 Node 内 部 类 构 成 的 一 个 双 向 链 表 结 构 的 同 步 队 列 ， 来 完 成 线 程 获 取 锁 的 排 队 工 作 ， 当 有 线 程 获 取 锁 失 败 后 ， 就 被 添 加 到 队 列 末 尾 。

Node 类 是 对 要 访 问 同 步 代 码 的 线 程 的 封 装 ， 包 含 了 线 程 本 身 及 其 状 态 叫waitStatus（ 有 五 种 不 同 取 值 ， 分 别 表 示 是 否 被 阻 塞 ， 是 否 等 待 唤 醒 ，是 否 已 经 被 取 消 等 ） ， 每 个 Node 结 点 关 联 其 prev 结 点 和 next 结点 ， 方 便 线 程 释 放 锁 后 快 速 唤 醒 下 一 个 在 等 待 的 线 程 ， 是 一 个 FIFO 的 过程 。

Node 类 有 两 个 常 量 ， SHARED 和 EXCLUSIVE， 分 别 代 表 共 享 模 式 和 独占 模 式 。 所 谓 共 享 模 式 是 一 个 锁 允 许 多 条 线 程 同 时 操 作 （ 信 号 量 Semaphore 就 是 基 于 AQS 的 共 享 模 式 实 现 的 ） ， 独 占 模 式 是 同 一 个 时 间 段 只 能 有 一 个 线 程 对 共 享 资 源 进 行 操 作 ， 多 余 的 请 求 线 程 需 要 排 队 等 待（ 如 ReentranLock） 。

3.  AQS 通 过 内 部 类 ConditionObject 构 建 等 待 队 列 （ 可 有 多 个 ） ， 当 Condition 调 用 wait() 方 法 后 ， 线 程 将 会 加 入 等 待 队 列 中 ， 而 当 Condition 调 用 signal() 方 法 后 ， 线 程 将 从 等 待 队 列 转 移 动 同 步 队 列 中 进 行 锁 竞 争 。
4.  AQS 和 Condition 各 自 维 护 了 不 同 的 队 列 ， 在 使 用 Lock 和Condition 的 时 候 ， 其 实 就 是 两 个 队 列 的 互 相 移 动 。


# 698.请 尽 可 能 详 尽 地 对 比 下 Synchronized 和 ReentrantLock 的 异 同 。

> 原文：[https://zwmst.com/4565.html](https://zwmst.com/4565.html)

ReentrantLock 是 Lock 的 实 现 类 ， 是 一 个 互 斥 的 同 步 锁 。

从 功 能 角 度 ， ReentrantLock 比 Synchronized 的 同 步 操 作 更 精 细（ 因 为 可 以 像 普 通 对 象 一 样 使 用 ） ， 甚 至 实 现 Synchronized 没 有 的高 级 功 能 ， 如 ：

1.  等 待 可 中 断 ： 当 持 有 锁 的 线 程 长 期 不 释 放 锁 的 时 候 ， 正 在 等 待 的 线 程 可以 选 择 放 弃 等 待 ， 对 处 理 执 行 时 间 非 常 长 的 同 步 块 很 有 用 。
2.  带 超 时 的 获 取 锁 尝 试 ： 在 指 定 的 时 间 范 围 内 获 取 锁 ， 如 果 时 间 到 了 仍 然无 法 获 取 则 返 回 。
3.  可 以 判 断 是 否 有 线 程 在 排 队 等 待 获 取 锁 。
4.  可 以 响 应 中 断 请 求 ： 与 Synchronized 不 同 ， 当 获 取 到 锁 的 线 程 被 中 断 时 ， 能 够 响 应 中 断 ， 中 断 异 常 将 会 被 抛 出 ， 同 时 锁 会 被 释 放 。
5.  可 以 实 现 公 平 锁 。

从 锁 释 放 角 度 ， Synchronized 在 JVM 层 面 上 实 现 的 ， 不 但 可 以 通 过 一 些 监 控 工 具 监 控 Synchronized 的 锁 定 ， 而 且 在 代 码 执 行 出 现 异 常 时 ， JVM 会 自 动 释 放 锁 定 ； 但 是 使 用 Lock 则 不 行 ， Lock 是 通 过 代 码 实 现 的 ， 要 保 证 锁 定 一 定 会 被 释 放 ， 就 必 须 将 unLock() 放 到 finally{} 中 。
从 性 能 角 度 ， Synchronized 早 期 实 现 比 较 低 效 ， 对 比 ReentrantLock， 大 多 数 场 景 性 能 都 相 差 较 大 。
但 是 在 Java 6 中 对 其 进 行 了 非 常 多 的 改 进 ， 在 竞 争 不 激 烈 时 ，Synchronized 的 性 能 要 优 于 ReetrantLock； 在 高 竞 争 情 况 下 ，Synchronized 的 性 能 会 下 降 几 十 倍 ， 但 是 ReetrantLock 的 性 能 能 维 持 常 态 。


# 699.ReentrantLock 是 如 何 实 现 可 重 入 性 的 ？

> 原文：[https://zwmst.com/4567.html](https://zwmst.com/4567.html)

ReentrantLock 内 部 自 定 义 了 同 步 器 Sync（ Sync 既 实 现 了 AQS，又 实 现 了 AOS， 而 AOS 提 供 了 一 种 互 斥 锁 持 有 的 方 式 ） ， 其 实 就 是 加 锁 的 时 候 通 过 CAS 算 法 ， 将 线 程 对 象 放 到 一 个 双 向 链 表 中 ， 每 次 获 取 锁 的 时 候 ， 看 下 当 前 维 护 的 那 个 线 程 ID 和 当 前 请 求 的 线 程 ID 是 否 一 样 ， 一 样 就 可 重 入 了 。


# 700.除 了 ReetrantLock， 你 还 接 触 过 JUC 中 的 哪 些 并 发 工 具 ？

> 原文：[https://zwmst.com/4569.html](https://zwmst.com/4569.html)

通 常 所 说 的 并 发 包 （ JUC） 也 就 是 java.util.concurrent 及 其 子 包 ， 集中 了 Java 并 发 的 各 种 基 础 工 具 类 ， 具 体 主 要 包 括 几 个 方 面 ：

1.  提 供 了 CountDownLatch、 CyclicBarrier、 Semaphore 等 ， 比 Synchronized 更 加 高 级 ， 可 以 实 现 更 加 丰 富 多 线 程 操 作 的 同 步 结 构 。
2.  提 供 了 ConcurrentHashMap、 有 序 的 ConcunrrentSkipListMap， 或 者 通 过 类 似 快 照 机 制 实 现 线 程 安 全 的 动 态 数 组 CopyOnWriteArrayList 等 ， 各 种 线 程 安 全 的 容 器 。
3.  提 供 了 ArrayBlockingQueue、 SynchorousQueue 或 针 对 特 定 场 景 的PriorityBlockingQueue 等 ， 各 种 并 发 队 列 实 现 。
4.  强 大 的 Executor 框 架 ， 可 以 创 建 各 种 不 同 类 型 的 线 程 池 ， 调 度 任 务 运行 等 。


# 701\. 请 谈 谈 ReadWriteLock 和 StampedLock。

> 原文：[https://zwmst.com/4571.html](https://zwmst.com/4571.html)

虽 然 ReentrantLock 和 Synchronized 简 单 实 用 ， 但 是 行 为 上 有 一 定 局 限 性 ， 要 么 不 占 ， 要 么 独 占 。 实 际 应 用 场 景 中 ， 有 时 候 不 需 要 大 量 竞 争 的 写 操 作 ， 而 是 以 并 发 读 取 为 主 ， 为 了 进 一 步 优 化 并 发 操 作 的 粒 度 ， Java 提 供 了 读 写 锁 。

读 写 锁 基 于 的 原 理 是 多 个 读 操 作 不 需 要 互 斥 ， 如 果 读 锁 试 图 锁 定 时 ， 写锁 是 被 某 个 线 程 持 有 ， 读 锁 将 无 法 获 得 ， 而 只 好 等 待 对 方 操 作 结 束 ， 这样 就 可 以 自 动 保 证 不 会 读 取 到 有 争 议 的 数 据 。

ReadWriteLock 代 表 了 一 对 锁 ， 下 面 是 一 个 基 于 读 写 锁 实 现 的 数 据 结 构 ， 当 数 据 量 较 大 ， 并 发 读 多 、 并 发 写 少 的 时 候 ， 能 够 比 纯 同 步 版 本 凸 显 出 优 势 ：

读 写 锁 看 起 来 比 Synchronized 的 粒 度 似 乎 细 一 些 ， 但 在 实 际 应 用 中 ， 其 表 现 也 并 不 尽 如 人 意 ， 主 要 还 是 因 为 相 对 比 较 大 的 开 销 。

所 以 ， JDK 在 后 期 引 入 了 StampedLock， 在 提 供 类 似 读 写 锁 的 同 时 ，还 支 持 优 化 读 模 式 。 优 化 读 基 于 假 设 ， 大 多 数 情 况 下 读 操 作 并 不 会 和 写 操 作 冲 突 ， 其 逻 辑 是 先 试 着 修 改 ， 然 后 通 过 validate 方 法 确 认 是 否 进 入 了 写 模 式 ， 如 果 没 有 进 入 ， 就 成 功 避 免 了 开 销 ； 如 果 进 入 ， 则 尝 试 获 取 读 锁


# 702\. 如 何 让 Java 的 线 程 彼 此 同 步 ？ 你 了 解 过 哪 些 同 步 器 ？ 请 分 别 介 绍 下 。

> 原文：[https://zwmst.com/4573.html](https://zwmst.com/4573.html)

JUC 中 的 同 步 器 三 个 主 要 的 成 员 ： CountDownLatch、 CyclicBarrier 和 Semaphore， 通 过 它 们 可 以 方 便 地 实 现 很 多 线 程 之 间 协 作 的 功 能 。
CountDownLatch 叫 倒 计 数 ， 允 许 一 个 或 多 个 线 程 等 待 某 些 操 作 完 成 。 看 几 个 场 景 ：

1.  跑 步 比 赛 ， 裁 判 需 要 等 到 所 有 的 运 动 员 （ “ 其 他 线 程 ” ） 都 跑 到 终 点（ 达 到 目 标 ） ， 才 能 去 算 排 名 和 颁 奖 。
2.  模 拟 并 发 ， 我 需 要 启 动 100 个 线 程 去 同 时 访 问 某 一 个 地 址 ， 我 希 望 它们 能 同 时 并 发 ， 而 不 是 一 个 一 个 的 去 执 行 。

用 法 ： CountDownLatch 构 造 方 法 指 明 计 数 数 量 ， 被 等 待 线 程 调 用 countDown 将 计 数 器 减 1， 等 待 线 程 使 用 await 进 行 线 程 等 待 。 一 个 简 单 的 例 子 ：

CyclicBarrier 叫 循 环 栅 栏 ， 它 实 现 让 一 组 线 程 等 待 至 某 个 状 态 之 后 再 全 部 同 时 执 行 ， 而 且 当 所 有 等 待 线 程 被 释 放 后 ， CyclicBarrier 可 以 被 重 复 使 用 。 CyclicBarrier 的 典 型 应 用 场 景 是 用 来 等 待 并 发 线 程 结 束 。

CyclicBarrier 的 主 要 方 法 是 await()， await() 每 被 调 用 一 次 ， 计 数 便 会 减 少 1， 并 阻 塞 住 当 前 线 程 。 当 计 数 减 至 0 时 ， 阻 塞 解 除 ， 所 有 在 此 CyclicBarrier 上 面 阻 塞 的 线 程 开 始 运 行 。

在 这 之 后 ， 如 果 再 次 调 用 await()， 计 数 就 又 会 变 成 N-1， 新 一 轮 重 新开 始 ， 这 便 是 Cyclic 的 含 义 所 在 。 CyclicBarrier.await() 带 有 返 回 值 ， 用 来 表 示 当 前 线 程 是 第 几 个 到 达 这 个 Barrier 的 线 程 。举 例 说 明 如 下 ：

Semaphore， Java 版 本 的 信 号 量 实 现 ， 用 于 控 制 同 时 访 问 的 线 程 个 数 ， 来 达 到 限 制 通 用 资 源 访 问 的 目 的 ， 其 原 理 是 通 过 acquire() 获 取 一 个 许 可 ， 如 果 没 有 就 等 待 ， 而 release() 释 放 一 个 许 可 。

如 果 Semaphore 的 数 值 被 初 始 化 为 1， 那 么 一 个 线 程 就 可 以 通 过 acquire 进 入 互 斥 状 态 ， 本 质 上 和 互 斥 锁 是 非 常 相 似 的 。 但 是 区 别 也 非 常 明 显 ， 比 如 互 斥 锁 是 有 持 有 者 的 ， 而 对 于 Semaphore 这 种 计 数 器 结 构 ， 虽 然 有 类 似 功 能 ， 但 其 实 不 存 在 真 正 意 义 的 持 有 者 ， 除 非 我 们 进 行 扩 展 包 装 。


# 703\. CyclicBarrier 和 CountDownLatch 看 起 来 很 相 似 ， 请 对 比 下 呢

> 原文：[https://zwmst.com/4607.html](https://zwmst.com/4607.html)

它 们 的 行 为 有 一 定 相 似 度 ， 区 别 主 要 在 于 ：

1.  CountDownLatch 是 不 可 以 重 置 的 ， 所 以 无 法 重 用 ， CyclicBarrier 没有 这 种 限 制 ， 可 以 重 用 。
2.  CountDownLatch 的 基 本 操 作 组 合 是 countDown/await， 调 用 await 的 线 程 阻 塞 等 待 countDown 足 够 的 次 数 ， 不 管 你 是 在 一 个 线 程 还 是 多 个 线 程 里 countDown， 只 要 次 数 足 够 即 可 。 CyclicBarrier 的 基 本 操 作 组 合 就 是 await， 当 所 有 的 伙 伴 都 调 用 了 await， 才 会 继 续 进 行 任 务 ， 并 自 动 进 行 重 置 。CountDownLatch 目 的 是 让 一 个 线 程 等 待 其 他 N 个 线 程 达 到 某 个 条件 后 ， 自 己 再 去 做 某 个 事 （ 通 过 CyclicBarrier 的 第 二 个 构 造 方 法public CyclicBarrier(int parties, Runnable barrierAction)， 在 新 线 程 里 做 事 可 以 达 到 同 样 的 效 果 ） 。 而 CyclicBarrier 的 目 的 是 让 N 多 线 程 互 相 等 待 直 到 所 有 的 都 达 到 某 个 状 态 ， 然 后 这 N 个 线 程 再 继 续 执 行 各 自 后 续 （ 通 过 CountDownLatch 在 某 些 场 合 也 能 完 成 类 似 的 效 果 ） 。


# 704.Java 中 的 线 程 池 是 如 何 实 现 的 ？

> 原文：[https://zwmst.com/4610.html](https://zwmst.com/4610.html)

1.  在 Java 中 ， 所 谓 的 线 程 池 中 的 “ 线 程 ” ， 其 实 是 被 抽 象 为 了 一 个 静 态 内 部 类 Worker， 它 基 于 AQS 实 现 ， 存 放 在 线 程 池 的 HashSet `<Worker>` workers 成 员 量 中 ；
2.  而 需 要 执 行 的 任 务 则 存 放 在 成 员 变 量 workQueue（ BlockingQueue`<Runnable>` workQueue） 中 。这 样 ， 整 个 线 程 池 实 现 的 基 本 思 想 就 是 ： 从 workQueue 中 不 断 取 出需 要 执 行 的 任 务 ， 放 在 Workers 中 进 行 处 理 。


# 705.创 建 线 程 池 的 几 个 核 心 构 造 参 数 ？

> 原文：[https://zwmst.com/4612.html](https://zwmst.com/4612.html)

Java 中 的 线 程 池 的 创 建 其 实 非 常 灵 活 ， 我 们 可 以 通 过 配 置 不 同 的 参 数 ， 创 建 出 行 为 不 同 的 线 程 池 ， 这 几 个 参 数 包 括 ：

1.  corePoolSize： 线 程 池 的 核 心 线 程 数 。
2.  maximumPoolSize： 线 程 池 允 许 的 最 大 线 程 数 。
3.  keepAliveTime： 超 过 核 心 线 程 数 时 闲 置 线 程 的 存 活 时 间 。
4.  workQueue： 任 务 执 行 前 保 存 任 务 的 队 列 ， 保 存 由 execute 方 法 提 交 的 Runnable 任 务 。


# 706.线 程 池 中 的 线 程 是 怎 么 创 建 的 ？ 是 一 开 始 就 随 着 线 程 池 的 启 动 创 建 好 的 吗 ？

> 原文：[https://zwmst.com/4614.html](https://zwmst.com/4614.html)

显 然 不 是 的 。 线 程 池 默 认 初 始 化 后 不 启 动 Worker， 等 待 有 请 求 时 才 启 动 。
每 当 我 们 调 用 execute() 方 法 添 加 一 个 任 务 时 ， 线 程 池 会 做 如 下 判 断 ：

1.  如 果 正 在 运 行 的 线 程 数 量 小 于 corePoolSize， 那 么 马 上 创 建 线 程 运 行 这 个 任 务 ；
2.  如 果 正 在 运 行 的 线 程 数 量 大 于 或 等 于 corePoolSize， 那 么 将 这 个 任 务 放 入 队 列 ；
3.  如 果 这 时 候 队 列 满 了 ， 而 且 正 在 运 行 的 线 程 数 量 小 于 maximumPoolSize， 那 么 还 是 要 创 建 非 核 心 线 程 立 刻 运 行 这 个 任 务 ；
4.  如 果 队 列 满 了 ， 而 且 正 在 运 行 的 线 程 数 量 大 于 或 等 于maximumPoolSize， 那 么 线 程 池 会 抛 出 异 常 RejectExecutionException。

当 一 个 线 程 完 成 任 务 时 ， 它 会 从 队 列 中 取 下 一 个 任 务 来 执 行 。 当 一 个 线 程 无 事 可 做 ， 超 过 一 定 的 时 间 （ keepAliveTime） 时 ， 线 程 池 会 判 断 。
如 果 当 前 运 行 的 线 程 数 大 于 corePoolSize， 那 么 这 个 线 程 就 被 停 掉 。所 以 线 程 池 的 所 有 任 务 完 成 后 ， 它 最 终 会 收 缩 到 corePoolSize 的 大 小 。


# 707.既 然 提 到 可 以 通 过 配 置 不 同 参 数 创 建 出 不 同 的 线 程 池 ， 那 么 Java 中 默 认 实 现 好 的 线 程 池 又 有 哪 些 呢 ？ 请 比 较 它 们 的 异 同 。

> 原文：[https://zwmst.com/4616.html](https://zwmst.com/4616.html)

## 1\. SingleThreadExecutor 线 程 池

这 个 线 程 池 只 有 一 个 核 心 线 程 在 工 作 ， 也 就 是 相 当 于 单 线 程 串 行 执 行 所有 任 务 。 如 果 这 个 唯 一 的 线 程 因 为 异 常 结 束 ， 那 么 会 有 一 个 新 的 线 程 来 替 代 它 。 此 线 程 池 保 证 所 有 任 务 的 执 行 顺 序 按 照 任 务 的 提 交 顺 序 执 行 。

1.  corePoolSize： 1， 只 有 一 个 核 心 线 程 在 工 作 。
2.  maximumPoolSize： 1。
3.  keepAliveTime： 0L。
4.  workQueue： new LinkedBlockingQueue`<Runnable>`()， 其 缓 冲 队 列是 无 界 的 。

## 2\. FixedThreadPool 线 程 池

FixedThreadPool 是 固 定 大 小 的 线 程 池 ， 只 有 核 心 线 程 。 每 次 提 交 一 个 任 务 就 创 建 一 个 线 程 ， 直 到 线 程 达 到 线 程 池 的 最 大 大 小 。 线 程 池 的 大 小 一 旦 达 到 最 大 值 就 会 保 持 不 变 ， 如 果 某 个 线 程 因 为 执 行 异 常 而 结 束 ， 那 么 线 程 池 会 补 充 一 个 新 线 程 。
FixedThreadPool 多 数 针 对 一 些 很 稳 定 很 固 定 的 正 规 并 发 线 程 ， 多 用 于 服 务 器 。

1.  corePoolSize： nThreads
2.  maximumPoolSize： nThreads
3.  keepAliveTime： 0L
4.  workQueue： new LinkedBlockingQueue`<Runnable>`()， 其 缓 冲 队 列是 无 界 的 。

## 3\. CachedThreadPool 线 程 池

CachedThreadPool 是 无 界 线 程 池 ， 如 果 线 程 池 的 大 小 超 过 了 处 理 任 务 所 需 要 的 线 程 ， 那 么 就 会 回 收 部 分 空 闲 （ 60 秒 不 执 行 任 务 ） 线 程 ， 当 任 务 数 增 加 时 ， 此 线 程 池 又 可 以 智 能 的 添 加 新 线 程 来 处 理 任 务 。
线 程 池 大 小 完 全 依 赖 于 操 作 系 统 （ 或 者 说 JVM） 能 够 创 建 的 最 大 线 程 大 小 。 SynchronousQueue 是 一 个 是 缓 冲 区 为 1 的 阻 塞 队 列 。
缓 存 型 池 子 通 常 用 于 执 行 一 些 生 存 期 很 短 的 异 步 型 任 务 ， 因 此 在 一 些 面 向 连 接 的 daemon 型 SERVER 中 用 得 不 多 。 但 对 于 生 存 期 短 的 异 步任 务 ， 它 是 Executor 的 首 选 。

1.  corePoolSize： 0
2.  maximumPoolSize： Integer.MAX_VALUE
3.  keepAliveTime： 60L
4.  workQueue： new SynchronousQueue`<Runnable>`()， 一 个 是 缓 冲 区为 1 的 阻 塞 队 列 。

## 4\. ScheduledThreadPool 线 程 池

ScheduledThreadPool： 核 心 线 程 池 固 定 ， 大 小 无 限 的 线 程 池 。 此 线 程 池 支 持 定 时 以 及 周 期 性 执 行 任 务 的 需 求 。 创 建 一 个 周 期 性 执 行 任 务 的 线 程 池 。 如 果 闲 置 ， 非 核 心 线 程 池 会 在 DEFAULT_KEEPALIVEMILLIS 时 间 内 回 收 。

1.  corePoolSize： corePoolSize
2.  maximumPoolSize： Integer.MAX_VALUE
3.  keepAliveTime： DEFAULT_KEEPALIVE_MILLIS
4.  workQueue： new DelayedWorkQueue()


# 708.如 何 在 Java 线 程 池 中 提 交 线 程 ？

> 原文：[https://zwmst.com/4618.html](https://zwmst.com/4618.html)

线 程 池 最 常 用 的 提 交 任 务 的 方 法 有 两 种 ：

1.  execute()： ExecutorService.execute 方 法 接 收 一 个 Runable 实 例 ， 它 用 来 执 行 一 个 任 务
2.  submit()： ExecutorService.submit() 方 法 返 回 的 是 Future 对 象 。 可 以 用 isDone() 来 查 询 Future 是 否 已 经 完 成 ， 当 任 务 完 成 时 ，它 具 有 一 个 结 果 ， 可 以 调 用 get() 来 获 取 结 果 。 也 可 以 不 用 isDone() 进 行 检 查 就 直 接 调 用 get()， 在 这 种 情 况 下 ， get() 将 阻 塞 ， 直 至 结 果 准 备 就 绪 。


# 709.什 么 是 Java 的 内 存 模 型 ， Java 中 各 个 线 程 是 怎 么 彼 此 看 到 对 方 的 变 量 的 ？

> 原文：[https://zwmst.com/4621.html](https://zwmst.com/4621.html)

Java 的 内 存 模 型 定 义 了 程 序 中 各 个 变 量 的 访 问 规 则 ， 即 在 虚 拟 机 中 将 变 量 存 储 到 内 存 和 从 内 存 中 取 出 这 样 的 底 层 细 节 。
此 处 的 变 量 包 括 实 例 字 段 、 静 态 字 段 和 构 成 数 组 对 象 的 元 素 ， 但 是 不 包括 局 部 变 量 和 方 法 参 数 ， 因 为 这 些 是 线 程 私 有 的 ， 不 会 被 共 享 ， 所 以 不存 在 竞 争 问 题 。
Java 中 各 个 线 程 是 怎 么 彼 此 看 到 对 方 的 变 量 的 呢 ？ Java 中 定 义 了 主 内 存 与 工 作 内 存 的 概 念 ：
所 有 的 变 量 都 存 储 在 主 内 存 ， 每 条 线 程 还 有 自 己 的 工 作 内 存 ， 保 存 了 被该 线 程 使 用 到 的 变 量 的 主 内 存 副 本 拷 贝 。
线 程 对 变 量 的 所 有 操 作 （ 读 取 、 赋 值 ） 都 必 须 在 工 作 内 存 中 进 行 ， 不 能直 接 读 写 主 内 存 的 变 量 。 不 同 的 线 程 之 间 也 无 法 直 接 访 问 对 方 工 作 内 存的 变 量 ， 线 程 间 变 量 值 的 传 递 需 要 通 过 主 内 存 。


# 710.请 谈 谈 volatile 有 什 么 特 点 ， 为 什 么 它 能 保 证 变 量 对 所 有 线 程 的 可 见 性

> 原文：[https://zwmst.com/4623.html](https://zwmst.com/4623.html)

关 键 字 volatile 是 Java 虚 拟 机 提 供 的 最 轻 量 级 的 同 步 机 制 。 当 一 个 变 量 被 定 义 成 volatile 之 后 ， 具 备 两 种 特 性 ：

1.  保 证 此 变 量 对 所 有 线 程 的 可 见 性 。 当 一 条 线 程 修 改 了 这 个 变 量 的 值 ， 新 值 对 于 其 他 线 程 是 可 以 立 即 得 知 的 。 而 普 通 变 量 做 不 到 这 一 点 。
2.  禁 止 指 令 重 排 序 优 化 。 普 通 变 量 仅 仅 能 保 证 在 该 方 法 执 行 过 程 中 ， 得 到正 确 结 果 ， 但 是 不 保 证 程 序 代 码 的 执 行 顺 序 。



# Java 的 内 存 模 型 定 义 了 8 种 内 存 间 操 作 ：

## lock 和 unlock

1.  把 一 个 变 量 标 识 为 一 条 线 程 独 占 的 状 态 。
2.  把 一 个 处 于 锁 定 状 态 的 变 量 释 放 出 来 ， 释 放 之 后 的 变 量 才 能 被 其 他 线 程 锁 定 。

## read 和 write

1.  把 一 个 变 量 值 从 主 内 存 传 输 到 线 程 的 工 作 内 存 ， 以 便 load。
2.  把 store 操 作 从 工 作 内 存 得 到 的 变 量 的 值 ， 放 入 主 内 存 的 变 量 中 。

## load 和 store

1.  把 read 操 作 从 主 内 存 得 到 的 变 量 值 放 入 工 作 内 存 的 变 量 副 本 中 。
2.  把 工 作 内 存 的 变 量 值 传 送 到 主 内 存 ， 以 便 write。

## use 和 assgin

1.  把 工 作 内 存 变 量 值 传 递 给 执 行 引 擎 。
2.  将 执 行 引 擎 值 传 递 给 工 作 内 存 变 量 值 。

volatile 的 实 现 基 于 这 8 种 内 存 间 操 作 ， 保 证 了 一 个 线 程 对 某 个 volatile 变 量 的 修 改 ， 一 定 会 被 另 一 个 线 程 看 见 ， 即 保 证 了 可 见 性 。


# 711.既 然 volatile 能 够 保 证 线 程 间 的 变 量 可 见 性 ， 是 不 是 就 意 味 着 基 于 volatile 变 量 的 运 算 就 是 并 发 安 全 的

> 原文：[https://zwmst.com/4626.html](https://zwmst.com/4626.html)

显 然 不 是 的 。 基 于 volatile 变 量 的 运 算 在 并 发 下 不 一 定 是 安 全 的 。volatile 变 量 在 各 个 线 程 的 工 作 内 存 ， 不 存 在 一 致 性 问 题 （ 各 个 线 程 的工 作 内 存 中 volatile 变 量 ， 每 次 使 用 前 都 要 刷 新 到 主 内 存 ） 。
但 是 Java 里 面 的 运 算 并 非 原 子 操 作 ， 导 致 volatile 变 量 的 运 算 在 并发 下 一 样 是 不 安 全 的 。


# 712.请 对 比 下 volatile 对 比 Synchronized 的 异 同 。

> 原文：[https://zwmst.com/4628.html](https://zwmst.com/4628.html)

Synchronized 既 能 保 证 可 见 性 ， 又 能 保 证 原 子 性 ， 而 volatile 只 能 保 证 可 见 性 ， 无 法 保 证 原 子 性 。
ThreadLocal 和 Synchonized 都 用 于 解 决 多 线 程 并 发 访 问 ， 防 止 任 务 在 共 享 资 源 上 产 生 冲 突 。 但 是 ThreadLocal 与 Synchronized 有 本 质 的 区 别 。
Synchronized 用 于 实 现 同 步 机 制 ， 是 利 用 锁 的 机 制 使 变 量 或 代 码 块 在 某 一 时 该 只 能 被 一 个 线 程 访 问 ， 是 一 种 “ 以 时 间 换 空 间 ” 的 方 式 。
而 ThreadLocal 为 每 一 个 线 程 都 提 供 了 变 量 的 副 本 ， 使 得 每 个 线 程 在 某 一 时 间 访 问 到 的 并 不 是 同 一 个 对 象 ， 根 除 了 对 变 量 的 共 享 ， 是 一 种“ 以 空 间 换 时 间 ” 的 方 式 。


# 713.请 谈 谈 ThreadLocal 是 怎 么 解 决 并 发 安 全 的 ？

> 原文：[https://zwmst.com/4630.html](https://zwmst.com/4630.html)

ThreadLocal 这 是 Java 提 供 的 一 种 保 存 线 程 私 有 信 息 的 机 制 ， 因 为 其 在 整 个 线 程 生 命 周 期 内 有 效 ， 所 以 可 以 方 便 地 在 一 个 线 程 关 联 的 不 同 业 务 模 块 之 间 传 递 信 息 ， 比 如 事 务 ID、 Cookie 等 上 下 文 相 关 信 息 。
ThreadLocal 为 每 一 个 线 程 维 护 变 量 的 副 本 ， 把 共 享 数 据 的 可 见 范 围 限 制 在 同 一 个 线 程 之 内 ， 其 实 现 原 理 是 ， 在 ThreadLocal 类 中 有 一 个 Map， 用 于 存 储 每 一 个 线 程 的 变 量 的 副 本 。


# 714.很 多 人 都 说 要 慎 用 ThreadLocal， 谈 谈 你 的 理 解 ， 使 用 ThreadLocal 需 要 注 意 些 什 么 ？

> 原文：[https://zwmst.com/4632.html](https://zwmst.com/4632.html)

**使 用 ThreadLocal 要 注 意 remove！
ThreadLocal 的 实 现 是 基 于 一 个 所 谓 的 ThreadLocalMap， 在 ThreadLocalMap 中 ， 它 的 key 是 一 个 弱 引 用 。
通 常 弱 引 用 都 会 和 引 用 队 列 配 合 清 理 机 制 使 用 ， 但 是 ThreadLocal 是 个 例 外 ， 它 并 没 有 这 么 做 。
这 意 味 着 ， 废 弃 项 目 的 回 收 依 赖 于 显 式 地 触 发 ， 否 则 就 要 等 待 线 程 结 束 ， 进 而 回 收 相 应 ThreadLocalMap！ 这 就 是 很 多 OOM 的 来 源 ， 所 以 通 常 都 会 建 议 ， 应 用 一 定 要 自 己 负 责 remove， 并 且 不 要 和 线 程 池 配 合 ， 因 为 worker 线 程 往 往 是 不 会 退 出 的


# 715\. stop() 和 suspend() 方法为何不推荐使用？

> 原文：[https://zwmst.com/4634.html](https://zwmst.com/4634.html)

反对使用 stop()，是因为它不安全。它会解除由线程获取的所有锁定，而且如果对象处于一种不连贯状态，那么其他线程能在那种状态下检查和修改它们。结果很难检查出真正的问题所在。
**suspend() 方法容易发生死锁**。调用 suspend() 的时候，目标线程会停下来，但却仍然持有在这之前获得的锁定。此时，其他任何线程都不能访问锁定的资源，除非被 "挂起" 的线程恢复运行。对任何线程来说，如果它们想恢复目标线程，同时又试图使用任何一个锁定的资源，就会造成死锁。所以不应该使用 suspend()，而应在自己的 Thread 类中置入一个标志，指出线程应该活动还是挂起。若标志指出线程应该挂起，便用 wait() 命其进入等待状态。若标志指出线程应当恢复，则用一个 notify() 重新启动线程。


# 716.sleep() 和 wait() 有什么区别

> 原文：[https://zwmst.com/4637.html](https://zwmst.com/4637.html)

sleep 就是正在执行的线程主动让出 cpu，cpu 去执行其他线程，在 sleep 指定的时间过后，cpu 才会回到这个线程上继续往下执行，如果当前线程进入了同步锁，sleep 方法并不会释放锁，即使当前线程使用 sleep 方法让出了 cpu，但其他被同步锁挡住了的线程也无法得到执行。
wait 是指在一个已经进入了同步锁的线程内，让自己暂时让出同步锁，以便其他正在等待此锁的线程可以得到同步锁并运行，只有其他线程调用了 notify 方法（notify 并不释放锁，只是告诉调用过 wait 方法的线程可以去参与获得锁的竞争了，但不是马上得到锁，因为锁还在别人手里，别人还没释放。如果 notify 方法后面的代码还有很多，需要这些代码执行完后才会释放锁，可以在 notfiy 方法后增加一个等待和一些代码，看看效果），调用 wait 方法的线程就会解除 wait 状态和程序可以再次得到锁后继续向下运行。


# 717.同步和异步有何异同，在什么情况下分别使用他们？

> 原文：[https://zwmst.com/4639.html](https://zwmst.com/4639.html)

如果数据将在线程间共享。例如正在写的数据以后可能被另一个线程读到，或者正在读的数据可能已经被另一个线程写过了，那么这些数据就是共享数据，必须进行同步存取。当应用程序在对象上调用了一个需要花费很长时间来执行的方法，并且不希望让程序等待方法的返回时，就应该使用异步编程，在很多情况下采用异步途径往往更有效率


# 718.当一个线程进入一个对象的一个 synchronized 方法后，其它线程是否可进入此对象的其 它方法?

> 原文：[https://zwmst.com/4641.html](https://zwmst.com/4641.html)

1.  其他方法前是否加了 synchronized 关键字，如果没加，则能。
2.  如果这个方法内部调用了 wait，则可以进入其他 synchronized 方法。
3.  如果其他个方法都加了 synchronized 关键字，并且内部没有调用 wait，则不能。
4.  如果其他方法是 static，它用的同步锁是当前类的字节码，与非静态的方法不能同步，因为非静态的方法用的是 this。


# 719.简述 synchronized 和 java.util.concurrent.locks.Lock 的异同？

> 原文：[https://zwmst.com/4643.html](https://zwmst.com/4643.html)

主要相同点：Lock 能完成 synchronized 所实现的所有功能。
主要不同点：Lock 有比 synchronized 更精确的线程语义和更好的性能。
synchronized 会自动释放锁，而 Lock 一定要求程序员手工释放，并且必须在 finally 从句中释放。Lock 还有更强大的功能，例如，它的 tryLock 方法可以非阻塞方式去拿锁。
举例说明（对下面的题用 lock 进行了改写）

```
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;
public class ThreadTest {
 /
 * @param args
 */
 private int j;
 private Lock lock = new ReentrantLock();
 public static void main(String[] args) {
 // TODO Auto-generated method stub
 ThreadTest tt = new ThreadTest();
 for(int i=0;i<2;i++)
 {
 new Thread(tt.new Adder()).start();
 new Thread(tt.new Subtractor()).start();
 }
 }
 private class Subtractor implements Runnable
 {
 @Override
 public void run() {
 // TODO Auto-generated method stub
 while(true)
 {
 /*synchronized (ThreadTest.this) { 
 System.out.println("j--=" + j--);
 //这里抛异常了，锁能释放吗？
 }*/
 lock.lock();
 try
 {
 System.out.println("j--=" + j--);
 }finally
 {
 lock.unlock();
 }
 }
 }
 }
 private class Adder implements Runnable
 {
 @Override
 public void run() {
 // TODO Auto-generated method stub
 while(true)
 {
 /*synchronized (ThreadTest.this) {
 System.out.println("j++=" + j++); 
 }*/
 lock.lock();
 try
 {
 System.out.println("j++=" + j++);
 }finally
 {
 lock.unlock();
 } 
 } 
 }
 }
}
```


# 720.概括的解释下线程的几种可用状态。

> 原文：[https://zwmst.com/4645.html](https://zwmst.com/4645.html)

1.  新建 new。
2.  就绪 放在可运行线程池中，等待被线程调度选中，获取 cpu。
3.  运行 获得了 cpu。
4.  阻塞
    1.  等待阻塞 执行 wait() 。
    2.  同步阻塞 获取对象的同步琐时，同步锁被别的线程占用。
    3.  其他阻塞 执行了 sleep() 或 join() 方法)。
5.  死亡。


# 721.什么是 ThreadLocal?

> 原文：[https://zwmst.com/4647.html](https://zwmst.com/4647.html)

ThreadLocal 用于创建线程的本地变量，我们知道一个对象的所有线程会共享它的全局变量，所以这些变量不是线程安全的，我们可以使用同步技术。但是当我们不想使用同步的时候，我们可以选择 ThreadLocal 变量。
每个线程都会拥有他们自己的 Thread 变量，它们可以使用 get()\set() 方法去获取他们的默认值或者在线程内部改变他们的值。ThreadLocal 实例通常是希望它们同线程状态关联起来是 private static 属性。


# 722.run() 和 start() 区别。

> 原文：[https://zwmst.com/4649.html](https://zwmst.com/4649.html)

**run( )**：只是调用普通 run 方法
**start( )**：启动了线程, 由 Jvm 调用 run 方法

启动一个线程是调用 start() 方法，使线程所代表的虚拟处理机处于可运行状态，这意味着它可以由 JVM 调度并执行。这并不意味着线程就会立即运行。run() 方法可以产生必须退出的标志来停止一个线程。


# 723.请说出你所知道的线程同步的方法。

> 原文：[https://zwmst.com/4651.html](https://zwmst.com/4651.html)

**wait()**：使一个线程处于等待状态，并且释放所持有的对象的 lock。
**sleep()**：使一个正在运行的线程处于睡眠状态，是一个静态方法，调用此方法要捕捉InterruptedException 异常。
**notify()**：唤醒一个处于等待状态的线程，注意的是在调用此方法的时候，并不能确切的唤醒某一个等待状态的线程，而是由 JVM 确定唤醒哪个线程，而且不是按优先级。
**notityAll()**：唤醒所有处入等待状态的线程，注意并不是给所有唤醒线程一个对象的锁，而是让它们竞争。


# 724.线程调度和线程控制。

> 原文：[https://zwmst.com/4654.html](https://zwmst.com/4654.html)

**线程调度（优先级）**:
与线程休眠类似，线程的优先级仍然无法保障线程的执行次序。只不过，优先级高的线程获取 CPU 资源的概率较大，优先级低的并非没机会执行。线程的优先级用 1-10 之间的整数表示，数值越大优先级越高，默认的优先级为 5。 在一个线程中开启另外一个新线程，则新开线程称为该线程的子线程，子线程初始优先级与父线程相同。

**线程控制
sleep( ) // 线程休眠 join( ) // 线程加入 yield( ) // 线程礼让
setDaemon( ) // 线程守护
**中断线程
stop( ) interrupt( ) ==(首先选用)==


# 725.什么是线程饿死，什么是活锁？

> 原文：[https://zwmst.com/4656.html](https://zwmst.com/4656.html)

当所有线程阻塞，或者由于需要的资源无效而不能处理，不存在非阻塞线程使资源可用。JavaAPI 中线程活锁可能发生在以下情形：

1.  当所有线程在序中执行 Object.wait(0)，参数为 0 的 wait 方法。程序将发生活锁直到在相应的对象上有线程调用 Object.notify() 或者 Object.notifyAll()。
2.  当所有线程卡在无限循环中。


# 726.多线程中的忙循环是什么?

> 原文：[https://zwmst.com/4658.html](https://zwmst.com/4658.html)

忙循环就是程序员用循环让一个线程等待，不像传统方法 wait(), sleep() 或 yield() 它们都放弃了 CPU 控制，而忙循环不会放弃 CPU，它就是在运行一个空循环。这么做的目的是为了保留 CPU 缓存。
在多核系统中，一个等待线程醒来的时候可能会在另一个内核运行，这样会重建缓存。为了避免重建缓存和减少等待重建的时间就可以使用它了。


# 727.volatile 变量是什么？volatile 变量和 atomic 变量有什么不同？

> 原文：[https://zwmst.com/4660.html](https://zwmst.com/4660.html)

volatile 则是保证了所修饰的变量的可见。因为 volatile 只是在保证了同一个变量在多线程中的可见性，所以它更多是用于修饰作为开关状态的变量，即 Boolean 类型的变量。
volatile 多用于修饰类似开关类型的变量、Atomic 多用于类似计数器相关的变量、其它多线程并发操作用 synchronized 关键字修饰。
**volatile 有两个功用：

1.  这个变量不会在多个线程中存在复本，直接从内存读取。
2.  这个关键字会禁止指令重排序优化。也就是说，在 volatile 变量的赋值操作后面会有一个内存屏障（生成的汇编代码上），读操作不会被重排序到内存屏障之前。


# 728.volatile 类型变量提供什么保证？能使得一个非原子操作变成原子操作吗？

> 原文：[https://zwmst.com/4662.html](https://zwmst.com/4662.html)

volatile 提供 happens-before 的保证，确保一个线程的修改能对其他线程是可见的。在 Java 中除了 long 和 double 之外的所有基本类型的读和赋值，都是原子性操作。
而 64 位的 long 和 double 变量由于会被 JVM 当作两个分离的 32 位来进行操作，所以不具有原子性，会产生字撕裂问题。但是当你定义 long 或 double 变量时，如果使用 volatile 关键字，就会获到（简单的赋值与返回操作的）原子性


# 729.多线程有什么用？

> 原文：[https://zwmst.com/4664.html](https://zwmst.com/4664.html)

1.  发挥多核CPU 的优势
    随着工业的进步，现在的笔记本、台式机乃至商用的应用服务器至少也都是双核的，4 核、8 核甚至 16 核的也都不少见，如果是单线程的程序，那么在双核 CPU 上就浪费了 50%， 在 4 核 CPU 上就浪费了 75%。单核 CPU 上所谓的"多线程"那是假的多线程，同一时间处理器只会处理一段逻辑，只不过线程之间切换得比较快，看着像多个线程"同时"运行罢了。多核 CPU 上的多线程才是真正的多线程，它能让你的多段逻辑同时工作，多线程，可以真正发挥出多核CPU 的优势来，达到充分利用CPU 的目的。

2.  防止阻塞
    从程序运行效率的角度来看，单核 CPU 不但不会发挥出多线程的优势，反而会因为在单核CPU 上运行多线程导致线程上下文的切换，而降低程序整体的效率。但是单核 CPU 我们还是要应用多线程，就是为了防止阻塞。试想，如果单核 CPU 使用单线程，那么只要这个线程阻塞了，比方说远程读取某个数据吧，对端迟迟未返回又没有设置超时时间，那么你的整个程序在数据返回回来之前就停止运行了。多线程可以防止这个问题，多条线程同时运行，哪怕一条线程的代码执行读取数据阻塞，也不会影响其它任务的执行。

3.  便于建模
    这是另外一个没有这么明显的优点了。假设有一个大的任务 A，单线程编程，那么就要考虑很多，建立整个程序模型比较麻烦。但是如果把这个大的任务 A 分解成几个小任务，任务B、任务 C、任务 D，分别建立程序模型，并通过多线程分别运行这几个任务，那就简单很多了。


# 730.线程和进程的区别是什么？

> 原文：[https://zwmst.com/4666.html](https://zwmst.com/4666.html)

进程和线程的主要差别在于它们是不同的操作系统资源管理方式。进程有独立的地址空间，一个进程崩溃后，在保护模式下不会对其它进程产生影响，而线程只是一个进程中的不同执行路径。线程有自己的堆栈和局部变量，但线程之间没有单独的地址空间，一个线程死掉就等于整个进程死掉，所以多进程的程序要比多线程的程序健壮，但在进程切换时，耗费资源较大，效率要差一些。但对于一些要求同时进行并且又要共享某些变量的并发操作，只能用线程，不能用进程。


# 731.Java 实现线程有哪几种方式？

> 原文：[https://zwmst.com/4668.html](https://zwmst.com/4668.html)

1.  继承 Thread 类实现多线程
2.  实现 Runnable 接口方式实现多线程
3.  使用 ExecutorService、Callable、Future 实现有返回结果的多线程


# 732.启动线程方法 start()和 run()有什么区别

> 原文：[https://zwmst.com/4670.html](https://zwmst.com/4670.html)

只有调用了 start()方法，才会表现出多线程的特性，不同线程的 run()方法里面的代码交替执行。如果只是调用 run()方法，那么代码还是同步执行的，必须等待一个线程的 run()方法里面的代码全部执行完毕之后，另外一个线程才可以执行其 run()方法里面的代码。


# 733.怎么终止一个线程？如何优雅地终止线程？

> 原文：[https://zwmst.com/4672.html](https://zwmst.com/4672.html)

stop 终止，不推荐


# 734.一个线程的生命周期有哪几种状态？它们之间如何流转的？

> 原文：[https://zwmst.com/4675.html](https://zwmst.com/4675.html)

**NEW**：毫无疑问表示的是刚创建的线程，还没有开始启动。
**RUNNABLE**: 表示线程已经触发 start()方式调用，线程正式启动，线程处于运行中状态。
**BLOCKED**：表示线程阻塞，等待获取锁，如碰到 synchronized、lock 等关键字等占用临界区的情况，一旦获取到锁就进行 RUNNABLE 状态继续运行。
**WAITING**：表示线程处于无限制等待状态，等待一个特殊的事件来重新唤醒，如通过wait()方法进行等待的线程等待一个 notify()或者 notifyAll()方法，通过 join()方法进行等待的线程等待目标线程运行结束而唤醒，一旦通过相关事件唤醒线程，线程就进入了 RUNNABLE 状态继续运行。
**TIMED_WAITING**：表示线程进入了一个有时限的等待，如 sleep(3000)，等待 3 秒后线程重新进行 RUNNABLE 状态继续运行。
**TERMINATED**：表示线程执行完毕后，进行终止状态。需要注意的是，一旦线程通过 start 方法启动后就再也不能回到初始 NEW 状态，线程终止后也不能再回到RUNNABLE 状


# 735.线程中的 wait()和 sleep()方法有什么区别

> 原文：[https://zwmst.com/4677.html](https://zwmst.com/4677.html)

这个问题常问，sleep 方法和 wait 方法都可以用来放弃 CPU 一定的时间，不同点在于如果线程持有某个对象的监视器，sleep 方法不会放弃这个对象的监视器，wait方法会放弃这个对象的监视器


# 736.多线程同步有哪几种方法？

> 原文：[https://zwmst.com/4679.html](https://zwmst.com/4679.html)

Synchronized 关键字，Lock 锁实现，分布式锁等


# 737.什么是死锁？如何避免死锁？

> 原文：[https://zwmst.com/4681.html](https://zwmst.com/4681.html)

死锁就是两个线程相互等待对方释放对象锁。


# 738.多线程之间如何进行通信？

> 原文：[https://zwmst.com/4683.html](https://zwmst.com/4683.html)

wait/notify


# 739.线程怎样拿到返回结果？

> 原文：[https://zwmst.com/4685.html](https://zwmst.com/4685.html)

实现Callable 接口。


# 740.violatile 关键字的作用

> 原文：[https://zwmst.com/4687.html](https://zwmst.com/4687.html)

volatile 关键字的作用主要有两个：

1.  多线程主要围绕可见性和原子性两个特性而展开，使用 volatile 关键字修饰的变量，保证了其在多线程之间的可见性，即每次读取到 volatile 变量，一定是最新的数据
2.  代码底层执行不像我们看到的高级语言—-Java 程序这么简单，它的执行是 Java代码–>字节码–>根据字节码执行对应的 C/C++代码–>C/C++代码被编译成汇编语言–>和硬件电路交互，现实中，为了获取更好的性能 JVM 可能会对指令进行重排序，多线程下可能会出现一些意想不到的问题。使用 volatile 则会对禁止语义重排序，当然这也一定程度上降低了代码执行效率从实践角度而言，volatile 的一个重要 作 用 就 是 和 CAS 结 合 ， 保 证 了 原 子 性 ， 详 细 的 可 以 参 见java.util.concurrent.atomic 包下的类，比如 AtomicInteger。


# 741.新建 T1、T2、T3 三个线程，如何保证它们按顺序执行？

> 原文：[https://zwmst.com/4689.html](https://zwmst.com/4689.html)

用 join 方法。


# 742.怎么控制同一时间只有 3 个线程运行？

> 原文：[https://zwmst.com/4691.html](https://zwmst.com/4691.html)

用 Semaphore。


# 743.为什么要使用线程池

> 原文：[https://zwmst.com/4736.html](https://zwmst.com/4736.html)

我们知道不用线程池的话，每个线程都要通过 new Thread(xxRunnable).start()的方式来创建并运行一个线程，线程少的话这不会是问题，而真实环境可能会开启多个线程让系统和程序达到最佳效率，当线程数达到一定数量就会耗尽系统的 CPU 和内存资源，也会造成 GC频繁收集和停顿，因为每次创建和销毁一个线程都是要消耗系统资源的，如果为每个任务都创建线程这无疑是一个很大的性能瓶颈。所以，线程池中的线程复用极大节省了系统资源，当线程一段时间不再有任务处理时它也会自动销毁，而不会长驻内存。


# 744.常用的几种线程池并讲讲其中的工作原理。

> 原文：[https://zwmst.com/4738.html](https://zwmst.com/4738.html)

**什么是线程池？
很简单，简单看名字就知道是装有线程的池子，我们可以把要执行的多线程交给线程池来处理，和连接池的概念一样，通过维护一定数量的线程池来达到多个线程的复用。
**线程池的好处
我们知道不用线程池的话，每个线程都要通过 new Thread(xxRunnable).start()的方式来创建并运行一个线程，线程少的话这不会是问题，而真实环境可能会开启多个线程让系统和程序达到最佳效率，当线程数达到一定数量就会耗尽系统的 CPU 和内存资源，也会造成 GC频繁收集和停顿，因为每次创建和销毁一个线程都是要消耗系统资源的，如果为每个任务都创建线程这无疑是一个很大的性能瓶颈。所以，线程池中的线程复用极大节省了系统资源，当线程一段时间不再有任务处理时它也会自动销毁，而不会长驻内存。
**线程池核心类
在 java.util.concurrent 包中我们能找到线程池的定义，其中 ThreadPoolExecutor 是我们线程池核心类，首先看看线程池类的主要参数有哪些。
**如何提交线程
如 可 以 先 随 便 定 义 一 个 固 定 大 小 的 线 程 池

```
ExecutorService es = Executors.newFixedThreadPool(3);
```

提交一个线程

```
es.submit(xxRunnble);
es.execute(xxRunnble);
```

**submit 和 execute 分别有什么区别呢？
execute 没有返回值，如果不需要知道线程的结果就使用 execute 方法，性能会好很多。
submit 返回一个 Future 对象，如果想知道线程结果就使用 submit 提交，而且它能在主线程中通过 Future 的 get 方法捕获线程中的异常。
**如何关闭线程池

```
es.shutdown();
```

不再接受新的任务，之前提交的任务等执行结束再关闭线程池。

```
es.shutdownNow();
```

不再接受新的任务，试图停止池中的任务再关闭线程池，返回所有未处理的线程list 列表。


# 745.线程池启动线程 submit()和 execute()方法有什么不同

> 原文：[https://zwmst.com/4740.html](https://zwmst.com/4740.html)

execute 没有返回值，如果不需要知道线程的结果就使用 execute 方法，性能会好很多。
submit 返回一个 Future 对象，如果想知道线程结果就使用 submit 提交，而且它能在主线程中通过 Future 的 get 方法捕获线程中的异常


# 746.CyclicBarrier 和 CountDownLatch 的区别？

> 原文：[https://zwmst.com/4742.html](https://zwmst.com/4742.html)

两个看上去有点像的类，都在 java.util.concurrent 下，都可以用来表示代码运行到某个点上，二者的区别在于：

1.  CyclicBarrier 的某个线程运行到某个点上之后，该线程即停止运行，直到所有的线程都到达了这个点，所有线程才重新运行；CountDownLatch 则不是，某线程运行到某个点上之后，只是给某个数值-1 而已，该线程继续运行
2.  CyclicBarrier 只能唤起一个任务，CountDownLatch 可以唤起多个任务
3.  CyclicBarrier 可 重 用 ， CountDownLatch 不 可 重 用 ， 计 数 值 为 0 该CountDownLatch就不可再用了


# 747.什么是活锁、饥饿、无锁、死锁？

> 原文：[https://zwmst.com/4745.html](https://zwmst.com/4745.html)

死锁、活锁、饥饿是关于多线程是否活跃出现的运行阻塞障碍问题，如果线程出现了这三种情况，即线程不再活跃，不能再正常地执行下去了。
**死锁
死锁是多线程中最差的一种情况，多个线程相互占用对方的资源的锁，而又相互等对方释放锁，此时若无外力干预，这些线程则一直处理阻塞的假死状态，形成死锁。举个例子，A 同学抢了 B 同学的钢笔，B 同学抢了 A 同学的书，两个人都相互占用对方的东西，都在让对方先还给自己自己再还，这样一直争执下去等待对方还而又得不到解决，老师知道此事后就让他们相互还给对方，这样在外力的干预下他们才解决，当然这只是个例子没有老师他们也能很好解决，计算机不像人如果发现这种情况没有外力干预还是会一直阻塞下去的。
**活锁
活锁这个概念大家应该很少有人听说或理解它的概念，而在多线程中这确实存在。活锁恰恰与死锁相反，死锁是大家都拿不到资源都占用着对方的资源，而活锁是拿到资源却又相互释放不执行。当多线程中出现了相互谦让，都主动将资源释放给别的线程使用，这样这个资源在多个线程之间跳动而又得不到执行，这就是活锁。
**饥饿
我们知道多线程执行中有线程优先级这个东西，优先级高的线程能够插队并优先执行，这样如果优先级高的线程一直抢占优先级低线程的资源，导致低优先级线程无法得到执行，这就是饥饿。当然还有一种饥饿的情况，一个线程一直占着一个资源不放而导致其他线程得不到执行，与死锁不同的是饥饿在以后一段时间内还是能够得到执行的，如那个占用资源的线程结束了并释放了资源。
**无锁
无锁，即没有对资源进行锁定，即所有的线程都能访问并修改同一个资源，但同时只有一个线程能修改成功。无锁典型的特点就是一个修改操作在一个循环内进行，线程会不断的尝试修改共享资源，如果没有冲突就修改成功并退出否则就会继续下一次循环尝试。所以，如果有多个线程修改同一个值必定会有一个线程能修改成功，而其他修改失败的线程会不断重试直到修改成功。之前的文章我介绍过 JDK 的CAS 原理及应用即是无锁的实现。
可以看出，无锁是一种非常良好的设计，它不会出现线程出现的跳跃性问题，锁使用不当肯定会出现系统性能问题，虽然无锁无法全面代替有锁，但无锁在某些场合下是非常高效的。


# 748.什么是原子性、可见性、有序性？

> 原文：[https://zwmst.com/4747.html](https://zwmst.com/4747.html)

原子性、可见性、有序性是多线程编程中最重要的几个知识点，由于多线程情况复杂，如何让每个线程能看到正确的结果，这是非常重要的。
**原子性
原子性是指一个线程的操作是不能被其他线程打断，同一时间只有一个线程对一个变量进行操作。在多线程情况下，每个线程的执行结果不受其他线程的干扰，比如说多个线程同时对同一个共享成员变量 n++100 次，如果 n 初始值为 0，n 最后的值应该是 100，所以说它们是互不干扰的，这就是传说的中的原子性。但 n++并不是原子性的操作，要使用 AtomicInteger 保证原子性。
**可见性
可见性是指某个线程修改了某一个共享变量的值，而其他线程是否可以看见该共享变量修改后的值。在单线程中肯定不会有这种问题，单线程读到的肯定都是最新的值，而在多线程编程中就不一定了。每个线程都有自己的工作内存，线程先把共享变量的值从主内存读到工作内存，形成一个副本，当计算完后再把副本的值刷回主
内存，从读取到最后刷回主内存这是一个过程，当还没刷回主内存的时候这时候对其他线程是不可见的，所以其他线程从主内存读到的值是修改之前的旧值。像CPU 的缓存优化、硬件优化、指令重排及对 JVM 编译器的优化，都会出现可见性的问题。
**有序性
我们都知道程序是按代码顺序执行的，对于单线程来说确实是如此，但在多线程情况下就不是如此了。为了优化程序执行和提高 CPU 的处理性能，JVM 和操作系统都会对指令进行重排，也就说前面的代码并不一定都会在后面的代码前面执行，即后面的代码可能会插到前面的代码之前执行，只要不影响当前线程的执行结果。所
以，指令重排只会保证当前线程执行结果一致，但指令重排后势必会影响多线程的执行结果。虽然重排序优化了性能，但也是会遵守一些规则的，并不能随便乱排序，只是重排序会影响多线程执行的结果。


# 749.什么是守护线程？有什么用？

> 原文：[https://zwmst.com/4749.html](https://zwmst.com/4749.html)

什么是守护线程？与守护线程相对应的就是用户线程，守护线程就是守护用户线程，当用户线程全部执行完结束之后，守护线程才会跟着结束。也就是守护线程必须伴随着用户线程，如果一个应用内只存在一个守护线程，没有用户线程，守护线程自然会退出。


# 750.一个线程运行时发生异常会怎样？

> 原文：[https://zwmst.com/4751.html](https://zwmst.com/4751.html)

如果异常没有被捕获该线程将会停止执行。Thread.UncaughtExceptionHandler 是用于处理未捕获异常造成线程突然中断情况的一个内嵌接口。当一个未捕获异常将造成线程中断的时 候 JVM 会 使 用Thread.getUncaughtExceptionHandler() 来 查 询 线程 的UncaughtExceptionHandler 并 将 线 程 和 异 常 作 为 参 数 传 递 给 handler 的uncaughtException()方法进行处理。


# 751.线程 yield()方法有什么用？

> 原文：[https://zwmst.com/4753.html](https://zwmst.com/4753.html)

Yield 方法可以暂停当前正在执行的线程对象，让其它有相同优先级的线程执行。
它是一个静态方法而且只保证当前线程放弃 CPU 占用而不能保证使其它线程一定能占用 CPU，执行yield()的线程有可能在进入到暂停状态后马上又被执行。


# 752.什么是重入锁？

> 原文：[https://zwmst.com/4755.html](https://zwmst.com/4755.html)

所谓重入锁，指的是以线程为单位，当一个线程获取对象锁之后，这个线程可以再次获取本对象上的锁，而其他的线程是不可以的。


# 753.Synchronized 有哪几种用法？

> 原文：[https://zwmst.com/4757.html](https://zwmst.com/4757.html)

锁类、锁方法、锁代码块。


# 754.Fork/Join 框架是干什么的？

> 原文：[https://zwmst.com/4759.html](https://zwmst.com/4759.html)

大任务自动分散小任务，并发执行，合并小任务结果。


# 756.线程数过多会造成什么异常？

> 原文：[https://zwmst.com/4761.html](https://zwmst.com/4761.html)

线程过多会造成栈溢出，也有可能会造成堆异常。


# 757.说说线程安全的和不安全的集合。

> 原文：[https://zwmst.com/4763.html](https://zwmst.com/4763.html)

Java 中平时用的最多的 Map 集合就是 HashMap 了，它是线程不安全的。看下面两个场景：
1、当用在方法内的局部变量时，局部变量属于当前线程级别的变量，其他线程访问不了，所以这时也不存在线程安全不安全的问题了。
2、当用在单例对象成员变量的时候呢？这时候多个线程过来访问的就是同一个HashMap 了，对同个 HashMap 操作这时候就存在线程安全的问题了。


# 758.什么是 CAS 算法？在多线程中有哪些应用

> 原文：[https://zwmst.com/4765.html](https://zwmst.com/4765.html)

CAS，全称为 Compare and Swap，即比较-替换。假设有三个操作数：内存值 V、旧的预期值 A、要修改的值 B，当且仅当预期值 A 和内存值 V 相同时，才会将内存值修改为 B 并返回 true，否则什么都不做并返回 false。当然 CAS 一定要 volatile变量配合，这样才能保证每次拿到的变量是主内存中最新的那个值，否则旧的预期值 A 对某条线程来说，永远是一个不会变的值 A，只要某次 CAS 操作失败，永远都不可能成功。
java.util.concurrent.atomic 包下面的 Atom****类都有 CAS 算法的应用


# 759.怎么检测一个线程是否拥有锁？

> 原文：[https://zwmst.com/4767.html](https://zwmst.com/4767.html)

java.lang.Thread#holdsLock 方法


# 755.Jdk 中排查多线程问题用什么命令？

> 原文：[https://zwmst.com/4770.html](https://zwmst.com/4770.html)

jstack


# 760.线程同步需要注意什么？

> 原文：[https://zwmst.com/4772.html](https://zwmst.com/4772.html)

1.  尽量缩小同步的范围，增加系统吞吐量。
2.  分布式同步锁无意义，要使用分布式锁。
3.  防止死锁，注意加锁顺序。


# 761.线程 wait()方法使用有什么前提

> 原文：[https://zwmst.com/4776.html](https://zwmst.com/4776.html)

要在同步块中使用。


# 762.Fork/Join 框架使用有哪些要注意的地方？

> 原文：[https://zwmst.com/4778.html](https://zwmst.com/4778.html)

如果任务拆解的很深，系统内的线程数量堆积，导致系统性能性能严重下降；
如果函数的调用栈很深，会导致栈内存溢出；


# 763.线程之间如何传递数据？

> 原文：[https://zwmst.com/4780.html](https://zwmst.com/4780.html)

通 过 在 线 程 之 间 共 享 对 象 就 可 以 了 ， 然 后 通 过 wait/notify/notifyAll 、await/signal/signalAll 进行唤起和等待，比方说阻塞队列 BlockingQueue 就是为线程之间共享数据而设计的


# 764.保证”可见性”有哪几种方式？

> 原文：[https://zwmst.com/4782.html](https://zwmst.com/4782.html)

synchronized 和 viotatile


# 765.说几个常用的 Lock 接口实现锁

> 原文：[https://zwmst.com/4784.html](https://zwmst.com/4784.html)

ReentrantLock、ReadWriteLock


# 766.ThreadLocal 是什么？有什么应用场景？

> 原文：[https://zwmst.com/4786.html](https://zwmst.com/4786.html)

ThreadLocal 的作用是提供线程内的局部变量，这种变量在线程的生命周期内起作用，减少同一个线程内多个函数或者组件之间一些公共变量的传递的复杂度。用来解决数据库连接、Session 管理等。


# 767.ReadWriteLock 有什么用？

> 原文：[https://zwmst.com/4788.html](https://zwmst.com/4788.html)

ReadWriteLock 是一个读写锁接口，ReentrantReadWriteLock 是 ReadWriteLock 接口的一个具体实现，实现了读写的分离，读锁是共享的，写锁是独占的，读和读之间不会互斥，读和写、写和读、写和写之间才会互斥，提升了读写的性能。


# 768.FutureTask 是什么？

> 原文：[https://zwmst.com/4790.html](https://zwmst.com/4790.html)

FutureTask 表示一个异步运算的任务，FutureTask 里面可以传入一个 Callable 的具体实现类，可以对这个异步运算的任务的结果进行等待获取、判断是否已经完成、取消任务等操作。


# 769.怎么唤醒一个阻塞的线程？

> 原文：[https://zwmst.com/4792.html](https://zwmst.com/4792.html)

如果线程是因为调用了 wait()、sleep()或者 join()方法而导致的阻塞，可以中断线程，并且通过抛出 InterruptedException 来唤醒它；如果线程遇到了 IO 阻塞，无能为力，因为 IO是操作系统实现的，Java 代码并没有办法直接接触到操作系统。


# 770.不可变对象对多线程有什么帮助？

> 原文：[https://zwmst.com/4794.html](https://zwmst.com/4794.html)

不可变对象保证了对象的内存可见性，对不可变对象的读取不需要进行额外的同步手段，提升了代码执行效率。


# 771.多线程上下文切换是什么意思？

> 原文：[https://zwmst.com/4796.html](https://zwmst.com/4796.html)

多线程的上下文切换是指 CPU 控制权由一个已经正在运行的线程切换到另外一个就绪并等待获取 CPU 执行权的线程的过程。


# 772.Java 中用到了什么线程调度算法？

> 原文：[https://zwmst.com/4798.html](https://zwmst.com/4798.html)

抢占式。一个线程用完 CPU 之后，操作系统会根据线程优先级、线程饥饿情况等数据算出一个总的优先级并分配下一个时间片给某个线程执行。


# 773.Thread.sleep(0)的作用是什么？

> 原文：[https://zwmst.com/4800.html](https://zwmst.com/4800.html)

由于 Java 采用抢占式的线程调度算法，因此可能会出现某条线程常常获取到 CPU控制权的情况，为了让某些优先级比较低的线程也能获取到 CPU 控制权，可以使用 Thread.sleep(0)手动触发一次操作系统分配时间片的操作，这也是平衡 CPU 控制权的一种操作。


# 774.Java 内存模型是什么，哪些区域是线程共享的，哪些是不共享 的？

> 原文：[https://zwmst.com/4802.html](https://zwmst.com/4802.html)

我们知道的 JVM 内存区域有：堆和栈，这是一种泛的分法，也是按运行时区域的一种分法，堆是所有线程共享的一块区域，而栈是线程隔离的，每个线程互不共享。线程不共享区域每个线程的数据区域包括程序计数器、虚拟机栈和本地方法栈，它们都是在新线程创建时才创建的。
**程序计数器（Program Counter Rerister）
程序计数器区域一块内存较小的区域，它用于存储线程的每个执行指令，每个线程都有自己的程序计数器，此区域不会有内存溢出的情况。
**虚拟机栈（VM Stack）
虚拟机栈描述的是 Java 方法执行的内存模型，每个方法被执行的时候都会同时创建一个栈帧（Stack Frame）用于存储局部变量表、操作数栈、动态链接、方法出口等信息。每一个方法被调用直至执行完成的过程就对应着一个栈帧在虚拟机栈中从入栈到出栈的过程。
**本地方法栈（Native Method Stack）
本地方法栈用于支持本地方法（native 标识的方法，即非 Java 语言实现的方法）。虚拟机栈和本地方法栈，当线程请求分配的栈容量超过 JVM 允许的最大容量时抛出StackOverflowError 异常。
**线程共享区域
线程共享区域包含：堆和方法区。
**堆（Heap）
堆是最常处理的区域，它存储在 JVM 启动时创建的数组和对象，JVM 垃圾收集也主要是在堆上面工作。如 果 实 际 所 需 的 堆 超 过 了 自 动 内 存 管 理 系 统 能 提 供 的 最 大 容 量 时 抛 出OutOfMemoryError 异常。
**方法区（Method Area）
方法区是可供各条线程共享的运行时内存区域。存储了每一个类的结构信息，例如运行时常量池（Runtime Constant Pool）、字段和方法数据、构造函数和普通方法的字节码内容、还包括一些在类、实例、接口初始化时用到的特殊方法。当创建类和接口时，如果构造运行时常量池所需的内存空间超过了方法区所能提供的最大内存空间后就会抛出 OutOfMemoryError
**运行时常量池（Runtime Constant Pool）
运行时常量池是方法区的一部分，每一个运行时常量池都分配在 JVM 的方法区中，在类和接口被加载到 JVM 后，对应的运行时常量池就被创建。运行时常量池是每一个类或接口的常量池（Constant_Pool）的运行时表现形式，它包括了若干种常量：编译器可知的数值字面量到必须运行期解析后才能获得的方法或字段的引用。如果方法区的内存空间不能满足内存分配请求，那 Java 虚 拟 机 将 抛 出 一 个OutOfMemoryError 异常。栈包含 Frames，当调用方法时，Frame 被推送到堆栈。一个 Frame 包含局部变量数组、操作数栈、常量池引用。


# 775.什么是乐观锁和悲观锁？

> 原文：[https://zwmst.com/4804.html](https://zwmst.com/4804.html)

**乐观锁**：就像它的名字一样，对于并发间操作产生的线程安全问题持乐观状态，乐观锁认为竞争不总是会发生，因此它不需要持有锁，将比较-替换这两个动作作为一个原子操作尝试去修改内存中的变量，如果失败则表示发生冲突，那么就应该有相应的重试逻辑。
**悲观锁**：还是像它的名字一样，对于并发间操作产生的线程安全问题持悲观状态，悲观锁认为竞争总是会发生，因此每次对某资源进行操作时，都会持有一个独占的锁，就像synchronized，不管三七二十一，直接上了锁就操作资源了。


# 776.Hashtable 的 size()方法为什么要做同步

> 原文：[https://zwmst.com/4806.html](https://zwmst.com/4806.html)

同一时间只能有一条线程执行固定类的同步方法，但是对于类的非同步方法，可以多条线程同时访问。所以，这样就有问题了，可能线程 A 在执行 Hashtable 的 put方法添加数据，线程 B 则可以正常调用 size()方法读取 Hashtable 中当前元素的个数，那读取到的值可能不是最新的，可能线程 A 添加了完了数据，但是没有对size++，线程 B 就已经读取 size了，那么对于线程 B 来说读取到的 size 一定是不准确的。而给 size()方法加了同步之后，意味着线程 B 调用 size()方法只有在线程 A调用 put 方法完毕之后才可以调用，这样就保证了线程安全性CPU 执行代码，执行的不是 Java 代码，这点很关键，一定得记住。Java 代码最终是被翻译成机器码执行的，机器码才是真正可以和硬件电路交互的代码。即使你看到 Java 代码只有一行，甚至你看到 Java 代码编译之后生成的字节码也只有一行，也不意味着对于底层来说这句语句的操作只有一个。一句"return count"假设被翻译成了三句汇编语句执行，一句汇编语句和其机器码做对应，完全可能执行完第一句，线程就切换了。


# 777.同步方法和同步块，哪种更好？

> 原文：[https://zwmst.com/4808.html](https://zwmst.com/4808.html)

同步块，这意味着同步块之外的代码是异步执行的，这比同步整个方法更提升代码的效率。
请知道一条原则：同步的范围越小越好。


# 778.什么是自旋锁？

> 原文：[https://zwmst.com/4810.html](https://zwmst.com/4810.html)

自旋锁是采用让当前线程不停地的在循环体内执行实现的，当循环的条件被其他线程改变时才能进入临界区。


# 779.Runnable 和 Thread 用哪个好？

> 原文：[https://zwmst.com/4812.html](https://zwmst.com/4812.html)

Java 不支持类的多重继承，但允许你实现多个接口。所以如果你要继承其他类，也为了减少类之间的耦合性，Runnable 会更好。


# 780.Java 中 notify 和 notifyAll 有什么区别？

> 原文：[https://zwmst.com/4814.html](https://zwmst.com/4814.html)

notify()方法不能唤醒某个具体的线程，所以只有一个线程在等待的时候它才有用武之地。
而 notifyAll()唤醒所有线程并允许他们争夺锁确保了至少有一个线程能继续运行。


# 781.为什么 wait/notify/notifyAll 这些方法不在 thread 类里面？

> 原文：[https://zwmst.com/4816.html](https://zwmst.com/4816.html)

这是个设计相关的问题，它考察的是面试者对现有系统和一些普遍存在但看起来不合理的事物的看法。回答这些问题的时候，你要说明为什么把这些方法放在 Object类里是有意义的，还有不把它放在 Thread 类里的原因。一个很明显的原因是JAVA 提供的锁是对象级的而不是线程级的，每个对象都有锁，通过线程获得。如果线程需要等待某些锁那么调用对象中的wait()方法就有意义了。如果 wait()方法定义在 Thread 类中，线程正在等待的是哪个锁就不明显了。简单的说，由于 wait，notify 和 notifyAll 都是锁级别的操作，所以把他们定义在 Object 类中因为锁属于对象。


# 782.为什么 wait 和 notify 方法要在同步块中调用？

> 原文：[https://zwmst.com/4818.html](https://zwmst.com/4818.html)

主 要 是 因 为 Java API 强 制 要 求 这 样 做 ， 如 果 你 不 这 么 做 ， 你 的 代 码会 抛 出IllegalMonitorStateException 异常。还有一个原因是为了避免 wait 和 notify之间产生竞态条件。


# 783.为什么你应该在循环中检查等待条件？

> 原文：[https://zwmst.com/4820.html](https://zwmst.com/4820.html)

处于等待状态的线程可能会收到错误警报和伪唤醒，如果不在循环中检查等待条件，程序就会在没有满足结束条件的情况下退出。因此，当一个等待线程醒来时，不能认为它原来的等待状态仍然是有效的，在 notify()方法调用之后和等待线程醒来之前这段时间它可能会改变。这就是在循环中使用 wait()方法效果更好的原因，你可以在 Eclipse 中创建模板调用 wait和 notify 试一试。


# 784.Java 中堆和栈有什么不同

> 原文：[https://zwmst.com/4822.html](https://zwmst.com/4822.html)

每个线程都有自己的栈内存，用于存储本地变量，方法参数和栈调用，一个线程中存储的变量对其它线程是不可见的。而堆是所有线程共享的一片公用内存区域。对象都在堆里创建，为了提升效率线程会从堆中弄一个缓存到自己的栈，如果多个线程使用该变量就可能引发问题，这时 volatile 变量就可以发挥作用了，它要求线程从主存中读取变量的值。


# 785.你如何在 Java 中获取线程堆栈？

> 原文：[https://zwmst.com/4824.html](https://zwmst.com/4824.html)

对于不同的操作系统，有多种方法来获得 Java 进程的线程堆栈。当你获取线程堆栈时，JVM会把所有线程的状态存到日志文件或者输出到控制台。在 Windows 你可以使用 Ctrl + Break 组合键来获取线程堆栈，Linux 下用 kill -3 命令。你也可以用 jstack 这个工具来获取，它对线程 id 进行操作，你可以用 jps 这个工具找到 id。


# 786.如何创建线程安全的单例模式？

> 原文：[https://zwmst.com/4826.html](https://zwmst.com/4826.html)

单例模式即一个 JVM 内存中只存在一个类的对象实例分类

1.  懒汉式
    类加载的时候就创建实例
2.  饿汉式
    使用的时候才创建实例


# 787.什么是阻塞式方法？

> 原文：[https://zwmst.com/4828.html](https://zwmst.com/4828.html)

阻塞式方法是指程序会一直等待该方法完成期间不做其他事情，ServerSocket 的accept()方法就是一直等待客户端连接。这里的阻塞是指调用结果返回之前，当前线程会被挂起，直到得到结果之后才会返回。此外，还有异步和非阻塞式方法在任务完成前就返回。


# 788.提交任务时线程池队列已满会时发会生什么？

> 原文：[https://zwmst.com/4830.html](https://zwmst.com/4830.html)

当线程数小于最大线程池数 maximumPoolSize 时就会创建新线程来处理，而线程数大于等于最大线程池数 maximumPoolSize 时就会执行拒绝策略


# 789.什么是线程？

> 原文：[https://zwmst.com/4832.html](https://zwmst.com/4832.html)

线程是操作系统能够进⾏运算调度的最⼩单位，它被包含在进程之中，是进程中的实际运作单位，可以使⽤线程对进⾏运算提速。
⽐如，如果⼀个线程完成⼀个任务要100毫秒，那么⽤⼗个线程完成改任务只需10毫秒


# 790\. 什么是线程安全和线程不安全？

> 原文：[https://zwmst.com/4834.html](https://zwmst.com/4834.html)

1.  线程安全
    线程安全: 就是多线程访问时，采⽤了加锁机制，当⼀个线程访问该类的某个数据时，进⾏保护，其他线程能进⾏访问，直到该线程读取完，其他线程才可使⽤。不会出现数据不⼀致或者数据污染。

Vector 是⽤同步⽅法来实现线程安全的, ⽽和它相似的ArrayList不是线程安全的。

2.  线程不安全
    线程不安全：就是不提供数据访问保护，有可能出现多个线程先后更改数据造成所得到的数据是脏数据线程安全问题都是由全局变量及静态变量引起的。

若每个线程中对全局变量、静态变量只有读操作，⽽⽆写操作，⼀般来说，这个全局变量是线程安全的；若多个线程同时执⾏写操作，⼀般都需要考虑线程同步，否则的话就可能影响线程安全。


# 791.什么是⾃旋锁？

> 原文：[https://zwmst.com/4836.html](https://zwmst.com/4836.html)

⾃旋锁是SMP架构中的⼀种low-level的同步机制。

1.  当线程A想要获取⼀把⾃旋锁⽽该锁⼜被其它线程锁持有时，线程A会在⼀个循环中⾃旋以检测锁是不是已经可⽤了。
2.  ⾃选锁需要注意：
    由于⾃旋时不释放CPU，因⽽持有⾃旋锁的线程应该尽快释放⾃旋锁，否则等待该⾃旋锁的线程会⼀直在那⾥⾃旋，这就会浪费CPU时间。
    持有⾃旋锁的线程在sleep之前应该释放⾃旋锁以便其它线程可以获得⾃旋锁。
3.  ⽬前的JVM实现⾃旋会消耗CPU，如果⻓时间不调⽤doNotify⽅法，doWait⽅法会⼀直⾃旋，CPU会消耗太⼤
4.  ⾃旋锁⽐较适⽤于锁使⽤者保持锁时间⽐较短的情况，这种情况⾃旋锁的效率⽐较⾼。
5.  ⾃旋锁是⼀种对多处理器相当有效的机制，⽽在单处理器⾮抢占式的系统中基本上没有作⽤。


# 792.什么是CAS？

> 原文：[https://zwmst.com/4838.html](https://zwmst.com/4838.html)

1.  CAS（compare and swap）的缩写，中⽂翻译成⽐较并交换。
2.  CAS 不通过JVM,直接利⽤java本地⽅ JNI（Java Native Interface为JAVA本地调⽤）,直接调⽤CPU 的cmpxchg（是汇编指令）指令。
3.  利⽤CPU的CAS指令，同时借助JNI来完成Java的⾮阻塞算法,实现原⼦操作。其它原⼦操作都是利⽤类似的特性完成的。
4.  整个java.util.concurrent都是建⽴在CAS之上的，因此对于synchronized阻塞算法，J.U.C在性能上有了很⼤的提升。
5.  CAS是项乐观锁技术，当多个线程尝试使⽤CAS同时更新同⼀个变量时，只有其中⼀个线程能更新变量的值，⽽其它线程都失败，失败的线程并不会被挂起，⽽是被告知这次竞争中失败，并可以再次尝试。
    `1、使⽤CAS在线程冲突严重时，会⼤幅降低程序性能；CAS只适合于线程冲突较少的情况使⽤。`
    `2、synchronized在jdk1.6之后，已经改进优化。synchronized的底层实现主要依靠Lock-Free的队列，基本思路是⾃旋后阻塞，竞争切换后继续竞争锁，稍微牺牲了公平性，但获得了⾼吞吐量。在线程冲突较少的情况下，可以获得和CAS类似的性能；⽽线程冲突严重的情况下，性能远⾼于CAS。`


# 793\. 什么是乐观锁和悲观锁？

> 原文：[https://zwmst.com/4840.html](https://zwmst.com/4840.html)

1.  悲观锁
    Java在JDK1.5之前都是靠synchronized关键字保证同步的，这种通过使⽤⼀致的锁定协议来协调对共享状态的访问，可以确保⽆论哪个线程持有共享变量的锁，都采⽤独占的⽅式来访问这些变量。独占锁其实就是⼀种悲观锁，所以可以说synchronized是悲观锁。
2.  乐观锁
    乐观锁（ Optimistic Locking）其实是⼀种思想。相对悲观锁⽽⾔，乐观锁假设认为数据⼀般情况下不会造成冲突，所以在数据进⾏提交更新的时候，才会正式对数据的冲突与否进⾏检测，如果发现冲突了，则让返回⽤户错误的信息，让⽤户决定如何去做。

`memcached使⽤了cas乐观锁技术保证数据⼀致性。`


# 794.什么是AQS？

> 原文：[https://zwmst.com/4842.html](https://zwmst.com/4842.html)

1.  AbstractQueuedSynchronizer简称AQS，是⼀个⽤于构建锁和同步容器的框架。事实上concurrent包内许多类都是基于AQS构建，例如ReentrantLock，Semaphore，CountDownLatch，ReentrantReadWriteLock，FutureTask等。AQS解决了在实现同步容器时设计的⼤量细节问题。
2.  AQS使⽤⼀个FIFO的队列表示排队等待锁的线程，队列头节点称作“哨兵节点”或者“哑节点”，它不与任何线程关联。

其他的节点与等待线程关联，每个节点维护⼀个等待状态waitStatus。


# 795\. 什么是原⼦操作？在Java Concurrency API中有哪些原⼦类(atomic classes)？

> 原文：[https://zwmst.com/4844.html](https://zwmst.com/4844.html)

1.  原⼦操作是指⼀个不受其他操作影响的操作任务单元。原⼦操作是在多线程环境下避免数据不⼀致必须的⼿段。
2.  int++并不是⼀个原⼦操作，所以当⼀个线程读取它的值并加1时，另外⼀个线程有可能会读到之前的值，这就会引发错误。
3.  为了解决这个问题，必须保证增加操作是原⼦的，在JDK1.5之前我们可以使⽤同步技术来做到这⼀点。

到JDK1.5，java.util.concurrent.atomic包提供了int和long类型的装类，它们可以⾃动的保证对于他们的操作是原⼦的并且不需要使⽤同步。


# 796.什么是Executors框架？

> 原文：[https://zwmst.com/4847.html](https://zwmst.com/4847.html)

Java通过Executors提供四种线程池，分别为：

1.  newCachedThreadPool创建⼀个可缓存线程池，如果线程池⻓度超过处理需要，可灵活回收空闲线程，若⽆可回收，则新建线程。
2.  newFixedThreadPool 创建⼀个定⻓线程池，可控制线程最⼤并发数，超出的线程会在队列中等待。
3.  newScheduledThreadPool 创建⼀个定⻓线程池，⽀持定时及周期性任务执⾏。
4.  newSingleThreadExecutor 创建⼀个单线程化的线程池，它只会⽤唯⼀的⼯作线程来执⾏任务，保证所有任务按照指定顺序(FIFO, LIFO, 优先级)执⾏。


# 797\. 什么是阻塞队列？如何使⽤阻塞队列来实现⽣产者-消费者模型？

> 原文：[https://zwmst.com/4849.html](https://zwmst.com/4849.html)

1.  JDK7提供了7个阻塞队列。（也属于并发容器）
    1.  ArrayBlockingQueue ：⼀个由数组结构组成的有界阻塞队列。
    2.  LinkedBlockingQueue ：⼀个由链表结构组成的有界阻塞队列。
    3.  PriorityBlockingQueue ：⼀个⽀持优先级排序的⽆界阻塞队列。
    4.  DelayQueue：⼀个使⽤优先级队列实现的⽆界阻塞队列。
    5.  SynchronousQueue：⼀个不存储元素的阻塞队列。
    6.  LinkedTransferQueue：⼀个由链表结构组成的⽆界阻塞队列。
    7.  LinkedBlockingDeque：⼀个由链表结构组成的双向阻塞队列。
2.  概念：阻塞队列是⼀个在队列基础上⼜⽀持了两个附加操作的队列。
3.  2个附加操作：
    ⽀持阻塞的插⼊⽅法：队列满时，队列会阻塞插⼊元素的线程，直到队列不满。
    ⽀持阻塞的移除⽅法：队列空时，获取元素的线程会等待队列变为⾮空。


# 798.什么是Callable和Future?

> 原文：[https://zwmst.com/4852.html](https://zwmst.com/4852.html)

1.  Callable 和 Future 是⽐较有趣的⼀对组合。当我们需要获取线程的执⾏结果时，就需要⽤到它们。Callable⽤于产⽣结果，Future⽤于获取结果。
2.  Callable接⼝使⽤泛型去定义它的返回类型。Executors类提供了⼀些有⽤的⽅法去在线程池中执⾏Callable内的任务。由于Callable任务是并⾏的，必须等待它返回的结果。java.util.concurrent.Future对象解决了这个问题。
3.  在线程池提交Callable任务后返回了⼀个Future对象，使⽤它可以知道Callable任务的状态和得到Callable返回的执⾏结果。Future提供了get()⽅法，等待Callable结束并获取它的执⾏结果。


# 799.什么是FutureTask?

> 原文：[https://zwmst.com/4854.html](https://zwmst.com/4854.html)

1.  FutureTask可⽤于异步获取执⾏结果或取消执⾏任务的场景。通过传⼊Runnable或者Callable的任务给FutureTask，直接调⽤其run⽅法或者放⼊线程池执⾏，之后可以在外部通过FutureTask的get⽅法异步获取执⾏结果，因此，FutureTask⾮常适合⽤于耗时的计算，主线程可以在完成⾃⼰的任务后，再去获取结果。另外，FutureTask还可以确保即使调⽤了多次run⽅法，它都只会执⾏⼀次Runnable或者Callable任务，或者通过cancel取消FutureTask的执⾏等。
2.  futuretask可⽤于执⾏多任务、以及避免⾼并发情况下多次创建数据机锁的出现。


# 800.什么是同步容器和并发容器的实现？

> 原文：[https://zwmst.com/4856.html](https://zwmst.com/4856.html)

1.  同步容器
    1.  主要代表有Vector和Hashtable，以及Collections.synchronizedXxx等。
    2.  锁的粒度为当前对象整体。
    3.  迭代器是及时失败的，即在迭代的过程中发现被修改，就会抛出ConcurrentModificationException。
2.  并发容器
    1.  主要代表有ConcurrentHashMap、CopyOnWriteArrayList、ConcurrentSkipListMap、ConcurrentSkipListSet。
    2.  锁的粒度是分散的、细粒度的，即读和写是使⽤不同的锁。
    3.  迭代器具有弱⼀致性，即可以容忍并发修改，不会抛出ConcurrentModificationException。

`ConcurrentHashMap`
`采⽤分段锁技术，同步容器中，是⼀个容器⼀个锁，但在ConcurrentHashMap中，会将hash表的数组部分分成若⼲段，每段维护⼀个锁，以达到⾼效的并发访问；`


# 801.什么是多线程的上下⽂切换？

> 原文：[https://zwmst.com/4858.html](https://zwmst.com/4858.html)

1.  多线程：是指从软件或者硬件上实现多个线程的并发技术。
2.  多线程的好处：
    1.  使⽤多线程可以把程序中占据时间⻓的任务放到后台去处理，如图⽚、视屏的下载
    2.  发挥多核处理器的优势，并发执⾏让系统运⾏的更快、更流畅，⽤户体验更好
3.  多线程的缺点：
    1.  ⼤量的线程降低代码的可读性；
    2.  更多的线程需要更多的内存空间
    3.  当多个线程对同⼀个资源出现争夺时候要注意线程安全的问题。
4.  多线程的上下⽂切换：
    CPU通过时间⽚分配算法来循环执⾏任务，当前任务执⾏⼀个时间⽚后会切换到下⼀个任务。但是，在切换前会保存上⼀个任务的状态，以便下次切换回这个任务时，可以再次加载这个任务的状态


# 802.ThreadLocal的设计理念与作⽤？

> 原文：[https://zwmst.com/4860.html](https://zwmst.com/4860.html)

Java中的ThreadLocal类允许我们创建只能被同⼀个线程读写的变量。因此，如果⼀段代码含有⼀个ThreadLocal变量的引⽤，即使两个线程同时执⾏这段代码，它们也⽆法访问到对⽅的ThreadLocal变量。

1.  概念：线程局部变量。在并发编程的时候，成员变量如果不做任何处理其实是线程不安全的，各个线程都在操作同⼀个变量，显然是不⾏的，并且我们也知道volatile这个关键字也是不能保证线程安全的。那么在有⼀种情况之下，我们需要满⾜这样⼀个条件：变量是同⼀个，但是每个线程都使⽤同⼀个初始值，也就是使⽤同⼀个变量的⼀个新的副本。这种情况之下ThreadLocal就⾮常适⽤，⽐如说DAO的数据库连接，我们知道DAO是单例的，那么他的属性Connection就不是⼀个线程安全的变量。⽽我们每个线程都需要使⽤他，并且各⾃使⽤各⾃的。这种情况，ThreadLocal就⽐较好的解决了这个问题。
2.  原理：从本质来讲，就是每个线程都维护了⼀个map，⽽这个map的key就是threadLocal，⽽值就是我们set的那个值，每次线程在get的时候，都从⾃⼰的变量中取值，既然从⾃⼰的变量中取值，那肯定就不存在线程安全问题，总体来讲，ThreadLocal这个变量的状态根本没有发⽣变化，他仅仅是充当⼀个key的⻆⾊，另外提供给每⼀个线程⼀个初始值。
3.  实现机制：每个Thread对象内部都维护了⼀个ThreadLocalMap这样⼀个ThreadLocal的Map，可以存放若⼲个ThreadLocal。

    ```
    1 /* ThreadLocal values pertaining to this thread. This map is maintained
    2 * by the ThreadLocal class. */
    3 ThreadLocal.ThreadLocalMap threadLocals = null;
    ```

4.  应⽤场景：当很多线程需要多次使⽤同⼀个对象，并且需要该对象具有相同初始化值的时候最适合使⽤ThreadLocal。


# 803.ThreadPool（线程池）⽤法与优势？

> 原文：[https://zwmst.com/4862.html](https://zwmst.com/4862.html)

1.  ThreadPool 优点
    1.  减少了创建和销毁线程的次数，每个⼯作线程都可以被重复利⽤，可执⾏多个任务
    2.  可以根据系统的承受能⼒，调整线程池中⼯作线线程的数⽬，防⽌因为因为消耗过多的内存，⽽把服务器累趴下(每个线程需要⼤约1MB内存，线程开的越多，消耗的内存也就越⼤，最后死机)
        1.  减少在创建和销毁线程上所花的时间以及系统资源的开销
        2.  如不使⽤线程池，有可能造成系统创建⼤量线程⽽导致消耗完系统内存
2.  ⽐较重要的⼏个类：

| 类 | 描述 |
| --- | --- |
| ExecutorService | 真正的线程池接⼝。 |
| ScheduledExecutorService | 能和Timer/TimerTask类似，解决那些需要任务重复执⾏的问题。 |
| ThreadPoolExecutor | ExecutorService的默认实现。 |
| ScheduledThreadPoolExecutor | 继承ThreadPoolExecutor的ScheduledExecutorService接⼝实现，周期性任务调度的类实现。 |

`Java⾥⾯线程池的顶级接⼜是Executor，但是严格意义上讲Executor并不是⼀个线程池，⽽只是⼀个执⾏线程的⼯具。真正的线程池接⼜是ExecutorService。`

3.  任务执⾏顺序：
    ![](img/3c3e68ad347f666cc4e2eed182bae4e6.png)
    1.  当线程数⼩于corePoolSize时，创建线程执⾏任务。
    2.  当线程数⼤于等于corePoolSize并且workQueue没有满时，放⼊workQueue中
    3.  线程数⼤于等于corePoolSize并且当workQueue满时，新任务新建线程运⾏，线程总数要⼩于maximumPoolSize
    4.  当线程总数等于maximumPoolSize并且workQueue满了的时候执⾏handler的rejectedExecution。也就是拒绝策略。


# 804\. Concurrent包⾥的其他东⻄：ArrayBlockingQueue、CountDownLatch等等。

> 原文：[https://zwmst.com/4865.html](https://zwmst.com/4865.html)

1.  ArrayBlockingQueue 数组结构组成的有界阻塞队列：
2.  CountDownLatch 允许⼀个或多个线程等待其他线程完成操作；

join⽤于让当前执⾏线程等待join线程执⾏结束。其实现原理是不停检查join线程是否存活，如果join线程存活则让当前线程永远wait


# 805.synchronized和ReentrantLock的区别？

> 原文：[https://zwmst.com/4867.html](https://zwmst.com/4867.html)

1.  基础知识
    **可重⼊锁**。可重⼊锁是指同⼀个线程可以多次获取同⼀把锁。ReentrantLock和synchronized都是可重⼊锁。
    **可中断锁**。可中断锁是指线程尝试获取锁的过程中，是否可以响应中断。synchronized是不可中断锁，⽽ReentrantLock则提供了中断功能。
    **公平锁与⾮公平锁**。公平锁是指多个线程同时尝试获取同⼀把锁时，获取锁的顺序按照线程达到的顺序，⽽⾮公平锁则允许线程“插队”。synchronized是⾮公平锁，⽽ReentrantLock的默认实现是⾮公平锁，但是也可以设置为公平锁。
    **CAS操作(CompareAndSwap)**。CAS操作简单的说就是⽐较并交换。CAS 操作包含三个操作数 —— 内存位置（V）、预期原值（A）和新值(B)。如果内存位置的值与预期原值相匹配，那么处理器会⾃动将该位置值更新为新值。否则，处理器不做任何操作。⽆论哪种情况，它都会在 CAS 指令之前返回该位置的值。CAS 有效地说明了“我认为位置 V 应该包含值 A；如果包含该值，则将 B 放到这个位置；否则，不要更改该位置，只告诉我这个位置现在的值即可。”

2.  Synchronized

    1.  synchronized是java内置的关键字，它提供了⼀种独占的加锁⽅式。synchronized的获取和释放锁由JVM实现，⽤户不需要显示的释放锁，⾮常⽅便。然⽽synchronized也有⼀定的局限性：
        1.  当线程尝试获取锁的时候，如果获取不到锁会⼀直阻塞。
        2.  如果获取锁的线程进⼊休眠或者阻塞，除⾮当前线程异常，否则其他线程尝试获取锁必须⼀直等待。
3.  ReentrantLock

    1.  ReentrantLock它是JDK 1.5之后提供的API层⾯的互斥锁，需要lock()和unlock()⽅法配合try/finally语句块来完成。
    2.  等待可中断避免，出现死锁的情况（如果别的线程正持有锁，会等待参数给定的时间，在等待的过程中，如果获取了锁定，就返回true，如果等待超时，返回false）
    3.  公平锁与⾮公平锁多个线程等待同⼀个锁时，必须按照申请锁的时间顺序获得锁，Synchronized锁⾮公平锁，
        ReentrantLock默认的构造函数是创建的⾮公平锁，可以通过参数true设为公平锁，但公平锁表现的性能不是很好。


# 806.Java Concurrency API中的Lock接⼝(Lock interface)是什么？对⽐同步它有什么优势？

> 原文：[https://zwmst.com/4869.html](https://zwmst.com/4869.html)

1.  Lock接⼝⽐同步⽅法和同步块提供了更具扩展性的锁操作。他们允许更灵活的结构，可以具有完全不同的性质，并且可以⽀持多个相关类的条件对象。
2.  它的优势有：
    1.  可以使锁更公平
    2.  可以使线程在等待锁的时候响应中断
    3.  可以让线程尝试获取锁，并在⽆法获取锁的时候⽴即返回或者等待⼀段时间
    4.  可以在不同的范围，以不同的顺序获取和释放锁


# 807\. Hashtable的size()⽅法中明明只有⼀条语句”return count”，为什么还要做同步？

> 原文：[https://zwmst.com/4871.html](https://zwmst.com/4871.html)

1.  同⼀时间只能有⼀条线程执⾏固定类的同步⽅法，但是对于类的⾮同步⽅法，可以多条线程同时访问。所以，这样就有问题了，可能线程A在执⾏Hashtable的put⽅法添加数据，线程B则可以正常调⽤size()⽅法读取Hashtable中当前元素的个数，那读取到的值可能不是最新的，可能线程A添加了完了数据，但是没有对size++，线程B就已经读取size了，那么对于线程B来说读取到的size⼀定是不准确的。
2.  ⽽给size()⽅法加了同步之后，意味着线程B调⽤size()⽅法只有在线程A调⽤put⽅法完毕之后才可以调⽤，这样就保证了线程安全性。


# 808.ConcurrentHashMap的并发度是什么？

> 原文：[https://zwmst.com/4873.html](https://zwmst.com/4873.html)

1.  ⼯作机制（分⽚思想）：它引⼊了⼀个“分段锁”的概念，具体可以理解为把⼀个⼤的Map拆分成N个⼩的segment，根据key.hashCode()来决定把key放到哪个HashTable中。可以提供相同的线程安全，但是效率提升N倍，默认提升16倍。
2.  应⽤：当读>写时使⽤，适合做缓存，在程序启动时初始化，之后可以被多个线程访问；
3.  hash冲突：
    1.  简介：HashMap中调⽤hashCode()⽅法来计算hashCode。由于在Java中两个不同的对象可能有⼀样的hashCode,所以不同的键可能有⼀样hashCode，从⽽导致冲突的产⽣。
    2.  hash冲突解决：使⽤平衡树来代替链表，当同⼀hash中的元素数量超过特定的值便会由链表切换到平衡树
4.  ⽆锁读：ConcurrentHashMap之所以有较好的并发性是因为ConcurrentHashMap是⽆锁读和加锁写，并且利⽤了分段锁（不是在所有的entry上加锁，⽽是在⼀部分entry上加锁）；


# 809.ReentrantReadWriteLock读写锁的使⽤？

> 原文：[https://zwmst.com/4875.html](https://zwmst.com/4875.html)

1.  读写锁：分为读锁和写锁，多个读锁不互斥，读锁与写锁互斥，这是由jvm⾃⼰控制的，你只要上好相应的锁即可。
2.  如果你的代码只读数据，可以很多⼈同时读，但不能同时写，那就上读锁；
3.  如果你的代码修改数据，只能有⼀个⼈在写，且不能同时读取，那就上写锁。总之，读的时候上读锁，写的时候上写锁！


# 810.CyclicBarrier和CountDownLatch的⽤法及区别？

> 原文：[https://zwmst.com/4878.html](https://zwmst.com/4878.html)

CyclicBarrier和CountDownLatch 都位于java.util.concurrent 这个包下

| CountDownLatch | CyclicBarrier |
| --- | --- |
| 减计数⽅式 | 加计数⽅式 |
| 计算为0时释放所有等待的线程 | 计数达到指定值时释放所有等待线程 |
| 计数为0时，⽆法重置 | 计数达到指定值时，计数置为0重新开始 |
| 调⽤countDown()⽅法计数减⼀，调⽤await()⽅法只进⾏阻塞，对计数没任何影响 | 调⽤await()⽅法计数加1，若加1后的值不等于构造⽅法的值，则线程阻塞 |
| 不可重复利⽤ | 可重复利⽤ |


# 811.Condition接⼝及其实现原理？

> 原文：[https://zwmst.com/4880.html](https://zwmst.com/4880.html)

1.  在java.util.concurrent包中，有两个很特殊的⼯具类，Condition和ReentrantLock，使⽤过的⼈都知道，ReentrantLock（重⼊锁）是jdk的concurrent包提供的⼀种独占锁的实现
2.  我们知道在线程的同步时可以使⼀个线程阻塞⽽等待⼀个信号，同时放弃锁使其他线程可以能竞争到锁
3.  在synchronized中我们可以使⽤Object的wait()和notify⽅法实现这种等待和唤醒
4.  但是在Lock中怎么实现这种wait和notify呢？答案是Condition，学习Condition主要是为了⽅便以后学习blockqueue和concurrenthashmap的源码，同时也进⼀步理解ReentrantLock。


# 812\. Fork/Join框架的理解?

> 原文：[https://zwmst.com/4882.html](https://zwmst.com/4882.html)

1.  Fork就是把⼀个⼤任务切分为若⼲⼦任务并⾏的执⾏。
2.  Join就是合并这些⼦任务的执⾏结果，最后得到这个⼤任务的结果。


# 813.wait()和sleep()的区别?

> 原文：[https://zwmst.com/4884.html](https://zwmst.com/4884.html)

1.  sleep()
    ⽅法是线程类（Thread）的静态⽅法，让调⽤线程进⼊睡眠状态，让出执⾏机会给其他线程，等到休眠时间结束后，线程进⼊就绪状态和其他线程⼀起竞争cpu的执⾏时间。
    因为sleep() 是static静态的⽅法，他不能改变对象的机锁，当⼀个synchronized块中调⽤了sleep() ⽅法，线程虽然进⼊休眠，但是对象的机锁没有被释放，其他线程依然⽆法访问这个对象。
2.  wait()
    wait()是Object类的⽅法，当⼀个线程执⾏到wait⽅法时，它就进⼊到⼀个和该对象相关的等待池，同时释放对象的机锁，使得其他线程能够访问，可以通过notify，notifyAll⽅法来唤醒等待的线程


# 814.线程的五个状态（五种状态，创建、就绪、运⾏、阻塞和死亡）?

> 原文：[https://zwmst.com/4886.html](https://zwmst.com/4886.html)

线程通常都有五种状态，创建、就绪、运⾏、阻塞和死亡。

1.  第⼀是创建状态。在⽣成线程对象，并没有调⽤该对象的start⽅法，这是线程处于创建状态。
2.  第⼆是就绪状态。当调⽤了线程对象的start⽅法之后，该线程就进⼊了就绪状态，但是此时线程调度程序还没有把该线程设置为当前线程，此时处于就绪状态。在线程运⾏之后，从等待或者睡眠中回来之后，也会处于就绪状态。
3.  第三是运⾏状态。线程调度程序将处于就绪状态的线程设置为当前线程，此时线程就进⼊了运⾏状态，开始运⾏run函数当中的代码。
4.  第四是阻塞状态。线程正在运⾏的时候，被暂停，通常是为了等待某个时间的发⽣(⽐如说某项资源就绪)之后再继续运⾏。sleep,suspend，wait等⽅法都可以导致线程阻塞。
5.  第五是死亡状态。如果⼀个线程的run⽅法执⾏结束或者调⽤stop⽅法后，该线程就会死亡。对于已经死亡的线程，⽆法再使⽤start⽅法令其进⼊就绪。


# 815.start()⽅法和run()⽅法的区别？

> 原文：[https://zwmst.com/4888.html](https://zwmst.com/4888.html)

1.  start()⽅法来启动⼀个线程，真正实现了多线程运⾏。
2.  如果直接调⽤run(),其实就相当于是调⽤了⼀个普通函数⽽已，直接调⽤run()⽅法必须等待run()⽅法执⾏完毕才能执⾏下⾯的代码，所以执⾏路径还是只有⼀条，根本就没有线程的特征，所以在多线程执⾏时要使⽤start()⽅法⽽不是run()⽅法。


# 816.Runnable接⼝和Callable接⼝的区别？

> 原文：[https://zwmst.com/4890.html](https://zwmst.com/4890.html)

1.  Runnable接⼝中的run()⽅法的返回值是void，它做的事情只是纯粹地去执⾏run()⽅法中的代码⽽已；
2.  Callable接⼝中的call()⽅法是有返回值的，是⼀个泛型，和Future、FutureTask配合可以⽤来获取异步执⾏的结果。


# 817.volatile关键字的作⽤？

> 原文：[https://zwmst.com/4892.html](https://zwmst.com/4892.html)

1.  多线程主要围绕可⻅性和原⼦性两个特性⽽展开，使⽤volatile关键字修饰的变量，保证了其在多线程之间的可⻅性，即每次读取到volatile变量，⼀定是最新的数据。
2.  代码底层执⾏不像我们看到的⾼级语⾔—-Java程序这么简单，它的执⾏是Java代码–>字节码–>根据字节码执⾏对应的C/C++代码–>C/C++代码被编译成汇编语⾔–>和硬件电路交互，现实中，为了获取更好的性能JVM可能会对指令进⾏重排序，多线程下可能会出现⼀些意想不到的问题。使⽤volatile则会对禁⽌语义重排序，当然这也⼀定程度上降低了代码执⾏效率。


# 818.Java中如何获取到线程dump⽂件？

> 原文：[https://zwmst.com/4894.html](https://zwmst.com/4894.html)

死循环、死锁、阻塞、⻚⾯打开慢等问题，查看线程dump是最好的解决问题的途径。所谓线程dump也就是线程堆栈，获取到线程堆栈有两步：

1.  获取到线程的pid，可以通过使⽤jps命令，在Linux环境下还可以使⽤ps -ef | grep java
2.  打印线程堆栈，可以通过使⽤jstack pid命令，在Linux环境下还可以使⽤kill -3 pid
3.  另外提⼀点，Thread类提供了⼀个getStackTrace()⽅法也可以⽤于获取线程堆栈。这是⼀个实例⽅法，因此此⽅法是和具体线程实例绑定的，每次获取到的是具体某个线程当前运⾏的堆栈。


# 819.线程和进程有什么区别？

> 原文：[https://zwmst.com/4896.html](https://zwmst.com/4896.html)

1.  进程是系统进⾏资源分配的基本单位，有独⽴的内存地址空间
2.  线程是CPU独⽴运⾏和独⽴调度的基本单位，没有单独地址空间，有独⽴的栈，局部变量，寄存器， 程序计数器等。
3.  创建进程的开销⼤，包括创建虚拟地址空间等需要⼤量系统资源
4.  创建线程开销⼩，基本上只有⼀个内核对象和⼀个堆栈。
5.  ⼀个进程⽆法直接访问另⼀个进程的资源；同⼀进程内的多个线程共享进程的资源。
6.  进程切换开销⼤，线程切换开销⼩；进程间通信开销⼤，线程间通信开销⼩。
7.  线程属于进程，不能独⽴执⾏。每个进程⾄少要有⼀个线程，成为主线程


# 820\. 线程实现的⽅式有⼏种（四种）？

> 原文：[https://zwmst.com/4898.html](https://zwmst.com/4898.html)

1.  继承Thread类，重写run⽅法
2.  实现Runnable接⼝，重写run⽅法，实现Runnable接⼝的实现类的实例对象作为Thread构造函数的target
3.  实现Callable接⼝通过FutureTask包装器来创建Thread线程
4.  通过线程池创建线程

    ```
    public class ThreadDemo03 {
    2 public static void main(String[] args) {
    3 Callable<Object> oneCallable = new Tickets<Object>();
    4 FutureTask<Object> oneTask = new FutureTask<Object>(oneCallable);
    5 Thread t = new Thread(oneTask);
    6 System.out.println(Thread.currentThread().getName());
    7 t.start();
    8 }
    9 }
    10
    11 class Tickets<Object> implements Callable<Object>{
    12 //重写call⽅法
    13 @Override
    14 public Object call() throws Exception {
    15 // TODO Auto-generated method stub
    16 System.out.println(Thread.currentThread().getName()+"-->我是通过实现Callable接⼝通过FutureTask包装器来实现的线程"
    17 return null;
    18 } 
    19 }
    ```


# 821\. ⾼并发、任务执⾏时间短的业务怎样使⽤线程池？并发不⾼、任务执⾏时间⻓的业务怎样使⽤线程池？并发⾼、 业务执⾏时间⻓的业务怎样使⽤线程池？

> 原文：[https://zwmst.com/4900.html](https://zwmst.com/4900.html)

1.  ⾼并发、任务执⾏时间短的业务：线程池线程数可以设置为CPU核数+1，减少线程上下⽂的切换。
2.  并发不⾼、任务执⾏时间⻓的业务要区分开看：
    1.  假如是业务时间⻓集中在IO操作上，也就是IO密集型的任务，因为IO操作并不占⽤CPU，所以不要让所有的CPU闲下来，可以加⼤线程池中的线程数⽬，让CPU处理更多的业务
    2.  假如是业务时间⻓集中在计算操作上，也就是计算密集型任务，这个就没办法了，和（1）⼀样吧，线程池中的线程数设置得少⼀些，减少线程上下⽂的切换
3.  并发⾼、业务执⾏时间⻓，解决这种类型任务的关键不在于线程池⽽在于整体架构的设计，看看这些业务⾥⾯某些数据是否能做缓存是第⼀步，增加服务器是第⼆步，⾄于线程池的设置，设置参考（2）。最后，业务执⾏时间⻓的问题，也可能需要分析⼀下，看看能不能使⽤中间件对任务进⾏拆分和解耦。


# 822.如果你提交任务时，线程池队列已满，这时会发⽣什么？

> 原文：[https://zwmst.com/4902.html](https://zwmst.com/4902.html)

1.  如果你使⽤的LinkedBlockingQueue，也就是⽆界队列的话，没关系，继续添加任务到阻塞队列中等待执⾏，因为LinkedBlockingQueue可以近乎认为是⼀个⽆穷⼤的队列，可以⽆限存放任务；
2.  如果你使⽤的是有界队列⽐⽅说ArrayBlockingQueue的话，任务⾸先会被添加到ArrayBlockingQueue中，ArrayBlockingQueue满了，则会使⽤拒绝策略RejectedExecutionHandler处理满了的任务，默认是AbortPolicy。


# 823.锁的等级：⽅法锁、对象锁、类锁?

> 原文：[https://zwmst.com/4904.html](https://zwmst.com/4904.html)

1.  ⽅法锁（synchronized修饰⽅法时）
    1.  通过在⽅法声明中加⼊ synchronized关键字来声明 synchronized ⽅法。
    2.  synchronized ⽅法控制对类成员变量的访问：
    3.  每个类实例对应⼀把锁，每个 synchronized ⽅法都必须获得调⽤该⽅法的类实例的锁⽅能执⾏，否则所属线程阻塞，⽅法⼀旦执⾏，就独占该锁，直到从该⽅法返回时才将锁释放，此后被阻塞的线程⽅能获得该锁，重新进⼊可执⾏状态。这种机制确保了同⼀时刻对于每⼀个类实例，其所有声明为 synchronized 的成员函数中⾄多只有⼀个处于可执⾏状态，从⽽有效避免了类成员变量的访问冲突。
2.  对象锁（synchronized修饰⽅法或代码块）
    1.  当⼀个对象中有synchronized method或synchronized block的时候调⽤此对象的同步⽅法或进⼊其同步区域时，就必须先获得对象锁。如果此对象的对象锁已被其他调⽤者占⽤，则需要等待此锁被释放。（⽅法锁也是对象锁）
    2.  java的所有对象都含有1个互斥锁，这个锁由JVM⾃动获取和释放。线程进⼊synchronized⽅法的时候获取该对象的锁，当然如果已经有线程获取了这个对象的锁，那么当前线程会等待；synchronized⽅法正常返回或者抛异常⽽终⽌，JVM会⾃动释放对象锁。这⾥也体现了⽤synchronized来加锁的1个好处，⽅法抛异常的时候，锁仍然可以由JVM来⾃动释放。　
3.  类锁(synchronized 修饰静态的⽅法或代码块)
    1.  由于⼀个class不论被实例化多少次，其中的静态⽅法和静态变量在内存中都只有⼀份。所以，⼀旦⼀个静态的⽅法被申明为synchronized。此类所有的实例化对象在调⽤此⽅法，共⽤同⼀把锁，我们称之为类锁。
4.  对象锁是⽤来控制实例⽅法之间的同步，类锁是⽤来控制静态⽅法（或静态变量互斥体）之间的同步


# 824.如果同步块内的线程抛出异常会发⽣什么？

> 原文：[https://zwmst.com/4906.html](https://zwmst.com/4906.html)

synchronized⽅法正常返回或者抛异常⽽终⽌，JVM会⾃动释放对象锁


# 825.并发编程（concurrency）并⾏编程（parallellism）有什么区别？

> 原文：[https://zwmst.com/4908.html](https://zwmst.com/4908.html)

1.  解释⼀：并⾏是指两个或者多个事件在同⼀时刻发⽣；⽽并发是指两个或多个事件在同⼀时间间隔发⽣。
2.  解释⼆：并⾏是在不同实体上的多个事件，并发是在同⼀实体上的多个事件。
3.  解释三：在⼀台处理器上“同时”处理多个任务，在多台处理器上同时处理多个任务。如hadoop分布式集群
    `所以并发编程的⽬标是充分的利⽤处理器的每⼀个核，以达到最⾼的处理性能。`


# 826.如何保证多线程下 i++ 结果正确？

> 原文：[https://zwmst.com/4911.html](https://zwmst.com/4911.html)

1.  volatile只能保证你数据的可⻅性，获取到的是最新的数据，不能保证原⼦性；
2.  ⽤AtomicInteger保证原⼦性。
3.  synchronized既能保证共享变量可⻅性，也可以保证锁内操作的原⼦性。


# 827.⼀个线程如果出现了运⾏时异常会怎么样?

> 原文：[https://zwmst.com/4913.html](https://zwmst.com/4913.html)

1.  如果这个异常没有被捕获的话，这个线程就停⽌执⾏了。
2.  另外重要的⼀点是：如果这个线程持有某个对象的监视器，那么这个对象监视器会被⽴即释放.


# 828\. 如何在两个线程之间共享数据?

> 原文：[https://zwmst.com/4915.html](https://zwmst.com/4915.html)

通过在线程之间共享对象就可以了，然后通过wait/notify/notifyAll、await/signal/signalAll进⾏唤起和等待，⽐⽅说阻塞队列BlockingQueue就是为线程之间共享数据⽽设计的。

1.  卖票系统：

```
1 package 多线程共享数据;
2 public class Ticket implements Runnable{
3 private int ticket = 10;
4 public void run() {
5 while(ticket>0){
6 ticket--;
7 System.out.println("当前票数为："+ticket);
8 }
9 }
10 }
11
12 package 多线程共享数据;
13 public class SellTicket {
14 public static void main(String[] args) {
15 Ticket t = new Ticket();
16 new Thread(t).start();
17 new Thread(t).start();
18 }
19 }
2\. 银⾏存取款：
1 public class MyData {
2 private int j=0;
3 public synchronized void add(){
4 j++;
5 System.out.println("线程"+Thread.currentThread().getName()+"j为："+j);
6 }
7 public synchronized void dec(){
8 j--;
9 System.out.println("线程"+Thread.currentThread().getName()+"j为："+j);
10 }
11 public int getData(){
12 return j;
13 }
14 }
15
16 public class AddRunnable implements Runnable{
17 MyData data;
18 public AddRunnable(MyData data){
19 this.data= data;
20 }
21 public void run() {
22 data.add();
23 }
24 }
25
26 public class DecRunnable implements Runnable {
27 MyData data;
28 public DecRunnable(MyData data){
29 this.data = data;
30 }
31 public void run() {
32 data.dec();
33 }
34 }
35
36 public class TestOne {
37 public static void main(String[] args) {
38 MyData data = new MyData();
39 Runnable add = new AddRunnable(data);
40 Runnable dec = new DecRunnable(data);
41 for(int i=0;i<2;i++){
42 new Thread(add).start();
43 new Thread(dec).start();
44 }
45 }
```


# 829\. ⽣产者消费者模型的作⽤是什么?

> 原文：[https://zwmst.com/4917.html](https://zwmst.com/4917.html)

1.  通过平衡⽣产者的⽣产能⼒和消费者的消费能⼒来提升整个系统的运⾏效率，这是⽣产者消费者模型最重要的作⽤。
2.  解耦，这是⽣产者消费者模型附带的作⽤，解耦意味着⽣产者和消费者之间的联系少，联系越少越可以独⾃发展⽽不需要受到相互的制约。


# 830.怎么唤醒⼀个阻塞的线程?

> 原文：[https://zwmst.com/4919.html](https://zwmst.com/4919.html)

1.  如果线程是因为调⽤了wait()、sleep()或者join()⽅法⽽导致的阻塞；
    1.  suspend与resume
        Java废弃 suspend() 去挂起线程的原因，是因为 suspend() 在导致线程暂停的同时，并不会去释放任何锁资源。其他线程都⽆法访问被它占⽤的锁。直到对应的线程执⾏ resume() ⽅法后，被挂起的线程才能继续，从⽽其它被阻塞在这个锁的线程才可以继续执⾏。
        但是，如果 resume() 操作出现在 suspend() 之前执⾏，那么线程将⼀直处于挂起状态，同时⼀直占⽤锁，这就产⽣了死锁。⽽且，对于被挂起的线程，它的线程状态居然还是 Runnable。
    2.  wait与notify
        wait与notify必须配合synchronized使⽤，因为调⽤之前必须持有锁，wait会⽴即释放锁，notify则是同步块执⾏完了才释放
    3.  await与singal
        Condition类提供，⽽Condition对象由new ReentLock().newCondition()获得，与wait和notify相同，因为使⽤Lock锁后⽆法使⽤wait⽅法
    4.  park与unpark
        LockSupport是⼀个⾮常⽅便实⽤的线程阻塞⼯具，它可以在线程任意位置让线程阻塞。和Thread.suspenf()相⽐，它弥补了由于resume()在前发⽣，导致线程⽆法继续执⾏的情况。和Object.wait()相⽐，它不需要先获得某个对象的锁，也不会抛出IException异常。可以唤醒指定线程。
2.  如果线程遇到了IO阻塞，⽆能为⼒，因为IO是操作系统实现的，Java代码并没有办法直接接触到操作系统。


# 831.Java中⽤到的线程调度算法是什么

> 原文：[https://zwmst.com/4921.html](https://zwmst.com/4921.html)

1.  抢占式。⼀个线程⽤完CPU之后，操作系统会根据线程优先级、线程饥饿情况等数据算出⼀个总的优先级并分配下⼀个时间⽚给某个线程执⾏。


# 832\. 单例模式的线程安全性?

> 原文：[https://zwmst.com/4923.html](https://zwmst.com/4923.html)

⽼⽣常谈的问题了，⾸先要说的是单例模式的线程安全意味着：某个类的实例在多线程环境下只会被创建⼀次出来。单例模式有很多种的写法，我总结⼀下：

1.  饿汉式单例模式的写法：线程安全
2.  懒汉式单例模式的写法：⾮线程安全
3.  双检锁单例模式的写法：线程安全


# 833.线程类的构造⽅法、静态块是被哪个线程调⽤的?

> 原文：[https://zwmst.com/4925.html](https://zwmst.com/4925.html)

线程类的构造⽅法、静态块是被new这个线程类所在的线程所调⽤的，⽽run⽅法⾥⾯的代码才是被线程⾃身所调⽤的。


# 834.同步⽅法和同步块，哪个是更好的选择?

> 原文：[https://zwmst.com/4927.html](https://zwmst.com/4927.html)

1.  同步块是更好的选择，因为它不会锁住整个对象（当然也可以让它锁住整个对象）。同步⽅法会锁住整个对象，哪怕这个类中有多个不相关联的同步块，这通常会导致他们停⽌执⾏并需要等待获得这个对象上的锁。synchronized(this)以及⾮static的synchronized⽅法（⾄于static synchronized⽅法请往下看），只能防⽌多个线程同时执⾏同⼀个对象的同步代码段。
    如果要锁住多个对象⽅法，可以锁住⼀个固定的对象，或者锁住这个类的Class对象。
    synchronized锁住的是括号⾥的对象，⽽不是代码。对于⾮static的synchronized⽅法，锁的就是对象本身也就是this。
2.  例如：

```
1 public class SynObj{
2
3 public synchronized void showA(){
4 System.out.println("showA..");
5 try {
6 Thread.sleep(3000);
7 } catch (InterruptedException e) {
8 e.printStackTrace();
9 }
10 }
11
12 public void showB(){
13 synchronized (this) {
14 System.out.println("showB..");
15 }
16 }
17 }
```


# 835.如何检测死锁？怎么预防死锁？

> 原文：[https://zwmst.com/4929.html](https://zwmst.com/4929.html)

1.  概念：
    是指两个或两个以上的进程在执⾏过程中，因争夺资源⽽造成的⼀种互相等待的现象，若⽆外⼒作⽤，它们都将⽆法推进下去。此时称系统处于死锁；
2.  死锁的四个必要条件：
    1.  互斥条件：进程对所分配到的资源不允许其他进程进⾏访问，若其他进程访问该资源，只能等待，直⾄占有该资源的进程使⽤完成后释放该资源
    2.  请求和保持条件：进程获得⼀定的资源之后，⼜对其他资源发出请求，但是该资源可能被其他进程占有，此时请求阻塞，但⼜对⾃⼰获得的资源保持不放
    3.  不可剥夺条件：是指进程已获得的资源，在未完成使⽤之前，不可被剥夺，只能在使⽤完后⾃⼰释放
    4.  环路等待条件：是指进程发⽣死锁后，若⼲进程之间形成⼀种头尾相接的循环等待资源关系
3.  死锁产⽣的原因：
    1.因竞争资源发⽣死锁 现象：系统中供多个进程共享的资源的数⽬不⾜以满⾜全部进程的需要时，就会引起对诸资源的竞争⽽发⽣死锁现象
    2.进程推进顺序不当发⽣死锁
4.  检查死锁
    1.  有两个容器，⼀个⽤于保存线程正在请求的锁，⼀个⽤于保存线程已经持有的锁。每次加锁之前都会做如下检测:
    2.  检测当前正在请求的锁是否已经被其它线程持有,如果有，则把那些线程找出来
    3.  遍历第⼀步中返回的线程，检查⾃⼰持有的锁是否正被其中任何⼀个线程请求，如果第⼆步返回真,表示出现了死锁
5.  死锁的解除与预防：控制不要让四个必要条件成⽴。


# 836\. HashMap在多线程环境下使⽤需要注意什么？

> 原文：[https://zwmst.com/4931.html](https://zwmst.com/4931.html)

要注意死循环的问题，HashMap的put操作引发扩容，这个动作在多线程并发下会发⽣线程死循环的问题。

1.  HashMap不是线程安全的；Hashtable线程安全，但效率低，因为是Hashtable是使⽤synchronized的，所有线程竞争同⼀把锁；⽽ConcurrentHashMap不仅线程安全⽽且效率⾼，因为它包含⼀个segment数组，将数据分段存储，给每⼀段数据配⼀把锁，也就是所谓的锁分段技术。
2.  HashMap为何线程不安全：
    1.  put时key相同导致其中⼀个线程的value被覆盖；
    2.  多个线程同时扩容，造成数据丢失；
    3.  多线程扩容时导致Node链表形成环形结构造成.next()死循环，导致CPU利⽤率接近100%；
    4.  ConcurrentHashMap最⾼效；


# 837.什么是守护线程？有什么⽤？

> 原文：[https://zwmst.com/4933.html](https://zwmst.com/4933.html)

守护线程（即daemon thread），是个服务线程，准确地来说就是服务其他的线程，这是它的作⽤——⽽其他的线程只有⼀种，那就是⽤户线程。所以java⾥线程分2种，

1.  守护线程，⽐如垃圾回收线程，就是最典型的守护线程。
2.  ⽤户线程，就是应⽤程序⾥的⾃定义线程。


# 838\. 如何实现线程串⾏执⾏？

> 原文：[https://zwmst.com/4935.html](https://zwmst.com/4935.html)

1.  为了控制线程执⾏的顺序，如ThreadA->ThreadB->ThreadC->ThreadA循环执⾏三个线程，我们需要确定唤醒、等待的顺序。这时我们可以同时使⽤ Obj.wait()、Obj.notify()与synchronized(Obj)来实现这个⽬标。线程中持有上⼀个线程类的对象锁以及⾃⼰的锁，由于这种依赖关系，该线程执⾏需要等待上个对象释放锁，从⽽保证类线程执⾏的顺序。
2.  通常情况下，wait是线程在获取对象锁后，主动释放对象锁，同时本线程休眠，直到有其它线程调⽤对象的notify()唤醒该线程，才能继续获取对象锁，并继续执⾏。⽽notify()则是对等待对象锁的线程的唤醒操作。但值得注意的是notify()调⽤后，并不是⻢上就释放对象锁，⽽是在相应的synchronized(){}语句块执⾏结束。释放对象锁后，JVM会在执⾏wait()等待对象锁的线程中随机选取⼀线程，赋予其对象锁，唤醒线程，继续执⾏。

```
1 public class ThreadSerialize {
2
3 public static void main(String[] args){
4 ThreadA threadA = new ThreadA();
5 ThreadB threadB = new ThreadB();
6 ThreadC threadC = new ThreadC();
7
8 threadA.setThreadC(threadC);
9 threadB.setThreadA(threadA);
10 threadC.setThreadB(threadB);
11
12 threadA.start();
13 threadB.start();
14 threadC.start();
15
16 while (true){
17 try {
18 Thread.currentThread().sleep(1000);
19 } catch (InterruptedException e) {
20 e.printStackTrace();
21 }
22 }
23 }
24 }
25
26 class ThreadA extends Thread{
27 private ThreadC threadC;
28 @Override
29 public void run() {
30 while (true){
31 synchronized (threadC){
32 synchronized (this){
33 System.out.println("I am ThreadA。。。");
34 this.notify();
35 }
36 try {
37 threadC.wait();
38 } catch (InterruptedException e) {
39 e.printStackTrace();
40 }
41 }
42 }
43
44 }
45
46 public void setThreadC(ThreadC threadC) {
47 this.threadC = threadC;
48 }
49 }
50 class ThreadB extends Thread{
51 private ThreadA threadA;
52 @Override
53 public void run() {
54 while (true){
55 synchronized (threadA){
56 synchronized (this){
57 System.out.println("I am ThreadB。。。");
58 this.notify();
59 }
60 try {
61 threadA.wait();
62 } catch (InterruptedException e) {
63 e.printStackTrace();
64 }
65 }
66 }
67
68 }
69
70 public void setThreadA(ThreadA threadA) {
71 this.threadA = threadA;
72 }
73 }
74 class ThreadC extends Thread{
75 private ThreadB threadB;
76 @Override
77 public void run() {
78 while (true){
79 synchronized (threadB){
80 synchronized (this){
81 System.out.println("I am ThreadC。。。");
82 this.notify();
83 }
84 try {
85 threadB.wait();
86 } catch (InterruptedException e) {
87 e.printStackTrace();
88 }
89 }
90 }
91
92 }
93
94 public void setThreadB(ThreadB threadB) {
95 this.threadB = threadB;
96 }
97 }
98
99
```


# 839.可以运⾏时kill掉⼀个线程吗？

> 原文：[https://zwmst.com/4937.html](https://zwmst.com/4937.html)

1.  不可以，线程有5种状态，新建（new）、可运⾏（runnable）、运⾏中（running）、阻塞（block）、死亡（dead）。
2.  只有当线程run⽅法或者主线程main⽅法结束，⼜或者抛出异常时，线程才会结束⽣命周期。


# 840.关于synchronized：

> 原文：[https://zwmst.com/4939.html](https://zwmst.com/4939.html)

1.  在某个对象的所有synchronized⽅法中,在某个时刻只能有⼀个唯⼀的⼀个线程去访问这些synchronized⽅法
    2.  如果⼀个⽅法是synchronized⽅法,那么该synchronized关键字表示给当前对象上锁(即this)相当于synchronized(this){}
    3.  如果⼀个synchronized⽅法是static的,那么该synchronized表示给当前对象所对应的class对象上锁(每个类不管⽣成多少对象,其对应的class对象只有⼀个)


# 841.分步式锁,程序数据库中死锁机制及解决⽅案

> 原文：[https://zwmst.com/4941.html](https://zwmst.com/4941.html)

基本原理：⽤⼀个状态值表示锁，对锁的占⽤和释放通过状态值来标识。

1.  三种分布式锁：
    1.  Zookeeper：基于zookeeper瞬时有序节点实现的分布式锁，其主要逻辑如下。⼤致思想即为：每个客户端对某个功能加锁时，在zookeeper上的与该功能对应的指定节点的⽬录下，⽣成⼀个唯⼀的瞬时有序节点。判断是否获取锁的⽅式很简单，只需要判断有序节点中序号最⼩的⼀个。当释放锁的时候，只需将这个瞬时节点删除即可。同时，其可以避免服务宕机导致的锁⽆法释放，⽽产⽣的死锁问题。
    2.  优点
        锁安全性⾼，zk可持久化，且能实时监听获取锁的客户端状态。⼀旦客户端宕机，则瞬时节点随之消失，zk因⽽能第⼀时间释放锁。这也省去了⽤分布式缓存实现锁的过程中需要加⼊超时时间判断的这⼀逻辑。
    3.  缺点
        性能开销⽐较⾼。因为其需要动态产⽣、销毁瞬时节点来实现锁功能。所以不太适合直接提供给⾼并发的场景使⽤。
    4.  实现
        可以直接采⽤zookeeper第三⽅库curator即可⽅便地实现分布式锁。
    5.  适⽤场景
        对可靠性要求⾮常⾼，且并发程度不⾼的场景下使⽤。如核⼼数据的定时全量/增量同步等。
2.  memcached：memcached带有add函数，利⽤add函数的特性即可实现分布式锁。add和set的区别在于：如果多线程并发set，则每个set都会成功，但最后存储的值以最后的set的线程为准。⽽add的话则相反，add会添加第⼀个到达的值，并返回true，后续的添加则都会返回false。利⽤该点即可很轻松地实现分布式锁。
    2.  优点
        并发⾼效
    3.  缺点
        memcached采⽤列⼊LRU置换策略，所以如果内存不够，可能导致缓存中的锁信息丢失。
        memcached⽆法持久化，⼀旦重启，将导致信息丢失。
    4.  使⽤场景
        ⾼并发场景。需要 1)加上超时时间避免死锁; 2)提供⾜够⽀撑锁服务的内存空间; 3)稳定的集群化管理。
3.  redis：redis分布式锁即可以结合zk分布式锁锁⾼度安全和memcached并发场景下效率很好的优点，其实现⽅式和memcached类似，采⽤setnx即可实现。需要注意的是，这⾥的redis也需要设置超时时间，以避免死锁。可以利⽤jedis客户端实现。

    ```
    1 ICacheKey cacheKey = new ConcurrentCacheKey(key, type);
    2 return RedisDao.setnx(cacheKey, "1");
    ```


# 842.数据库死锁机制和解决⽅案

> 原文：[https://zwmst.com/4943.html](https://zwmst.com/4943.html)

1.  死锁：死锁是指两个或者两个以上的事务在执⾏过程中，因争夺锁资源⽽造成的⼀种互相等待的现象。
2.  处理机制：解决死锁最有⽤最简单的⽅法是不要有等待，将任何等待都转化为回滚，并且事务重新开始。但是有可能影响并发性能。
    1.  超时回滚，innodb_lock_wait_time设置超时时间；
    2.  wait-for-graph⽅法：跟超时回滚⽐起来，这是⼀种更加主动的死锁检测⽅式。InnoDB引擎也采⽤这种⽅式。


# 843.spring单例为什么没有安全问题(ThreadLocal)

> 原文：[https://zwmst.com/4945.html](https://zwmst.com/4945.html)

1.  ThreadLocal：spring使⽤ThreadLocal解决线程安全问题；ThreadLocal会为每⼀个线程提供⼀个独⽴的变量副本，从⽽隔离了多个线程对数据的访问冲突。因为每⼀个线程都拥有⾃⼰的变量副本，从⽽也就没有必要对该变量进⾏同步了。ThreadLocal提供了线程安全的共享对象，在编写多线程代码时，可以把不安全的变量封装进ThreadLocal。概括起来说，对于多线程资源共享的问题，同步机制采⽤了“以时间换空间”的⽅式，⽽ThreadLocal采⽤了“以空间换时间”的⽅式。前者仅提供⼀份变量，让不同的线程排队访问，⽽后者为每⼀个线程都提供了⼀份变量，因此可以同时访问⽽互不影响。在很多情况下，ThreadLocal⽐直接使⽤synchronized同步机制解决线程安全问题更简单，更⽅便，且结果程序拥有更⾼的并发性。
2.  单例：⽆状态的Bean(⽆状态就是⼀次操作，不能保存数据。⽆状态对象(Stateless Bean)，就是没有实例变量的对象，不能保存数据，是不变类，是线程安全的。)适合⽤不变模式，技术就是单例模式，这样可以共享实例，提⾼性能。


# 844.线程池原理：

> 原文：[https://zwmst.com/4947.html](https://zwmst.com/4947.html)

1.  使⽤场景：假设⼀个服务器完成⼀项任务所需时间为：T1-创建线程时间，T2-在线程中执⾏任务的时间，T3-销毁线程时间。如果T1+T3远⼤于T2，则可以使⽤线程池，以提⾼服务器性能；
2.  组成：
    1.  线程池管理器（ThreadPool）：⽤于创建并管理线程池，包括 创建线程池，销毁线程池，添加新任务；
    2.  ⼯作线程（PoolWorker）：线程池中线程，在没有任务时处于等待状态，可以循环的执⾏任务；
    3.  任务接⼝（Task）：每个任务必须实现的接⼝，以供⼯作线程调度任务的执⾏，它主要规定了任务的⼊⼝，任务执⾏完后的收尾⼯作，任务的执⾏状态等；
    4.  任务队列（taskQueue）：⽤于存放没有处理的任务。提供⼀种缓冲机制。
3.  原理：线程池技术正是关注如何缩短或调整T1,T3时间的技术，从⽽提⾼服务器程序性能的。它把T1，T3分别安排在服务器程序的启动和结束的时间段或者⼀些空闲的时间段，这样在服务器程序处理客户请求时，不会有T1，T3的开销了。
4.  ⼯作流程：
    1.  线程池刚创建时，⾥⾯没有⼀个线程(也可以设置参数prestartAllCoreThreads启动预期数量主线程)。任务队列是作为参数传进来的。不过，就算队列⾥⾯有任务，线程池也不会⻢上执⾏它们。
    2.  当调⽤ execute() ⽅法添加⼀个任务时，线程池会做如下判断：
        1.  如果正在运⾏的线程数量⼩于 corePoolSize，那么⻢上创建线程运⾏这个任务；
        2.  如果正在运⾏的线程数量⼤于或等于 corePoolSize，那么将这个任务放⼊队列；
        3.  如果这时候队列满了，⽽且正在运⾏的线程数量⼩于 maximumPoolSize，那么还是要创建⾮核⼼线程⽴刻运⾏这个任务；
        4.  如果队列满了，⽽且正在运⾏的线程数量⼤于或等于 maximumPoolSize，那么线程池会抛出异常RejectExecutionException。
    3.  当⼀个线程完成任务时，它会从队列中取下⼀个任务来执⾏。
    4.  当⼀个线程⽆事可做，超过⼀定的时间（keepAliveTime）时，线程池会判断，如果当前运⾏的线程数⼤于corePoolSize，那么这个线程就被停掉。所以线程池的所有任务完成后，它最终会收缩到 corePoolSize 的⼤⼩。


# 845.java锁多个对象：

> 原文：[https://zwmst.com/4949.html](https://zwmst.com/4949.html)

例如： 在银⾏系统转账时，需要锁定两个账户，这个时候，顺序使⽤两个synchronized可能存在死锁的情况，在⽹上搜索到下⾯的例⼦：

```
1 public class Bank {
2 final static Object obj_lock = new Object();
3
4 // Deadlock crisis 死锁
5 public void transferMoney(Account from, Account to, int number) {
6 synchronized (from) {
7 synchronized (to) {
8 from.debit();
9 to.credit();
10 }
11 }
12 }
13
14 // Thread safe
15 public void transferMoney2(final Account from, final Account to, int number) {
16 class Help {
17 void transferMoney2() {
18 from.debit();
19 to.credit();
20 }
21 }
22
23 //通过hashCode⼤⼩调整加锁顺序
24 int fromHash = from.hashCode();
25 int toHash = to.hashCode();
26
27 if (fromHash < toHash) {
28 synchronized (from) {
29 synchronized (to) {
30 new Help().transferMoney2();
31 }
32 }
33 } else if (toHash < fromHash) {
34 synchronized (to) {
35 synchronized (from) {
36 new Help().transferMoney2();
37 }
38 }
39 } else {
40 synchronized (obj_lock) {
41 synchronized (to) {
42 synchronized (from) {
43 new Help().transferMoney2();
44 }
45 }
46 }
47 }
48 }
49 }
```

若操作账户A，B：

1.  A的hashCode⼩于B， 先锁A再锁B
2.  B的hashCode⼩于A， 先锁B再锁A
3.  产⽣的hashCode相等，先锁住⼀个全局静态变量，在锁A，B 这样就避免了两个线程分别操作账户A,B和B,A⽽产⽣死锁的情况。需要为Account对象写⼀个好的hashCode算法，使得不同账户间产⽣的hashCode尽量不同。


# 846.java线程如何启动：

> 原文：[https://zwmst.com/4951.html](https://zwmst.com/4951.html)

1.  继承Thread类；
2.  实现Runnable接⼝；
3.  直接在函数体内：
4.  ⽐较：
    1.  实现Runnable接⼝优势：
        1.  适合多个相同的程序代码的线程去处理同⼀个资源
        2.  可以避免java中的单继承的限制
        3.  增加程序的健壮性，代码可以被多个线程共享，代码和数据独⽴。
            2.  继承Thread类优势：
            3.  可以将线程类抽象出来，当需要使⽤抽象⼯⼚模式设计时。
            4.  多线程同步
            5.  在函数体使⽤优势
            6.  ⽆需继承thread或者实现Runnable，缩⼩作⽤域。


# 847\. java中加锁的⽅式有哪些,如何实现怎么个写法.

> 原文：[https://zwmst.com/4953.html](https://zwmst.com/4953.html)

1.  java中有两种锁：⼀种是⽅法锁或者对象锁(在⾮静态⽅法或者代码块上加锁)，第⼆种是类锁(在静态⽅法或者class上加锁)；
2.  注意：其他线程可以访问未加锁的⽅法和代码；synchronized同时修饰静态⽅法和实例⽅法，但是运⾏结果是交替进⾏的，这证明了类锁和对象锁是两个不⼀样的锁，控制着不同的区域，它们是互不⼲扰的。
3.  示例代码：
    1.  ⽅法锁和同步代码块：

```
1 public class TestSynchronized 
2 { 
3 public void test1() 
4 { 
5 synchronized(this) 
6 { 
7 int i = 5; 
8 while( i-- > 0) 
9 { 
10 System.out.println(Thread.currentThread().getName() + " : " + i); 
11 try 
12 { 
13 Thread.sleep(500); 
14 } 
15 catch (InterruptedException ie) 
16 { 
17 } 
18 } 
19 } 
20 } 
21 
22 public synchronized void test2() 
23 { 
24 int i = 5; 
25 while( i-- > 0) 
26 { 
27 System.out.println(Thread.currentThread().getName() + " : " + i); 
28 try 
29 { 
30 Thread.sleep(500); 
31 } 
32 catch (InterruptedException ie) 
33 { 
34 } 
35 } 
36 } 
37 
38 public static void main(String[] args) 
39 { 
40 final TestSynchronized myt2 = new TestSynchronized(); 
41 Thread test1 = new Thread( new Runnable() { public void run() { myt2.test1(); } },
42 Thread test2 = new Thread( new Runnable() { public void run() { myt2.test2(); } },
43 test1.start();; 
44 test2.start(); 
45 // TestRunnable tr=new TestRunnable(); 
46 // Thread test3=new Thread(tr); 
47 // test3.start(); 
48 } 
49 }
```

```
2\. 类锁：
```

```
1 public class TestSynchronized 
2 { 
3 public void test1() 
4 { 
5 synchronized(TestSynchronized.class) 
6 { 
7 int i = 5; 
8 while( i-- > 0) 
9 { 
10 System.out.println(Thread.currentThread().getName() + " : " + i); 
11 try 
12 { 
13 Thread.sleep(500); 
14 } 
15 catch (InterruptedException ie) 
16 { 
17 } 
18 } 
19 } 
20 } 
21 
22 public static synchronized void test2() 
23 { 
24 int i = 5; 
25 while( i-- > 0) 
26 { 
27 System.out.println(Thread.currentThread().getName() + " : " + i); 
28 try 
29 { 
30 Thread.sleep(500); 
31 } 
32 catch (InterruptedException ie) 
33 { 
34 } 
35 } 
36 } 
37 
38 public static void main(String[] args) 
39 { 
40 final TestSynchronized myt2 = new TestSynchronized(); 
41 Thread test1 = new Thread( new Runnable() { public void run() { myt2.test1(); } },
42 Thread test2 = new Thread( new Runnable() { public void run() { TestSynchronized.test2
43 test1.start(); 
44 test2.start(); 
45 // TestRunnable tr=new TestRunnable(); 
46 // Thread test3=new Thread(tr); 
47 // test3.start(); 
48 } 
49 
50 }
```


# 848.如何保证数据不丢失：

> 原文：[https://zwmst.com/4955.html](https://zwmst.com/4955.html)

1.  使⽤消息队列，消息持久化；
2.  添加标志位：未处理 0，处理中 1，已处理 2。定时处理。


# 849.ThreadLocal为什么会发⽣内存泄漏？

> 原文：[https://zwmst.com/4957.html](https://zwmst.com/4957.html)

1.  threadlocal原理图：
    ![](img/07e5e40c2ba6e52a7ee93d9f7abcb1c5.png)
2.  OOM实现：
    1.  ThreadLocal的实现是这样的：每个Thread 维护⼀个 ThreadLocalMap 映射表，这个映射表的 key 是 ThreadLocal实例本身，value 是真正需要存储的 Object。
    2.  也就是说 ThreadLocal 本身并不存储值，它只是作为⼀个 key 来让线程从 ThreadLocalMap 获取 value。值得注意的是图中的虚线，表示 ThreadLocalMap 是使⽤ ThreadLocal 的弱引⽤作为 Key 的，弱引⽤的对象在 GC 时会被回收。
    3.  ThreadLocalMap使⽤ThreadLocal的弱引⽤作为key，如果⼀个ThreadLocal没有外部强引⽤来引⽤它，那么系统 GC的时候，这个ThreadLocal势必会被回收，这样⼀来，ThreadLocalMap中就会出现key为null的Entry，就没有办法访问这些key为null的Entry的value，如果当前线程再迟迟不结束的话，这些key为null的Entry的value就会⼀直存在⼀条强引⽤链：Thread Ref -> Thread -> ThreaLocalMap -> Entry -> value永远⽆法回收，造成内存泄漏。
3.  预防办法：在ThreadLocal的get(),set(),remove()的时候都会清除线程ThreadLocalMap⾥所有key为null的value。但是这些被动的预防措施并不能保证不会内存泄漏：
    1.  使⽤static的ThreadLocal，延⻓了ThreadLocal的⽣命周期，可能导致内存泄漏。
    2.  分配使⽤了ThreadLocal⼜不再调⽤get(),set(),remove()⽅法，那么就会导致内存泄漏，因为这块内存⼀直存在。


# 850.、jdk8中对ConcurrentHashmap的改进

> 原文：[https://zwmst.com/4960.html](https://zwmst.com/4960.html)

1.  Java 7为实现并⾏访问，引⼊了Segment这⼀结构，实现了分段锁，理论上最⼤并发度与Segment个数相等。
2.  Java 8为进⼀步提⾼并发性，摒弃了分段锁的⽅案，⽽是直接使⽤⼀个⼤的数组。同时为了提⾼哈希碰撞下的寻址性能，Java 8在链表⻓度超过⼀定阈值（8）时将链表（寻址时间复杂度为O(N)）转换为红⿊树（寻址时间复杂度为O(long(N))）。
    其数据结构如下图所示
    ![](img/2ef146b6155abb0955b40e50526b5231.png)
3.  源码：

    ```
     1 public V put(K key, V value) {
    2 return putVal(key, value, false);
    3 }
    4
    5 /** Implementation for put and putIfAbsent */
    6 final V putVal(K key, V value, boolean onlyIfAbsent) {
    7 //ConcurrentHashMap 不允许插⼊null键，HashMap允许插⼊⼀个null键
    8 if (key == null || value == null) throw new NullPointerException();
    9 //计算key的hash值
    10 int hash = spread(key.hashCode());
    11 int binCount = 0;
    12 //for循环的作⽤：因为更新元素是使⽤CAS机制更新，需要不断的失败重试，直到成功为⽌。
    13 for (Node<K,V>[] tab = table;;) {
    14 // f：链表或红⿊⼆叉树头结点，向链表中添加元素时，需要synchronized获取f的锁。
    15 Node<K,V> f; int n, i, fh;
    16 //判断Node[]数组是否初始化，没有则进⾏初始化操作
    17 if (tab == null || (n = tab.length) == 0)
    18 tab = initTable();
    19 //通过hash定位Node[]数组的索引坐标，是否有Node节点，如果没有则使⽤CAS进⾏添加（链表的头结点），添加失败则进⼊下次循环。
    20 else if ((f = tabAt(tab, i = (n - 1) & hash)) == null) {
    21 if (casTabAt(tab, i, null,
    22 new Node<K,V>(hash, key, value, null)))
    23 break; // no lock when adding to empty bin
    24 }
    25 //检查到内部正在移动元素（Node[] 数组扩容）
    26 else if ((fh = f.hash) == MOVED)
    27 //帮助它扩容
    28 tab = helpTransfer(tab, f);
    29 else {
    30 V oldVal = null;
    31 //锁住链表或红⿊⼆叉树的头结点
    32 synchronized (f) {
    33 //判断f是否是链表的头结点
    34 if (tabAt(tab, i) == f) {
    35 //如果fh>=0 是链表节点
    36 if (fh >= 0) {
    37 binCount = 1;
    38 //遍历链表所有节点
    39 for (Node<K,V> e = f;; ++binCount) {
    40 K ek;
    41 //如果节点存在，则更新value
    42 if (e.hash == hash &&
    43 ((ek = e.key) == key ||
    44 (ek != null && key.equals(ek)))) {
    45 oldVal = e.val;
    46 if (!onlyIfAbsent)
    47 e.val = value;
    48 break;
    49 }
    50 //不存在则在链表尾部添加新节点。
    51 Node<K,V> pred = e;
    52 if ((e = e.next) == null) {
    53 pred.next = new Node<K,V>(hash, key,
    54 value, null);
    55 break;
    56 }
    57 }
    58 }
    59 //TreeBin是红⿊⼆叉树节点
    60 else if (f instanceof TreeBin) {
    61 Node<K,V> p;
    62 binCount = 2;
    63 //添加树节点
    64 if ((p = ((TreeBin<K,V>)f).putTreeVal(hash, key,
    65 value)) != null) {
    66 oldVal = p.val;
    67 if (!onlyIfAbsent)
    68 p.val = value;
    69 }
    70 }
    71 }
    72 }
    73 
    74 if (binCount != 0) {
    75 //如果链表⻓度已经达到临界值8 就需要把链表转换为树结构
    76 if (binCount >= TREEIFY_THRESHOLD)
    77 treeifyBin(tab, i);
    78 if (oldVal != null)
    79 return oldVal;
    80 break;
    81 }
    82 }
    83 }
    84 //将当前ConcurrentHashMap的size数量+1
    85 addCount(1L, binCount);
    86 return null;
    87 }
    ```


# 851.concurrent包下有哪些类？

> 原文：[https://zwmst.com/4963.html](https://zwmst.com/4963.html)

ConcurrentHashMap、Future、FutureTask、AtomicInteger…


# 852.线程a,b,c,d运⾏任务，怎么保证当a,b,c线程执⾏完再执⾏d线程?

> 原文：[https://zwmst.com/4965.html](https://zwmst.com/4965.html)

1.  CountDownLatch类
    ⼀个同步辅助类，常⽤于某个条件发⽣后才能执⾏后续进程。给定计数初始化CountDownLatch，调⽤countDown(）⽅法，在计数到达零之前，await⽅法⼀直受阻塞。
    重要⽅法为countdown()与await()；
2.  join⽅法
    将线程B加⼊到线程A的尾部，当A执⾏完后B才执⾏。

    ```
    1 public static void main(String[] args) throws Exception {
    2 Th t = new Th("t1");
    3 Th t2 = new Th("t2");
    4 t.start();
    5 t.join();
    6 t2.start();
    7 }
    ```

3.  notify、wait⽅法，Java中的唤醒与等待⽅法，关键为synchronized代码块，参数线程间应相同，也常⽤Object作为参数。


# 853.⾼并发系统如何做性能优化？如何防⽌库存超卖？

> 原文：[https://zwmst.com/4967.html](https://zwmst.com/4967.html)

1.  ⾼并发系统性能优化：优化程序，优化服务配置，优化系统配置
    1.  尽量使⽤缓存，包括⽤户缓存，信息缓存等，多花点内存来做缓存，可以⼤量减少与数据库的交互，提⾼性能。
    2.  ⽤jprofiler等⼯具找出性能瓶颈，减少额外的开销。
    3.  优化数据库查询语句，减少直接使⽤hibernate等⼯具的直接⽣成语句（仅耗时较⻓的查询做优化）。
    4.  优化数据库结构，多做索引，提⾼查询效率。
    5.  统计的功能尽量做缓存，或按每天⼀统计或定时统计相关报表，避免需要时进⾏统计的功能。
    6.  能使⽤静态⻚⾯的地⽅尽量使⽤，减少容器的解析（尽量将动态内容⽣成静态html来显示）。
    7.  解决以上问题后，使⽤服务器集群来解决单台的瓶颈问题。
2.  防⽌库存超卖：
    1.  悲观锁：在更新库存期间加锁，不允许其它线程修改；
        1.  数据库锁：select xxx for update；
        2.  分布式锁；
    2.  乐观锁：使⽤带版本号的更新。每个线程都可以并发修改，但在并发时，只有⼀个线程会修改成功，其它会返回失败。
        1.  redis watch：监视键值对，作⽤时如果事务提交exec时发现监视的监视对发⽣变化，事务将被取消。
3.  消息队列：通过 FIFO 队列，使修改库存的操作串⾏化。
4.  总结：总的来说，不能把压⼒放在数据库上，所以使⽤ "select xxx for update" 的⽅式在⾼并发的场景下是不可⾏的。FIFO 同步队列的⽅式，可以结合库存限制队列⻓，但是在库存较多的场景下，⼜不太适⽤。所以相对来说，我会倾向于选择：乐观锁 / 缓存锁 / 分布式锁的⽅式。


# 854.线程池的参数配置，为什么java官⽅提供⼯⼚⽅法给线程池？

> 原文：[https://zwmst.com/4969.html](https://zwmst.com/4969.html)

1.  线程池简介：
    ![](img/a071b2cbf925ec6ed54487be2ffeabcd.png)
2.  核⼼参数：
    ![](img/783375db8dd01016d477632c3433a77e.png)
3.  ⼯⼚⽅法作⽤：ThreadPoolExecutor类就是Executor的实现类，但ThreadPoolExecutor在使⽤上并不是那么⽅便，在实例化时需要传⼊很多歌参数，还要考虑线程的并发数等与线程池运⾏效率有关的参数，所以官⽅建议使⽤Executors⼯程类来创建线程池对象。


# 说说synchronized的实现原理

> 原文：[https://zwmst.com/862.html](https://zwmst.com/862.html)

在 Java 中，每个对象都隐式包含一个 monitor（监视器）对象，加锁的过程其实就是竞争 monitor 的过程，当线程进入字节码 monitorenter 指令之后，线程将持有 monitor 对象， 执行 monitorexit 时释放 monitor 对象，当其他线程没有拿到 monitor 对象时，则需要阻塞 等待获取该对象。


# ReentrantLock与synchronized的区别

> 原文：[https://zwmst.com/864.html](https://zwmst.com/864.html)

ReentrantLock 有如下特点：

1.  可重入 ReentrantLock 和 syncronized 关键字一样，都是可重入锁，不过两者实现原理稍有差 别， RetrantLock 利用 AQS 的的 state 状态来判断资源是否已锁，同一线程重入加锁， state 的状态 +1 ; 同一线程重入解锁, state 状态 -1 (解锁必须为当前独占线程，否则异 常); 当 state 为 0 时解锁成功。

2.  需要手动加锁、解锁 synchronized 关键字是自动进行加锁、解锁的，而 ReentrantLock 需要 lock() 和 unlock() 方法配合 try/finally 语句块来完成，来手动加锁、解锁。

3.  支持设置锁的超时时间 synchronized 关键字无法设置锁的超时时间，如果一个获得锁的线程内部发生死锁，那 么其他线程就会一直进入阻塞状态，而 ReentrantLock 提供 tryLock 方法，允许设置线 程获取锁的超时时间，如果超时，则跳过，不进行任何操作，避免死锁的发生。

4.  支持公平/非公平锁 synchronized 关键字是一种非公平锁，先抢到锁的线程先执行。而 ReentrantLock 的 构造方法中允许设置 true/false 来实现公平、非公平锁，如果设置为 true ，则线程获取 锁要遵循"先来后到"的规则，每次都会构造一个线程 Node ，然后到双向链表的"尾 巴"后面排队，等待前面的 Node 释放锁资源。

5.  可中断锁 ReentrantLock 中的 lockInterruptibly() 方法使得线程可以在被阻塞时响应中断，比 如一个线程 t1 通过 lockInterruptibly() 方法获取到一个可重入锁，并执行一个长时间 的任务，另一个线程通过 interrupt() 方法就可以立刻打断 t1 线程的执行，来获取t1持 有的那个可重入锁。而通过 ReentrantLock 的 lock() 方法或者 Synchronized 持有锁 的线程是不会响应其他线程的 interrupt() 方法的，直到该方法主动释放锁之后才会响应 interrupt() 方法。


# 说一下synchronized锁升级过程

> 原文：[https://zwmst.com/870.html](https://zwmst.com/870.html)

1.  偏向锁 在 JDK1.8 中，其实默认是轻量级锁，但如果设定了 -XX:BiasedLockingStartupDelay = 0 ，那在对一个 Object 做 syncronized 的时候，会立即上一把偏向锁。当处于偏向锁 状态时， markwork 会记录当前线程 ID 。

2.  升级到轻量级锁 当下一个线程参与到偏向锁竞争时，会先判断 markword 中保存的线程 ID 是否与这个 线程 ID 相等，如果不相等，会立即撤销偏向锁，升级为轻量级锁。每个线程在自己的线 程栈中生成一个 LockRecord ( LR )，然后每个线程通过 CAS (自旋)的操作将锁对象头 中的 markwork 设置为指向自己的 LR 的指针，哪个线程设置成功，就意味着获得锁。 关于 synchronized 中此时执行的 CAS 操作是通过 native 的调用 HotSpot 中 bytecodeInterpreter.cpp 文件 C++ 代码实现的，有兴趣的可以继续深挖。

3.  升级到重量级锁 如果锁竞争加剧(如线程自旋次数或者自旋的线程数超过某阈值， JDK1.6 之后，由 JVM 自己控制该规则)，就会升级为重量级锁。此时就会向操作系统申请资源，线程挂起，进 入到操作系统内核态的等待队列中，等待操作系统调度，然后映射回用户态。在重量级 锁中，由于需要做内核态到用户态的转换，而这个过程中需要消耗较多时间，也就 是"重"的原因之一。


# 了解过什么是“伪共享”吗？

> 原文：[https://zwmst.com/872.html](https://zwmst.com/872.html)

CPU缓存从内存读数据时，是按缓存行读取的，即使只用到一个变量，也要将整行数据进行读 取，这行数据量可能包含其他变量。当多个线程同时修改同一个缓存行里的不同变量时，由于 同时只能有一个线程在操作，所以相比将每个变量放到不同缓存行里，性能会有所下降。多个 线程同时修改了同一个缓存行上的不同变量，由于不能并发修改，所以称为“伪共享”。


# “伪共享”出现的原因是什么？

> 原文：[https://zwmst.com/874.html](https://zwmst.com/874.html)

因为CPU缓存和内存交换数据的单位是缓存行，而同一个缓存行里的多个变量不能同时被多个 线程修改。


# 如何避免“伪共享”？

> 原文：[https://zwmst.com/876.html](https://zwmst.com/876.html)

1.  字节填充（创建变量时，使用字段对其进行填充，避免多个变量被分派到同一个缓存行 里）。

2.  JDK8提供了一个Contended注解来解决伪共享。


# Java里的线程有哪些状态？

> 原文：[https://zwmst.com/878.html](https://zwmst.com/878.html)

1.  初始(NEW)：新创建了一个线程对象，但还没有调用start()方法。

2.  运行(RUNNABLE)：Java线程中将就绪（ready）和运行中（running）两种状态笼统 的称为“运行”。线程对象创建后，其他线程(比如main线程）调用了该对象的start()方 法。该状态的线程位于可运行线程池中，等待被线程调度选中，获取CPU的使用权，此 时处于就绪状态（ready）。就绪状态的线程在获得CPU时间片后变为运行中状态 （running）。

3.  阻塞(BLOCKED)：表示线程阻塞于锁。

4.  等待(WAITING)：进入该状态的线程需要等待其他线程做出一些特定动作（通知或中 断）。

5.  超时等待(TIMED_WAITING)：该状态不同于WAITING，它可以在指定的时间后自行 返回。

6.  终止(TERMINATED)：表示该线程已经执行完毕。


# 什么是悲观锁？什么是乐观锁？

> 原文：[https://zwmst.com/880.html](https://zwmst.com/880.html)

当我们要对一个数据库中的一条数据进行修改的时候，为了避免同时被其他人修改，最好的办 法就是直接对该数据进行加锁以防止并发。

这种借助数据库锁机制在修改数据之前先锁定，再修改的方式被称之为悲观并发控制（又名 “悲观锁”，Pessimistic Concurrency Control，缩写“PCC”）。

之所以叫做悲观锁，是因为这是一种对数据的修改抱有悲观态度的并发控制方式。我们一般认 为数据被并发修改的概率比较大，所以需要在修改之前先加锁。

乐观锁（ Optimistic Locking ） 是相对悲观锁而言的，乐观锁假设数据一般情况下不会造成 冲突，所以在数据进行提交更新的时候，才会正式对数据的冲突与否进行检测，如果发现冲突 了，则让返回用户错误的信息，让用户决定如何去做。

相对于悲观锁，在对数据库进行处理的时候，乐观锁并不会使用数据库提供的锁机制。一般的 实现乐观锁的方式就是记录数据版本。


# 并发编程三要素？

> 原文：[https://zwmst.com/882.html](https://zwmst.com/882.html)

1）原子性 原子性指的是一个或者多个操作，要么全部执行并且在执行的过程中不被其他操作打断，要么 就全部都不执行。

2）可见性 可见性指多个线程操作一个共享变量时，其中一个线程对变量进行修改后，其他线程可以立即 看到修改的结果。

3）有序性 有序性，即程序的执行顺序按照代码的先后顺序来执行。


# 创建线程有哪些方式？

> 原文：[https://zwmst.com/884.html](https://zwmst.com/884.html)

1）继承Thread类创建线程类

2）通过Runnable接口创建线程类

3）通过Callable和Future创建线程

4）通过线程池创建


# 线程池的优点？

> 原文：[https://zwmst.com/886.html](https://zwmst.com/886.html)

1）重用存在的线程，减少对象创建销毁的开销。

2）可有效的控制最大并发线程数，提高系统资源的使用率，同时避免过多资源竞争，避免堵 塞。

3）提供定时执行、定期执行、单线程、并发数控制等功能。


# CyclicBarrier和CountDownLatch的区别

> 原文：[https://zwmst.com/888.html](https://zwmst.com/888.html)

1）CountDownLatch简单的说就是一个线程等待，直到他所等待的其他线程都执行完成并且 调用countDown()方法发出通知后，当前线程才可以继续执行。

2）cyclicBarrier是所有线程都进行等待，直到所有线程都准备好进入await()方法之后，所有 线程同时开始执行！

3）CountDownLatch的计数器只能使用一次。而CyclicBarrier的计数器可以使用reset() 方 法重置。所以CyclicBarrier能处理更为复杂的业务场景，比如如果计算发生错误，可以重置计 数器，并让线程们重新执行一次。

4）CyclicBarrier还提供其他有用的方法，比如getNumberWaiting方法可以获得 CyclicBarrier阻塞的线程数量。isBroken方法用来知道阻塞的线程是否被中断。如果被中断 返回true，否则返回false。


# 什么是CAS？

> 原文：[https://zwmst.com/890.html](https://zwmst.com/890.html)

CAS是compare and swap的缩写，即我们所说的比较交换。

cas是一种基于锁的操作，而且是乐观锁。在java中锁分为乐观锁和悲观锁。悲观锁是将资源 锁住，等一个之前获得锁的线程释放锁之后，下一个线程才可以访问。而乐观锁采取了一种宽 泛的态度，通过某种方式不加锁来处理资源，比如通过给记录加version来获取数据，性能较 悲观锁有很大的提高。

CAS 操作包含三个操作数 —— 内存位置（V）、预期原值（A）和新值(B)。如果内存地址里 面的值和A的值是一样的，那么就将内存里面的值更新成B。CAS是通过无限循环来获取数据 的，若果在第一轮循环中，a线程获取地址里面的值被b线程修改了，那么a线程需要自旋，到 下次循环才有可能机会执行。

java.util.concurrent.atomic 包下的类大多是使用CAS操作来实现的(AtomicInteger,AtomicBoolean,AtomicLong)。


# CAS的问题

> 原文：[https://zwmst.com/892.html](https://zwmst.com/892.html)

1）CAS容易造成ABA问题

一个线程a将数值改成了b，接着又改成了a，此时CAS认为是没有变化，其实是已经变化过 了，而这个问题的解决方案可以使用版本号标识，每操作一次version加1。在java5中，已经 提供了AtomicStampedReference来解决问题。

2） 不能保证代码块的原子性

CAS机制所保证的知识一个变量的原子性操作，而不能保证整个代码块的原子性。比如需要保 证3个变量共同进行原子性的更新，就不得不使用synchronized了。

3）CAS造成CPU利用率增加

之前说过了CAS里面是一个循环判断的过程，如果线程一直没有获取到状态，cpu资源会一直 被占用。


# 什么是AQS？

> 原文：[https://zwmst.com/894.html](https://zwmst.com/894.html)

AQS是AbustactQueuedSynchronizer的简称，它是一个Java提高的底层同步工具类，用一 个int类型的变量表示同步状态，并提供了一系列的CAS操作来管理这个同步状态。

AQS是一个用来构建锁和同步器的框架，使用AQS能简单且高效地构造出应用广泛的大量的同 步器，比如我们提到的ReentrantLock，Semaphore，其他的诸如 ReentrantReadWriteLock，SynchronousQueue，FutureTask等等皆是基于AQS的。


# AQS支持几种同步方式？

> 原文：[https://zwmst.com/896.html](https://zwmst.com/896.html)

1）独占式

2）共享式

这样方便使用者实现不同类型的同步组件，独占式如ReentrantLock，共享式如 Semaphore，CountDownLatch，组合式的如ReentrantReadWriteLock。

总之，AQS为使 用提供了底层支撑，如何组装实现，使用者可以自由发挥。


# 什么是自旋锁？

> 原文：[https://zwmst.com/898.html](https://zwmst.com/898.html)

自旋锁是SMP架构中的一种low-level的同步机制。

当线程A想要获取一把自旋锁而该锁又被其它线程锁持有时，线程A会在一个循环中自旋以检测 锁是不是已经可用了。

自旋锁需要注意：

由于自旋时不释放CPU，因而持有自旋锁的线程应该尽快释放自旋锁，否则等待该自旋锁的线 程会一直在那里自旋，这就会浪费CPU时间。

持有自旋锁的线程在sleep之前应该释放自旋锁以便其它线程可以获得自旋锁。


# 什么是多线程的上下文切换？

> 原文：[https://zwmst.com/900.html](https://zwmst.com/900.html)

即使是单核CPU也支持多线程执行代码，CPU通过给每个线程分配CPU时间片来实现这个机 制。时间片是CPU分配给各个线程的时间，因为时间片非常短，所以CPU通过不停地切换线程 执行，让我们感觉多个线程时同时执行的，时间片一般是几十毫秒（ms）

上下文切换过程中，CPU会停止处理当前运行的程序，并保存当前程序运行的具体位置以便之后继续运行 CPU通过时间片分配算法来循环执行任务，当前任务执行一个时间片后会切换到下一个任务。

但是，在切换前会保存上一个任务的状态，以便下次切换回这个任务时，可以再次加载这个任务的状态从任务保存到再加载的过程就是一次上下文切换


# 什么是线程和进程?

> 原文：[https://zwmst.com/902.html](https://zwmst.com/902.html)

进程：在操作系统中能够独立运行，并且作为资源分配的基本单位。它表示运行中的程序。系 统运行一个程序就是一个进程从创建、运行到消亡的过程。

线程：是一个比进程更小的执行单位，能够完成进程中的一个功能，也被称为轻量级进程。一 个进程在其执行的过程中可以产生多个线程。

线程与进程不同的是：同类的多个线程共享进程的堆和方法区资源，但每个线程有自己的程序 计数器、虚拟机栈和本地方法栈，所以系统在产生一个线程，或是在各个线程之间作切换工作 时，负担要比进程小得多。


# 程序计数器为什么是私有的?

> 原文：[https://zwmst.com/905.html](https://zwmst.com/905.html)

程序计数器主要有下面两个作用：

字节码解释器通过改变程序计数器来依次读取指令，从而实现代码的流程控制，如：顺序执 行、选择、循环、异常处理。 在多线程的情况下，程序计数器用于记录当前线程执行的位置，从而当线程被切换回来的时候 能够知道该线程上次运行到哪儿了。

（需要注意的是，如果执行的是 native 方法，那么程序计数器记录的是 undefined 地址，只 有执行的是 Java 代码时程序计数器记录的才是下一条指令的地址。）

所以，程序计数器私有主要是为了线程切换后能恢复到正确的执行位置。


# 虚拟机栈和本地方法栈为什么是私有的?

> 原文：[https://zwmst.com/907.html](https://zwmst.com/907.html)

虚拟机栈： 每个 Java 方法在执行的同时会创建一个栈帧用于存储局部变量表、操作数栈、常量池引用等信息。从方法调用直至执行完成的过程，就对应着一个栈帧在 Java 虚拟机栈中入栈和出栈的过程。

本地方法栈： 和虚拟机栈所发挥的作用非常相似，区别是： 虚拟机栈为虚拟机执行 Java 方法 （也就是字节码）服务，而本地方法栈则为虚拟机使用到的 Native 方法服务。

在 HotSpot 虚 拟机中和 Java 虚拟机栈合二为一。 所以，为了保证线程中的局部变量不被别的线程访问到，虚拟机栈和本地方法栈是线程私有 的。


# 并发与并行的区别？

> 原文：[https://zwmst.com/909.html](https://zwmst.com/909.html)

并发指的是多个任务交替进行，并行则是指真正意义上的“同时进行”。

实际上，如果系统内只有一个CPU，使用多线程时，在真实系统环境下不能并行，只能通过切 换时间片的方式交替进行，从而并发执行任务。真正的并行只能出现在拥有多个CPU的系统 中。


# 什么是线程死锁?如何避免死锁?

> 原文：[https://zwmst.com/911.html](https://zwmst.com/911.html)

多个线程同时被阻塞，它们中的一个或者全部都在等待某个资源被释放。由于线程被无限期地 阻塞，因此程序不可能正常终止。

假如线程 A 持有资源 2，线程 B 持有资源 1，他们同时都想申请对方的资源，所以这两个线程 就会互相等待而进入死锁状态。

避免死锁的几个常见方法： 避免一个线程同时获取多个锁 避免一个线程在锁内同时占用多个资源，尽量保证每个锁只占用一个资源。

尝试使用定时锁，使用 lock.tryLock(timeout) 来代替使用内部锁机制。

对于数据库锁，加锁和解锁必须在一个数据库连接里，否则会出现解锁失败的情况。


# sleep() 方法和 wait() 方法的区别和共同点?

> 原文：[https://zwmst.com/913.html](https://zwmst.com/913.html)

相同点： 两者都可以暂停线程的执行，都会让线程进入等待状态。

不同点： sleep()方法没有释放锁，而 wait()方法释放了锁。

sleep()方法属于Thread类的静态方法，作用于当前线程；而wait()方法是Object类的实例方 法，作用于对象本身。

执行sleep()方法后，可以通过超时或者调用interrupt()方法唤醒休眠中的线程；执行wait() 方法后，通过调用notify()或notifyAll()方法唤醒等待线程。


# 为什么我们调用 start() 方法时会执行 run() 方法，为什么我们不能直接调用 run() 方法？

> 原文：[https://zwmst.com/915.html](https://zwmst.com/915.html)

new 一个 Thread，线程进入初始状态；调用 start()方法，会启动一个线程并使线程进入了就 绪状态，当分配到时间片后就可以开始运行了。 start() 会执行线程的相应准备工作，然后自 动执行 run() 方法的内容，这是真正的多线程工作。 而直接执行 run() 方法，会把 run 方法 当成一个 main 线程下的普通方法去执行，并不会在某个线程中执行它，所以这并不是多线程 工作。

总结： 调用 start 方法可启动线程并使线程进入就绪状态，而 run 方法只是 thread 的一个普 通方法调用，还是在主线程里执行。


# 什么是线程安全问题？如何解决？

> 原文：[https://zwmst.com/917.html](https://zwmst.com/917.html)

线程安全问题指的是在某一线程从开始访问到结束访问某一数据期间，该数据被其他的线程所 修改，那么对于当前线程而言，该线程就发生了线程安全问题，表现形式为数据的缺失，数据 不一致等。

线程安全问题发生的条件：

1）多线程环境下，即存在包括自己在内存在有多个线程。

2）多线程环境下存在共享资源，且多线程操作该共享资源。

3）多个线程必须对该共享资源有非原子性操作。

线程安全问题的解决思路：

1）尽量不使用共享变量，将不必要的共享变量变成局部变量来使用。

2）使用synchronized关键字同步代码块，或者使用jdk包中提供的Lock为操作进行加锁。

3）使用ThreadLocal为每一个线程建立一个变量的副本，各个线程间独立操作，互不影响。


# 什么是活锁？

> 原文：[https://zwmst.com/919.html](https://zwmst.com/919.html)

活锁体现了一种谦让的美德，每个线程都想把资源让给对方，但是由于机器“智商”不够，可能 会产生一直将资源让来让去，导致资源在两个线程间跳动而无法使某一线程真正的到资源并执 行，这就是活锁的问题。


# 什么是线程的饥饿问题？如何解决？

> 原文：[https://zwmst.com/921.html](https://zwmst.com/921.html)

饥饿指的是某一线程或多个线程因为某些原因一直获取不到资源，导致程序一直无法执行。如 某一线程优先级太低导致一直分配不到资源，或者是某一线程一直占着某种资源不放，导致该 线程无法执行等。

解决方法： 与死锁相比，饥饿现象还是有可能在一段时间之后恢复执行的。可以设置合适的线程优先级来 尽量避免饥饿的产生。


# 什么是线程的阻塞问题？如何解决？

> 原文：[https://zwmst.com/923.html](https://zwmst.com/923.html)

阻塞是用来形容多线程的问题，几个线程之间共享临界区资源，那么当一个线程占用了临界区 资源后，所有需要使用该资源的线程都需要进入该临界区等待，等待会导致线程挂起，一直不 能工作，这种情况就是阻塞，如果某一线程一直都不释放资源，将会导致其他所有等待在这个 临界区的线程都不能工作。当我们使用synchronized或重入锁时，我们得到的就是阻塞线 程，如论是synchronized或者重入锁，都会在试图执行代码前，得到临界区的锁，如果得不 到锁，线程将会被挂起等待，知道其他线程执行完成并释放锁且拿到锁为止。

解决方法： 可以通过减少锁持有时间，读写锁分离，减小锁的粒度，锁分离，锁粗化等方式来优化锁的性 能。


# synchronized 关键字和 volatile 关键字的区别

> 原文：[https://zwmst.com/925.html](https://zwmst.com/925.html)

volatile关键字是线程同步的轻量级实现，所以volatile性能比synchronized关键字要好。但 是volatile关键字只能用于变量而synchronized关键字可以修饰方法以及代码块。

多线程访问volatile关键字不会发生阻塞，而synchronized关键字可能会发生阻塞。 volatile关键字主要用于解决变量在多个线程之间的可见性，而 synchronized关键字解决的 是多个线程之间访问资源的同步性。

volatile关键字能保证数据的可见性，但不能保证数据的原子性。synchronized关键字两者都 能保证。


# 说一说几种常见的线程池及适用场景？

> 原文：[https://zwmst.com/927.html](https://zwmst.com/927.html)

FixedThreadPool：可重用固定线程数的线程池。（适用于负载比较重的服务器） FixedThreadPool使用无界队列LinkedBlockingQueue作为线程池的工作队列 该线程池中的线程数量始终不变。当有一个新的任务提交时，线程池中若有空闲线程，则立即 执行。若没有，则新的任务会被暂存在一个任务队列中，待有线程空闲时，便处理在任务队列 中的任务。

SingleThreadExecutor：只会创建一个线程执行任务。（适用于需要保证顺序执行各个任 务；并且在任意时间点，没有多线程活动的场景。） SingleThreadExecutorl也使用无界队列LinkedBlockingQueue作为工作队列 若多余一个任务被提交到该线程池，任务会被保存在一个任务队列中，待线程空闲，按先入先 出的顺序执行队列中的任务。

CachedThreadPool：是一个会根据需要调整线程数量的线程池。（大小无界，适用于执行很 多的短期异步任务的小程序，或负载较轻的服务器） CachedThreadPool使用没有容量的SynchronousQueue作为线程池的工作队列，但 CachedThreadPool的maximumPool是无界的。 线程池的线程数量不确定，但若有空闲线程可以复用，则会优先使用可复用的线程。若所有线 程均在工作，又有新的任务提交，则会创建新的线程处理任务。所有线程在当前任务执行完毕 后，将返回线程池进行复用。

ScheduledThreadPool：继承自ThreadPoolExecutor。它主要用来在给定的延迟之后运行 任务，或者定期执行任务。使用DelayQueue作为任务队列。


# 线程池都有哪几种工作队列？

> 原文：[https://zwmst.com/929.html](https://zwmst.com/929.html)

ArrayBlockingQueue：是一个基于数组结构的有界阻塞队列，此队列按FIFO（先进先出）原 则对元素进行排序。

LinkedBlockingQueue：是一个基于链表结构的阻塞队列，此队列按FIFO排序元素，吞吐量 通常要高于ArrayBlockingQueue。静态工厂方法Executors.newFixedThreadPool()使用了 这个队列。

SynchronousQueue：是一个不存储元素的阻塞队列。每个插入操作必须等到另一个线程调用 移除操作，否则插入操作一直处于阻塞状态，吞吐量通常要高于Linked-BlockingQueue，静 态工厂方法Executors.newCachedThreadPool使用了这个队列。

PriorityBlockingQueue：一个具有优先级的无限阻塞队列。


# 什么是线程安全？

> 原文：[https://zwmst.com/931.html](https://zwmst.com/931.html)

如果你的代码在多线程下执行和在单线程下执行永远都能获得一样的结果，那么你的代码就是 线程安全的。

这个问题有值得一提的地方，就是线程安全也是有几个级别的：

1）不可变

像String、Integer、Long这些，都是final类型的类，任何一个线程都改变不了它们的值，要 改变除非新创建一个，因此这些不可变对象不需要任何同步手段就可以直接在多线程环境下使 用

2）绝对线程安全

不管运行时环境如何，调用者都不需要额外的同步措施。要做到这一点通常需要付出许多额外 的代价，Java中标注自己是线程安全的类，实际上绝大多数都不是线程安全的，不过绝对线程 安全的类，Java中也有，比方说CopyOnWriteArrayList、CopyOnWriteArraySet

3）相对线程安全

相对线程安全也就是我们通常意义上所说的线程安全，像Vector这种，add、remove方法都 是原子操作，不会被打断，但也仅限于此，如果有个线程在遍历某个Vector、有个线程同时在 add这个Vector，99%的情况下都会出现ConcurrentModificationException，也就是failfast机制。

4）线程非安全

这个就没什么好说的了，ArrayList、LinkedList、HashMap等都是线程非安全的类，点击这 里了解为什么不安全。


# Java中如何获取到线程dump文件

> 原文：[https://zwmst.com/933.html](https://zwmst.com/933.html)

死循环、死锁、阻塞、页面打开慢等问题，打线程dump是最好的解决问题的途径。所谓线程 dump也就是线程堆栈，获取到线程堆栈有两步：

1）获取到线程的pid，可以通过使用jps命令，在Linux环境下还可以使用ps -ef | grep java

2）打印线程堆栈，可以通过使用jstack pid命令，在Linux环境下还可以使用kill -3 pid

另外提一点，Thread类提供了一个getStackTrace()方法也可以用于获取线程堆栈。这是一个 实例方法，因此此方法是和具体线程实例绑定的，每次获取获取到的是具体某个线程当前运行 的堆栈。


# Java中用到的线程调度算法是什么？

> 原文：[https://zwmst.com/935.html](https://zwmst.com/935.html)

抢占式。一个线程用完CPU之后，操作系统会根据线程优先级、线程饥饿情况等数据算出一个 总的优先级并分配下一个时间片给某个线程执行。


# Thread.sleep(0)的作用是什么？

> 原文：[https://zwmst.com/937.html](https://zwmst.com/937.html)

由于Java采用抢占式的线程调度算法，因此可能会出现某条线程常常获取到CPU控制权的情 况，为了让某些优先级比较低的线程也能获取到CPU控制权，可以使用Thread.sleep(0)手动 触发一次操作系统分配时间片的操作，这也是平衡CPU控制权的一种操作。


# 单例模式的线程安全性

> 原文：[https://zwmst.com/939.html](https://zwmst.com/939.html)

1）饿汉式单例模式的写法：线程安全

2）懒汉式单例模式的写法：非线程安全

3）双检锁单例模式的写法：线程安全


# Semaphore有什么作用？

> 原文：[https://zwmst.com/941.html](https://zwmst.com/941.html)

Semaphore就是一个信号量，它的作用是限制某段代码块的并发数。

Semaphore有一个构造 函数，可以传入一个int型整数n，表示某段代码最多只有n个线程可以访问，如果超出了n，那 么请等待，等到某个线程执行完毕这段代码块，下一个线程再进入。

由此可以看出如果 Semaphore构造函数中传入的int型整数n=1，相当于变成了一个synchronized了。


# Hashtable的size()方法中明明只有一条语句”return count”，为什么还要做同步？

> 原文：[https://zwmst.com/943.html](https://zwmst.com/943.html)

1）同一时间只能有一条线程执行固定类的同步方法，但是对于类的非同步方法，可以多条线程 同时访问。所以，这样就有问题了，可能线程A在执行Hashtable的put方法添加数据，线程B 则可以正常调用size()方法读取Hashtable中当前元素的个数，那读取到的值可能不是最新 的，可能线程A添加了完了数据，但是没有对size++，线程B就已经读取size了，那么对于线 程B来说读取到的size一定是不准确的。而给size()方法加了同步之后，意味着线程B调用 size()方法只有在线程A调用put方法完毕之后才可以调用，这样就保证了线程安全性

2）CPU执行代码，执行的不是Java代码，这点很关键，一定得记住。Java代码最终是被翻译 成机器码执行的，机器码才是真正可以和硬件电路交互的代码。即使你看到Java代码只有一 行，甚至你看到Java代码编译之后生成的字节码也只有一行，也不意味着对于底层来说这句语 句的操作只有一个。一句"return count"假设被翻译成了三句汇编语句执行，一句汇编语句和 其机器码做对应，完全可能执行完第一句，线程就切换了。


# 同步方法和同步块，哪个是更好的选择？

> 原文：[https://zwmst.com/945.html](https://zwmst.com/945.html)

同步块，这意味着同步块之外的代码是异步执行的，这比同步整个方法更提升代码的效率。请 知道一条原则：同步的范围越小越好。

虽说同步的范围越少越好，但是在Java虚拟机中还是存在着一种叫做锁粗化的优化方法，这种 方法就是把同步范围变大。这是有用的，比方说StringBuffer，它是一个线程安全的类，自然 最常用的append()方法是一个同步方法，我们写代码的时候会反复append字符串，这意味着 要进行反复的加锁->解锁，这对性能不利，因为这意味着Java虚拟机在这条线程上要反复地在 内核态和用户态之间进行切换，因此Java虚拟机会将多次append方法调用的代码进行一个锁 粗化的操作，将多次的append的操作扩展到append方法的头尾，变成一个大的同步块，这样 就减少了加锁–>解锁的次数，有效地提升了代码执行的效率。


# 高并发、任务执行时间短的业务怎样使用线程池？并发不高、任务执行时间长的业务 怎样使用线程池？并发高、业务执行时间长的业务怎样使用线程池？

> 原文：[https://zwmst.com/947.html](https://zwmst.com/947.html)

1）高并发、任务执行时间短的业务，线程池线程数可以设置为CPU核数+1，减少线程上下文 的切换

2）并发不高、任务执行时间长的业务要区分开看：

a）假如是业务时间长集中在IO操作上，也就是IO密集型的任务，因为IO操作并不占用CPU， 所以不要让所有的CPU闲下来，可以加大线程池中的线程数目，让CPU处理更多的业务

b）假如是业务时间长集中在计算操作上，也就是计算密集型任务，这个就没办法了，和（1） 一样吧，线程池中的线程数设置得少一些，减少线程上下文的切换

c）并发高、业务执行时间长，解决这种类型任务的关键不在于线程池而在于整体架构的设 计，看看这些业务里面某些数据是否能做缓存是第一步，增加服务器是第二步，至于线程池的 设置，设置参考其他有关线程池的文章。最后，业务执行时间长的问题，也可能需要分析一 下，看看能不能使用中间件对任务进行拆分和解耦。


# 在Java中Lock接口比synchronized块的优势是什么？你需要实现一个高效的缓存， 它允许多个用户读，但只允许一个用户写，以此来保持它的完整性，你会怎样去实现 它？

> 原文：[https://zwmst.com/949.html](https://zwmst.com/949.html)

lock接口在多线程和并发编程中最大的优势是它们为读和写分别提供了锁，它能满足你写像 ConcurrentHashMap这样的高性能数据结构和有条件的阻塞。Java线程面试的问题越来越会 根据面试者的回答来提问。我强烈建议在你去参加多线程的面试之前认真读一下Locks，因为 当前其大量用于构建电子交易终统的客户端缓存和交易连接空间。


# 你将如何使用thread dump？你将如何分析Thread dump？

> 原文：[https://zwmst.com/951.html](https://zwmst.com/951.html)

在UNIX中你可以使用kill -3，然后thread dump将会打印日志，在windows中你可以使用” CTRL+Break”。非常简单和专业的线程面试问题，但是如果他问你怎样分析它，就会很棘 手。


# 67.JAVA 线程实现/创建方式

> 原文：[https://zwmst.com/3037.html](https://zwmst.com/3037.html)

1.  继承 Thread 类
    Thread 类本质上是实现了 Runnable 接口的一个实例，代表一个线程的实例。启动线程的唯一方法就是通过 Thread 类的 start()实例方法。**start()方法是一个 native 方法**，它将启动一个新线程，并执行 run()方法。

    ```
    public class MyThread extends Thread { 
    public void run() { 
    System.out.println("MyThread.run()"); 
    } 
    } 
    MyThread myThread1 = new MyThread(); 
    myThread1.start(); 
    ```

2.  实现 Runnable 接口。
    如果自己的类已经 extends 另一个类，就无法直接 extends Thread，此时，可以实现一个Runnable 接口。

    ```
    public class MyThread extends OtherClass implements Runnable { 
    public void run() { 
    System.out.println("MyThread.run()"); 
    } 
    } 
    //启动 MyThread，需要首先实例化一个 Thread，并传入自己的 MyThread 实例：
    MyThread myThread = new MyThread(); 
    Thread thread = new Thread(myThread); 
    thread.start(); 
    //事实上，当传入一个 Runnable target 参数给 Thread 后，Thread 的 run()方法就会调用
    target.run()
    public void run() { 
    if (target != null) { 
    target.run(); 
    } 
    } 
    ```

3.  ExecutorService、Callable`<Class>`、Future 有返回值线程有返回值的任务必须实现 Callable 接口，类似的，无返回值的任务必须 Runnable 接口。执行Callable 任务后，可以获取一个 Future 的对象，在该对象上调用 get 就可以获取到 Callable 任务返回的 Object 了，再结合线程池接口 ExecutorService 就可以实现传说中有返回结果的多线程了。

    ```
    //创建一个线程池
    ExecutorService pool = Executors.newFixedThreadPool(taskSize);
    // 创建多个有返回值的任务
    List<Future> list = new ArrayList<Future>(); 
    for (int i = 0; i < taskSize; i++) { 
    Callable c = new MyCallable(i + " "); 
    // 执行任务并获取 Future 对象
    Future f = pool.submit(c); 
    list.add(f); 
    } 
    // 关闭线程池
    pool.shutdown(); 
    // 获取所有并发任务的运行结果
    for (Future f : list) { 
    // 从 Future 对象上获取任务的返回值，并输出到控制台
    System.out.println("res：" + f.get().toString()); 
    } 
    ```

4.  基于线程池的方式
    线程和数据库连接这些资源都是非常宝贵的资源。那么每次需要的时候创建，不需要的时候销毁，是非常浪费资源的。那么我们就可以使用缓存的策略，也就是使用线程池。

    ```
    // 创建线程池
    ExecutorService threadPool = Executors.newFixedThreadPool(10);
    while(true) {
    threadPool.execute(new Runnable() { // 提交多个线程任务，并执行
    @Override
    public void run() {
    System.out.println(Thread.currentThread().getName() + " is running ..");
    try {
    Thread.sleep(3000);
    } catch (InterruptedException e) {
    e.printStackTrace();
    }
    }
    });
    }
    }
    ```


# 68.4 种线程池

> 原文：[https://zwmst.com/3039.html](https://zwmst.com/3039.html)

Java 里面线程池的顶级接口是 Executor，但是严格意义上讲Executor 并不是一个线程池，而只是一个执行线程的工具。真正的线程池接口是 ExecutorService。

1.  newCachedThreadPool
    创建一个可根据需要创建新线程的线程池，但是在以前构造的线程可用时将重用它们。对于执行很多短期异步任务的程序而言，这些线程池通常可提高程序性能。**调用 execute 将重用以前构造的线程（如果线程可用）。如果现有线程没有可用的，则创建一个新线程并添加到池中。终止并从缓存中移除那些已有 60 秒钟未被使用的线程**。因此，长时间保持空闲的线程池不会使用任何资源。

2.  newFixedThreadPool
    创建一个可重用固定线程数的线程池，以共享的无界队列方式来运行这些线程。在任意点，在大多数 nThreads 线程会处于处理任务的活动状态。如果在所有线程处于活动状态时提交附加任务，则在有可用线程之前，附加任务将在队列中等待。如果在关闭前的执行期间由于失败而导致任何线程终止，那么一个新线程将代替它执行后续的任务（如果需要）。在某个线程被显式地关闭之前，池中的线程将一直存在。

3.  newScheduledThreadPool
    创建一个线程池，它可安排在给定延迟后运行命令或者定期地执行。

    ```
    ScheduledExecutorService scheduledThreadPool= Executors.newScheduledThreadPool(3); 
    scheduledThreadPool.schedule(newRunnable(){ 
    @Override 
    public void run() {
    System.out.println("延迟三秒");
    }
    }, 3, TimeUnit.SECONDS);
    scheduledThreadPool.scheduleAtFixedRate(newRunnable(){ 
    @Override 
    public void run() {
    System.out.println("延迟 1 秒后每三秒执行一次");
    }
    },1,3,TimeUnit.SECONDS);
    ```

4.  newSingleThreadExecutor
    Executors.newSingleThreadExecutor()返回一个线程池（这个线程池只有一个线程）,**这个线程池可以在线程死后（或发生异常时）重新启动一个线程来替代原来的线程继续执行下去**！


# 69.线程生命周期(状态)

> 原文：[https://zwmst.com/3041.html](https://zwmst.com/3041.html)

当线程被创建并启动以后，它既不是一启动就进入了执行状态，也不是一直处于执行状态。在线程的生命周期中，它要经过新建(New)、就绪（Runnable）、运行（Running）、阻塞(Blocked)和死亡(Dead)5 种状态。尤其是当线程启动以后，它不可能一直"霸占"着 CPU 独自运行，所以 CPU 需要在多条线程之间切换，于是线程状态也会多次在运行、阻塞之间切换


# 70.新建状态（NEW）

> 原文：[https://zwmst.com/3043.html](https://zwmst.com/3043.html)

当程序**使用 new 关键字创建了一个线程之后**，该线程就处于新建状态，此时仅由 JVM 为其分配内存，并初始化其成员变量的值


# 71.就绪状态（RUNNABLE）

> 原文：[https://zwmst.com/3045.html](https://zwmst.com/3045.html)

当线程对象**调用了 start()方法之后**，该线程处于就绪状态。Java 虚拟机会为其创建方法调用栈和程序计数器，等待调度运行。


# 72.运行状态（RUNNING）

> 原文：[https://zwmst.com/3047.html](https://zwmst.com/3047.html)

如果处于**就绪状态的线程获得了 CPU，开始执行 run()方法的线程执行体**，则该线程处于运行状态。


# 73.阻塞状态（BLOCKED）

> 原文：[https://zwmst.com/3049.html](https://zwmst.com/3049.html)

阻塞状态是指线程因为某种原因放弃了 cpu 使用权，也即让出了 cpu timeslice，暂时停止运行。直到线程进入可运行(runnable)状态，才有机会再次获得 cpu timeslice 转到运行(running)状态。阻塞的情况分三种：

### 等待阻塞（o.wait->等待对列）：

```
运行(running)的线程执行 o.wait()方法，JVM 会把该线程放入等待队列(waitting queue)中。
```

### 同步阻塞(lock->锁池)

```
运行(running)的线程在获取对象的同步锁时，若该同步锁被别的线程占用，则 JVM 会把该线程放入锁池(lock pool)中。
```

### 其他阻塞(sleep/join)

```
运行(running)的线程执行 Thread.sleep(long ms)或 t.join()方法，或者发出了 I/O 请求时，JVM 会把该线程置为阻塞状态。当 sleep()状态超时、join()等待线程终止或者超时、或者 I/O处理完毕时，线程重新转入可运行(runnable)状态。
```


# 74.线程死亡（DEAD）

> 原文：[https://zwmst.com/3051.html](https://zwmst.com/3051.html)

线程会以下面三种方式结束，结束后就是死亡状态。

## 正常结束

1.  run()或 call()方法执行完成，线程正常结束。

## 异常结束

2.  线程抛出一个未捕获的 Exception 或 Error。

## 调用 stop

3.  直接调用该线程的 stop()方法来结束该线程—该方法通常容易导致死锁，不推荐使用。


# 75\. 终止线程 4 种方式

> 原文：[https://zwmst.com/3053.html](https://zwmst.com/3053.html)

1.  正常运行结束
    程序运行结束，线程自动结束。

2.  使用退出标志退出线程
    一般 run()方法执行完，线程就会正常结束，然而，常常有些线程是伺服线程。它们需要长时间的运行，只有在外部某些条件满足的情况下，才能关闭这些线程。使用一个变量来控制循环，例如：
    最直接的方法就是设一个 boolean 类型的标志，并通过设置这个标志为 true 或 false 来控制 while循环是否退出，代码示例：

    ```
    public class ThreadSafe extends Thread {
    public volatile boolean exit = false; 
    public void run() { 
    while (!exit){
    //do something
    }
    } 
    }
    ```

    定义了一个退出标志 exit，当 exit 为 true 时，while 循环退出，exit 的默认值为 false.在定义 exit时，使用了一个 Java 关键字 volatile，这个关键字的目的是使 exit 同步，也就是说在同一时刻只能由一个线程来修改 exit 的值。

3.  Interrupt 方法结束线程
    使用 interrupt()方法来中断线程有两种情况：

    1.  线程处于阻塞状态：如使用了 sleep,同步锁的 wait,socket 中的 receiver,accept 等方法时，会使线程处于阻塞状态。当调用线程的 interrupt()方法时，会抛出 InterruptException 异常。阻塞中的那个方法抛出这个异常，通过代码捕获该异常，然后 break 跳出循环状态，从而让我们有机会结束这个线程的执行。通常很多人认为只要调用 interrupt 方法线程就会结束，实际上是错的， 一定要先捕获 InterruptedException 异常之后通过 break 来跳出循环，才能正常结束 run 方法。
    2.  线程未处于阻塞状态：使用 isInterrupted()判断线程的中断标志来退出循环。当使用interrupt()方法时，中断标志就会置 true，和使用自定义的标志来控制循环是一样的道理。

        ```
        public class ThreadSafe extends Thread {
        public void run() { 
        while (!isInterrupted()){ //非阻塞过程中通过判断中断标志来退出
        try{
        Thread.sleep(5*1000);//阻塞过程捕获中断异常来退出
        }catch(InterruptedException e){
        e.printStackTrace();
        break;//捕获到异常之后，执行 break 跳出循环
        }
        }
        } 
        }
        ```

4.  stop 方法终止线程（线程不安全）
    程序中可以直接使用 thread.stop()来强行终止线程，但是 stop 方法是很危险的，就象突然关闭计算机电源，而不是按正常程序关机一样，可能会产生不可预料的结果，不安全主要是：thread.stop()调用之后，创建子线程的线程就会抛出 ThreadDeatherror 的错误，并且会释放子线程所持有的所有锁。一般任何进行加锁的代码块，都是为了保护数据的一致性，如果在调用thread.stop()后导致了该线程所持有的所有锁的突然释放(不可控制)，那么被保护数据就有可能呈现不一致性，其他线程在使用这些被破坏的数据时，有可能导致一些很奇怪的应用程序错误。因此，并不推荐使用 stop 方法来终止线程。


# 76\. sleep 与 wait 区别

> 原文：[https://zwmst.com/3057.html](https://zwmst.com/3057.html)

1.  对于 sleep()方法，我们首先要知道该方法是属于 Thread 类中的。而 wait()方法，则是属于Object 类中的。
2.  sleep()方法导致了程序暂停执行指定的时间，让出 cpu 该其他线程，但是他的监控状态依然保持者，当指定的时间到了又会自动恢复运行状态。
3.  在调用 sleep()方法的过程中，线程不会释放对象锁。
4.  而当调用 wait()方法的时候，线程会放弃对象锁，进入等待此对象的等待锁定池，只有针对此对象调用 notify()方法后本线程才进入对象锁定池准备获取对象锁进入运行状态。


# 77.start 与 run 区别

> 原文：[https://zwmst.com/3059.html](https://zwmst.com/3059.html)

1.  start（）方法来启动线程，真正实现了多线程运行。这时无需等待 run 方法体代码执行完毕，可以直接继续执行下面的代码。
2.  通过调用 Thread 类的 start()方法来启动一个线程， 这时此线程是处于就绪状态， 并没有运行。
3.  方法 run()称为线程体，它包含了要执行的这个线程的内容，线程就进入了运行状态，开始运行 run 函数当中的代码。 Run 方法运行结束， 此线程终止。然后 CPU 再调度其它线程。


# 78.JAVA 后台线程

> 原文：[https://zwmst.com/3062.html](https://zwmst.com/3062.html)

1.  定义：守护线程–也称“服务线程”，他是后台线程，它有一个特性，即为用户线程 提供 公共服务，在没有用户线程可服务时会自动离开。
2.  优先级：守护线程的优先级比较低，用于为系统中的其它对象和线程提供服务。
3.  设置：通过 setDaemon(true)来设置线程为“守护线程”；将一个用户线程设置为守护线程的方式是在 线程对象创建 之前 用线程对象的 setDaemon 方法。
4.  在 Daemon 线程中产生的新线程也是 Daemon 的。
5.  线程则是 JVM 级别的，以 Tomcat 为例，如果你在 Web 应用中启动一个线程，这个线程的生命周期并不会和 Web 应用程序保持同步。也就是说，即使你停止了 Web 应用，这个线程依旧是活跃的。
6.  example: 垃圾回收线程就是一个经典的守护线程，当我们的程序中不再有任何运行的Thread,程序就不会再产生垃圾，垃圾回收器也就无事可做，所以当垃圾回收线程是 JVM 上仅剩的线程时，垃圾回收线程会自动离开。它始终在低级别的状态中运行，用于实时监控和管理系统中的可回收资源。
7.  生命周期：守护进程（Daemon）是运行在后台的一种特殊进程。它独立于控制终端并且周期性地执行某种任务或等待处理某些发生的事件。也就是说守护线程不依赖于终端，但是依赖于系统，与系统“同生共死”。当 JVM 中所有的线程都是守护线程的时候，JVM 就可以退出了；如果还有一个或以上的非守护线程则 JVM 不会退出。


# 79.乐观锁

> 原文：[https://zwmst.com/3064.html](https://zwmst.com/3064.html)

乐观锁是一种乐观思想，即认为读多写少，遇到并发写的可能性低，每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是**在更新的时候会判断一下在此期间别人有没有去更新这个数据，采取在写时先读出当前版本号，然后加锁操作**（比较跟上一次的版本号，如果一样则更新），如果失败则要重复读-比较-写的操作。

java 中的乐观锁基本都是通过 CAS 操作实现的，CAS 是一种更新的原子操作，**比较当前值跟传入值是否一样，一样则更新，否则失败**。


# 80.悲观锁

> 原文：[https://zwmst.com/3066.html](https://zwmst.com/3066.html)

悲观锁是就是悲观思想，即认为写多，遇到并发写的可能性高，每次去拿数据的时候都认为别人会修改，所以每次在读写数据的时候都会上锁，这样别人想读写这个数据就会 block 直到拿到锁。

java中的悲观锁就是**Synchronized**,AQS框架下的锁则是先尝试cas乐观锁去获取锁，获取不到，才会转换为悲观锁，如RetreenLock。


# 81.自旋锁

> 原文：[https://zwmst.com/3068.html](https://zwmst.com/3068.html)

自旋锁原理非常简单，**如果持有锁的线程能在很短时间内释放锁资源，那么那些等待竞争锁的线程就不需要做内核态和用户态之间的切换进入阻塞挂起状态，它们只需要等一等（自旋），等持有锁的线程释放锁后即可立即获取锁，这样就避免用户线程和内核的切换的消耗**。

线程自旋是需要消耗 cup 的，说白了就是让 cup 在做无用功，如果一直获取不到锁，那线程也不能一直占用 cup 自旋做无用功，所以需要设定一个自旋等待的最大时间。

如果持有锁的线程执行的时间超过自旋等待的最大时间扔没有释放锁，就会导致其它争用锁的线程在最大等待时间内还是获取不到锁，这时争用线程会停止自旋进入阻塞状态。

### 自旋锁的优缺点

自旋锁尽可能的减少线程的阻塞，这对于锁的竞争不激烈，且占用锁时间非常短的代码块来说性能能大幅度的提升，因为自旋的消耗会小于线程阻塞挂起再唤醒的操作的消耗，这些操作会导致线程发生两次上下文切换！

但是如果锁的竞争激烈，或者持有锁的线程需要长时间占用锁执行同步块，这时候就不适合使用自旋锁了，因为自旋锁在获取锁前一直都是占用 cpu 做无用功，占着 XX 不 XX，同时有大量线程在竞争一个锁，会导致获取锁的时间很长，线程自旋的消耗大于线程阻塞挂起操作的消耗，其它需要 cup 的线程又不能获取到 cpu，造成 cpu 的浪费。所以这种情况下我们要关闭自旋锁；

### 自旋锁时间阈值（1.6 引入了适应性自旋锁）

自旋锁的目的是为了占着 CPU 的资源不释放，等到获取到锁立即进行处理。但是如何去选择自旋的执行时间呢？如果自旋执行时间太长，会有大量的线程处于自旋状态占用 CPU 资源，进而会影响整体系统的性能。因此自旋的周期选的额外重要！

JVM 对于自旋周期的选择，jdk1.5 这个限度是一定的写死的，**在 1.6 引入了适应性自旋锁**，适应性自旋锁意味着自旋的时间不在是固定的了，而是**由前一次在同一个锁上的自旋时间以及锁的拥有者的状态来决定**，基本认为一个线程上下文切换的时间是最佳的一个时间，同时 JVM 还针对当前 CPU 的负荷情况做了较多的优化，如果平均负载小于 CPUs 则一直自旋，如果有超过(CPUs/2)个线程正在自旋，则后来线程直接阻塞，如果正在自旋的线程发现 Owner 发生了变化则延迟自旋
时间（自旋计数）或进入阻塞，如果 CPU 处于节电模式则停止自旋，自旋时间的最坏情况是 CPU的存储延迟（CPU A 存储了一个数据，到 CPU B 得知这个数据直接的时间差），自旋时会适当放弃线程优先级之间的差异。

### 自旋锁的开启

JDK1.6 中-XX:+UseSpinning 开启；
-XX:PreBlockSpin=10 为自旋次数；
JDK1.7 后，去掉此参数，由 jvm 控制；


# 82.Synchronized 同步锁

> 原文：[https://zwmst.com/3070.html](https://zwmst.com/3070.html)

synchronized 它可以把任意一个非 NULL 的对象当作锁。**他属于独占式的悲观锁，同时属于可重入锁**。


# 83.Synchronized 作用范围

> 原文：[https://zwmst.com/3072.html](https://zwmst.com/3072.html)

1.  作用于方法时，锁住的是对象的实例(this)；
2.  当作用于静态方法时，锁住的是Class实例，又因为Class的相关数据存储在永久带PermGen（jdk1.8 则是 metaspace），永久带是全局共享的，因此静态方法锁相当于类的一个全局锁，会锁所有调用该方法的线程；
3.  synchronized 作用于一个对象实例时，锁住的是所有以该对象为锁的代码块。它有多个队列，当多个线程一起访问某个对象监视器的时候，对象监视器会将这些线程存储在不同的容器中。


# 84.Synchronized 核心组件

> 原文：[https://zwmst.com/3074.html](https://zwmst.com/3074.html)

1) Wait Set：哪些调用 wait 方法被阻塞的线程被放置在这里；
2) Contention List：**竞争队列**，所有请求锁的线程首先被放在这个竞争队列中；
3) Entry List：Contention List 中那些**有资格成为候选资源的线程被移动到 Entry List 中**；
4) OnDeck：任意时刻，**最多只有一个线程正在竞争锁资源，该线程被成为 OnDeck**；
5) Owner：当前已经获取到所资源的线程被称为 Owner；
6) !Owner：当前释放锁的线程。


# 85.Synchronized 实现

> 原文：[https://zwmst.com/3076.html](https://zwmst.com/3076.html)

1.  JVM 每次从队列的尾部取出一个数据用于锁竞争候选者（OnDeck），但是并发情况下，ContentionList 会被大量的并发线程进行 CAS 访问，为了降低对尾部元素的竞争，JVM 会将一部分线程移动到 EntryList 中作为候选竞争线程。

2.  Owner 线程会在 unlock 时，将 ContentionList 中的部分线程迁移到 EntryList 中，并指定EntryList 中的某个线程为 OnDeck 线程（一般是最先进去的那个线程）。

3.  Owner 线程并不直接把锁传递给 OnDeck 线程，而是把锁竞争的权利交给 OnDeck，OnDeck 需要重新竞争锁。这样虽然牺牲了一些公平性，但是能极大的提升系统的吞吐量，在JVM 中，也把这种选择行为称之为“竞争切换”。

4.  OnDeck 线程获取到锁资源后会变为 Owner 线程，而没有得到锁资源的仍然停留在 EntryList中。如果 Owner 线程被 wait 方法阻塞，则转移到 WaitSet 队列中，直到某个时刻通过 notify或者 notifyAll 唤醒，会重新进去 EntryList 中。

5.  处于 ContentionList、EntryList、WaitSet 中的线程都处于阻塞状态，该阻塞是由操作系统来完成的（Linux 内核下采用 pthread_mutex_lock 内核函数实现的）。

6.  Synchronized 是非公平锁。 Synchronized 在线程进入 ContentionList 时，等待的线程会先尝试自旋获取锁，如果获取不到就进入 ContentionList，这明显对于已经进入队列的线程是不公平的，还有一个不公平的事情就是自旋获取锁的线程还可能直接抢占 OnDeck 线程的锁资源。
    参考：[https://blog.csdn.net/zqz_zqz/article/details/70233767](https://blog.csdn.net/zqz_zqz/article/details/70233767)

7.  每个对象都有个 monitor 对象，加锁就是在竞争 monitor 对象，代码块加锁是在前后分别加上 monitorenter 和 monitorexit 指令来实现的，方法加锁是通过一个标记位来判断的

8.  synchronized 是一个重量级操作，需要调用操作系统相关接口，性能是低效的，有可能给线程加锁消耗的时间比有用操作消耗的时间更多。

9.  Java1.6，synchronized 进行了很多的优化，有适应自旋、锁消除、锁粗化、轻量级锁及偏向锁等，效率有了本质上的提高。在之后推出的 Java1.7 与 1.8 中，均对该关键字的实现机理做了优化。引入了偏向锁和轻量级锁。都是在对象头中有标记位，不需要经过操作系统加锁。

10.  锁可以从偏向锁升级到轻量级锁，再升级到重量级锁。这种升级过程叫做锁膨胀；

11.  JDK 1.6 中默认是开启偏向锁和轻量级锁，可以通过-XX:-UseBiasedLocking 来禁用偏向锁。


# 86.ReentrantLock

> 原文：[https://zwmst.com/3078.html](https://zwmst.com/3078.html)

ReentantLock 继承接口 Lock 并实现了接口中定义的方法，他是一种可重入锁，除了能完成 synchronized 所能完成的所有工作外，还**提供了诸如可响应中断锁、可轮询锁请求、定时锁等避免多线程死锁的方法**。


# 87.Lock 接口的主要方法

> 原文：[https://zwmst.com/3080.html](https://zwmst.com/3080.html)

1.  void lock(): 执行此方法时, 如果锁处于空闲状态, 当前线程将获取到锁. 相反, 如果锁已经被其他线程持有, 将禁用当前线程, 直到当前线程获取到锁.
2.  boolean tryLock()：如果锁可用, 则获取锁, 并立即返回 true, 否则返回 false. 该方法和lock()的区别在于, tryLock()只是"试图"获取锁, 如果锁不可用, 不会导致当前线程被禁用, 当前线程仍然继续往下执行代码. 而 lock()方法则是一定要获取到锁, 如果锁不可用, 就一直等待, 在未获得锁之前,当前线程并不继续向下执行.
3.  void unlock()：执行此方法时, 当前线程将释放持有的锁. 锁只能由持有者释放, 如果线程并不持有锁, 却执行该方法, 可能导致异常的发生.
4.  Condition newCondition()：条件对象，获取等待通知组件。该组件和当前的锁绑定，当前线程只有获取了锁，才能调用该组件的 await()方法，而调用后，当前线程将缩放锁。
5.  getHoldCount() ：查询当前线程保持此锁的次数，也就是执行此线程执行 lock 方法的次数。
6.  getQueueLength（）：返回正等待获取此锁的线程估计数，比如启动 10 个线程，1 个线程获得锁，此时返回的是 9
7.  getWaitQueueLength：（Condition condition）返回等待与此锁相关的给定条件的线程估计数。比如 10 个线程，用同一个 condition 对象，并且此时这 10 个线程都执行了condition 对象的 await 方法，那么此时执行此方法返回 10
8.  hasWaiters(Condition condition)：查询是否有线程等待与此锁有关的给定条件(condition)，对于指定 contidion 对象，有多少线程执行了 condition.await 方法
9.  hasQueuedThread(Thread thread)：查询给定线程是否等待获取此锁
10.  hasQueuedThreads()：是否有线程等待此锁
11.  isFair()：该锁是否公平锁
12.  isHeldByCurrentThread()： 当前线程是否保持锁锁定，线程的执行 lock 方法的前后分别是 false 和 true
13.  isLock()：此锁是否有任意线程占用
14.  lockInterruptibly（）：如果当前线程未被中断，获取锁
15.  tryLock（）：尝试获得锁，仅在调用时锁未被线程占用，获得锁
16.  tryLock(long timeout TimeUnit unit)：如果锁在给定等待时间内没有被另一个线程保持，则获取该锁。


# 88.非公平锁

> 原文：[https://zwmst.com/3082.html](https://zwmst.com/3082.html)

JVM 按随机、就近原则分配锁的机制则称为不公平锁，ReentrantLock 在构造函数中提供了是否公平锁的初始化方式，默认为非公平锁。非公平锁实际执行的效率要远远超出公平锁，除非程序有特殊需要，否则最常用非公平锁的分配机制。


# 89.公平锁

> 原文：[https://zwmst.com/3084.html](https://zwmst.com/3084.html)

公平锁指的是锁的分配机制是公平的，通常先对锁提出获取请求的线程会先被分配到锁，ReentrantLock 在构造函数中提供了是否公平锁的初始化方式来定义公平锁。


# 90.ReentrantLock 与 synchronized

> 原文：[https://zwmst.com/3086.html](https://zwmst.com/3086.html)

1.  ReentrantLock 通过方法 lock()与 unlock()来进行加锁与解锁操作，与 **synchronized 会被 JVM 自动解锁机制不同，ReentrantLock 加锁后需要手动进行解锁**。为了避免程序出现异常而无法正常解锁的情况，使用 ReentrantLock 必须在 finally 控制块中进行解锁操作。
2.  ReentrantLock 相比 synchronized 的优势是可中断、公平锁、多个锁。这种情况下需要使用 ReentrantLock。


# 91.ReentrantLock 实现

> 原文：[https://zwmst.com/3089.html](https://zwmst.com/3089.html)

```
public class MyService {
 private Lock lock = new ReentrantLock();
//Lock lock=new ReentrantLock(true);//公平锁
 //Lock lock=new ReentrantLock(false);//非公平锁
 private Condition condition=lock.newCondition();//创建 Condition
 public void testMethod() {
 try {
 lock.lock();//lock 加锁
//1：wait 方法等待：
 //System.out.println("开始 wait");
 condition.await();
//通过创建 Condition 对象来使线程 wait，必须先执行 lock.lock 方法获得锁
//:2：signal 方法唤醒
condition.signal();//condition 对象的 signal 方法可以唤醒 wait 线程
 for (int i = 0; i < 5; i++) {
System.out.println("ThreadName=" + Thread.currentThread().getName()+ (" " + (i + 1)));
 }
 } catch (InterruptedException e) {
 e.printStackTrace();
 }
 finally
 {
 lock.unlock();
 }
 }
}
```


# 92.Condition 类和 Object 类锁方法区别区别

> 原文：[https://zwmst.com/3091.html](https://zwmst.com/3091.html)

1.  Condition 类的 awiat 方法和 Object 类的 wait 方法等效
2.  Condition 类的 signal 方法和 Object 类的 notify 方法等效
3.  Condition 类的 signalAll 方法和 Object 类的 notifyAll 方法等效
4.  ReentrantLock 类可以唤醒指定条件的线程，而 object 的唤醒是随机的


# 93.tryLock 和 lock 和 lockInterruptibly 的区别

> 原文：[https://zwmst.com/3093.html](https://zwmst.com/3093.html)

1.  tryLock 能获得锁就返回 true，不能就立即返回 false，tryLock(long timeout,TimeUnit unit)，可以增加时间限制，如果超过该时间段还没获得锁，返回 false
2.  lock 能获得锁就返回 true，不能的话一直等待获得锁
3.  lock 和 lockInterruptibly，如果两个线程分别执行这两个方法，但此时**中断这两个线程，lock 不会抛出异常，而 lockInterruptibly 会抛出异常**。


# 94.Semaphore 信号

> 原文：[https://zwmst.com/3095.html](https://zwmst.com/3095.html)

Semaphore 是一种基于计数的信号量。它可以设定一个阈值，基于此，多个线程竞争获取许可信号，做完自己的申请后归还，超过阈值后，线程申请许可信号将会被阻塞。Semaphore 可以用来构建一些对象池，资源池之类的，比如数据库连接池


# 95.实现互斥锁（计数器为 1）

> 原文：[https://zwmst.com/3097.html](https://zwmst.com/3097.html)

我们也可以创建计数为 1 的 Semaphore，将其作为一种类似互斥锁的机制，这也叫二元信号量，表示两种互斥状态。

### 代码实现

它的用法如下：

```
// 创建一个计数阈值为 5 的信号量对象
// 只能 5 个线程同时访问
Semaphore semp = new Semaphore(5);
try { // 申请许可
semp.acquire();
try {
// 业务逻辑
} catch (Exception e) {
} finally {
// 释放许可
semp.release();
}
} catch (InterruptedException e) {
}
```


# 96.Semaphore 与 ReentrantLock

> 原文：[https://zwmst.com/3099.html](https://zwmst.com/3099.html)

Semaphore 基本能完成 ReentrantLock 的所有工作，使用方法也与之类似，通过 acquire()与release()方法来获得和释放临界资源。经实测，Semaphone.acquire()方法默认为可响应中断锁，与 ReentrantLock.lockInterruptibly()作用效果一致，也就是说在等待临界资源的过程中可以被Thread.interrupt()方法中断。

此外，Semaphore 也实现了可轮询的锁请求与定时锁的功能，除了方法名 tryAcquire 与 tryLock不同，其使用方法与 ReentrantLock 几乎一致。Semaphore 也提供了公平与非公平锁的机制，也可在构造函数中进行设定。

Semaphore 的锁释放操作也由手动进行，因此与 ReentrantLock 一样，为避免线程因抛出异常而无法正常释放锁的情况发生，释放锁的操作也必须在 finally 代码块中完成。


# 97.AtomicInteger

> 原文：[https://zwmst.com/3101.html](https://zwmst.com/3101.html)

首先说明，此处 AtomicInteger ，一个提供原子操作的 Integer 的类，常见的还有AtomicBoolean、AtomicInteger、AtomicLong、AtomicReference 等，他们的实现原理相同，区别在与运算对象类型的不同。令人兴奋地，还可以通过`AtomicReference<V>`将一个对象的所有操作转化成原子操作。

我们知道，**在多线程程序中，诸如++i 或 i++等运算不具有原子性，是不安全的线程操作之一**。通常我们会使用 synchronized 将该操作变成一个原子操作，但 JVM 为此类操作特意提供了一些同步类，使得使用更方便，且使程序运行效率变得更高。通过相关资料显示，通常AtomicInteger的性能是 ReentantLock 的好几倍。


# 98.可重入锁（递归锁）

> 原文：[https://zwmst.com/3104.html](https://zwmst.com/3104.html)

本文里面讲的是广义上的可重入锁，而不是单指 JAVA 下的 ReentrantLock。**可重入锁，也叫做递归锁，指的是同一线程 外层函数获得锁之后 ，内层递归函数仍然有获取该锁的代码，但不受影响**。在 JAVA 环境下 ReentrantLock 和 synchronized 都是 可重入锁。


# 99.公平锁（Fair）

> 原文：[https://zwmst.com/3106.html](https://zwmst.com/3106.html)

加锁前检查是否有排队等待的线程，优先排队等待的线程，先来先得


# 100.非公平锁（Nonfair）

> 原文：[https://zwmst.com/3108.html](https://zwmst.com/3108.html)

加锁时不考虑排队等待问题，直接尝试获取锁，获取不到自动到队尾等待

1.  非公平锁性能比公平锁高 5~10 倍，因为公平锁需要在多核的情况下维护一个队列
2.  Java 中的 synchronized 是非公平锁，ReentrantLock 默认的 lock()方法采用的是非公平锁。


# 101.ReadWriteLock 读写锁

> 原文：[https://zwmst.com/3110.html](https://zwmst.com/3110.html)

**为了提高性能，Java 提供了读写锁，在读的地方使用读锁，在写的地方使用写锁，灵活控制**，如果没有写锁的情况下，读是无阻塞的,在一定程度上提高了程序的执行效率。读写锁分为读锁和写锁，多个读锁不互斥，读锁与写锁互斥，这是由 jvm 自己控制的，你只要上好相应的锁即可。

### 读锁

如果你的代码只读数据，可以很多人同时读，但不能同时写，那就上读锁

### 写锁

如果你的代码修改数据，只能有一个人在写，且不能同时读取，那就上写锁。总之，读的时候上读锁，写的时候上写锁！

Java 中 读 写 锁 有 个 接 口java.util.concurrent.locks.ReadWriteLock ， 也 有 具 体 的 实 现ReentrantReadWriteLock。


# 102.共享锁和独占锁

> 原文：[https://zwmst.com/3112.html](https://zwmst.com/3112.html)

java 并发包提供的加锁模式分为独占锁和共享锁。

### 独占锁

独占锁模式下，每次只能有一个线程能持有锁，ReentrantLock 就是以独占方式实现的互斥锁。独占锁是一种悲观保守的加锁策略，它避免了读/读冲突，如果某个只读线程获取锁，则其他读线程都只能等待，这种情况下就限制了不必要的并发性，因为读操作并不会影响数据的一致性。

### 共享锁

共享锁则允许多个线程同时获取锁，并发访问 共享资源，如：ReadWriteLock。共享锁则是一种乐观锁，它放宽了加锁策略，允许多个执行读操作的线程同时访问共享资源。

1.  AQS 的内部类 Node 定义了两个常量 SHARED 和 EXCLUSIVE，他们分别标识 AQS 队列中等待线程的锁获取模式。
2.  java 的并发包中提供了 ReadWriteLock，读-写锁。它允许一个资源可以被多个读操作访问，或者被一个 写操作访问，但两者不能同时进行


# 103.重量级锁（Mutex Lock）

> 原文：[https://zwmst.com/3114.html](https://zwmst.com/3114.html)

Synchronized 是通过对象内部的一个叫做监视器锁（monitor）来实现的。但是监视器锁本质又是依赖于底层的操作系统的 Mutex Lock 来实现的。而操作系统实现线程之间的切换这就需要从用户态转换到核心态，这个成本非常高，状态之间的转换需要相对比较长的时间，这就是为什么Synchronized 效率低的原因。因此，**这种依赖于操作系统 Mutex Lock 所实现的锁我们称之为“重量级锁”**。JDK 中对 Synchronized 做的种种优化，其核心都是为了减少这种重量级锁的使用。JDK1.6 以后，为了减少获得锁和释放锁所带来的性能消耗，提高性能，引入了“轻量级锁”和“偏向锁”。


# 104.轻量级锁

> 原文：[https://zwmst.com/3116.html](https://zwmst.com/3116.html)

锁的状态总共有四种：无锁状态、偏向锁、轻量级锁和重量级锁。

### 锁升级

随着锁的竞争，锁可以从偏向锁升级到轻量级锁，再升级的重量级锁（但是锁的升级是单向的，也就是说只能从低到高升级，不会出现锁的降级）。

“轻量级”是相对于使用操作系统互斥量来实现的传统锁而言的。但是，首先需要强调一点的是，轻量级锁并不是用来代替重量级锁的，它的本意是在没有多线程竞争的前提下，减少传统的重量
级锁使用产生的性能消耗。在解释轻量级锁的执行过程之前，先明白一点，**轻量级锁所适应的场景是线程交替执行同步块的情况，如果存在同一时间访问同一锁的情况，就会导致轻量级锁膨胀为重量级锁**。


# 105.偏向锁

> 原文：[https://zwmst.com/3118.html](https://zwmst.com/3118.html)

Hotspot 的作者经过以往的研究发现大多数情况下锁不仅不存在多线程竞争，而且总是由同一线程多次获得。**偏向锁的目的是在某个线程获得锁之后，消除这个线程锁重入（CAS）的开销，看起来让这个线程得到了偏护**。引入偏向锁是为了在无多线程竞争的情况下尽量减少不必要的轻量级锁执行路径，因为轻量级锁的获取及释放依赖多次 CAS 原子指令，**而偏向锁只需要在置换ThreadID 的时候依赖一次 CAS 原子指令**（由于一旦出现多线程竞争的情况就必须撤销偏向锁，所以偏向锁的撤销操作的性能损耗必须小于节省下来的 CAS 原子指令的性能消耗）。上面说过，**轻量级锁是为了在线程交替执行同步块时提高性能，而偏向锁则是在只有一个线程执行同步块时进一步提高性能**。


# 106.分段锁

> 原文：[https://zwmst.com/3120.html](https://zwmst.com/3120.html)

分段锁也并非一种实际的锁，而是一种思想 ConcurrentHashMap 是学习分段锁的最好实践


# 107.锁优化

> 原文：[https://zwmst.com/3122.html](https://zwmst.com/3122.html)

### 减少锁持有时间

只用在有线程安全要求的程序上加锁

### 减小锁粒度

将大对象（这个对象可能会被很多线程访问），拆成小对象，大大增加并行度，降低锁竞争。降低了锁的竞争，偏向锁，轻量级锁成功率才会提高。最最典型的减小锁粒度的案例就是ConcurrentHashMap。

### 锁分离

**最常见的锁分离就是读写锁 ReadWriteLock**，根据功能进行分离成读锁和写锁，这样读读不互斥，读写互斥，写写互斥，即保证了线程安全，又提高了性能，具体也请查看[高并发 Java 五] JDK 并发包 1。读写分离思想可以延伸，只要操作互不影响，锁就可以分离。比如LinkedBlockingQueue 从头部取出，从尾部放数据

### 锁粗化

通常情况下，为了保证多线程间的有效并发，会要求每个线程持有锁的时间尽量短，即在使用完公共资源后，应该立即释放锁。但是，凡事都有一个度，**如果对同一个锁不停的进行请求、同步和释放，其本身也会消耗系统宝贵的资源，反而不利于性能的优化** 。

### 锁消除

锁消除是在编译器级别的事情。在即时编译器时，如果发现不可能被共享的对象，则可以消除这些对象的锁操作，多数是因为程序员编码不规范引起。

参考：[https://www.jianshu.com/p/39628e1180a9](https://www.jianshu.com/p/39628e1180a9)


# 108.线程基本方法

> 原文：[https://zwmst.com/3124.html](https://zwmst.com/3124.html)

线程相关的基本方法有 wait，notify，notifyAll，sleep，join，yield 等。


# 109.线程等待（wait）

> 原文：[https://zwmst.com/3126.html](https://zwmst.com/3126.html)

调用该方法的线程进入 WAITING 状态，只有等待另外线程的通知或被中断才会返回，需要注意的是调用 wait()方法后，**会释放对象的锁**。因此，wait 方法一般用在同步方法或同步代码块中。


# 110.线程睡眠（sleep）

> 原文：[https://zwmst.com/3128.html](https://zwmst.com/3128.html)

sleep 导致当前线程休眠，与 wait 方法不同的是 **sleep 不会释放当前占有的锁**,sleep(long)会导致线程进入 `TIMED-WATING 状态`，而 `wait()方法会导致当前线程进入 WATING` 状态


# 111.线程让步（yield）

> 原文：[https://zwmst.com/3130.html](https://zwmst.com/3130.html)

yield 会使当前线程让出 **CPU 执行时间片**，与其他线程一起重新竞争 CPU 时间片。一般情况下，优先级高的线程有更大的可能性成功竞争得到 CPU 时间片，但这又不是绝对的，有的操作系统对线程优先级并不敏感。


# 112.线程中断（interrupt）

> 原文：[https://zwmst.com/3133.html](https://zwmst.com/3133.html)

中断一个线程，其本意是**给这个线程一个通知信号，会影响这个线程内部的一个中断标识位。这个线程本身并不会因此而改变状态(如阻塞，终止等)**。

1.  **调用 interrupt()方法并不会中断一个正在运行的线程**。也就是说处于 Running 状态的线程并不会因为被中断而被终止，仅仅改变了内部维护的中断标识位而已。
2.  若调用 sleep()而使线程处于 TIMED-WATING 状态，这时调用 interrupt()方法，会抛出InterruptedException,从而使线程提前结束 TIMED-WATING 状态。
3.  许多声明抛出 InterruptedException 的方法(如 Thread.sleep(long mills 方法))，抛出异常前，都会清除中断标识位，所以抛出异常后，调用 isInterrupted()方法将会返回 false。
4.  中断状态是线程固有的一个标识位，可以通过此标识位安全的终止线程。比如,你想终止一个线程 thread 的时候，可以调用 thread.interrupt()方法，在线程的 run 方法内部可以根据 **thread.isInterrupted()的值来优雅的终止线程**。


# 113.Join 等待其他线程终止

> 原文：[https://zwmst.com/3135.html](https://zwmst.com/3135.html)

**join() 方法，等待其他线程终止**，在当前线程中调用一个线程的 join() 方法，则当前线程转为阻塞状态，回到另一个线程结束，当前线程再由阻塞状态变为就绪状态，等待 cpu 的宠幸。


# 114.为什么要用 join()方法？

> 原文：[https://zwmst.com/3137.html](https://zwmst.com/3137.html)

很多情况下，主线程生成并启动了子线程，需要用到子线程返回的结果，也就是需要主线程需要在子线程结束后再结束，这时候就要用到 join() 方法。

```
System.out.println(Thread.currentThread().getName() + "线程运行开始!");
 Thread6 thread1 = new Thread6();
 thread1.setName("线程 B");
 thread1.join();
System.out.println("这时 thread1 执行完毕之后才能执行主线程"); 
```


# 115.线程唤醒（notify）

> 原文：[https://zwmst.com/3139.html](https://zwmst.com/3139.html)

Object 类中的 notify() 方法，**唤醒在此对象监视器上等待的单个线程**，如果所有线程都在此对象上等待，则会选择唤醒其中一个线程，选择是任意的，并在对实现做出决定时发生，线程通过调用其中一个 wait() 方法，在对象的监视器上等待，**直到当前的线程放弃此对象上的锁定，才能继续执行被唤醒的线程**，被唤醒的线程将以常规方式与在该对象上主动同步的其他所有线程进行竞争。类似的方法还有 notifyAll() ，唤醒再次监视器上等待的所有线程。


# 116.其他方法

> 原文：[https://zwmst.com/3143.html](https://zwmst.com/3143.html)

1.  sleep()：强迫一个线程睡眠Ｎ毫秒。
2.  isAlive()： 判断一个线程是否存活。
3.  join()： 等待线程终止。
4.  activeCount()： 程序中活跃的线程数。
5.  enumerate()： 枚举程序中的线程。
6.  currentThread()： 得到当前线程。
7.  isDaemon()： 一个线程是否为守护线程。
8.  setDaemon()： 设置一个线程为守护线程。(用户线程和守护线程的区别在于，是否等待主线程依赖于主线程结束而结束)
9.  setName()： 为线程设置一个名称。
10.  wait()： 强迫一个线程等待。
11.  notify()： 通知一个线程继续运行。
12.  setPriority()： 设置一个线程的优先级。
13.  getPriority():：获得一个线程的优先级。


# 117.线程上下文切换

> 原文：[https://zwmst.com/3147.html](https://zwmst.com/3147.html)

巧妙地利用了时间片轮转的方式, CPU 给每个任务都服务一定的时间，然后把当前任务的状态保存下来，在加载下一任务的状态后，继续服务下一任务，**任务的状态保存及再加载, 这段过程就叫做上下文切换**。时间片轮转的方式使多个任务在同一颗 CPU 上执行变成了可能。


# 118.进程

> 原文：[https://zwmst.com/3149.html](https://zwmst.com/3149.html)

（有时候也称做任务）是指一个程序运行的实例。在 Linux 系统中，线程就是能并行运行并且与他们的父进程（创建他们的进程）共享同一地址空间（一段内存区域）和其他资源的轻量级的进程。


# 119.上下文

> 原文：[https://zwmst.com/3151.html](https://zwmst.com/3151.html)

是指某一时间点 **CPU 寄存器和程序计数器**的`内容`。


# 120.寄存器

> 原文：[https://zwmst.com/3153.html](https://zwmst.com/3153.html)

是 CPU 内部的数量较少但是速度很快的内存（与之对应的是 CPU 外部相对较慢的 RAM 主内存）。寄存器通过对常用值（通常是运算的中间值）的快速访问来提高计算机程序运行的速度。


# 121.程序计数器

> 原文：[https://zwmst.com/3155.html](https://zwmst.com/3155.html)

是一个专用的寄存器，**用于表明指令序列中 CPU 正在执行的位置**，存的值为正在执行的指令的位置或者下一个将要被执行的指令的位置，具体依赖于特定的系统。


# 122.PCB-“切换桢”

> 原文：[https://zwmst.com/3158.html](https://zwmst.com/3158.html)

上下文切换可以认为是内核（操作系统的核心）在 CPU 上对于进程（包括线程）进行切换，上下文切换过程中的信息是保存在进程控制块（PCB, process control block）中的。PCB 还经常被称作“切换桢”（switchframe）。信息会一直保存到 CPU 的内存中，直到他们被再次使用。


# 123.上下文切换的活动

> 原文：[https://zwmst.com/3160.html](https://zwmst.com/3160.html)

1.  挂起一个进程，将这个进程在 CPU 中的状态（上下文）存储于内存中的某处。
2.  在内存中检索下一个进程的上下文并将其在 CPU 的寄存器中恢复。
3.  跳转到程序计数器所指向的位置（即跳转到进程被中断时的代码行），以恢复该进程在程序中。


# 124.引起线程上下文切换的原因

> 原文：[https://zwmst.com/3163.html](https://zwmst.com/3163.html)

1.  当前执行任务的时间片用完之后，系统 CPU 正常调度下一个任务；
2.  当前执行任务碰到 IO 阻塞，调度器将此任务挂起，继续下一任务；
3.  多个任务抢占锁资源，当前任务没有抢到锁资源，被调度器挂起，继续下一任务；
4.  用户代码挂起当前任务，让出 CPU 时间；
5.  硬件中断；


# 125.同步锁

> 原文：[https://zwmst.com/3165.html](https://zwmst.com/3165.html)

当多个线程同时访问同一个数据时，很容易出现问题。为了避免这种情况出现，我们要**保证线程同步互斥，就是指并发执行的多个线程，在同一时间内只允许一个线程访问共享数据**。 Java 中可以使用 synchronized 关键字来取得一个对象的同步锁。


# 126.死锁

> 原文：[https://zwmst.com/3167.html](https://zwmst.com/3167.html)

何为死锁，就是多个线程同时被阻塞，它们中的一个或者全部都在等待某个资源被释放。


# 127.线程池原理

> 原文：[https://zwmst.com/3169.html](https://zwmst.com/3169.html)

线程池做的工作主要是控制运行的线程的数量，处理过程中将任务放入队列，然后在线程创建后启动这些任务，如果线程数量超过了最大数量**超出数量的线程排队等候**，等其它线程执行完毕，再从队列中取出任务来执行。他的主要特点为：**线程复用；控制最大并发数；管理线程**。


# 128.线程复用

> 原文：[https://zwmst.com/3171.html](https://zwmst.com/3171.html)

每一个 Thread 的类都有一个 start 方法。 当调用 start 启动线程时 Java 虚拟机会调用该类的 run 方法。 那么该类的 run() 方法中就是调用了 Runnable 对象的 run() 方法。 **我们可以继承重写Thread 类，在其 start 方法中添加不断循环调用传递过来的 Runnable 对象**。 这就是线程池的实现原理。**循环方法中不断获取 Runnable 是用 Queue 实现的**，在获取下一个 Runnable 之前可以是阻塞的。


# 129.线程池的组成

> 原文：[https://zwmst.com/3173.html](https://zwmst.com/3173.html)

一般的线程池主要分为以下 4 个组成部分：

1.  线程池管理器：用于创建并管理线程池
2.  工作线程：线程池中的线程
3.  任务接口：每个任务必须实现的接口，用于工作线程调度其运行
4.  任务队列：用于存放待处理的任务，提供一种缓冲机制

Java 中的线程池是通过 Executor 框架实现的，该框架中用到了 Executor，Executors，ExecutorService，ThreadPoolExecutor ，Callable 和 Future、FutureTask 这几个类。

ThreadPoolExecutor 的构造方法如下：

```
public ThreadPoolExecutor(int corePoolSize,int maximumPoolSize, long keepAliveTime,
TimeUnit unit, BlockingQueue<Runnable> workQueue) {
this(corePoolSize, maximumPoolSize, keepAliveTime, unit, workQueue,
Executors.defaultThreadFactory(), defaultHandler);
}
```

1.  corePoolSize：指定了线程池中的线程数量。
2.  maximumPoolSize：指定了线程池中的最大线程数量。
3.  keepAliveTime：当前线程池数量超过 corePoolSize 时，多余的空闲线程的存活时间，即多次时间内会被销毁。
4.  unit：keepAliveTime 的单位。
5.  workQueue：任务队列，被提交但尚未被执行的任务。
6.  threadFactory：线程工厂，用于创建线程，一般用默认的即可。
7.  handler：拒绝策略，当任务太多来不及处理，如何拒绝任务。


# 130.拒绝策略

> 原文：[https://zwmst.com/3177.html](https://zwmst.com/3177.html)

线程池中的线程已经用完了，无法继续为新任务服务，同时，等待队列也已经排满了，再也塞不下新任务了。这时候我们就需要拒绝策略机制合理的处理这个问题。
JDK 内置的拒绝策略如下：

1.  AbortPolicy ： 直接抛出异常，阻止系统正常运行。
2.  CallerRunsPolicy ： 只要线程池未关闭，该策略直接在调用者线程中，运行当前被丢弃的任务。显然这样做不会真的丢弃任务，但是，任务提交线程的性能极有可能会急剧下降。
3.  DiscardOldestPolicy ： 丢弃最老的一个请求，也就是即将被执行的一个任务，并尝试再次提交当前任务。
4.  DiscardPolicy ： 该策略默默地丢弃无法处理的任务，不予任何处理。如果允许任务丢失，这是最好的一种方案。

以上内置拒绝策略均实现了 **RejectedExecutionHandler** 接口，若以上策略仍无法满足实际
需要，完全可以自己扩展 RejectedExecutionHandler 接口。


# 131.Java 线程池工作过程

> 原文：[https://zwmst.com/3179.html](https://zwmst.com/3179.html)

1.  线程池刚创建时，里面没有一个线程。任务队列是作为参数传进来的。不过，就算队列里面有任务，线程池也不会马上执行它们。
2.  当调用 execute() 方法添加一个任务时，线程池会做如下判断：
    1.  如果正在运行的线程数量小于 corePoolSize，那么马上创建线程运行这个任务；
    2.  如果正在运行的线程数量大于或等于 corePoolSize，那么将这个任务放入队列；
    3.  如果这时候队列满了，而且正在运行的线程数量小于 maximumPoolSize，那么还是要创建非核心线程立刻运行这个任务；
    4.  如果队列满了，而且正在运行的线程数量大于或等于 maximumPoolSize，那么线程池会抛出异常 RejectExecutionException。
3.  当一个线程完成任务时，它会从队列中取下一个任务来执行。
4.  当一个线程无事可做，超过一定的时间（keepAliveTime）时，线程池会判断，如果当前运行的线程数大于 corePoolSize，那么这个线程就被停掉。所以线程池的所有任务完成后，它最终会收缩到 corePoolSize 的大小。


# 132.JAVA 阻塞队列原理

> 原文：[https://zwmst.com/3181.html](https://zwmst.com/3181.html)

阻塞队列，关键字是阻塞，先理解阻塞的含义，在阻塞队列中，线程阻塞有这样的两种情况：

1.  当队列中没有数据的情况下，消费者端的所有线程都会被自动阻塞（挂起），直到有数据放入队列。
2.  当队列中填满数据的情况下，生产者端的所有线程都会被自动阻塞（挂起），直到队列中有空的位置，线程被自动唤醒。


# 133.阻塞队列的主要方法

> 原文：[https://zwmst.com/3183.html](https://zwmst.com/3183.html)

![](img/0ae0b51896f32b4312cfa288c98009df.png)
— 抛出异常：抛出一个异常；
— 特殊值：返回一个特殊值（null 或 false,视情况而定）
— 则塞：在成功操作之前，一直阻塞线程
— 超时：放弃前只在最大的时间内阻塞


# 134.插入操作

> 原文：[https://zwmst.com/3186.html](https://zwmst.com/3186.html)

1.  public abstract boolean add(E paramE)：将指定元素插入此队列中（如果立即可行且不会违反容量限制），成功时返回 true，如果当前没有可用的空间，则抛出 IllegalStateException。如果该元素是 NULL，则会抛出 NullPointerException 异常。

2.  public abstract boolean offer(E paramE)：将指定元素插入此队列中（如果立即可行且不会违反容量限制），成功时返回 true，如果当前没有可用的空间，则返回 false。

3.  public abstract void put(E paramE) throws InterruptedException： 将指定元素插入此队列中，将等待可用的空间（如果有必要）

    ```
    public void put(E paramE) throws InterruptedException {
    checkNotNull(paramE);
    ReentrantLock localReentrantLock = this.lock;
    localReentrantLock.lockInterruptibly();
    try {
    while (this.count == this.items.length)
    this.notFull.await();//如果队列满了，则线程阻塞等待
    enqueue(paramE);
    localReentrantLock.unlock();
    } finally {
    localReentrantLock.unlock();
    }
    }
    ```

4.  offer(E o, long timeout, TimeUnit unit)：可以设定等待的时间，如果在指定的时间内，还不能往队列中加入 BlockingQueue，则返回失败。


# 135.获取数据操作

> 原文：[https://zwmst.com/3188.html](https://zwmst.com/3188.html)

1.  poll(time):取走 BlockingQueue 里排在首位的对象,若不能立即取出,则可以等 time 参数规定的时间,取不到时返回 null;
2.  poll(long timeout, TimeUnit unit)：从 BlockingQueue 取出一个队首的对象，如果在指定时间内，队列一旦有数据可取，则立即返回队列中的数据。否则直到时间超时还没有数据可取，返回失败。
3.  take():取走 BlockingQueue 里排在首位的对象,若 BlockingQueue 为空,阻断进入等待状态直到 BlockingQueue 有新的数据被加入。
4.  drainTo():一次性从 BlockingQueue 获取所有可用的数据对象（还可以指定获取数据的个数），通过该方法，可以提升获取数据效率；不需要多次分批加锁或释放锁。


# 136.Java 中的阻塞队列

> 原文：[https://zwmst.com/3190.html](https://zwmst.com/3190.html)

1.  ArrayBlockingQueue ：由数组结构组成的有界阻塞队列。
2.  LinkedBlockingQueue ：由链表结构组成的有界阻塞队列。
3.  PriorityBlockingQueue ：支持优先级排序的无界阻塞队列。
4.  DelayQueue：使用优先级队列实现的无界阻塞队列。
5.  SynchronousQueue：不存储元素的阻塞队列。
6.  LinkedTransferQueue：由链表结构组成的无界阻塞队列。
7.  LinkedBlockingDeque：由链表结构组成的双向阻塞队列


# 137.ArrayBlockingQueue（公平、非公平）

> 原文：[https://zwmst.com/3192.html](https://zwmst.com/3192.html)

用数组实现的有界阻塞队列。此队列按照先进先出（FIFO）的原则对元素进行排序。**默认情况下不保证访问者公平的访问队列**，所谓公平访问队列是指阻塞的所有生产者线程或消费者线程，当队列可用时，可以按照阻塞的先后顺序访问队列，即先阻塞的生产者线程，可以先往队列里插入元素，先阻塞的消费者线程，可以先从队列里获取元素。通常情况下为了保证公平性会降低吞吐量。我们可以使用以下代码**创建一个公平的阻塞队列**：

```
ArrayBlockingQueue fairQueue = new ArrayBlockingQueue(1000,true);
```


# 138.LinkedBlockingQueue（两个独立锁提高并发）

> 原文：[https://zwmst.com/3195.html](https://zwmst.com/3195.html)

基于链表的阻塞队列，同 ArrayListBlockingQueue 类似，此队列按照先进先出（FIFO）的原则对元素进行排序。而 LinkedBlockingQueue 之所以能够高效的**处理并发数据**，还因为其**对于生产者端和消费者端分别采用了独立的锁来控制数据同步**，这也意味着在高并发的情况下生产者和消费者可以并行地操作队列中的数据，以此来提高整个队列的并发性能。

LinkedBlockingQueue 会默认一个类似无限大小的容量（Integer.MAX_VALUE）。


# 139.PriorityBlockingQueue（compareTo 排序实现优先）

> 原文：[https://zwmst.com/3197.html](https://zwmst.com/3197.html)

是一个支持优先级的无界队列。默认情况下元素采取自然顺序升序排列。**可以自定义实现compareTo()**方法来指定元素进行排序规则，或者初始化 PriorityBlockingQueue 时，指定构造参数 Comparator 来对元素进行排序。需要注意的是不能保证同优先级元素的顺序。


# 140.DelayQueue（缓存失效、定时任务 ）

> 原文：[https://zwmst.com/3199.html](https://zwmst.com/3199.html)

是一个支持延时获取元素的无界阻塞队列。队列使用 PriorityQueue 来实现。队列中的元素必须实现 Delayed 接口，在创建元素时可以指定多久才能从队列中获取当前元素。只有在延迟期满时才能从队列中提取元素。我们可以将 DelayQueue 运用在以下应用场景：

1.  缓存系统的设计：可以用 DelayQueue 保存缓存元素的有效期，使用一个线程循环查询DelayQueue，一旦能从 DelayQueue 中获取元素时，表示缓存有效期到了。

2.  定时任务调度：使用 DelayQueue 保存当天将会执行的任务和执行时间，一旦从DelayQueue 中获取到任务就开始执行，从比如 TimerQueue 就是使用 DelayQueue 实现的。


# 141.SynchronousQueue（不存储数据、可用于传递数据）

> 原文：[https://zwmst.com/3201.html](https://zwmst.com/3201.html)

**是一个不存储元素的阻塞队列。每一个 put 操作必须等待一个 take 操作，否则不能继续添加元素**。

SynchronousQueue 可以看成是一个传球手，负责把生产者线程处理的数据直接传递给消费者线程。队列本身并不存储任何元素，非常适合于传递性场景,比如在一个线程中使用的数据，传递给另 外 一 个 线 程 使 用 ， SynchronousQueue 的 吞 吐 量 高 于 LinkedBlockingQueue 和ArrayBlockingQueue。


# 142.LinkedTransferQueue

> 原文：[https://zwmst.com/3203.html](https://zwmst.com/3203.html)

是 一 个 由 链 表 结 构 组 成 的 无 界 阻 塞 TransferQueue 队 列 。 相 对 于 其 他 阻 塞 队 列 ，LinkedTransferQueue 多了 tryTransfer 和 transfer 方法。

1.  transfer 方法：如果当前有消费者正在等待接收元素（消费者使用 take()方法或带时间限制的poll()方法时），transfer 方法可以把生产者传入的元素立刻 transfer（传输）给消费者。如果没有消费者在等待接收元素，transfer 方法会将元素存放在队列的 tail 节点，并等到该元素被消费者消费了才返回。
2.  tryTransfer 方法。则是用来试探下生产者传入的元素是否能直接传给消费者。如果没有消费者等待接收元素，则返回 false。和 transfer 方法的区别是 tryTransfer 方法无论消费者是否接收，方法立即返回。而 transfer 方法是必须等到消费者消费了才返回。

对于带有时间限制的 tryTransfer(E e, long timeout, TimeUnit unit)方法，则是试图把生产者传入的元素直接传给消费者，但是如果没有消费者消费该元素则等待指定的时间再返回，如果超时还没消费元素，则返回 false，如果在超时时间内消费了元素，则返回 true。


# 143.LinkedBlockingDequ

> 原文：[https://zwmst.com/3205.html](https://zwmst.com/3205.html)

是一个由链表结构组成的**双向阻塞队列**。所谓双向队列指的**你可以从队列的两端插入和移出元素**。

双端队列因为多了一个操作队列的入口，在多线程同时入队时，也就减少了一半的竞争。相比其他的阻塞队列，LinkedBlockingDeque 多了 addFirst，addLast，offerFirst，offerLast，peekFirst，peekLast 等方法，以 First 单词结尾的方法，表示插入，获取（peek）或移除双端队列的第一个元素。以 Last 单词结尾的方法，表示插入，获取或移除双端队列的最后一个元素。另外插入方法 add 等同于 addLast，移除方法 remove 等效于 removeFirst。但是 take 方法却等同于 takeFirst，不知道是不是 Jdk 的 bug，使用时还是用带有 First 和 Last 后缀的方法更清楚。

在初始化 LinkedBlockingDeque 时可以设置容量防止其过渡膨胀。另外双向阻塞队列可以运用在“工作窃取”模式中。


# 144.CountDownLatch（线程计数器 ）

> 原文：[https://zwmst.com/3207.html](https://zwmst.com/3207.html)

CountDownLatch 类位于 java.util.concurrent 包下，利用它可以实现类似计数器的功能。比如有一个任务 A，它要等待其他 4 个任务执行完毕之后才能执行，此时就可以利用 CountDownLatch来实现这种功能了。

```
final CountDownLatch latch = new CountDownLatch(2);
new Thread(){public void run() {
System.out.println("子线程"+Thread.currentThread().getName()+"正在执行");
 Thread.sleep(3000);
 System.out.println("子线程"+Thread.currentThread().getName()+"执行完毕");
 latch.countDown();
};}.start();
new Thread(){ public void run() {
System.out.println("子线程"+Thread.currentThread().getName()+"正在执行");
 Thread.sleep(3000);
 System.out.println("子线程"+Thread.currentThread().getName()+"执行完毕");
 latch.countDown();
};}.start();
System.out.println("等待 2 个子线程执行完毕...");
latch.await();
System.out.println("2 个子线程已经执行完毕");
System.out.println("继续执行主线程");
}
```


# 145.CyclicBarrier（回环栅栏-等待至 barrier 状态再全部同时执行）

> 原文：[https://zwmst.com/3210.html](https://zwmst.com/3210.html)

字面意思回环栅栏，通过它可以实现让一组线程等待至某个状态之后再全部同时执行。叫做回环是因为当所有等待线程都被释放以后，CyclicBarrier 可以被重用。我们暂且把这个状态就叫做barrier，当调用 await()方法之后，线程就处于 barrier 了。

CyclicBarrier 中最重要的方法就是 await 方法，它有 2 个重载版本：

1.  public int await()：用来挂起当前线程，直至所有线程都到达 barrier 状态再同时执行后续任务；
2.  public int await(long timeout, TimeUnit unit)：让这些线程等待至一定的时间，如果还有线程没有到达 barrier 状态就直接让到达 barrier 的线程执行后续任务。

具体使用如下，另外 CyclicBarrier 是可以重用的。

```
 public static void main(String[] args) 
 int N = 4;
 CyclicBarrier barrier = new CyclicBarrier(N);
 for(int i=0;i
```


# 146.Semaphore（信号量-控制同时访问的线程个数）

> 原文：[https://zwmst.com/3212.html](https://zwmst.com/3212.html)

Semaphore 翻译成字面意思为 信号量，**Semaphore 可以控制同时访问的线程个数**，通过acquire() 获取一个许可，如果没有就等待，而 release() 释放一个许可。

Semaphore 类中比较重要的几个方法：

1.  public void acquire(): 用来获取一个许可，若无许可能够获得，则会一直等待，直到获得许可。
2.  public void acquire(int permits):获取 permits 个许可
3.  public void release() { } :释放许可。注意，在释放许可之前，必须先获获得许可。
4.  public void release(int permits) { }:释放 permits 个许可

上面 4 个方法都会被阻塞，如果想立即得到执行结果，可以使用下面几个方法

1.  public boolean tryAcquire():尝试获取一个许可，若获取成功，则立即返回 true，若获取失败，则立即返回 false
2.  public boolean tryAcquire(long timeout, TimeUnit unit):尝试获取一个许可，若在指定的时间内获取成功，则立即返回 true，否则则立即返回 false
3.  public boolean tryAcquire(int permits):尝试获取 permits 个许可，若获取成功，则立即返回 true，若获取失败，则立即返回 false
4.  public boolean tryAcquire(int permits, long timeout, TimeUnit unit): 尝试获取 permits个许可，若在指定的时间内获取成功，则立即返回 true，否则则立即返回 false
5.  还可以通过 availablePermits()方法得到可用的许可数目。

例子：若一个工厂有 5 台机器，但是有 8 个工人，一台机器同时只能被一个工人使用，只有使用完
了，其他工人才能继续使用。那么我们就可以通过 Semaphore 来实现：

```
int N = 8; //工人数
Semaphore semaphore = new Semaphore(5); //机器数目
for(int i=0;i<N;i++)
new Worker(i,semaphore).start();
}
static class Worker extends Thread{
private int num;
private Semaphore semaphore;
public Worker(int num,Semaphore semaphore){
this.num = num;
this.semaphore = semaphore;
}
@Override
public void run() {
try {
semaphore.acquire();
System.out.println("工人"+this.num+"占用一个机器在生产...");
Thread.sleep(2000);
System.out.println("工人"+this.num+"释放出机器");
semaphore.release();
} catch (InterruptedException e) {
e.printStackTrace();
}
}
```

1.  CountDownLatch 和 CyclicBarrier 都能够实现线程之间的等待，只不过它们侧重点不同；CountDownLatch 一般用于某个线程 A 等待若干个其他线程执行完任务之后，它才执行；而CyclicBarrier 一般用于一组线程互相等待至某个状态，然后这一组线程再同时执行；另外，CountDownLatch 是不能够重用的，而 CyclicBarrier 是可以重用的。
    2.Semaphore 其实和锁有点类似，它一般用于控制对某组资源的访问权限。


# 147.volatile 关键字的作用

> 原文：[https://zwmst.com/3214.html](https://zwmst.com/3214.html)

Java 语言提供了一种稍弱的同步机制，即 volatile 变量，用来确保将变量的更新操作通知到其他线程。volatile 变量具备两种特性，volatile 变量不会被缓存在寄存器或者对其他处理器不可见的地方，因此在读取 volatile 类型的变量时总会返回最新写入的值。


# 148.变量可见性

> 原文：[https://zwmst.com/3216.html](https://zwmst.com/3216.html)

其一是保证该变量对所有线程可见，这里的可见性指的是当一个线程修改了变量的值，那么新的值对于其他线程是可以立即获取的。


# 149.禁止重排序

> 原文：[https://zwmst.com/3218.html](https://zwmst.com/3218.html)

volatile 禁止了指令重排。


# 150.比 sychronized 更轻量级的同步锁

> 原文：[https://zwmst.com/3220.html](https://zwmst.com/3220.html)

在访问 volatile 变量时不会执行加锁操作，因此也就不会使执行线程阻塞，因此 volatile 变量是一种比 sychronized 关键字更轻量级的同步机制。volatile 适合这种场景：一个变量被多个线程共享，线程直接给这个变量赋值。

当对非 volatile 变量进行读写的时候，每个线程先从内存拷贝变量到 CPU 缓存中。如果计算机有多个 CPU，每个线程可能在不同的 CPU 上被处理，这意味着每个线程可以拷贝到不同的 CPU cache 中。而声明变量是 volatile 的，JVM 保证了每次读变量都从内存中读，跳过 CPU cache 这一步。


# 151.适用场景

> 原文：[https://zwmst.com/3222.html](https://zwmst.com/3222.html)

值得说明的是对 volatile 变量的单次读/写操作可以保证原子性的，如 long 和 double 类型变量，但是并不能保证 i++这种操作的原子性，因为本质上 i++是读、写两次操作。在某些场景下可以代替 Synchronized。但是,volatile 的不能完全取代 Synchronized 的位置，只有在一些特殊的场景下，才能适用 volatile。总的来说，必须同时满足下面两个条件才能保证在并发环境的线程安全：

1.  对变量的写操作不依赖于当前值（比如 i++），或者说是单纯的变量赋值（boolean flag = true）。
2.  该变量没有包含在具有其他变量的不变式中，也就是说，不同的 volatile 变量之间，不能互相依赖。只有在状态真正独立于程序内其他内容时才能使用 volatile。


# 152.如何在两个线程之间共享数据

> 原文：[https://zwmst.com/3224.html](https://zwmst.com/3224.html)

Java 里面进行多线程通信的主要方式就是共享内存的方式，共享内存主要的关注点有两个：可见性和有序性原子性。Java 内存模型（JMM）解决了可见性和有序性的问题，而锁解决了原子性的问题，理想情况下我们希望做到“同步”和“互斥”。有以下常规实现方法：

### 将数据抽象成一个类，并将数据的操作作为这个类的方法

1.  将数据抽象成一个类，并将对这个数据的操作作为这个类的方法，这么设计可以和容易做到同步，只要在方法上加”synchronized“

    ```
    public class MyData {
    private int j=0;
    public synchronized void add(){
    j++;
    System.out.println("线程"+Thread.currentThread().getName()+"j 为："+j);
    }
    public synchronized void dec(){
    j--;
    System.out.println("线程"+Thread.currentThread().getName()+"j 为："+j);
    }
    public int getData(){
    return j;
    }
    }
    public class AddRunnable implements Runnable{
    MyData data;
    public AddRunnable(MyData data){
    this.data= data;
    }
    public void run() {
    data.add();
    }
    }
    public class DecRunnable implements Runnable {
    MyData data;
    public DecRunnable(MyData data){
    this.data = data;
    }
    public void run() {
    data.dec();
    }
    }
    public static void main(String[] args) {
    MyData data = new MyData();
    Runnable add = new AddRunnable(data);
    Runnable dec = new DecRunnable(data);
    for(int i=0;i<2;i++){
    new Thread(add).start();
    new Thread(dec).start();
    }
    ```

    ### Runnable 对象作为一个类的内部类

2.  将 Runnable 对象作为一个类的内部类，共享数据作为这个类的成员变量，每个线程对共享数据的操作方法也封装在外部类，以便实现对数据的各个操作的同步和互斥，作为内部类的各个 Runnable 对象调用外部类的这些方法。

    ```
    public class MyData {
    private int j=0;
    public synchronized void add(){
    j++;
    System.out.println("线程"+Thread.currentThread().getName()+"j 为："+j);
    }
    public synchronized void dec(){
    j--;
    System.out.println("线程"+Thread.currentThread().getName()+"j 为："+j);
    }
    public int getData(){
    return j;
    }
    }
    public class TestThread {
    public static void main(String[] args) {
    final MyData data = new MyData();
    for(int i=0;i<2;i++){
    new Thread(new Runnable(){
    public void run() {
    data.add();
    }
    }).start();
    new Thread(new Runnable(){
    public void run() {
    data.dec(); 
    }
    }).start();
    }
    }
    }
    ```


# 153.ThreadLocal 作用（线程本地存储）

> 原文：[https://zwmst.com/3226.html](https://zwmst.com/3226.html)

ThreadLocal，很多地方叫做线程本地变量，也有些地方叫做线程本地存储，ThreadLocal 的作用是提供线程内的局部变量，**这种变量在线程的生命周期内起作用，减少同一个线程内多个函数**或者组件之间一些**公共变量的传递的复杂度**。


# 154.ThreadLocalMap（线程的一个属性）

> 原文：[https://zwmst.com/3228.html](https://zwmst.com/3228.html)

1.  每个线程中都有一个自己的 ThreadLocalMap 类对象，可以将线程自己的对象保持到其中，各管各的，线程可以正确的访问到自己的对象。
2.  将一个共用的 ThreadLocal 静态实例作为 key，将不同对象的引用保存到不同线程的ThreadLocalMap 中，然后在线程执行的各处通过这个静态 ThreadLocal 实例的 get()方法取得自己线程保存的那个对象，避免了将这个对象作为参数传递的麻烦。
3.  ThreadLocalMap 其实就是线程里面的一个属性，它在 Thread 类中定义

    ```
    ThreadLocal.ThreadLocalMap threadLocals = null;
    ```


# 155.使用场景

> 原文：[https://zwmst.com/3230.html](https://zwmst.com/3230.html)

最常见的 ThreadLocal 使用场景为 用来解决 数据库连接、Session 管理等。

```
private static final ThreadLocal threadSession = new ThreadLocal(); 
public static Session getSession() throws InfrastructureException { 
 Session s = (Session) threadSession.get(); 
 try { 
 if (s == null) { 
 s = getSessionFactory().openSession(); 
 threadSession.set(s); 
 } 
 } catch (HibernateException ex) { 
 throw new InfrastructureException(ex); 
 } 
 return s; 
}
```


# 156.synchronized 和 ReentrantLock 的区别

> 原文：[https://zwmst.com/3245.html](https://zwmst.com/3245.html)

1.  两者的共同点：

    1.  都是用来协调多线程对共享对象、变量的访问
    2.  都是可重入锁，同一线程可以多次获得同一个锁
    3.  都保证了可见性和互斥性
2.  两者的不同点：

    1.  ReentrantLock 显示的获得、释放锁，synchronized 隐式获得释放锁
    2.  ReentrantLock 可响应中断、可轮回，synchronized 是不可以响应中断的，为处理锁的不可用性提供了更高的灵活性
    3.  ReentrantLock 是 API 级别的，synchronized 是 JVM 级别的
    4.  ReentrantLock 可以实现公平锁
    5.  ReentrantLock 通过 Condition 可以绑定多个条件
    6.  底层实现不一样， synchronized 是同步阻塞，使用的是悲观并发策略，lock 是同步非阻塞，采用的是乐观并发策略
    7.  Lock 是一个接口，而 synchronized 是 Java 中的关键字，synchronized 是内置的语言实现。
    8.  synchronized 在发生异常时，会自动释放线程占有的锁，因此不会导致死锁现象发生；而 Lock 在发生异常时，如果没有主动通过 unLock()去释放锁，则很可能造成死锁现象，因此使用 Lock 时需要在 finally 块中释放锁。
    9.  Lock 可以让等待锁的线程响应中断，而 synchronized 却不行，使用 synchronized 时，等待的线程会一直等待下去，不能够响应中断。
    10.  通过 Lock 可以知道有没有成功获取锁，而 synchronized 却无法办到。
    11.  Lock 可以提高多个线程进行读操作的效率，既就是实现读写锁等。


# 157.ConcurrentHashMap 并发

> 原文：[https://zwmst.com/3248.html](https://zwmst.com/3248.html)

### 减小锁粒度

减小锁粒度是指缩小锁定对象的范围，从而减小锁冲突的可能性，从而提高系统的并发能力。减小锁粒度是一种削弱多线程锁竞争的有效手段，这种技术典型的应用是 ConcurrentHashMap(高性能的 HashMap)类的实现。对于 HashMap 而言，最重要的两个方法是 get 与 set 方法，如果我们对整个 HashMap 加锁，可以得到线程安全的对象，但是加锁粒度太大。**Segment 的大小也被称为 ConcurrentHashMap 的并发度**。


# 158.ConcurrentHashMap 分段锁

> 原文：[https://zwmst.com/3250.html](https://zwmst.com/3250.html)

ConcurrentHashMap，它内部细分了若干个小的 HashMap，称之为段(Segment)。默认情况下一个 **ConcurrentHashMap 被进一步细分为 16 个段**，既就是锁的并发度。

如果需要在ConcurrentHashMap 中添加一个新的表项，并不是将整个 HashMap 加锁，而是首先根据 hashcode 得到该表项应该存放在哪个段中，然后对该段加锁，并完成 put 操作。在多线程环境中，如果多个线程同时进行 put操作，只要被加入的表项不存放在同一个段中，则线程间可以做到真正的并行。


# 159.抢占式调度

> 原文：[https://zwmst.com/3252.html](https://zwmst.com/3252.html)

抢占式调度指的是每条线程执行的时间、线程的切换都由系统控制，系统控制指的是在系统某种运行机制下，可能每条线程都分同样的执行时间片，也可能是某些线程执行的时间片较长，甚至某些线程得不到执行的时间片。在这种机制下，一个线程的堵塞不会导致整个进程堵塞。


# 160.协同式调度

> 原文：[https://zwmst.com/3254.html](https://zwmst.com/3254.html)

协同式调度指某一线程执行完后主动通知系统切换到另一线程上执行，这种模式就像接力赛一样，一个人跑完自己的路程就把接力棒交接给下一个人，下个人继续往下跑。线程的执行时间由线程本身控制，线程切换可以预知，不存在多线程同步问题，但它有一个致命弱点：如果一个线程编写有问题，运行到一半就一直堵塞，那么可能导致整个系统崩溃。


# 161.JVM 的线程调度实现（抢占式调度）

> 原文：[https://zwmst.com/3256.html](https://zwmst.com/3256.html)

java 使用的线程调使用抢占式调度，Java 中线程会按优先级分配 CPU 时间片运行，且优先级越高越优先执行，但优先级高并不代表能独自占用执行时间片，可能是优先级高得到越多的执行时间片，反之，优先级低的分到的执行时间少但不会分配不到执行时间。


# 162.线程让出 cpu 的情况

> 原文：[https://zwmst.com/3258.html](https://zwmst.com/3258.html)

1.  当前运行线程主动放弃 CPU，JVM 暂时放弃 CPU 操作（基于时间片轮转调度的 JVM 操作系统不会让线程永久放弃 CPU，或者说放弃本次时间片的执行权），例如调用 yield()方法。
2.  当前运行线程因为某些原因进入阻塞状态，例如阻塞在 I/O 上。
3.  当前运行线程结束，即运行完 run()方法里面的任务。


# 163.优先调度算法

> 原文：[https://zwmst.com/3260.html](https://zwmst.com/3260.html)

1.  先来先服务调度算法（FCFS）
    当在作业调度中采用该算法时，每次调度都是从后备作业队列中选择一个或多个最先进入该队列的作业，将它们调入内存，为它们分配资源、创建进程，然后放入就绪队列。在进程调度中采用 FCFS 算法时，则每次调度是从就绪队列中选择一个最先进入该队列的进程，为之分配处理机，使之投入运行。该进程一直运行到完成或发生某事件而阻塞后才放弃处理机，特点是：算法比较简单，可以实现基本上的公平。

2.  短作业(进程)优先调度算法
    短作业优先(SJF)的调度算法是从后备队列中选择一个或若干个估计运行时间最短的作业，将它们调入内存运行。而短进程优先(SPF)调度算法则是从就绪队列中选出一个估计运行时间最短的进程，将处理机分配给它，使它立即执行并一直执行到完成，或发生某事件而被阻塞放弃处理机时再重新调度。该算法未照顾紧迫型作业。


# 164.高优先权优先调度算法

> 原文：[https://zwmst.com/3262.html](https://zwmst.com/3262.html)

为了照顾紧迫型作业，使之在进入系统后便获得优先处理，引入了最高优先权优先(FPF)调度算法。当把该算法用于作业调度时，系统将从后备队列中选择若干个优先权最高的作业装入内存。当用于进程调度时，该算法是把处理机分配给就绪队列中优先权最高的进程。

1.  非抢占式优先权算法
    在这种方式下，系统一旦把处理机分配给就绪队列中优先权最高的进程后，该进程便一直执行下去，直至完成；或因发生某事件使该进程放弃处理机时。这种调度算法主要用于批处理系统中；也可用于某些对实时性要求不严的实时系统中。

2.  抢占式优先权调度算法
    在这种方式下，系统同样是把处理机分配给优先权最高的进程，使之执行。但在其执行期间，只要又出现了另一个其优先权更高的进程，进程调度程序就立即停止当前进程(原优先权最高的进程)的执行，重新将处理机分配给新到的优先权最高的进程。显然，这种抢占式的优先权调度算法能更好地满足紧迫作业的要求，故而常用于要求比较严格的实时系统中，以及对性能要求较高的批处理和分时系统中。


# 165.高响应比优先调度算法

> 原文：[https://zwmst.com/3264.html](https://zwmst.com/3264.html)

在批处理系统中，短作业优先算法是一种比较好的算法，其主要的不足之处是长作业的运行得不到保证。如果我们能为每个作业引入前面所述的动态优先权，并使作业的优先级随着等待时间的增加而以速率 a 提高，则长作业在等待一定的时间后，必然有机会分配到处理机。该优先权的变化规律可描述为：
![](img/009e7df9f586e5956f7cfbbcfbda701c.png)

1.  如果作业的等待时间相同，则要求服务的时间愈短，其优先权愈高，因而该算法有利于短作业。
2.  当要求服务的时间相同时，作业的优先权决定于其等待时间，等待时间愈长，其优先权愈高，因而它实现的是先来先服务。
3.  对于长作业，作业的优先级可以随等待时间的增加而提高，当其等待时间足够长时，其优先级便可升到很高，从而也可获得处理机。简言之，该算法既照顾了短作业，又考虑了作业到达的先后次序，不会使长作业长期得不到服务。因此，该算法实现了一种较好的折衷。当然，在利用该算法时，每要进行调度之前，都须先做响应比的计算，这会增加系统开销。


# 166.时间片轮转法

> 原文：[https://zwmst.com/3267.html](https://zwmst.com/3267.html)

在早期的时间片轮转法中，系统将所有的就绪进程按先来先服务的原则排成一个队列，每次调度时，把 CPU 分配给队首进程，并令其执行一个时间片。时间片的大小从几 ms 到几百 ms。**当执行的时间片用完时，由一个计时器发出时钟中断请求，调度程序便据此信号来停止该进程的执行，并将它送往就绪队列的末尾；然后，再把处理机分配给就绪队列中新的队首进程**，同时也让它执行一个时间片。这样就可以保证就绪队列中的所有进程在一给定的时间内均能获得一时间片的处理机执行时间。


# 167.多级反馈队列调度算法

> 原文：[https://zwmst.com/3269.html](https://zwmst.com/3269.html)

1.  应设置多个就绪队列，并为各个队列赋予不同的优先级。第一个队列的优先级最高，第二个队列次之，其余各队列的优先权逐个降低。该算法赋予各个队列中进程执行时间片的大小也各不相同，在优先权愈高的队列中，为每个进程所规定的执行时间片就愈小。例如，第二个队列的时间片要比第一个队列的时间片长一倍，……，第 i+1 个队列的时间片要比第 i 个队列的时间片长一倍。
2.  当一个新进程进入内存后，首先将它放入第一队列的末尾，按 FCFS 原则排队等待调度。当轮到该进程执行时，如它能在该时间片内完成，便可准备撤离系统；如果它在一个时间片结束时尚未完成，调度程序便将该进程转入第二队列的末尾，再同样地按 FCFS 原则等待调度执行；如果它在第二队列中运行一个时间片后仍未完成，再依次将它放入第三队列，……，如此下去，当一个长作业(进程)从第一队列依次降到第 n 队列后，在第 n 队列便采取按时间片轮转的方式运行。
3.  仅当第一队列空闲时，调度程序才调度第二队列中的进程运行；仅当第 1～(i-1)队列均空时，才会调度第 i 队列中的进程运行。如果处理机正在第 i 队列中为某进程服务时，又有新进程进入优先权较高的队列(第 1～(i-1)中的任何一个队列)，则此时新进程将抢占正在运行进程的处理机，即由调度程序把正在运行的进程放回到第 i 队列的末尾，把处理机分配给新到的高优先权进程。

    在多级反馈队列调度算法中，如果规定第一个队列的时间片略大于多数人机交互所需之处理时间时，便能够较好的满足各种类型用户的需要。


# 168\. CAS（比较并交换-乐观锁机制-锁自旋）概念及特性

> 原文：[https://zwmst.com/3271.html](https://zwmst.com/3271.html)

CAS（Compare And Swap/Set）比较并交换，CAS 算法的过程是这样：它包含 3 个参数CAS(V,E,N)。**V 表示要更新的变量(内存值)，E 表示预期值(旧的)，N 表示新值。当且仅当 V 值等于 E 值时，才会将 V 的值设为 N，如果 V 值和 E 值不同，则说明已经有其他线程做了更新，则当前线程什么都不做。最后，CAS 返回当前 V 的真实值**。
CAS 操作是抱着乐观的态度进行的(乐观锁)，它总是认为自己可以成功完成操作。**当多个线程同时使用 CAS 操作一个变量时，只有一个会胜出，并成功更新，其余均会失败。失败的线程不会被挂起，仅是被告知失败，并且允许再次尝试，当然也允许失败的线程放弃操作**。基于这样的原理，CAS 操作即使没有锁，也可以发现其他线程对当前线程的干扰，并进行恰当的处理。


# 169.原子包 java.util.concurrent.atomic（锁自旋）

> 原文：[https://zwmst.com/3273.html](https://zwmst.com/3273.html)

JDK1.5 的原子包：java.util.concurrent.atomic 这个包里面提供了一组原子类。其基本的特性就是在多线程环境下，当有多个线程同时执行这些类的实例包含的方法时，具有排他性，即**当某个线程进入方法，执行其中的指令时，不会被其他线程打断，而别的线程就像自旋锁一样，一直等到该方法执行完成，才由 JVM 从等待队列中选择一个另一个线程进入**，这只是一种逻辑上的理解。相对于对于 synchronized 这种阻塞算法，CAS 是非阻塞算法的一种常见实现。**由于一般 CPU 切换时间比 CPU 指令集操作更加长**， 所以 J.U.C 在性能上有了很大的提升。如下代码：

```
public class AtomicInteger extends Number implements java.io.Serializable { 
 private volatile int value; 
public final int get() { 
 return value; 
 } 
 public final int getAndIncrement() { 
 for (;;) { //CAS 自旋，一直尝试，直达成功
 int current = get(); 
 int next = current + 1; 
 if (compareAndSet(current, next)) 
 return current; 
 } 
 } 
 public final boolean compareAndSet(int expect, int update) { 
 return unsafe.compareAndSwapInt(this, valueOffset, expect, update); 
 } 
}
```

getAndIncrement 采用了 CAS 操作，每次从内存中读取数据然后将此数据和+1 后的结果进行CAS 操作，如果成功就返回结果，否则重试直到成功为止。而 compareAndSet 利用 JNI 来完成CPU 指令的操作。


# 170.ABA 问题

> 原文：[https://zwmst.com/3275.html](https://zwmst.com/3275.html)

CAS 会导致“ABA 问题”。**CAS 算法实现一个重要前提需要取出内存中某时刻的数据，而在下时刻比较并替换，那么在这个时间差类会导致数据的变化**。

比如说一个线程 **one 从内存位置 V 中取出 A**，这时候另一个线程 **two 也从内存中取出 A**，并且
**two 进行了一些操作变成了 B**，然后 **two 又将 V 位置的数据变成 A**，这时候线程 **one 进行 CAS 操作发现内存中仍然是 A**，然后 one 操作成功。尽管线程 one 的 CAS 操作成功，但是不代表这个过程就是没有问题的。

部分乐观锁的实现是通过版本号（version）的方式来解决 ABA 问题，乐观锁每次在执行数据的修改操作时，都会带上一个版本号，一旦版本号和数据的版本号一致就可以执行修改操作并对版本号执行+1 操作，否则就执行失败。因为每次操作的版本号都会随之增加，所以不会出现 ABA 问题，因为版本号只会增加不会减少。


# 171.什么是 AQS（抽象的队列同步器）

> 原文：[https://zwmst.com/3277.html](https://zwmst.com/3277.html)

AbstractQueuedSynchronizer 类如其名，抽象的队列式的同步器，AQS 定义了一套多线程访问共享资源的同步器框架，许多同步类实现都依赖于它，如常用的ReentrantLock/Semaphore/CountDownLatch。

它维护了一个 volatile int state（代表共享资源）和一个 FIFO 线程等待队列（多线程争用资源被阻塞时会进入此队列）。这里 volatile 是核心关键词，具体 volatile 的语义，在此不述。state 的
访问方式有三种:
getState()
setState()
compareAndSetState()



# AQS 定义两种资源共享方式

### Exclusive 独占资源-ReentrantLock

Exclusive（独占，只有一个线程能执行，如 ReentrantLock）

* * 

### Share 共享资源-Semaphore/CountDownLatch

Share（共享，多个线程可同时执行，如Semaphore/CountDownLatch）。

* * 

**AQS 只是一个框架，具体资源的获取/释放方式交由自定义同步器去实现**，AQS 这里只定义了一个接口，具体资源的获取交由自定义同步器去实现了（通过 state 的 get/set/CAS)之所以没有定义成abstract ，是 因 为独 占模 式 下 只 用实现 tryAcquire-tryRelease ，而 共享 模 式 下 只用 实 现tryAcquireShared-tryReleaseShared。如果都定义成abstract，那么每个模式也要去实现另一模式下的接口。不同的自定义同步器争用共享资源的方式也不同。自定义同步器在实现时只需要实现共享资源 state 的获取与释放方式即可，至于具体线程等待队列的维护（如获取资源失败入队/唤醒出队等），AQS 已经在顶层实现好了。自定义同步器实现时主要实现以下几种方法：

1.  isHeldExclusively()：该线程是否正在独占资源。只有用到 condition 才需要去实现它。
2.  tryAcquire(int)：独占方式。尝试获取资源，成功则返回 true，失败则返回 false。
3.  tryRelease(int)：独占方式。尝试释放资源，成功则返回 true，失败则返回 false。
4.  tryAcquireShared(int)：共享方式。尝试获取资源。负数表示失败；0 表示成功，但没有剩余可用资源；正数表示成功，且有剩余资源。
5.  tryReleaseShared(int)：共享方式。尝试释放资源，如果释放后允许唤醒后续等待结点返回true，否则返回 false。


# 172.同步器的实现是 ABS 核心（state 资源状态计数）

> 原文：[https://zwmst.com/3279.html](https://zwmst.com/3279.html)

同步器的实现是 ABS 核心，以 ReentrantLock 为例，**state 初始化为 0，表示未锁定状态。A 线程lock()时，会调用 tryAcquire()独占该锁并将 state+1。此后，其他线程再 tryAcquire()时就会失败，直到 A 线程 unlock()到 state=0（即释放锁）为止**，其它线程才有机会获取该锁。当然，释放锁之前，**A 线程自己是可以重复获取此锁的（state 会累加），这就是可重入的概念**。但要注意，获取多少次就要释放多么次，这样才能保证 state 是能回到零态的。

以 CountDownLatch 以例，任务分为 N 个子线程去执行，state 也初始化为 N（注意 N 要与线程个数一致）。这 N 个子线程是并行执行的，**每个子线程执行完后 countDown()一次，state会 CAS 减 1。等到所有子线程都执行完后(即 state=0)，会 unpark()主调用线程**，然后主调用线程就会从 await()函数返回，继续后余动作。


# 173.ReentrantReadWriteLock 实现独占和共享两种方式

> 原文：[https://zwmst.com/3284.html](https://zwmst.com/3284.html)

一般来说，自定义同步器要么是独占方法，要么是共享方式，他们也只需实现 tryAcquiretryRelease、tryAcquireShared-tryReleaseShared 中的一种即可。**但 AQS 也支持自定义同步器同时实现独占和共享两种方式，如ReentrantReadWriteLock**。

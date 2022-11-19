<!--yml
category: Java
date: 2022-11-19 13:21:49
-->

# Java线程面试指南二 - 分布式编程

> 来源：[https://zthinker.com/archives/java-thread-interview-2](https://zthinker.com/archives/java-thread-interview-2)

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

Java多线程:多线程是同时执行多个线程的过程。Java支持单线程以及多线程操作。单线程程序具有一个入口点(main()方法)和一个出口点。多线程程序具有一个初始入口点(main()方法),其后是许多入口点和出口点,它们与main()同时运行。术语并发是指同时执行多个任务。多处理和多线程都用于执行多任务。

多线程是同时执行多个线程的过程。

它的主要优点是:

*   线程共享相同的地址空间。
*   线程是轻量级的。
*   线程之间的切换成本低

当我们在Java程序中创建线程时,它被称为用户线程。守护程序线程在后台运行,并且不会阻止JVM终止。当没有用户线程在运行时,JVM会关闭程序并退出。从守护程序线程创建的子线程也是守护程序线程。

上下文切换是存储和恢复CPU状态的过程,以便可以在以后的某个时间点从同一点恢复线程执行。上下文切换是多任务操作系统的基本功能,并且支持多线程环境。

在多线程编程中,多个线程同时执行可以提高性能,因为在某些线程正在等待获取某些资源的情况下,CPU不会处于空闲状态。多个线程共享堆内存,因此最好创建多个线程来执行某些任务,而不要创建多个进程。例如,Servlet的性能比CGI更好,因为Servlet支持多线程,但CGI不支持。

当我们在Java程序中创建线程时,其状态为“新建”。然后,我们启动将其状态更改为Runnable的线程。线程调度程序负责将CPU分配给可运行线程池中的线程,并将其状态更改为正在运行。其他线程状态为Waiting,Blocked和Dead。

进程是一个自包含的执行环境,可以将其视为程序或应用程序,而线程是进程中执行的单个任务。Java运行时环境作为单个进程运行,其中包含不同的类和程序作为进程。线程可以称为轻量级进程。线程需要较少的资源来创建并存在于流程中,线程共享流程资源。

在抢占式调度下,最高优先级的任务会一直执行,直到进入等待状态或死机状态或存在更高优先级的任务为止。在时间分片下,任务将执行预定义的时间片,然后重新进入就绪任务池。然后,调度程序根据优先级和其他因素确定下一步应执行的任务。

不,不可能两次启动一个线程。如果这样做,它将引发异常。

是的,但是它将不能用作线程,而可以用作普通对象,因此在线程之间不会进行上下文切换。

我们可以使用Thread类的sleep()方法将Thread的执行暂停一定时间。请注意,这不会在特定时间内停止线程的处理,一旦线程从睡眠中醒来,其状态将更改为可运行,并根据线程调度执行该线程。

**线程调度程序**是一种操作系统服务,它将CPU时间分配给可用的可运行线程。创建并启动线程后,其执行取决于Thread Scheduler的实现。

**时间分片**是将可用CPU时间划分为可用可运行线程的过程。可以根据线程优先级为线程分配CPU时间,或者等待更长时间的线程将在获得CPU时间时获得更高的优先级。线程调度不能由Java控制,因此始终最好从应用程序本身控制线程调度。

当线程共享资源时,线程之间的通信对于协调其工作很重要。对象类的wait(),notify()和notifyAll()方法允许线程就资源的锁定状态进行通信。

有几种方法可以在Java中实现线程安全:synchronization, atomic concurrent classes, implementing concurrent Lock interface,使用volatile关键字,使用不可变类和Thread安全类。

线程类setDaemon(true)可用于在Java中创建守护程序线程。我们需要在调用start()方法之前调用此方法,否则它将引发IllegalThreadStateException。

Java ThreadLocal用于创建线程局部变量。我们知道对象的所有线程都共享它的变量,因此,如果变量不是线程安全的,则可以使用同步,但是如果要避免同步,则可以使用ThreadLocal变量。

每个线程都有自己的ThreadLocal变量,他们可以使用它的get()和set()方法获取默认值或将其本地值更改为Thread。ThreadLocal实例通常是希望将状态与线程关联的类中的私有静态字段。

Thread Dump是JVM中所有活动线程的列表,Thread Dump对于分析应用程序中的瓶颈和分析死锁情况非常有帮助。我们可以使用多种方法来Dump Thread –使用Profiler,Kill -3命令,jstack工具等。我更喜欢使用jstack工具来进行 Dump Thread,因为它易于使用并且随JDK安装一起提供。由于它是基于终端的工具,因此我们可以创建脚本以定期Dump Thread,以供日后分析。

线程池管理工作线程池;它包含一个使任务等待执行的队列。

线程池管理可运行线程的集合,工作线程从队列中执行可运行线程。

java.util.concurrent.Executors提供java.util.concurrent.Executor接口的实现,以在Java中创建线程池。线程池示例程序显示了如何在Java中创建和使用线程池。或阅读ScheduledThreadPoolExecutor示例以了解如何在特定延迟后安排任务。

同步是控制多个线程对任何共享资源的访问的能力。它用于:

1.  为了防止线程干扰。
2.  以防止一致性问题。

*   同步块用于锁定任何共享资源的对象。
*   同步块的范围小于该方法。

如果将任何静态方法设置为已同步,则锁定将锁定在类上而不是对象上。
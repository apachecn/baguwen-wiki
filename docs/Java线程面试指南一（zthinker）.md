<!--yml
category: Java
date: 2022-11-19 13:21:46
-->

# Java线程面试指南一（zthinker）

> 来源：[https://zthinker.com/archives/java-thread-interview-1](https://zthinker.com/archives/java-thread-interview-1)

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

Java支持单线程以及多线程操作。线程是程序的执行路径。今天编写的大多数程序都是作为单线程运行的,当需要同时发生多个事件或动作时会引起问题。单线程程序具有一个入口点(main()方法)和一个出口点。

可以使用两种不同的机制来创建线程:

扩展Thread类

实现Runnable接口

*   线程以最佳方式消耗CPU,因此可以进行多处理。多线程减少了CPU的空闲时间,从而提高了应用程序的性能。
*   线程是轻量级的过程。
*   线程类属于java.lang包。
*   即使我们不创建任何线程,我们也可以在Java中创建多个线程,至少一个线程确实存在,即主线程。
*   多个线程在Java中并行运行。
*   线程有自己的堆栈。
*   线程的优点:假设一个线程需要10分钟才能完成某些任务,一次使用10个线程可以在1分钟内完成该任务,因为线程可以并行运行。

一个进程可以有多个线程,

线程是进程的细分。一个或多个线程在进程的上下文中运行。线程可以执行过程的任何部分。进程的同一部分可以由多个线程执行。

进程具有其父进程的数据段的副本,而线程可以直接访问其进程的数据段。

进程具有自己的地址,而线程共享创建它的进程的地址空间。

流程创建需要完成很多工作,我们可能需要复制整个父流程,但是可以轻松创建线程。

进程可以轻松地与子进程进行通信,但是进程间的通信很困难。同时,线程可以使用wait()和notify()方法轻松地与同一进程的其他线程通信。

在处理过程中,所有线程共享系统资源(例如堆内存等),而线程具有其自己的堆栈。

对进程所做的任何更改都不会影响子进程,但是对线程所做的任何更改都可能影响该进程其他线程的行为。

查看在不同进程和相同进程上创建线程的位置的示例。

这是非常基本的线程问题。可以通过两种方法来创建线程:通过实现java.lang.Runnable接口或扩展java.lang.Thread类,然后扩展run方法。

线程有其自己的变量和方法,它在堆上生存和死亡。但是执行线程是具有自己的调用堆栈的单个进程。线程是Java中的轻量级进程。

通过实现java.lang.Runnable interface创建线程。

我们将创建实现Runnable接口的类的对象:

```
MyRunnable runnable=new MyRunnable();

Thread thread=new Thread(runnable); 
```

然后通过调用构造函数并传递Runnable接口的引用(即runnable object)来创建Thread对象:

```
Thread thread=new Thread(runnable); 
```

是的,线程有自己的堆栈。这是一个非常有趣的问题,面试官倾向于检查您有关线程如何内部维护自己的堆栈的基本知识。

很好的答案是,只有在您想要修改run()和其他方法时,才必须扩展Thread。如果只想修改实现Runnable的run()方法是最好的选择(Runnable接口只有一个抽象方法,即run())。 

java中不允许多重继承:当我们实现Runnable接口时,我们也可以扩展另一个类,但是如果我们扩展Thread类,则不能扩展任何其他类,因为Java不允许多重继承。因此,通过实现Runnable和扩展Thread可以完成相同的工作,但是在实现Runnable的情况下,我们仍然可以选择扩展其他类。因此,最好实现Runnable。

*   线程安全性:当我们实现Runnable接口时,同一对象在多个线程之间共享,但是当我们扩展Thread类时,每个线程都与新对象相关联。
*   继承(实现Runnable是轻量级操作):当我们不必要地扩展Thread时,所有Thread类的功能都会被继承,但是当我们实现Runnable接口时,不会继承任何额外的功能,因为Runnable仅包含一个抽象方法,即run()方法。因此,实现Runnable是轻量级的操作。
*   编码到接口:甚至java也建议编码到接口。因此,我们必须实现Runnable而不是扩展线程。另外,Thread类实现Runnable接口。
*   除非要修改类的基本行为,否则不要扩展,Runnable接口只有一个抽象方法,即run():仅当您希望修改run()和其他方法时,才必须扩展Thread。如果只想修改实现Runnable的run()方法是最好的选择(Runnable接口只有一个抽象方法,即run())。除非我们要修改Thread类的基本行为,否则我们不能扩展Thread类。
*   实现Runnable时代码的灵活性:当我们首先扩展Thread时,所有线程功能都被继承,并且我们的类成为Thread的直接子类,因此我们正在做的任何操作都在Thread类中。但是,当我们实现Runnable时,我们创建了一个新线程并将runnable对象作为参数传递,我们可以将runable对象传递给执行程序Service等等。因此,当我们实现Runnable时,我们有更多选择,并且代码变得更加灵活。
*   Executor Service:如果我们实现Runnable,则可以使用Executor Service启动在可运行对象上创建的多个线程(因为我们可以使用新线程来启动Runnable对象),但是在扩展Thread的情况下则不会(因为线程只能启动一次) 。

问题的解决方案非常简单,线程行为是不可预测的,因为线程的执行取决于线程调度程序,线程调度程序在Windows,Unix等不同平台上的实现方式可能不同。即使在同一平台上,相同的线程程序在后续执行中也可能产生不同的输出。

为了实现这一点,我们将在同一个Runnable对象上创建2个线程,在run()方法中创建for循环并启动两个线程。不能确定哪个线程将首先完成,两个线程都将在for循环中匿名输入。

仅当同一进程的线程同时执行时,线程才是轻量级进程。但是,如果不同进程的线程同时执行,那么线程就是重量级进程。

面试官倾向于了解面试者对Thread方法的了解。因此,现在该通过正确回答来证明您的观点了。我们可以使用join()方法来确保所有从main开始的线程必须按照它们开始的顺序结束,并且main也应该在最后结束。换句话说,等待该线程死亡。内部调用join()方法将调用join(0);

详细说明:Join()方法–确保从main开始的所有线程必须按它们开始的顺序结束,并且main也应最后结束。具有程序的join()方法的类型-join的10个显着特征。

这是一个非常有趣的问题,它可能会使您感到困惑,并且有时可能使您认为使用run()和start()方法启动线程之间确实存在任何区别。

当您调用start()方法时,主线程在内部调用run()方法以启动新创建的线程,因此run()方法最终被新创建的线程调用。

当您调用run()方法主线程而不是使用新线程启动run()方法,它将自行启动run()方法。

Java允许线程访问共享变量。通常,为确保一致地更新共享变量,线程应通过获取对这些共享变量强制执行互斥的锁来确保其专有使用此类变量。

如果将字段声明为易失性,则在这种情况下,Java内存模型可确保所有线程看到的变量值均一致。
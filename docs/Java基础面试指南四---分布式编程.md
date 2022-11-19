<!--yml
category: Java
date: 2022-11-19 13:21:43
-->

# Java基础面试指南四 - 分布式编程

> 来源：[https://zthinker.com/archives/java-basic-interview-4](https://zthinker.com/archives/java-basic-interview-4)

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

我们不能通过受保护的方法重写公共方法。子类中方法的访问修饰符在覆盖时不能限制父类方法的范围。这是因为我们通过超类引用调用该方法，该超类引用通过子实现覆盖父实现。由于引用的类型是Parent类，因此客户端代码知道范围更广(公共)的API，并且是基于父API编写的。因此，限制覆盖(子级)方法的范围没有任何意义，但是相反的做法当然是可能的。

字符串在Java中是不可变的。当我们在String中进行更改时，它将创建一个新的String对象。我们的程序在运行时创建了很多String对象。为了提供最佳性能，JVM最小化了String对象的创建，并在堆内存中维护了String文字池(从Java 7开始)。因此，当需要创建String文字时，它首先在池中检查它是否存在。如果找到，它将返回该对象的引用。否则，它将创建对象并将其保留在池中，以供以后再使用。 

不变类不允许在创建后更改其对象的状态。如果我们需要更改对象的状态，它将创建一个新对象。不可变类的最受欢迎的例子之一是String。我们需要注意几件事，以使类型不可变。 

1.  该类必须是最后的。不允许扩展的原因是子类可以访问敏感字段或方法，而这些字段或方法可能会更改对象的状态。 
2.  该类应将其所有成员声明为私有。 
3.  它不应提供API或公共方法来更改其状态。例如setter方法。即使这样做，它也应该创建自己的副本，在那里进行更改并返回对象。 
4.  如果该类的任何成员是可变的，则应将其声明为final。 
5.  我们应该通过构造函数来初始化对象，对作为构造函数参数传递的可变对象进行深层克隆。 
6.  我们不应该在类之外公开可变成员的引用。如果需要执行此操作，则需要正确克隆该成员并返回它。这样可以确保即使通过其引用更改了对象，它也不是同一对象。 

在Java的早期版本(最高1.7)中，该接口被设计为仅具有方法签名。从Java 8开始，该接口现在还可以包含方法实现。这些方法应标记为default关键字，并称为接口的默认方法。这意味着不必强制覆盖实现类中的默认方法。当接口被许多应用程序广泛使用时，很难在同一接口中添加新方法，因为它会破坏代码。实现者需要在许多地方更改其代码。为了克服这种复杂性并使接口向后兼容，引入了此更改。公共接口形状{ 

```
public interface Shape {
    default double area() { 
        return 0.0;
    } 

    default double volume() { 
        return 0.0;
    }
} 
```

堆栈内存用于在通过线程执行方法时创建局部变量和对象引用。这意味着每个线程都有一个单独的堆栈和一组局部变量。堆栈不包含实际的对象-它仅包含引用。实际对象的内存空间在堆内存中分配。堆内存由许多部分组成-年轻一代(伊甸园和幸存者空间)和老一代。对于每个方法调用，JVM都会创建一个包含局部变量的新堆栈框架。将它们保持为堆栈有助于检索最近的堆栈帧，即方法返回时轻松调用方方法的变量集。 

是的，String是一个不变的类。字符串广泛用于不同的情况下，例如共享作为方法的参数，按其名称加载类，作为值返回。因此，很可能在没有其他用户任何知识的情况下更改String对象，并导致在系统中捕获错误。在HashMap或HashTable中，字符串已作为键很受欢迎。HashMap中密钥的良好候选人应该是一成不变的。如果String是可变的并且更改了其状态，则可能会导致为同一键检索错误的值或根本找不到它。从字符串池中获取字符串文字，而不是每次都创建它。如果String是可变的，这将是不可能的，因为在其状态发生任何更改后，它无法识别该值是否存在于池中。  

克隆意味着创建对象的副本或创建重复的对象-它们的状态应该相同。一个对象可能由其他几个对象组成。浅克隆将创建一个新对象，并将其字段值分配给新对象的相应字段。由于字段仅包含驻留在堆中的对象的引用，因此新对象的字段也指向相同的组件实例。浅克隆虽然速度很快，但缺点是，如果更改了任何组件对象，它也会在克隆的对象中反映出来，因为这两个对象都持有相同对象的引用。 

另一方面，深度克隆不会复制字段中的引用，它还会创建组件对象的副本。与深度克隆中一样，所有组件对象都被克隆，这比较慢，但是会创建实际对象的真实副本。

远程方法调用是Java中的API，它通过允许对象在可能位于同一台计算机或另一台远程计算机上但在另一个地址空间上的另一个对象上调用方法来管理分布式应用程序的创建。

RMI中客户端和服务器之间的通信是通过分别使用客户端和服务器端上的存根对象和框架对象来完成的。

下图提供了有关存根对象和骨架对象的详细信息：

![客户端与服务器之间的通信 ](img/48245e4ea81e268c85d56e92d04586d8.png)

*   **存根对象： **客户端的所有传出请求都通过存根对象进行路由，因此它也被称为客户端对象的网关。
*   **骨架对象： **服务器端的所有传入请求都通过骨架对象进行路由，因此也称为服务器端对象的网关。

创建远程方法调用程序的步骤如下：

1.  首先，创建远程接口。
2.  提供了远程接口的实现。
3.  编译实现类，并创建存根和骨架对象。
4.  使用rmiregistry工具启动注册表服务。
5.  远程应用程序已创建并启动。
6.  客户端应用程序已创建并启动。

Predicate是java.util.Function包中定义的功能接口。它有助于改善代码的控制。可以在lambda表达式和功能接口中用作分配目标。功能接口是只有一种抽象方法的那些接口。

@FunctionalInterface
public interface Predicate

方法：

boolean test(T t)

test()方法根据给定的参数评估Predicate。

default Predicate <t>and(Predicate<? super T> other)</t>

and()方法通过该Predicate与另一个Predicate的短路逻辑与返回一个公式化的Predicate。如果另一个为null，则抛出NullPointerException。如果此Predicate为假，则不评估另一个Predicate。

default Predicate <t>negate()</t>

negate()方法返回表示该Predicate逻辑非的Predicate。

default Predicate <t>or(Predicate<? super T> other)</t>

or()方法返回由该Predicate和另一个Predicate的短路或得出的公式化Predicate。如果该Predicate为true，则不评估另一个Predicate。

static <t>Predicate <t>isEqual(Object targetRef)</t></t>

isEqual()方法返回一个Predicate，该Predicate根据Objects.equals(Object，Object)测试两个参数是否相等。

这是Java中Predicate的示例程序：

```
import java.util.function.Predicate;  
public class Example
{  
   public static void main(String[] args)
   {
      Predicate<Integer> a = n-> (n%3==0);  // Creating predicate with lambda expression
      System.out.println(a.test(36));  // Calling Predicate method test(Object)
   }
}

**输出如下：**

$javac Example.java
$java Example
true 
```

Java 8引入了新的日期/时间应用程序接口(API)作为以前的日期/时间API的缺点。

*   **不是线程安全的**：java.util.Date类不是线程安全的。当Date类的线程彼此之间的顺序不完整时，这迫使开发人员解决并发问题。新的日期时间API是不可变的，并且没有setter方法。
*   **设计不良**：默认日期自1900年开始就已过时，月份从1开始，而天从0开始。因此无法实现统一性。旧的API对于要执行的功能没有那么直接的方法。新的API为此类操作提供了许多有用的方法。
*   **时区的不便处理：时区**所面临的问题需要开发人员编写大量代码。开发新API时要牢记特定领域的蓝图。
*   新的API已列在java.time包下。java.time包下的一些重要类是：
*   **Local**：Local类是简化的数据/时间API，没有时区处理的麻烦
*   **Zoned**：Zoned类是考虑了时区的简化的Data / Time API

让我们看一下带有新的Date / Time API的Local类的示例：

```
import java.time.LocalDate;
import java.time.LocalTime;
import java.time.LocalDateTime;
import java.time.Month;
public class Example
{
  public void checkDate()
    {
       LocalDateTime currentTime = LocalDateTime.now(); // computing local Date/Time
       System.out.println("Present DateTime: " + currentTime);
       LocalDate date = currentTime.toLocalDate();  // computing local Data
       System.out.println("Present Local Date : " + date);
    // computing current local time in hours, minutes and seconds
       int second = currentTime.getSecond();   
       int minute =currentTime.getMinute();
       int hour=currentTime.getHour();
       System.out.println("Hour: " + hour +"|Minute: " + minute +"|seconds: " + second);
      }
  public static void main(String args[])
  {
     Example obj = new Example();
     obj.checkDate();
  }
}

**输出如下：**

$javac Example.java
$java Example
Present DateTime: 2018-12-13T18:39:24.730
Present Local Date : 2018-12-13
Hour: 18|Minute: 39|seconds: 24 
```

现在，让我们看看带有新的Date / Time API的Zoned类的示例：

```
import java.time.LocalDateTime;
import java.time.ZoneId;
import java.time.ZonedDateTime;
import java.time.format.DateTimeFormatter;
public class Example
{
   public static void Zone()
   {
    LocalDateTime dt = LocalDateTime.now();
    DateTimeFormatter format = DateTimeFormatter.ofPattern(" HH:mm:ss dd-MM-YYYY");  
    String fcd = dt.format(format); // stores the formatted current date
    System.out.println("Present formatted Time and Date: "+fcd);  
    ZonedDateTime zone = ZonedDateTime.now();  
    System.out.println("The Present zone is "+zone.getZone());  
   }
   public static void main(String[] args)  
   {
    Zone();
   }
}

**输出如下：**

$javac Example.java
$java Example
Present formatted Time and Date:  19:24:52 13-12-2019
The Present zone is Etc/UTC 
```

Optional的是一个对象容器，其中可能不包含非null值。如果有值，则isPresent()将返回true，而get()将返回该值。提供了依赖于包含值的可用性的补充方法，例如orElse()方法(如果不存在值，则返回默认值)和ifPresent()(如果存在值，则执行代码块)。

Optional的语法

public final class Optional <t>extends Object</t>

Optional是基于值的类。与身份有关的操作，包括引用相等(==)，身份哈希码或对该类对象的同步，可能会产生空前的结果，应避免使用。

让我们看一个使用Optional的isPresent()方法的示例：

```
import java.util.Optional;   
public class Example
{   
   public static void main(String[] args)
   {
       String s1 = new String("Hello");
       String s2 = null;
       Optional<String> obj1 = Optional.ofNullable(s1);
       Optional<String> obj2 = Optional.ofNullable(s2);
       if (obj1.isPresent())    // checks if String object is present
       {
          System.out.println(s1.toUpperCase());   
       }
       else
       System.out.println("s1 is a Null string");
       if(obj2.isPresent())   // checks if String object is present
       {
            System.out.println(s1.toUpperCase());
       }
       else
       System.out.println("s2 is a Null string");
   }
}

**输出如下：**

$javac Example.java
$java Example
HELLO
s2 is a Null string 
```

Base64类包含用于获取用于Base64编码的编码器和解码器的静态方法。Java 8允许我们使用三种类型的编码：

*   **基本** -输出被绘制为一组以Base64字母形式存在的字符。编码器不会在输出中添加任何换行符，并且解码器会拒绝除Base64字母以外的任何字符。
*   **统一资源定位符(URL)和文件名安全 ** -将输出绘制为以Base64字母表示的字符集。解码器拒绝包含Base64字母之外的字符的数据。
*   **多用途Internet邮件扩展(MIME)** -输出被绘制为MIME兼容格式。编码后的输出必须每行最多包含76个字符，并应用回车符'\ r'，然后立即使用换行符'\ n'作为行分隔符。编码输出的末尾没有换行分隔符。解码器将忽略除Base64字母以外的所有字符。

Base64类的声明如下：

public class Base64
extends Object

让我们看一下基本Base64编码和解码的示例：

```
import java.util.Base64;
public class Example
{
   public static void main(String[] args)
   {
       String enc = Base64.getEncoder().encodeToString("Encoding in Base64".getBytes());
       System.out.println("Encoder Output : " + enc);
       byte[] dec = Base64.getDecoder().decode(enc);
      System.out.println("Decoder Output : " + new String(dec));
   }
}

**输出如下：**

$javac Example.java
$java -Xmx128M -Xms16M Example
Encoder Output : RW5jb2RpbmcgaW4gQmFzZTY0
Decoder Output : Encoding in Base64 
```

字符串的字谜是具有相同字符和相同频率的字符串。只有字符顺序可以不同。字谜的示例如下：

String = silent
Anagram = listen

给出了一个程序，该程序检查两个字符串在Java中是否彼此变位。

```
import java.io.*;
import java.util.*;
public class Demo
{
   static boolean checkAnagram(char s1[], char s2[])
   {
       int alphaCount1[] = new int [256];
       Arrays.fill(alphaCount1, 0);
       int alphaCount2[] = new int [256];
       Arrays.fill(alphaCount2, 0);
       int i;
       for (i = 0; i <s1.length && i < s2.length ; i++)
       {
           alphaCount1[s1[i]]++;
           alphaCount2[s2[i]]++;
       }
       if (s1.length != s2.length)
           return false;
       for (i = 0; i < 256; i++)
       {
           if (alphaCount1[i] != alphaCount2[i])
               return false;
       }
       return true;
   }
   public static void main(String args[])
   {
       String str1 = "triangle";
       String str2 = "integral";
       char s1[] = str1.toCharArray();
       char s2[] = str2.toCharArray();
       System.out.println("String 1: " + str1 );
       System.out.println("String 2: " + str2 );
       if ( checkAnagram(s1, s2) )
           System.out.println("The two strings are anagram of each other");
       else
           System.out.println("The two strings are not anagram of each other");
   }
}

**上面程序的输出如下：**

String 1: triangle
String 2: integral
The two strings are anagram of each other 
```

可以使用sleep()或wait()方法在Java中的多线程环境中暂停线程的执行。使用sleep()将线程暂停所需的时间，而使用wait()使其进入等待状态，则只能通过调用notify()或notifyAll()来使线程恢复。

sleep()和wait()之间的一些区别如下：

| sleep()方法 | wait()方法 |
| --- | --- |
| 通常在当前正在执行的线程上调用sleep()方法。 | 在对象上调用wait()方法。锁定对象必须与当前线程同步。 |
| sleep()方法不会释放监视器或锁定。 | wait()方法释放监视器或锁定。 |
| sleep()方法用于在指定的时间内暂停执行。 | wait()方法可用于线程间通信。 |
| 在使用sleep()或interrupt()所需的时间后，线程被唤醒。 | 对象调用notify()或notifyAll()方法后，线程被唤醒。 |
| sleep()方法可用于多线程同步。 | wait()方法可用于时间同步。 |

以下是sleep()的示例：

```
synchronized(LOCK)
{  
   Thread.sleep(1000);
} 
```

给出了一个wait()示例，如下所示：

```
synchronized(LOCK)
{  
   LOCK.wait();
} 
```

多个线程可以使用同步来管理对共享资源的访问，其中一次只能有一个线程访问该资源。

Java中有两种类型的线程同步。给出如下：

1.  互斥
2.  线程间通讯

线程同步程序如下：

```
 class Demo {

    synchronized void display(int n) {
        for (int i = 1; i <= 5; i++) {
            System.out.println(n);
            try {
                Thread.sleep(400);
            } catch (Exception e) {
                System.out.println(e);
            }
        }
    }
}

class Thread1 extends Thread {

    Demo obj;

    Thread1(Demo obj) {
        this.obj = obj;
    }
    public void run() {
        obj.display(8);
    }
}

class Thread2 extends Thread {

    Demo obj;
    Thread2(Demo obj) {
        this.obj = obj;
    }

    public void run() {
        obj.display(3);
    }
}

public class SynchronizationDemo {
    public static void main(String args[]) {
        Demo obj1 = new Demo();
        Thread1 thr1 = new Thread1(obj1);
        Thread2 thr2 = new Thread2(obj1);
        thr1.start();
        thr2.start();
    }
}  

**上面程序的输出如下：**

8
8
8
8
8
3
3
3
3
3 
```

double类型和float类型都用于表示Java中的浮点数。但是，在某些情况下，双精度型更好，在某些情况下，浮型更好。

如果需要更精确的结果，则双精度型优于浮型。双精度型的精度最高为15到16个小数点，而浮点型的精度仅为6到7个十进制数字。

双重类型优于浮动类型的另一个原因是它具有更大的范围。它对符号使用1位，对指数使用11位，对尾数使用52位，而float型仅对符号使用1位，对指数使用8位，对尾数使用23位。

给出了一个在Java中演示double-type和float-type的程序，如下所示：

```
public class Demo
{
   public static void main(String []args)
   {
       double d = 55.637848675695785;
       float f = 25.657933f;
       System.out.println("Value of double = " + d);
       System.out.println("Value of float = " + f);
   }
}

**上面程序的输出如下：**

Value of double = 55.637848675695786
Value of float = 25.657932 
```

使用多线程可以实现线程最重要的用法。这意味着多个任务可以并行运行。Java的一些多线程最佳实践如下：

**1.最小化锁定范围**

由于不能同时执行锁中的任何代码，因此应将锁定范围最小化，这会降低应用程序性能。

**2.并发收集应优先于同步收集**

并发集合应该比同步集合更可取，因为它们可以提供更多的可伸缩性和性能。

**3.首选不可变类**

应该使用不可变的类(例如String，Integer等)以及其他包装器类，因为它们可以简化并发代码的编写。这是因为无需担心状态。

**4.应该首选线程池执行器，而不是线程**

对于可伸缩的Java应用程序来说，线程池是更好的选择，因为线程创建非常昂贵。

**5.使用局部变量**

不应使用类或实例变量，而应尽可能使用局部变量。

**6.生产者-消费者设计应首选BlockingQueue**

实施生产者使用者设计模式的最佳方法是使用BlockingQueue。这是非常重要的，因为许多并发问题都是基于生产者消费者设计的。

**7.同步实用程序应优先于等待通知**

有许多同步实用程序，例如CyclicBarrier，CountDownLatch和Semaphore都应使用，而不是等待和通知。

**8.使用信号量创建边界**

建立一个稳定的系统应该在不同的资源(例如文件系统，数据库，套接字等)上有界限。可以使用信号量创建这些界限。

可以使用Java的Collections API提供的体系结构来存储和操作一组对象。可以使用Java集合执行Java中所有可能的操作，例如搜索，排序，删除，插入等。

在Java中使用Collections时的一些最佳实践如下：

**1.选择合适的集合**

在使用集合之前，需要根据需要解决的问题选择合适的集合。

**2.使用数组和集合实用程序类**

应该根据需要使用Java Collections Framework提供的Arrays和Collections实用程序类，因为它们提供了许多有用的方法来搜索，排序和修改集合中的元素

**3.如果可能，指定集合的​​初始容量**

集合的初始容量始终由几乎所有具体集合类中都包含的重载构造函数指定。

**4.优先于isEmpty()而不是size()**

在检查集合是否为空时，应优先使用isEmpty()方法而不是size()方法。即使这两种方法在性能上存在差异，也可以这样做以提高此代码的可读性。

**5.不要在返回集合的方法中返回null**

如果方法返回一个集合，那么如果集合中没有元素，则该方法不应返回null。相反，它应该返回一个空集合。

**6.在集合上使用Stream API**

Java 8中的每个集合中都有一个流方法，该方法返回元素流。这意味着可以使用Stream API轻松地执行聚合功能。

**7.不要使用经典的for循环**

与其使用经典的for循环来迭代列表集合，不如使用迭代器。这是因为如果在循环内部更改了for循环变量，则可能导致错误。

流支持聚合操作，并在Java 8中引入。它是一系列对象，具有诸如Sorted，Map，Filter等操作。

对于流，使用以下软件包：

import java.util.stream.*;

这是Java 8中用于操作map和collect的Stream操作的示例：

```
import java.util.*;
import java.util.stream.*;
public class Demo
{
 public static void main(String args[])
 {
   List<Integer> l = Arrays.asList(29, 35, 67);
   List<Integer> res = l.stream().map(a -> a*a).collect(Collectors.toList());
   System.out.println(res);
 }
} 
```

Java中的所有对象都是从堆内存中分配的内存。当由于没有更多的可用内存而无法分配对象任何内存，并且使用垃圾回收器无法获得任何内存时，则Java中会发生OutOfMemoryError异常。

如果一次处理的数据过多或对象保留的时间太长，通常会发生内存不足错误。由于程序员无法控制的问题(例如在部署后无法清除的应用服务器)也可能发生此异常

给出了一个演示Java内存不足错误的程序，如下所示：

```
import java.util.*;
public class Demo
{
   static List<String> l = new ArrayList<String>();
   public static void main(String args[]) throws Exception
   {
       Integer[] arr = new Integer[5000 * 5000];
   }
}

**上面程序的输出如下：**

Exception in thread "main" java.lang.OutOfMemoryError: Java heap space
at Demo.main(Demo.java:9) 
```

使用volatile关键字可以使类成为线程安全的。这意味着多个线程可以同时使用类实例或方法，而不会出现任何问题。

在特定变量上使用volatile关键字的含义如下：

1.  具有volatile关键字的变量的值永远不会在本地缓存线程。这意味着对变量的所有读和写操作都保存在主存储器中。
2.  对该变量的访问就好像它被包含在一个同步块中并且本身已同步一样。

volatile关键字的示例如下：

```
class Shared
{
  static volatile int value = 15;
} 
```

在上面的示例中，如果一个线程进行了任何更改，那么它们也将使用volatile关键字反映在其他线程中。

** volatile 和 synchronized之间的区别**

易失性和同步之间的一些区别如下：
| 特性 | volatile | synchronized之间的区别 |
|----------------------|----------------------------------|--------------|
| 是否可以使用null? | 是 | 没有 |
| 变量类型 | 对象变量或原始变量 | 对象变量 |
| 何时同步? | 当访问volatile变量时 | 显式进入或退出同步块时。 |
| 所有缓存的变量是否在访问时同步? | 从Java 5开始，这是正确的。 | 是 |
| 可以用于将多个操作合并为一个原子操作吗? | 在Java 5之前这是不可能的。 | 是 |

Java中的Iterator和ListIterator都是Collection框架中的接口。迭代器用于通过向前迭代各个元素来遍历Collection元素。

ListIterator扩展了Iterator，并用于在向前和向后两个方向遍历Collection元素。另外，可以使用ListIterator在Collection中添加，修改和删除元素，而使用Iterator则无法实现。

Iterator和ListIterator之间的区别如下：

| 迭代器 | ListIterator |
| --- | --- |
| 迭代器用于沿向前方向遍历Collection元素。 | ListIterator用于在向前和向后方向遍历Collection元素。 |
| 可以使用迭代器遍历地图，列表，集合等。 | 使用ListIterator只能遍历List对象。 |
| 元素不能由Iterator修改Collection中的元素。 | 可以通过ListIterator在Collection中修改元素。 |
| 元素不能由迭代器添加到集合中。 | 元素可以通过ListIterator添加到Collection中。 |
| 迭代器中没有方法可以在Collection中查找元素索引。 | ListIterator中有一个方法可以在Collection中查找元素索引。 |

可以使用关键字final对Java中的类限制继承。换句话说，如果将一个类声明为final，则不能从该类扩展任何其他类。这在创建不可变类时非常有用  

下面是一个示例：

```
final class C1
{
    // methods and fields
}
class C2 extends C1
{
    // Not possible
} 
```

如果类C2试图扩展类C1，因为它是最终类，因此将无法继承，则会生成错误。

Java中的final变量是一种特殊类型的变量，只能在声明时或在其他时间一次赋值。

在声明时未分配值的最终变量称为空白或未初始化的最终变量。换句话说，此变量不会在其声明时初始化。给出一个示例，如下所示：

```
final int val;    // This is a blank final variable
val = 6;

给出了一个在Java中演示空白或未初始化的最终变量的程序，如下所示：

class Demo
{
   final int num;
   Demo(int num1)
   {
       num = num1;
   }
}
public class Main
{
   public static void main(String args[])
   {
       Demo obj = new Demo(87);
       System.out.println("Value of num is: " + obj.num);
   }
}

**上面程序的输出如下： **

Value of num is: 87 
```

当用户需要限制文件允许的操作时，将在文件上设置文件许可权。

文件的允许权限如下：

1.  **可读** -此权限测试应用程序是否可以读取由抽象路径名表示的文件。
2.  **可写** -此权限测试应用程序是否可以更改由抽象路径名表示的文件。
3.  **可执行文件** -此权限测试应用程序是否可以执行由抽象路径名表示的文件。

可用于更改文件权限的方法为setExecutable，setReadable和setWritable。

演示文件权限的程序如下所示：

```
import java.io.*;
public class Demo
{
   public static void main(String[] args)
   {
       File f = new File("C:\\Users\\Aaron\\Desktop\\text.txt");
       boolean exists = f.exists();
       if(exists == true)
       {
           f.setExecutable(true);
           f.setReadable(true);
           f.setWritable(false);
           System.out.println("The File permissions are now changed.");
           System.out.println("Executable: " + f.canExecute());
           System.out.println("Readable: " + f.canRead());
           System.out.println("Writable: "+ f.canWrite());
       }
       else
       {
           System.out.println("File not found.");
       }
   }
}

**上面程序的输出如下：**

The File permissions are now changed.
Executable: true
Readable: true
Writable: false 
```

Java中的不可变类是在构造后无法更改其状态的类。在Java中创建不可变类的一些要求如下：

1.  该类应该是最终类，以便其他类不能扩展它。
2.  该类的所有字段都应为final，以便它们只能在构造函数中初始化一次。
3.  设置方法不应该公开。
4.  如果公开了任何修改类状态的方法，则应返回该类的新实例。
5.  如果构造函数中存在可变对象，则仅应使用传递的参数的克隆副本。

给出了一个示例，演示如何用Java创建不可变类：

```
public final class Employee
{
   final int empNum;
   final String name;
   final int salary;
   public Employee(int empNum, String name, int salary)
   {
       this.empNum = empNum;
       this.name = name;
       this.salary = salary;
   }
   public int empNumReturn()
   {
       return empNum;
   }
   public String nameReturn()
   {
       return name;
   }
   public int salaryReturn()
   {
       return salary;
   }
} 
```

上面给出的类是基本的不可变类。此类不包含任何可变对象或任何setter方法。这种类型的基本类通常用于缓存。

协变返回类型是指重写方法的返回类型。从Java 5开始，子类中的重写方法可能具有不同的返回类型。但是，子类的返回类型应该是父类的返回类型的子类型。

给出了一个演示Java中协变量返回类型的程序，如下所示：

```
class C1
{  
   C1 ret()
   {
       return this;
   }  
}  
public class C2 extends C1
{  
   C2 ret()
   {
       return this;
   }  
   void display()
   {
       System.out.println("This is the covariant return type");
   }  
   public static void main(String args[])
   {  
       new C2().ret().display();  
   }  
}  

**上面程序的输出如下：**

This is the covariant return type 
```

上面的程序演示了协变量返回类型，因为C1类ret()方法的返回类型为C1，而C2 ret()类方法的返回类型为C2，并且这两种方法都具有不同的返回类型时，它是方法覆盖的。
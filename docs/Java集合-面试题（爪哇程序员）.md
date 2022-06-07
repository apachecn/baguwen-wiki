<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 常见的集合有哪些？

> 原文：[https://zwmst.com/1712.html](https://zwmst.com/1712.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:18:42+08:00"> 2021-08-15 </time> ](https://zwmst.com/1712.html)  Collection接口的子接口包括：Set接口和List接口

Map接口的实现类主要有：HashMap、TreeMap、Hashtable、ConcurrentHashMap以及 Properties等

Set接口的实现类主要有：HashSet、TreeSet、LinkedHashSet等

List接口的实现类主要有：ArrayList、LinkedList、Stack以及Vector等*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 常见的集合底层实现

> 原文：[https://zwmst.com/1714.html](https://zwmst.com/1714.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:19:08+08:00"> 2021-08-15 </time> ](https://zwmst.com/1714.html)  ArrayList底层是数组。

LinkedList底层是双向链表。

HashMap底层与HashTable原理相同，Java 8版本以后如果同一位置哈希冲突大于8则链表 变成红黑树。

HashTable底层是链地址法组成的哈希表（即数组+单项链表组成）。

HashSet底层是HashMap。

LinkedHashMap底层修改自HashMap，包含一个维护插入顺序的双向链表。

TreeMap底层是红黑树。

LinkedHashSet底层是LinkedHashMap。

TreeSet底层是TreeMap。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# HashMap与HashTable的区别？

> 原文：[https://zwmst.com/1716.html](https://zwmst.com/1716.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:19:20+08:00"> 2021-08-15 </time> ](https://zwmst.com/1716.html)  HashMap没有考虑同步，是线程不安全的；Hashtable使用了synchronized关键字，是线程 安全的；

HashMap允许K/V都为null；后者K/V都不允许为null；*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# ConcurrentHashMap和Hashtable的区别？

> 原文：[https://zwmst.com/1718.html](https://zwmst.com/1718.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:19:32+08:00"> 2021-08-15 </time> ](https://zwmst.com/1718.html)  ConcurrentHashMap 结合了 HashMap 和 HashTable 二者的优势。HashMap 没有考虑同 步，HashTable 考虑了同步的问题。

但是 HashTable 在每次同步执行时都要锁住整个结构。 ConcurrentHashMap 锁的方式是稍微细粒度的。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# ConcurrentHashMap实现原理

> 原文：[https://zwmst.com/1720.html](https://zwmst.com/1720.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:19:42+08:00"> 2021-08-15 </time> ](https://zwmst.com/1720.html)  JDK1.7 : 【数组（Segment） + 数组（HashEntry） + 链表（HashEntry节点）】

ConcurrentHashMap（分段锁） 对整个桶数组进行了分割分段(Segment)，每一把锁只锁 容器其中一部分数据，多线程访问容器里不同数据段的数据，就不会存在锁竞争，提高并发访问率。

Segment是一种可重入锁ReentrantLock，在ConcurrentHashMap里扮演锁的角色，HashEntry则用于存储键值对数据。

JDK1.8 : Node数组+链表 / 红黑树

利用CAS+Synchronized来保证并发更新的安全，底层依然采用数组+链表+红黑树的存储结 构。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# ArrayList 和 Vector 的区别？

> 原文：[https://zwmst.com/1722.html](https://zwmst.com/1722.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:19:54+08:00"> 2021-08-15 </time> ](https://zwmst.com/1722.html)  Vector 是线程安全的，ArrayList 是线程不安全的。

Vector在数据满时增长为原来的两倍，而 ArrayList在数据量达到容量的一半时,增长为原容量 的1.5倍。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# ArrayList和LinkedList的区别？

> 原文：[https://zwmst.com/1724.html](https://zwmst.com/1724.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:20:06+08:00"> 2021-08-15 </time> ](https://zwmst.com/1724.html)  LinkedList基于链表的数据结构；ArrayList基于动态数组的数据结构 LinkedList 在插入和删除数据时效率更高，ArrayList 查询效率更高；*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# HashMap 默认的初始化长度是多少？

> 原文：[https://zwmst.com/1726.html](https://zwmst.com/1726.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:20:16+08:00"> 2021-08-15 </time> ](https://zwmst.com/1726.html)  在JDK中默认长度是16，并且默认长度和扩容后的长度都必须是 2 的幂。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 谈谈对HashMap 构造方法中初始容量、加载因子的理解

> 原文：[https://zwmst.com/1728.html](https://zwmst.com/1728.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:20:40+08:00"> 2021-08-15 </time> ](https://zwmst.com/1728.html)  初始容量代表了哈希表中桶的初始数量，即 Entry< K,V>[] table 数组的初始长度。

加载因子是哈希表在其容量自动增加之前可以达到多满的一种饱和度百分比，其衡量了一个散 列表的空间的使用程度，负载因子越大表示散列表的装填程度越高，反之愈小。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Java集合框架是什么？说出一些集合框架的优点？

> 原文：[https://zwmst.com/1730.html](https://zwmst.com/1730.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:20:51+08:00"> 2021-08-15 </time> ](https://zwmst.com/1730.html)  每种编程语言中都有集合，最初的Java版本包含几种集合类：Vector、Stack、HashTable和 Array。随着集合的广泛使用，Java1.2提出了囊括所有集合接口、实现和算法的集合框架。在 保证线程安全的情况下使用泛型和并发集合类，Java已经经历了很久。它还包括在Java并发包 中，阻塞接口以及它们的实现。集合框架的部分优点如下：

（1）使用核心集合类降低开发成本，而非实现我们自己的集合类。

（2）随着使用经过严格测试的集合框架类，代码质量会得到提高。

（3）通过使用JDK附带的集合类，可以降低代码维护成本。

（4）复用性和可操作性。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 集合框架中的泛型有什么优点？

> 原文：[https://zwmst.com/1732.html](https://zwmst.com/1732.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:21:01+08:00"> 2021-08-15 </time> ](https://zwmst.com/1732.html)  Java1.5引入了泛型，所有的集合接口和实现都大量地使用它。泛型允许我们为集合提供一个可 以容纳的对象类型，因此，如果你添加其它类型的任何元素，它会在编译时报错。这避免了在 运行时出现ClassCastException，因为你将会在编译时得到报错信息。泛型也使得代码整 洁，我们不需要使用显式转换和instanceOf操作符。它也给运行时带来好处，因为不会产生类 型检查的字节码指令。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 为何Collection不从Cloneable和Serializable接口继承？

> 原文：[https://zwmst.com/1734.html](https://zwmst.com/1734.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:21:12+08:00"> 2021-08-15 </time> ](https://zwmst.com/1734.html)  Collection接口指定一组对象，对象即为它的元素。如何维护这些元素由Collection的具体实 现决定。例如，一些如List的Collection实现允许重复的元素，而其它的如Set就不允许。很多 Collection实现有一个公有的clone方法。然而，把它放到集合的所有实现中也是没有意义 的。这是因为Collection是一个抽象表现。重要的是实现。

当与具体实现打交道的时候，克隆或序列化的语义和含义才发挥作用。所以，具体实现应该决 定如何对它进行克隆或序列化，或它是否可以被克隆或序列化。

在所有的实现中授权克隆和序列化，最终导致更少的灵活性和更多的限制。特定的实现应该决 定它是否可以被克隆和序列化。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 为何Map接口不继承Collection接口？

> 原文：[https://zwmst.com/1736.html](https://zwmst.com/1736.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:21:23+08:00"> 2021-08-15 </time> ](https://zwmst.com/1736.html)  尽管Map接口和它的实现也是集合框架的一部分，但Map不是集合，集合也不是Map。因此， Map继承Collection毫无意义，反之亦然。

如果Map继承Collection接口，那么元素去哪儿？Map包含key-value对，它提供抽取key或 value列表集合的方法，但是它不适合“一组对象”规范。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Iterator是什么？

> 原文：[https://zwmst.com/1738.html](https://zwmst.com/1738.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:21:34+08:00"> 2021-08-15 </time> ](https://zwmst.com/1738.html)  Iterator接口提供遍历任何Collection的接口。我们可以从一个Collection中使用迭代器方法 来获取迭代器实例。迭代器取代了Java集合框架中的Enumeration。迭代器允许调用者在迭 代过程中移除元素。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Enumeration和Iterator接口的区别？

> 原文：[https://zwmst.com/1740.html](https://zwmst.com/1740.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:21:46+08:00"> 2021-08-15 </time> ](https://zwmst.com/1740.html)  Enumeration的速度是Iterator的两倍，也使用更少的内存。Enumeration是非常基础的， 也满足了基础的需要。但是，与Enumeration相比，Iterator更加安全，因为当一个集合正在 被遍历的时候，它会阻止其它线程去修改集合。

迭代器取代了Java集合框架中的Enumeration。迭代器允许调用者从集合中移除元素，而 Enumeration不能做到。为了使它的功能更加清晰，迭代器方法名已经经过改善。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Iterater和ListIterator之间有什么区别？

> 原文：[https://zwmst.com/1742.html](https://zwmst.com/1742.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:21:59+08:00"> 2021-08-15 </time> ](https://zwmst.com/1742.html)  （1）我们可以使用Iterator来遍历Set和List集合，而ListIterator只能遍历List。

（2）Iterator只可以向前遍历，而LIstIterator可以双向遍历。

（3）ListIterator从Iterator接口继承，然后添加了一些额外的功能，比如添加一个元素、替 换一个元素、获取前面或后面元素的索引位置。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# fail-fast与fail-safe有什么区别？

> 原文：[https://zwmst.com/1744.html](https://zwmst.com/1744.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:22:19+08:00"> 2021-08-15 </time> ](https://zwmst.com/1744.html)  Iterator的fail-fast属性与当前的集合共同起作用，因此它不会受到集合中任何改动的影响。 Java.util包中的所有集合类都被设计为fail-fast的，而java.util.concurrent中的集合类都为 fail-safe的。Fail-fast迭代器抛出ConcurrentModificationException，而fail-safe迭代器 从不抛出ConcurrentModificationException。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# hashCode()和equals()方法有何重要性？

> 原文：[https://zwmst.com/1746.html](https://zwmst.com/1746.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:22:30+08:00"> 2021-08-15 </time> ](https://zwmst.com/1746.html)  HashMap使用Key对象的hashCode()和equals()方法去决定key-value对的索引。当我们试 着从HashMap中获取值的时候，这些方法也会被用到。如果这些方法没有被正确地实现，在 这种情况下，两个不同Key也许会产生相同的hashCode()和equals()输出，HashMap将会认 为它们是相同的，然后覆盖它们，而非把它们存储到不同的地方。同样的，所有不允许存储重 复数据的集合类都使用hashCode()和equals()去查找重复，所以正确实现它们非常重要。 equals()和hashCode()的实现应该遵循以下规则：

（1）如果o1.equals(o2)，那么o1.hashCode() == o2.hashCode()总是为true的。

（2）如果o1.hashCode() == o2.hashCode()，并不意味着o1.equals(o2)会为true。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 我们能否使用任何类作为Map的key？

> 原文：[https://zwmst.com/1748.html](https://zwmst.com/1748.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:22:42+08:00"> 2021-08-15 </time> ](https://zwmst.com/1748.html)  我们可以使用任何类作为Map的key，然而在使用它们之前，需要考虑以下几点：

（1）如果类重写了equals()方法，它也应该重写hashCode()方法。

（2）类的所有实例需要遵循与equals()和hashCode()相关的规则。请参考之前提到的这些规 则。

（3）如果一个类没有使用equals()，你不应该在hashCode()中使用它。

（4）用户自定义key类的最佳实践是使之为不可变的，这样，hashCode()值可以被缓存起 来，拥有更好的性能。不可变的类也可以确保hashCode()和equals()在未来不会改变，这样 就会解决与可变相关的问题了。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 如何决定选用HashMap还是TreeMap？

> 原文：[https://zwmst.com/1750.html](https://zwmst.com/1750.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:22:57+08:00"> 2021-08-15 </time> ](https://zwmst.com/1750.html)  对于在Map中插入、删除和定位元素这类操作，HashMap是最好的选择。然而，假如你需要 对一个有序的key集合进行遍历，TreeMap是更好的选择。基于你的collection的大小，也许 向HashMap中添加元素会更快，将map换为TreeMap进行有序key的遍历。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 哪些集合类提供对元素的随机访问？

> 原文：[https://zwmst.com/1752.html](https://zwmst.com/1752.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:23:11+08:00"> 2021-08-15 </time> ](https://zwmst.com/1752.html)  ArrayList、HashMap、TreeMap和HashTable类提供对元素的随机访问。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# BlockingQueue是什么？

> 原文：[https://zwmst.com/1754.html](https://zwmst.com/1754.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:23:22+08:00"> 2021-08-15 </time> ](https://zwmst.com/1754.html)  Java.util.concurrent.BlockingQueue是一个队列，在进行检索或移除一个元素的时候，它会 等待队列变为非空；当在添加一个元素时，它会等待队列中的可用空间。BlockingQueue接口 是Java集合框架的一部分，主要用于实现生产者-消费者模式。我们不需要担心等待生产者有 可用的空间，或消费者有可用的对象，因为它都在BlockingQueue的实现类中被处理了。Java 提供了集中BlockingQueue的实现，比如ArrayBlockingQueue、LinkedBlockingQueue、 PriorityBlockingQueue,、SynchronousQueue等。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 队列和栈是什么，列出它们的区别？

> 原文：[https://zwmst.com/1756.html](https://zwmst.com/1756.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:23:36+08:00"> 2021-08-15 </time> ](https://zwmst.com/1756.html)  栈和队列两者都被用来预存储数据。java.util.Queue是一个接口，它的实现类在Java并发包 中。队列允许先进先出（FIFO）检索元素，但并非总是这样。

Deque接口允许从两端检索元 素。

栈与队列很相似，但它允许对元素进行后进先出（LIFO）进行检索。

Stack是一个扩展自Vector的类，而Queue是一个接口。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Collections类是什么？

> 原文：[https://zwmst.com/1758.html](https://zwmst.com/1758.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:23:49+08:00"> 2021-08-15 </time> ](https://zwmst.com/1758.html)  Java.util.Collections是一个工具类仅包含静态方法，它们操作或返回集合。它包含操作集合 的多态算法，返回一个由指定集合支持的新集合和其它一些内容。这个类包含集合框架算法的 方法，比如折半搜索、排序、混编和逆序等。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Comparable和Comparator接口有何区别？

> 原文：[https://zwmst.com/1760.html](https://zwmst.com/1760.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-08-15T16:24:01+08:00"> 2021-08-15 </time> ](https://zwmst.com/1760.html)  Comparable和Comparator接口被用来对对象集合或者数组进行排序。Comparable接口被 用来提供对象的自然排序，我们可以使用它来提供基于单个逻辑的排序。

Comparator接口被用来提供不同的排序算法，我们可以选择需要使用的Comparator来对给 定的对象集合进行排序。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 56.接口继承关系和实现

> 原文：[https://zwmst.com/3010.html](https://zwmst.com/3010.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-09-14T23:40:13+08:00"> 2021-09-14 </time> ](https://zwmst.com/3010.html)  集合类存放于 Java.util 包中，主要有 3 种：set(集）、list(列表包含 Queue）和 map(映射)。

1.  Collection：Collection 是集合 List、Set、Queue 的最基本的接口。
2.  Iterator：迭代器，可以通过迭代器遍历集合中的数据
3.  Map：是映射表的基础接口*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 57.List

> 原文：[https://zwmst.com/3012.html](https://zwmst.com/3012.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-09-14T23:46:46+08:00"> 2021-09-14 </time> ](https://zwmst.com/3012.html)  Java 的 List 是非常常用的数据类型。List 是有序的 Collection。Java List 一共三个实现类：分别是 ArrayList、Vector 和 LinkedList。

1.  ArrayList（数组）
    ArrayList 是最常用的 List 实现类，内部是通过数组实现的，它允许对元素进行快速随机访问。数组的缺点是每个元素之间不能有间隔，**当数组大小不满足时需要增加存储能力，就要将已经有数组的数据复制到新的存储空间中。当从 ArrayList 的中间位置插入或者删除元素时，需要对数组进行复制、移动、代价比较高。因此，它适合随机查找和遍历，不适合插入和删除**。

2.  Vector（数组实现、线程同步）
    Vector 与 ArrayList 一样，也是通过数组实现的，不同的是**它支持线程的同步，即某一时刻只有一个线程能够写 Vector**，避免多线程同时写而引起的不一致性，但实现同步需要很高的花费，因此，访问它比访问 ArrayList 慢。

3.  LinkList（链表）
    **LinkedList 是用链表结构存储数据的，很适合数据的动态插入和删除**，随机访问和遍历速度比较慢。另外，他还提供了 List 接口中没有定义的方法，专门用于操作表头和表尾元素，可以当作堆栈、队列和双向队列使用。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 58.Set

> 原文：[https://zwmst.com/3014.html](https://zwmst.com/3014.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-09-14T23:52:43+08:00"> 2021-09-14 </time> ](https://zwmst.com/3014.html)  Set 注重独一无二的性质,该体系集合用于存储无序(存入和取出的顺序不一定相同)元素，值不能重复。对象的相等性本质是对象 hashCode 值（java 是依据对象的内存地址计算出的此序号）判断的，如果想要让两个不同的对象视为相等的，就必须覆盖 Object 的 hashCode 方法和 equals 方法。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 59.HashSet（Hash 表）

> 原文：[https://zwmst.com/3018.html](https://zwmst.com/3018.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-09-15T00:00:41+08:00"> 2021-09-14 </time> ](https://zwmst.com/3018.html)  哈希表边存放的是哈希值。HashSet 存储元素的顺序并不是按照存入时的顺序（和 List 显然不同） 而是按照哈希值来存的所以取数据也是按照哈希值取得。元素的哈希值是通过元素的hashcode 方法来获取的, **HashSet 首先判断两个元素的哈希值，如果哈希值一样，接着会比较equals 方法 如果 equls 结果为 true ，HashSet 就视为同一个元素。如果 equals 为 false 就不是同一个元素**。

哈希值相同 equals 为 false 的元素是怎么存储呢,就是在同样的哈希值下顺延（可以认为哈希值相同的元素放在一个哈希桶中）。也就是哈希一样的存一列。如图 1 表示 hashCode 值不相同的情况；图 2 表示 hashCode 值相同，但 equals 不相同的情况。
![](img/2617297a9d0b0be24f6ac0d631511c73.png)
HashSet 通过 hashCode 值来确定元素在内存中的位置。**一个 hashCode 位置上可以存放多个元素**。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 60.TreeSet（二叉树）

> 原文：[https://zwmst.com/3021.html](https://zwmst.com/3021.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-09-15T00:01:37+08:00"> 2021-09-14 </time> ](https://zwmst.com/3021.html)  1.  TreeSet()是使用二叉树的原理对新 add()的对象按照指定的顺序排序（升序、降序），每增加一个对象都会进行排序，将对象插入的二叉树指定的位置。
2.  Integer 和 String 对象都可以进行默认的 TreeSet 排序，而自定义类的对象是不可以的，自己定义的类必须实现 Comparable 接口，并且覆写相应的 compareTo()函数，才可以正常使用。
3.  在覆写 compare()函数时，要返回相应的值才能使 TreeSet 按照一定的规则来排序
4.  比较此对象与指定对象的顺序。如果该对象小于、等于或大于指定对象，则分别返回负整数、零或正整数。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 61.LinkHashSet（HashSet+LinkedHashMap）

> 原文：[https://zwmst.com/3023.html](https://zwmst.com/3023.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-09-15T00:03:09+08:00"> 2021-09-14 </time> ](https://zwmst.com/3023.html)  对于 LinkedHashSet 而言，它继承与 HashSet、又基于LinkedHashMap 来实现的。LinkedHashSet 底层使用LinkedHashMap 来保存所有元素，它继承与 HashSet，其所有的方法操作上又与 HashSet 相同，因此 LinkedHashSet 的实现上非常简单，只提供了四个构造方法，并通过传递一个标识参数，调用父类的构造器，底层构造一个 LinkedHashMap 来实现，在相关操作上与父类 HashSet 的操作相同，直接调用父类 HashSet 的方法即可。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 62.HashMap（数组+链表+红黑树）

> 原文：[https://zwmst.com/3025.html](https://zwmst.com/3025.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-09-15T00:06:31+08:00"> 2021-09-14 </time> ](https://zwmst.com/3025.html)  HashMap 根据键的 hashCode 值存储数据，大多数情况下可以直接定位到它的值，因而具有很快的访问速度，但遍历顺序却是不确定的。 HashMap 最多只允许一条记录的键为 null，允许多条记录的值为 null。HashMap 非线程安全，即任一时刻可以有多个线程同时写 HashMap，可能会导致数据的不一致。如果需要满足线程安全，可以用 Collections 的synchronizedMap 方法使HashMap 具有线程安全的能力，或者使用ConcurrentHashMap。

1.  JAVA7 实现
    大方向上，HashMap 里面是一个数组，然后数组中每个元素是一个单向链表。上图中，每个绿色的实体是嵌套类 Entry 的实例，Entry 包含四个属性：**key, value, hash 值和用于单向链表的 next**。

    1.  capacity：当前数组容量，始终保持 2^n，可以扩容，扩容后数组大小为当前的 2 倍。
    2.  loadFactor：负载因子，默认为 0.75。
    3.  threshold：扩容的阈值，等于 capacity * loadFactor
2.  JAVA8 实现
    Java8 对 HashMap 进行了一些修改，最大的不同就是利用了红黑树，所以其由 **数组+链表+红黑树** 组成。

    根据 Java7 HashMap 的介绍，我们知道，查找的时候，根据 hash 值我们能够快速定位到数组的具体下标，但是之后的话，**需要顺着链表一个个比较下去才能找到我们需要的，时间复杂度取决于链表的长度，为 O(n)**。为了降低这部分的开销，在 Java8 中，当链表中的元素超过了 8 个以后，会将链表转换为红黑树，在这些位置进行查找的时候可以降低时间复杂度为 O(logN)。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 63.ConcurrentHashMap

> 原文：[https://zwmst.com/3027.html](https://zwmst.com/3027.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-09-15T00:09:32+08:00"> 2021-09-14 </time> ](https://zwmst.com/3027.html)  1.  Segment 段
    ConcurrentHashMap 和 HashMap 思路是差不多的，但是因为它支持并发操作，所以要复杂一些。整个 ConcurrentHashMap 由一个个 Segment 组成，Segment 代表”部分“或”一段“的意思，所以很多地方都会将其描述为分段锁。注意，行文中，我很多地方用了“槽”来代表一个segment。

2.  线程安全（Segment 继承 ReentrantLock 加锁）
    简单理解就是，ConcurrentHashMap 是一个 Segment 数组，Segment 通过继承ReentrantLock 来进行加锁，所以每次需要加锁的操作锁住的是一个 segment，这样只要保证每个 Segment 是线程安全的，也就实现了全局的线程安全。

3.  并行度（默认 16）
    concurrencyLevel：并行级别、并发数、Segment 数，怎么翻译不重要，理解它。默认是 16，也就是说 **ConcurrentHashMap 有 16 个 Segments**，所以理论上，这个时候，最多可以同时支持 16 个线程并发写，只要它们的操作分别分布在不同的 Segment 上。这个值可以在初始化的时候设置为其他值，但是一旦初始化以后，它是不可以扩容的。再具体到每个 Segment 内部，其实每个 Segment 很像之前介绍的 HashMap，不过它要保证线程安全，所以处理起来要麻烦些。

4.  Java8 实现 （引入了红黑树）
    Java8 对 ConcurrentHashMap 进行了比较大的改动,Java8 也引入了红黑树。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 64.HashTable（线程安全）

> 原文：[https://zwmst.com/3030.html](https://zwmst.com/3030.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-09-15T00:19:24+08:00"> 2021-09-14 </time> ](https://zwmst.com/3030.html)  Hashtable 是遗留类，很多映射的常用功能与 HashMap 类似，不同的是它承自 Dictionary 类，并且是线程安全的，任一时间只有一个线程能写 Hashtable，并发性不如 ConcurrentHashMap，因为 ConcurrentHashMap 引入了分段锁。Hashtable 不建议在新代码中使用，不需要线程安全的场合可以用 HashMap 替换，需要线程安全的场合可以用 ConcurrentHashMap 替换。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 65.TreeMap（可排序）

> 原文：[https://zwmst.com/3032.html](https://zwmst.com/3032.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-09-15T00:21:35+08:00"> 2021-09-14 </time> ](https://zwmst.com/3032.html)  TreeMap 实现 SortedMap 接口，能够把它保存的记录根据键排序，默认是按键值的升序排序，也可以指定排序的比较器，当用 Iterator 遍历 TreeMap 时，得到的记录是排过序的。如果使用排序的映射，建议使用 TreeMap。在使用 TreeMap 时，key 必须实现 Comparable 接口或者在构造 TreeMap 传入自定义的Comparator，否则会在运行时抛出java.lang.ClassCastException 类型的异常。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 66.LinkHashMap（记录插入顺序）

> 原文：[https://zwmst.com/3034.html](https://zwmst.com/3034.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-09-15T00:22:21+08:00"> 2021-09-14 </time> ](https://zwmst.com/3034.html)  LinkedHashMap 是 HashMap 的一个子类，保存了记录的插入顺序，在用 Iterator 遍历LinkedHashMap 时，先得到的记录肯定是先插入的，也可以在构造时带参数，按照访问次序排序。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 178.动态语言

> 原文：[https://zwmst.com/3294.html](https://zwmst.com/3294.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-09-18T01:11:20+08:00"> 2021-09-17 </time> ](https://zwmst.com/3294.html)  动态语言，是指程序在运行时可以改变其结构：新的函数可以引进，已有的函数可以被删除等结构上的变化。比如常见的 JavaScript 就是动态语言，除此之外 Ruby,Python 等也属于动态语言，而 C、C++则不属于动态语言。从反射角度说 JAVA 属于半动态语言。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 855.ArrayList 和 Vector 的区别。

> 原文：[https://zwmst.com/4973.html](https://zwmst.com/4973.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T22:21:28+08:00"> 2021-10-14 </time> ](https://zwmst.com/4973.html)  这两个类都实现了 List 接口（List 接口继承了 Collection 接口），他们都是有序集合，即存储在这两个集合中的元素的位置都是有顺序的，相当于一种动态的数组，我们以后可以按位置索引号取出某个元素，并且其中的数据是允许重复的，这是HashSet 之类的集合的最大不同处，HashSet 之类的集合不可以按索引号去检索其中的元素，也不允许有重复的元素（本来题目问的与 hashset 没有任何关系，但为了说清楚 ArrayList 与 Vector 的功能，我们使用对比方式，更有利于说明问题）。接着才说 ArrayList 与 Vector 的区别，这主要包括两个方面。

1.  同步性：
    Vector 是线程安全的，也就是说是它的方法之间是线程同步的，而 ArrayList 是线程序不安全的，它的方法之间是线程不同步的。如果只有一个线程会访问到集合，那最好是使用 ArrayList，因为它不考虑线程安全，效率会高些；如果有多个线程会访问到集合，那最好是使用 Vector，因为不需要我们自己再去考虑和编写线程安全的代码。
    **备注**：对于 Vector&ArrayList、Hashtable&HashMap，要记住线程安全的问题，记住 Vector 与 Hashtable 是旧的，是 java 一诞生就提供了的，它们是线程安全的，ArrayList 与 HashMap 是 java2 时才提供的，它们是线程不安全的。所以，我们讲课时先讲老的。
2.  数据增长：
    ArrayList 与 Vector 都有一个初始的容量大小，当存储进它们里面的元素的个数超过了容量时，就需要增加 ArrayList 与 Vector 的存储空间，每次要增加存储空间时，不是只增加一个存储单元，而是增加多个存储单元，每次增加的存储单元的个数在内存空间利用与程序效率之间要取得一定的平衡。Vector 默认增长为原来两倍，而ArrayList 的增长策略在文档中没有明确规定（从源代码看到的是增长为原来的 1.5倍）。ArrayList 与 Vector 都可以设置初始的空间大小，Vector 还可以设置增长的空间大小，而 ArrayList 没有提供设置增长空间的方法。
    **总结：即 Vector 增长原来的一倍，ArrayList 增加原来的 0.5 倍。***
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 856.说说 ArrayList,Vector, LinkedList 的存储性能和特性。

> 原文：[https://zwmst.com/4975.html](https://zwmst.com/4975.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T22:40:05+08:00"> 2021-10-14 </time> ](https://zwmst.com/4975.html)  ArrayList 和 Vector 都是使用数组方式存储数据，此数组元素数大于实际存储的数据以便增加和插入元素，它们都允许直接按序号索引元素，但是插入元素要涉及数组元素移动等内存操作，所以索引数据快而插入数据慢，Vector 由于使用了
synchronized 方法（线程安全）。
通常性能上较 ArrayList 差，而 LinkedList 使用双向链表实现存储，按序号索引数据需要进行前向或后向遍历，但是插入数据时只需要记录本项的前后项即可，所以插入速度较快 。
ArrayList 在查找时速度快，LinkedList 在插入与删除时更具优势。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 857.快速失败 (fail-fast) 和安全失败 (fail-safe) 的区别是什么？

> 原文：[https://zwmst.com/4977.html](https://zwmst.com/4977.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T22:41:47+08:00"> 2021-10-14 </time> ](https://zwmst.com/4977.html)  Iterator 的安全失败是基于对底层集合做拷贝，因此，它不受源集合上修改的影响。
java.util 包下面的所有的集合类都是快速失败的，而 java.util.concurrent 包下面的所有的类都是安全失败的。快速失败的迭代器会抛出ConcurrentModificationException 异常，而安全失败的迭代器永远不会抛出这样的异常。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 858.hashmap 的数据结构。

> 原文：[https://zwmst.com/4979.html](https://zwmst.com/4979.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T22:42:48+08:00"> 2021-10-14 </time> ](https://zwmst.com/4979.html)  在 java 编程语言中，最基本的结构就是两种，一个是数组，另外一个是模拟指针（引用），所有的数据结构都可以用这两个基本结构来构造的，hashmap 也不例外。Hashmap 实际上是一个数组和链表的结合体（在数据结构中，一般称之为 “链表散列 “）*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 859.HashMap 的工作原理是什么?

> 原文：[https://zwmst.com/4981.html](https://zwmst.com/4981.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T22:43:42+08:00"> 2021-10-14 </time> ](https://zwmst.com/4981.html)  Java 中的 HashMap 是以键值对 (key-value) 的形式存储元素的。HashMap 需要一个 hash 函数，它使用 hashCode()和 equals()方法来向集合 / 从集合添加和检索元素。当调用 put() 方法的时候，HashMap 会计算 key 的 hash 值，然后把键值对存储在集合中合适的索引上。 如果 key 已经存在了，value 会被更新成新值。HashMap 的一些重要的特性是它的容量 (capacity)，负载因子 (load factor) 和扩容极限(threshold resizing)。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 860.Hashmap 什么时候进行扩容呢？

> 原文：[https://zwmst.com/4983.html](https://zwmst.com/4983.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T22:45:36+08:00"> 2021-10-14 </time> ](https://zwmst.com/4983.html)  当 hashmap 中的元素个数超过数组大小 loadFactor 时，就会进行数组扩容，loadFactor 的默认值为 0.75，也就是说，默认情况下，数组大小为 16，那么当hashmap 中元素个数超过 160.75=12 的时候，就把数组的大小扩展为 216=32，即扩大一倍，然后重新计算每个元素在数组中的位置，而这是一个非常消耗性能的操作，所以如果我们已经预知 hashmap 中元素的个数，那么预设元素的个数能够有效的提高 hashmap 的性能。比如说，我们有 1000 个元素 new HashMap(1000),但是理论上来讲 new HashMap(1024) 更合适，不过上面 annegu 已经说过，即使是 1000，hashmap 也自动会将其设置为 1024。 但是 new HashMap(1024) 还不是更合适的，因为 0.75*1000 < 1000, 也就是说为了让 0.75* size > 1000, 我们必须这样 new HashMap(2048) 才最合适，既考虑了 & 的问题，也避免了 resize的问题。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 861.List、Map、Set 三个接口，存取元素时，各有什么特点？

> 原文：[https://zwmst.com/4985.html](https://zwmst.com/4985.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T22:53:58+08:00"> 2021-10-14 </time> ](https://zwmst.com/4985.html)  这样的题属于随意发挥题：这样的题比较考水平，两个方面的水平：一是要真正明白
这些内容，二是要有较强的总结和表述能力。如果你明白，但表述不清楚，在别人那
里则等同于不明白。
首先，List 与 Set 具有相似性，它们都是单列元素的集合，所以，它们有一个功共同
的父接口，叫 Collection。Set 里面不允许有重复的元素，所谓重复，即不能有两个
相等（注意，不是仅仅是相同）的对象 ，即假设 Set 集合中有了一个 A 对象，现在
我要向 Set 集合再存入一个 B 对象，但 B 对象与 A 对象 equals 相等，则 B 对
象存储不进去，所以，Set 集合的 add 方法有一个 boolean 的返回值，当集合中
没有某个元素，此时 add 方法可成功加入该元素时，则返回 true，当集合含有与某
个元素 equals 相等的元素时，此时 add 方法无法加入该元素，返回结果为 false。
Set 取元素时，没法说取第几个，只能以 Iterator 接口取得所有的元素，再逐一遍历
各个元素。
List 表示有先后顺序的集合， 注意，不是那种按年龄、按大小、按价格之类的排序。
当我们多次调用 add(Obj e) 方法时，每次加入的对象就像火车站买票有排队顺序一样，按先来后到的顺序排序。有时候，也可以插队，即调用 add(int index,Obj e) 方法，就可以指定当前对象在集合中的存放位置。一个对象可以被反复存储进 List 中，每调用一次 add 方法，这个对象就被插入进集合中一次，其实，并不是把这个对象本身存储进了集合中，而是在集合中用一个索引变量指向这个对象，当这个对象被add 多次时，即相当于集合中有多个索引指向了这个对象，如图 x 所示。List 除了可以以 Iterator 接口取得所有的元素，再逐一遍历各个元素之外，还可以调用get(index i) 来明确说明取第几个。
Map 与 List 和 Set 不同，它是双列的集合，其中有 put 方法，定义如下：put(obj key,obj value)，每次存储时，要存储一对 key/value，不能存储重复的key，这个重复的规则也是按 equals 比较相等。取则可以根据 key 获得相应的value，即 get(Object key) 返回值为 key 所对应的 value。另外，也可以获得所有的 key 的结合，还可以获得所有的 value 的结合，还可以获得 key 和 value 组合成的 Map.Entry 对象的集合。
List 以特定次序来持有元素，可有重复元素。Set 无法拥有重复元素, 内部排序。
Map 保存 key-value 值，value 可多值。
HashSet 按照 hashcode 值的某种运算方式进行存储，而不是直接按 hashCode值的大小进行存储。例如，"abc" —> 78，"def" —> 62，"xyz" —> 65 在hashSet 中的存储顺序不是 62,65,78，这些问题感谢以前一个叫崔健的学员提出，最后通过查看源代码给他解释清楚，看本次培训学员当中有多少能看懂源码。LinkedHashSet 按插入的顺序存储，那被存储对象的 hashcode 方法还有什么作用呢？学员想想! hashset 集合比较两个对象是否相等，首先看 hashcode 方法是否相等，然后看 equals 方法是否相等。new 两个 Student 插入到 HashSet 中，看HashSet 的 size，实现 hashcode 和 equals 方法后再看 size。
同一个对象可以在 Vector 中加入多次。往集合里面加元素，相当于集合里用一根绳子连接到了目标对象。往 HashSet 中却加不了多次的。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 862.Set 里的元素是不能重复的，那么用什么方法来区分重复与否呢? 是用 == 还是 equals()? 它们有何区别?

> 原文：[https://zwmst.com/4987.html](https://zwmst.com/4987.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T23:00:27+08:00"> 2021-10-14 </time> ](https://zwmst.com/4987.html)  Set 里的元素是不能重复的，元素重复与否是使用 equals() 方法进行判断的。
equals() 和 == 方法决定引用值是否指向同一对象 equals() 在类中被覆盖，为的是当两个分离的对象的内容和类型相配的话，返回真值。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 863.两个对象值相同 (x.equals(y) == true)，但却可有不同的 hash code，这句话对不对?

> 原文：[https://zwmst.com/4989.html](https://zwmst.com/4989.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T23:18:11+08:00"> 2021-10-14 </time> ](https://zwmst.com/4989.html)  对。如果对象要保存在 HashSet 或 HashMap 中，它们的 equals 相等，那么，它们的 hashcode 值就必须相等。
如果不是要保存在 HashSet 或 HashMap，则与 hashcode 没有什么关系了，这时候 hashcode 不等是可以的，例如 arrayList 存储的对象就不用实现 hashcode，当然，我们没有理由不实现，通常都会去实现的。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 864.heap 和 stack 有什么区别。

> 原文：[https://zwmst.com/4991.html](https://zwmst.com/4991.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T23:19:01+08:00"> 2021-10-14 </time> ](https://zwmst.com/4991.html)  Java 的内存分为两类，一类是栈内存，一类是堆内存。栈内存是指程序进入一个方法时，会为这个方法单独分配一块私属存储空间，用于存储这个方法内部的局部变量，当这个方法结束时，分配给这个方法的栈会释放，这个栈中的变量也将随之释放。
堆是与栈作用不同的内存，一般用于存放不放在当前方法栈中的那些数据，例如，使用 new 创建的对象都放在堆里，所以，它不会随方法的结束而消失。方法中的局部变量使用 final 修饰后，放在堆中，而不是栈中。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 865.Java 集合类框架的基本接口有哪些？

> 原文：[https://zwmst.com/4993.html](https://zwmst.com/4993.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T23:21:36+08:00"> 2021-10-14 </time> ](https://zwmst.com/4993.html)  集合类接口指定了一组叫做元素的对象。集合类接口的每一种具体的实现类都可以选择以它 自己的方式对元素进行保存和排序。有的集合类允许重复的键，有些不允许。
Java 集合类提供了一套设计良好的支持对一组对象进行操作的接口和类。Java 集合类里面 最基本的接口有：
**Collection**：代表一组对象，每一个对象都是它的子元素。
**Set**：不包含重复元素的 Collection。
**List**：有顺序的 collection，并且可以包含重复元素。
**Map**：可以把键 (key) 映射到值 (value) 的对象，键不能重复。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 866.HashSet 和 TreeSet 有什么区别？

> 原文：[https://zwmst.com/4995.html](https://zwmst.com/4995.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T23:22:37+08:00"> 2021-10-14 </time> ](https://zwmst.com/4995.html)  HashSet 是由一个 hash 表来实现的，因此，它的元素是无序的。add()，remove()，contains()
TreeSet 是由一个树形的结构来实现的，它里面的元素是有序的。因此，add()，remove()，contains() 方法的时间复杂度是 O(logn)。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 867.HashSet 的底层实现是什么?

> 原文：[https://zwmst.com/4997.html](https://zwmst.com/4997.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T23:23:27+08:00"> 2021-10-14 </time> ](https://zwmst.com/4997.html)  通过看源码知道 HashSet 的实现是依赖于 HashMap 的，HashSet 的值都是存储在 HashMap 中的。在 HashSet 的构造法中会初始化一个 HashMap 对象，HashSet 不允许值重复，因此，HashSet 的值是作为 HashMap 的 key 存储在HashMap 中的，当存储的值已经存在时返回 false。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 868.LinkedHashMap 的实现原理?

> 原文：[https://zwmst.com/4999.html](https://zwmst.com/4999.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T23:24:18+08:00"> 2021-10-14 </time> ](https://zwmst.com/4999.html)  LinkedHashMap 也是基于 HashMap 实现的，不同的是它定义了一个 Entryheader，这个 header 不是放在 Table 里，它是额外独立出来的。
LinkedHashMap 通过继承 hashMap 中的 Entry, 并添加两个属性 Entrybefore,after, 和 header 结合起来组成一个双向链表，来实现按插入顺序或访问顺序排序。LinkedHashMap 定义了排序模式 accessOrder，该属性为 boolean 型变量，对于访问顺序，为 true；对于插入顺序，则为 false。一般情况下，不必指定排序模式，其迭代顺序即为默认为插入顺序。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 869.为什么集合类没有实现 Cloneable 和 Serializable 接口？

> 原文：[https://zwmst.com/5001.html](https://zwmst.com/5001.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T23:24:59+08:00"> 2021-10-14 </time> ](https://zwmst.com/5001.html)  克隆 (cloning) 或者是序列化 (serialization) 的语义和含义是跟具体的实现相关的。
因此，应该 由集合类的具体实现来决定如何被克隆或者是序列化。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 870.什么是迭代器 (Iterator)？

> 原文：[https://zwmst.com/5003.html](https://zwmst.com/5003.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T23:26:02+08:00"> 2021-10-14 </time> ](https://zwmst.com/5003.html)  Iterator 接口提供了很多对集合元素进行迭代的方法。每一个集合类都包含了可以返回迭代 器实例的迭代方法。迭代器可以在迭代的过程中删除底层集合的元素, 但是不可以直接调用集合的 remove(Object Obj) 删除，可以通过迭代器的 remove() 方法删除。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 871.Iterator 和 ListIterator 的区别是什么？

> 原文：[https://zwmst.com/5005.html](https://zwmst.com/5005.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T23:28:49+08:00"> 2021-10-14 </time> ](https://zwmst.com/5005.html)  下面列出了他们的区别：
Iterator 可用来遍历 Set 和 List 集合，但是 ListIterator 只能用来遍历 List。
Iterator 对集合只能是前向遍历，ListIterator 既可以前向也可以后向。
ListIterator 实现了 Iterator 接口，并包含其他的功能，比如：增加元素，替换元素，获取前一个和后一个元素的索引，等等。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 872.数组 (Array) 和列表 (ArrayList) 有什么区别？什么时候应该使用 Array 而不是 ArrayList？

> 原文：[https://zwmst.com/5007.html](https://zwmst.com/5007.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T23:31:56+08:00"> 2021-10-14 </time> ](https://zwmst.com/5007.html)  Array 可以包含基本类型和对象类型，ArrayList 只能包含对象类型。
Array 大小是固定的，ArrayList 的大小是动态变化的。
ArrayList 处理固定大小的基本数据类型的时候，这种方式相对比较慢。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 873.Java 集合类框架的最佳实践有哪些？

> 原文：[https://zwmst.com/5009.html](https://zwmst.com/5009.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T23:33:32+08:00"> 2021-10-14 </time> ](https://zwmst.com/5009.html)  1.  假如元素的大小是固 定的，而且能事先知道，我们就应该用 Array 而不是ArrayList。
2.  有些集合类允许指定初始容量。因此，如果我们能估计出存储的元素的数目，我们可以设置 初始容量来避免重新计算 hash 值或者是扩容。
3.  为了类型安全，可读性和健壮性的原因总是要使用泛型。同时，使用泛型还可以避免运行时的 ClassCastException。
4.  使用 JDK 提供的不变类 (immutable class) 作为 Map 的键可以避免为我们自己的类实现 hashCode()和 equals()方法。
5.  编程的时候接口优于实现。
6.  底层的集合实际上是空的情况下，返回长度是 0 的集合或者是数组，不要返回 null。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 874.Set 里的元素是不能重复的，那么用什么方法来区分重复与否呢？是用 == 还是 equals()？它们有何区别？

> 原文：[https://zwmst.com/5011.html](https://zwmst.com/5011.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T23:34:46+08:00"> 2021-10-14 </time> ](https://zwmst.com/5011.html)  Set 里的元素是不能重复的，那么用 iterator() 方法来区分重复与否。equals() 是判读两个 Set 是否相等equals() 和 == 方法决定引用值是否指向同一对象 equals() 在类中被覆盖，为的是当两个分离的对象的内容和类型相配的话，返回真值*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 875.Comparable 和 Comparator 接口是干什么的？列出它们的区别。

> 原文：[https://zwmst.com/5013.html](https://zwmst.com/5013.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T23:38:08+08:00"> 2021-10-14 </time> ](https://zwmst.com/5013.html)  Java 提供了只包含一个 compareTo() 方法的 Comparable 接口。这个方法可以个给两个对象排序。具体来说，它返回负数，0，正数来表明输入对象小于，等于，大于已经存在的对象。
Java 提供了包含 compare() 和 equals() 两个方法的 Comparator 接口。
compare() 方法用来给两个输入参数排序，返回负数，0，正数表明第一个参数是小于，等于，大于第二个参数。equals() 方法需要一个对象作为参数，它用来决定输入参数是否和 comparator 相等。只有当输入参数也是一个 comparator 并且输入参数和当前 comparator 的排序结果是相同的时 候，这个方法才返回 true。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 876.Collection 和 Collections 的区别。

> 原文：[https://zwmst.com/5015.html](https://zwmst.com/5015.html)

   [ *Java集合* ](https://zwmst.com/java%e9%9b%86%e5%90%88)*[ <time datetime="2021-10-14T23:39:03+08:00"> 2021-10-14 </time> ](https://zwmst.com/5015.html)  collection 是集合类的上级接口, 继承与它的接口主要是 set 和 list。
collections 类是针对集合类的一个帮助类. 它提供一系列的静态方法对各种集合的搜索, 排序, 线程安全化等操作*
<!--yml
category: Java
date: 2022-11-19 13:21:34
-->

# Java基础面试指南一（zthinker）

> 来源：[https://zthinker.com/archives/java-basic-interview-1](https://zthinker.com/archives/java-basic-interview-1)

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

当今世界上使用最广泛的编程语言之一是Java。Java是通用的高级编程语言。核心java是java编程技术概念的基础,该术语由sun Microsystems用来描述Java的标准版本(JSE)。核心Java只是Java的一部分,它代表J2SE,其中包含Java的所有基础知识,包括一些原理和软件包详细信息。Java核心概念涵盖了所有OOPS概念,特殊运算符,数据类型,包装类,异常处理,多态性,多线程,链接列表,队列,堆栈,数组列表。它最常用于开发桌面应用程序和服务器环境(开发独立应用程序)。

JDK(Java开发工具包)是一个开发目的,它还包括执行环境。但是JVM纯粹是运行时环境,因此您将无法使用JVM编译源文件。

抽象化

多态性

继承

封装

多态被简要描述为“一个接口,许多实现”。多态性是能够在不同上下文中为某事物赋予不同含义或用法的一种特征-具体来说,就是允许诸如变量,函数或对象之类的实体具有多种形式。

内部类是嵌套在另一个类中的一个类。内部类具有对其嵌套的类的访问权限,并且可以访问在外部类中定义的所有变量和方法。

子类是从另一个称为超类的类继承的类。子类可以访问其父类的所有公共和受保护的方法以及字段。

在Java中,访问说明符是在定义访问范围的类名之前使用的关键字。类的访问说明符的类型为:

*   **public:**类,方法,字段可从任何地方访问。
*   **Protected::**方法,字段可以从它们所属的同一类或子类以及同一包的类中访问,但不能从外部访问。
*   **default:** Method,Field,class只能从同一程序包访问,而不能从其本机程序包外部访问。
*   **private:**方法,字段可以从它们所属的相同类中访问。

当需要在一个类的多个对象之间共享方法或变量,而不是为每个对象创建单独的副本时,我们使用static关键字使所有对象共享一个方法或变量。

没有

是的,派生类仍然可以覆盖重载的方法。多态仍然可能发生。编译器将不会绑定方法调用,因为它已被重载,因为它可能会在现在或将来被覆盖。

封装是面向对象编程中的一个概念,用于在单个单元中组合属性和方法。

封装可帮助程序员遵循模块化的方法进行软件开发,因为每个对象都有自己的一组方法和变量,并且其功能独立于其他对象。封装还用于数据隐藏。

Java中的单例类只能有一个实例,因此其所有方法和变量都只属于一个实例。单例类概念对于需要限制一个类的对象数量的情况很有用。

单例使用情况的最佳示例是,由于某些驱动程序限制或任何许可问题,只有一个数据库连接存在限制。

它是一个线程,不会阻止JVM在程序完成但该线程仍在运行时退出。守护程序线程的一个示例是垃圾回收。

循环在编程中用于重复执行一条语句或语句块。Java中有三种循环类型:

**for**

在Java中,for循环用于重复执行给定次数的语句。当程序员知道执行语句的次数时,将使用for循环。

**While循环**

当某些语句需要重复执行直到满足条件时,使用while循环。在while循环中,在执行语句之前先检查条件。

**do While**

Do While循环与while循环相同,只是执行语句块后检查条件的不同。因此,在do while循环的情况下,语句至少执行一次。

死锁描述了一种情况,其中两个或多个线程永远被阻塞,互相等待。

无限循环无条件运行,并且无限运行。通过在语句块的主体中​​定义任何中断逻辑,可以中断无限循环。

无限循环声明如下:

for(;;)

{

//要执行的语句

//添加任何循环中断逻辑

}

中断和继续是循环中使用的两个重要关键字。在循环中使用break关键字时,循环会立即中断,而在使用continue关键字时,当前迭代会中断,并且循环会继续进行下一次迭代。

在下面的示例中,当计数器达到4时,循环中断。

```
for (counter=0;counter
  System.out.println(counter);
  If (counter==4) {
    Break;
  }
} 
```

在下面的示例中,当计数器达到4时,循环会跳至tonext迭代,而continue关键字之后的所有语句都将跳过当前迭代。

```
for (counter=0;counter
  System.out.println(counter);
  If (counter==4) {
    continue;
  }
  System.outprintln(“This will not get printed when counter is 4”);
} 
```

在Java中,float占用4个字节的内存,而Double占用8个字节的内存。浮点数是单精度浮点十进制数,而双精度数是双精度十进制数。

javac从* .java文件生成Java字节码。它是您的源代码的中间表示,其中包含指示

在Java中,使用关键字Final声明一个常量。值只能分配一次,分配后不能更改常量的值。

在下面的示例中,声明了名称为const_val的常量,并为其分配了一个值:

```
private Final int const_val=100 
```

当一个方法声明为final方法时,它不能被子类覆盖。此方法比任何其他方法都快,因为它们在编译时已解决。

当一个类声明为final时,则不能将其子类化。示例String,Integer和其他包装器类。

三元运算符(也称为条件运算符)用于根据布尔值评估来决定将哪个值分配给变量。表示为?

在下面的示例中,如果等级为1,则为状态分配值“Done”,否则为“Pending”。

```
 public class conditionTest {

    public static void main(string args[]) {

        String status;

        int rank;

        status= (rank == 1) ? “Done”: “Pending”;

    }

} 
```

在Java中,运算符可以分为以下六种类型:

**算术运算符**

用于算术计算。例如**+,-,*,/,%,++,–**

**关系运算符**

用于关系比较。例如==,!=,>,<,<=,> =

**按位运算符**

用于逐位操作。例如&,|,^,〜

**逻辑运算符**

用于逻辑比较。例如&&,|| ,!

**赋值运算符**

用于为变量分配值。例如=,+ =,-=,* =,/ =

java.lang.object

在Java中,main()方法无法返回任何数据,因此,始终使用无效的返回类型进行声明。

在Java中,包是类和接口的集合,这些类和接口相互关联在一起,因此捆绑在一起。软件包的使用有助于开发人员对代码进行模块化,并对代码进行分组以进行适当的重用。将代码打包到Packages中之后,就可以将其导入其他类中并使用了。

是的,即使没有任何抽象方法,我们也可以在类名之前使用abstract关键字来创建一个抽象类。但是,如果一个类甚至具有一个抽象方法,则必须将其声明为抽象方法,否则将产生错误。

**堆内存**由应用程序的所有部分使用。每当创建对象时,它始终存储在堆空间中,并且堆栈存储器包含对该对象的引用。内存管理在Heap内存中更为复杂,因为它在全局范围内使用。

**堆栈存储器**仅由一个执行线程使用。堆栈内存仅包含局部原始变量和堆空间中对象的引用变量。堆栈中的内存管理以LIFO方式完成

抽象类和接口之间的主要区别在于,接口只能拥有没有具体实现的公共静态方法的声明,而抽象类可以具有带有或不带有具体实现的带有任何访问说明符(公共,私有等)的成员。

使用抽象类和接口的另一个主要区别是,实现接口的类必须实现接口的所有方法,而从抽象类继承的类则不需要实现其超类的所有方法。

一个类可以实现多个接口,但只能扩展一个抽象类。

与抽象类相比,接口的性能较慢,因为接口需要额外的间接调用。开发人员要考虑的另一个关键因素是,任何类只能扩展一个抽象类,而一个类可以实现许多接口。

每当在类中实现接口时,使用接口也给开发人员带来了额外的负担;开发人员被迫实现每种接口方法。

在Java中,当导入包时,不会导入其子包,并且如果需要,开发人员需要分别导入它们。

例如,如果开发人员导入了一个软件包university。*,则将装入名为university的软件包中的所有类,但不会装入该子软件包中的任何类。

在Java中,main方法必须是public static以便正确运行任何应用程序。如果将main方法声明为私有方法,则开发人员将不会获得任何编译错误,它将无法执行,并会给出运行时错误。

在Java中,我们只能通过值而不是通过引用将参数传递给函数。

在Java中,要通过序列化将对象转换为字节流,该类将实现一个名为Serializable的接口。实现可序列化接口的类的所有对象均被序列化,其状态保存在字节流中。

当需要通过网络传输数据时,使用串行化。使用序列化,可以保存对象的状态并将其转换为字节流。字节流通过网络传输,并且在目标位置重新创建对象。

尝试阻止之后,需要紧接着是Catch阻止,finally阻止或二者兼有。从try块引发的任何异常都需要捕获在catch块中,或者必须在代码中止之前将要执行的任何特定任务放入Final块中。

如果在Try块中引发异常,则控制传递到catch块(如果存在),否则传递到finally块。当发生异常时,总是执行finally块,避免在finally块中执行任何语句的唯一方法是通过在try块的末尾编写以下代码行来强行中止代码:

System.exit(0);

是的,一个类可以具有多个带有不同参数的构造函数。用于创建对象的构造函数取决于创建对象时传递的参数。

当您在子类中重写方法时,可以使用super关键字来访问该方法。

我们不能覆盖静态方法。静态方法属于一个类,而不属于单个对象,并且在编译时(而不是在运行时)解析。即使我们尝试覆盖静态方法,也不会遇到编译错误,也不会在运行代码时产生覆盖的影响。

```
public class superclass {
    public void displayResult() {
        System.out.println(“Printing from superclass”);
    }
}

public class subclass extends superclass {

    public void displayResult() {

        System.out.println(“Displaying from subClass”);

        super.displayResult();

    }

    public static void main(String args[]) {

        subclass obj=new subclass();

        obj.displayResult();

    }

}

Output will be:

Displaying from subclass

Displaying from superclass 
```

字符串不是Java中的原始数据类型。在Java中创建字符串时,它实际上是创建的Java.Lang.String类的对象。创建此字符串对象后,可以在该字符串对象上使用String类的所有内置方法。
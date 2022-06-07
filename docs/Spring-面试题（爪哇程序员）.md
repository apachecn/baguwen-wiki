<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是spring?

> 原文：[https://zwmst.com/1838.html](https://zwmst.com/1838.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:40:03+08:00"> 2021-08-15 </time> ](https://zwmst.com/1838.html)  Spring 是个java企业级应用的开源开发框架。Spring主要用来开发Java应用，但是有些扩展 是针对构建J2EE平台的web应用。Spring 框架目标是简化Java企业级应用开发，并通过POJO 为基础的编程模型促进良好的编程习惯。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 使用Spring框架的好处是什么？

> 原文：[https://zwmst.com/1840.html](https://zwmst.com/1840.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:40:14+08:00"> 2021-08-15 </time> ](https://zwmst.com/1840.html)  轻量：Spring 是轻量的，基本的版本大约2MB。

控制反转：Spring通过控制反转实现了松散耦合，对象们给出它们的依赖，而不是创建 或查找依赖的对象们。

面向切面的编程(AOP)：Spring支持面向切面的编程，并且把应用业务逻辑和系统服务 分开。

容器：Spring 包含并管理应用中对象的生命周期和配置。

MVC框架：Spring的WEB框架是个精心设计的框架，是Web框架的一个很好的替代 品。 事务管理：Spring 提供一个持续的事务管理接口，可以扩展到上至本地事务下至全局事 务（JTA）。

异常处理：Spring 提供方便的API把具体技术相关的异常（比如由JDBC，Hibernate or JDO抛出的）转化为一致的unchecked 异常。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring由哪些模块组成?

> 原文：[https://zwmst.com/1842.html](https://zwmst.com/1842.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:40:25+08:00"> 2021-08-15 </time> ](https://zwmst.com/1842.html)  以下是Spring 框架的基本模块：

Core module

Bean module

Context module

Expression Language module

JDBC module

ORM module

OXM module

Java Messaging Service(JMS) module

Transaction module

Web module

Web-Servlet module

Web-Struts module

Web-Portlet module*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring是怎么解决循环依赖的？

> 原文：[https://zwmst.com/1844.html](https://zwmst.com/1844.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:40:36+08:00"> 2021-08-15 </time> ](https://zwmst.com/1844.html)  整个IOC容器解决循环依赖，用到的几个重要成员： singletonObjects：一级缓存，存放完全初始化好的Bean的集合，从这个集合中取出来的 Bean可以立马返回 earlySingletonObjects：二级缓存，存放创建好但没有初始化属性的Bean的集合，它用来解 决循环依赖 singletonFactories：三级缓存，存放单实例Bean工厂的集合 singletonsCurrentlyInCreation：存放正在被创建的Bean的集合

IOC容器解决循环依赖的思路：

1.  初始化Bean之前，将这个BeanName放入三级缓存

2.  创建Bean将准备创建的Bean放入 singletonsCurrentlyInCreation （正在创建的 Bean）

3.  createNewInstance 方法执行完后执行 addSingletonFactory，将这个实例化但没有 属性赋值的Bean放入二级缓存，并从三级缓存中移除

4.  属性赋值&自动注入时，引发关联创建

5.  关联创建时，检查“正在被创建的Bean”中是否有即将注入的Bean。如果有，检查二级 缓存中是否有当前创建好但没有赋值初始化的Bean。如果没有，检查三级缓存中是否有 正在创建中的Bean。至此一般会有，将这个Bean放入二级缓存，并从三级缓存中移除

6.  之后Bean被成功注入，最后执行 addSingleton，将这个完全创建好的Bean放入一级缓 存，从二级缓存和三级缓存移除，并记录已经创建了的单实例Bean*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring Boot手动装配有哪几种方式？

> 原文：[https://zwmst.com/1846.html](https://zwmst.com/1846.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:40:49+08:00"> 2021-08-15 </time> ](https://zwmst.com/1846.html)  1.  使用模式注解 @Component 等（Spring2.5+）

2.  使用配置类 @Configuration 与 @Bean （Spring3.0+）

3.  使用模块装配 @EnableXXX 与 @Import （Spring3.1+）

其中使用 @Component 及衍生注解很常见，咱开发中常用的套路，不再赘述。

但模式注解只能在自己编写的代码中标注，无法装配jar包中的组件。

为此可以使用 @Configuration 与 @Bean，手动装配组件。

但这种方式一旦注册过多，会导致编码成本高，维护不灵活等问题。

SpringFramework 提供了模块装配功能，通过给配置类标注 @EnableXXX 注解，再在注解 上标注 @Import 注解，即可完成组件装配的效果。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 谈谈自己对于Spring IOC的理解

> 原文：[https://zwmst.com/1850.html](https://zwmst.com/1850.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:41:55+08:00"> 2021-08-15 </time> ](https://zwmst.com/1850.html)  IOC（Inversion Of Controll，控制反转）是一种设计思想，就是将原本在程序中手动创建对 象的控制权，交由给Spring框架来管理。IOC在其他语言中也有应用，并非Spring特有。IOC 容器是Spring用来实现IOC的载体，IOC容器实际上就是一个Map(key, value)，Map中存放 的是各种对象。

将对象之间的相互依赖关系交给IOC容器来管理，并由IOC容器完成对象的注入。这样可以很 大程度上简化应用的开发，把应用从复杂的依赖关系中解放出来。IOC容器就像是一个工厂一 样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可，完全不用考虑对象是 如何被创建出来的。在实际项目中一个Service类可能由几百甚至上千个类作为它的底层，假 如我们需要实例化这个Service，可能要每次都搞清楚这个Service所有底层类的构造函数，这 可能会把人逼疯。如果利用IOC的话，你只需要配置好，然后在需要的地方引用就行了，大大增加了项目的可维护性且降低了开发难度。

Spring时代我们一般通过XML文件来配置Bean，后来开发人员觉得用XML文件来配置不太 好，于是Sprng Boot注解配置就慢慢开始流行起来。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring AOP和AspectJ AOP有什么区别？

> 原文：[https://zwmst.com/1853.html](https://zwmst.com/1853.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:42:07+08:00"> 2021-08-15 </time> ](https://zwmst.com/1853.html)  Spring AOP是属于运行时增强，而AspectJ是编译时增强。Spring AOP基于代理 （Proxying），而AspectJ基于字节码操作（Bytecode Manipulation）。

Spring AOP已经集成了AspectJ，AspectJ应该算得上是Java生态系统中最完整的AOP框架 了。AspectJ相比于Spring AOP功能更加强大，但是Spring AOP相对来说更简单。

如果我们的切面比较少，那么两者性能差异不大。但是，当切面太多的话，最好选择 AspectJ，它比SpringAOP快很多。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 谈谈自己对于Spring AOP的理解

> 原文：[https://zwmst.com/1855.html](https://zwmst.com/1855.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:42:18+08:00"> 2021-08-15 </time> ](https://zwmst.com/1855.html)  AOP（Aspect-Oriented Programming，面向切面编程）能够将那些与业务无关，却为业务 模块所共同调用的逻辑或责任（例如事务处理、日志管理、权限控制等）封装起来，便于减少 系统的重复代码，降低模块间的耦合度，并有利于未来的可扩展性和可维护性。

Spring AOP是基于动态代理的，如果要代理的对象实现了某个接口，那么Spring AOP就会使 用JDK动态代理去创建代理对象；而对于没有实现接口的对象，就无法使用JDK动态代理，转 而使用CGlib动态代理生成一个被代理对象的子类来作为代理。 当然也可以使用AspectJ，Spring AOP中已经集成了AspectJ，AspectJ应该算得上是Java生 态系统中最完整的AOP框架了。使用AOP之后我们可以把一些通用功能抽象出来，在需要用到 的地方直接使用即可，这样可以大大简化代码量。我们需要增加新功能也方便，提高了系统的 扩展性。日志功能、事务管理和权限管理等场景都用到了AOP。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring中的bean的作用域有哪些？

> 原文：[https://zwmst.com/1857.html](https://zwmst.com/1857.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:42:33+08:00"> 2021-08-15 </time> ](https://zwmst.com/1857.html)  1.singleton：唯一bean实例，Spring中的bean默认都是单例的。

2.prototype：每次请求都会创建一个新的bean实例。

3.request：每一次HTTP请求都会产生一个新的bean，该bean仅在当前HTTP request内有 效。

4.session：每一次HTTP请求都会产生一个新的bean，该bean仅在当前HTTP session内有 效。

5.global-session：全局session作用域，仅仅在基于Portlet的Web应用中才有意义，

Spring5中已经没有了。Portlet是能够生成语义代码（例如HTML）片段的小型Java Web插 件。它们基于Portlet容器，可以像Servlet一样处理HTTP请求。但是与Servlet不同，每个 Portlet都有不同的会话。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring中的单例bean的线程安全问题了解吗？

> 原文：[https://zwmst.com/1859.html](https://zwmst.com/1859.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:42:44+08:00"> 2021-08-15 </time> ](https://zwmst.com/1859.html)  大部分时候我们并没有在系统中使用多线程，所以很少有人会关注这个问题。单例bean存在线 程问题，主要是因为当多个线程操作同一个对象的时候，对这个对象的非静态成员变量的写操 作会存在线程安全问题。

有两种常见的解决方案：

1.在bean对象中尽量避免定义可变的成员变量（不太现实）。

2.在类中定义一个ThreadLocal成员变量，将需要的可变成员变量保存在ThreadLocal中（推 荐的一种方式）。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring中的bean生命周期了解过吗？

> 原文：[https://zwmst.com/1861.html](https://zwmst.com/1861.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:42:54+08:00"> 2021-08-15 </time> ](https://zwmst.com/1861.html)  1.Bean容器找到配置文件中Spring Bean的定义。

2.Bean容器利用Java Reflection API创建一个Bean的实例。

3.如果涉及到一些属性值，利用set()方法设置一些属性值。

4.如果Bean实现了BeanNameAware接口，调用setBeanName()方法，传入Bean的名字。

5.如果Bean实现了BeanClassLoaderAware接口，调用setBeanClassLoader()方法，传入 ClassLoader对象的实例。

6.如果Bean实现了BeanFactoryAware接口，调用setBeanClassFacotory()方法，传入 ClassLoader对象的实例。

7.与上面的类似，如果实现了其他*Aware接口，就调用相应的方法。

8.如果有和加载这个Bean的Spring容器相关的BeanPostProcessor对象，执行 postProcessBeforeInitialization()方法。

9.如果Bean实现了InitializingBean接口，执行afeterPropertiesSet()方法。

10.如果Bean在配置文件中的定义包含init-method属性，执行指定的方法。

11.如果有和加载这个Bean的Spring容器相关的BeanPostProcess对象，执行 postProcessAfterInitialization()方法。

12.当要销毁Bean的时候，如果Bean实现了DisposableBean接口，执行destroy()方法。

13.当要销毁Bean的时候，如果Bean在配置文件中的定义包含destroy-method属性，执行指 定的方法。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring MVC的工作原理了解嘛？

> 原文：[https://zwmst.com/1863.html](https://zwmst.com/1863.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:43:05+08:00"> 2021-08-15 </time> ](https://zwmst.com/1863.html)  1.客户端（浏览器）发送请求，直接请求到DispatcherServlet。

2.DispatcherServlet根据请求信息调用HandlerMapping，解析请求对应的Handler。

3.解析到对应的Handler（也就是我们平常说的Controller控制器）。

4.HandlerAdapter会根据Handler来调用真正的处理器来处理请求和执行相对应的业务逻 辑。

5.处理器处理完业务后，会返回一个ModelAndView对象，Model是返回的数据对象，View 是逻辑上的View。

6.ViewResolver会根据逻辑View去查找实际的View。

7.DispatcherServlet把返回的Model传给View（视图渲染）。

8.把View返回给请求者（浏览器）。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring框架中用到了哪些设计模式？

> 原文：[https://zwmst.com/1865.html](https://zwmst.com/1865.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:43:16+08:00"> 2021-08-15 </time> ](https://zwmst.com/1865.html)  1.工厂设计模式：Spring使用工厂模式通过BeanFactory和ApplicationContext创建bean对 象。

2.代理设计模式：Spring AOP功能的实现。

3.单例设计模式：Spring中的bean默认都是单例的。

4.模板方法模式：Spring中的jdbcTemplate、hibernateTemplate等以Template结尾的对 数据库操作的类，它们就使用到了模板模式。

5.包装器设计模式：我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要 会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。

6.观察者模式：Spring事件驱动模型就是观察者模式很经典的一个应用。

7.适配器模式：Spring AOP的增强或通知（Advice）使用到了适配器模式、Spring MVC中也 是用到了适配器模式适配Controller。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# @Component和@Bean的区别是什么？

> 原文：[https://zwmst.com/1867.html](https://zwmst.com/1867.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:43:27+08:00"> 2021-08-15 </time> ](https://zwmst.com/1867.html)  1.作用对象不同。@Component注解作用于类，而@Bean注解作用于方法。

2.@Component注解通常是通过类路径扫描来自动侦测以及自动装配到Spring容器中（我们 可以使用@ComponentScan注解定义要扫描的路径）。@Bean注解通常是在标有该注解的 方法中定义产生这个bean，告诉Spring这是某个类的实例，当我需要用它的时候还给我。

3.@Bean注解比@Component注解的自定义性更强，而且很多地方只能通过@Bean注解来 注册bean。比如当引用第三方库的类需要装配到Spring容器的时候，就只能通过@Bean注解 来实现。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 将一个类声明为Spring的bean的注解有哪些？

> 原文：[https://zwmst.com/1869.html](https://zwmst.com/1869.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:43:38+08:00"> 2021-08-15 </time> ](https://zwmst.com/1869.html)  我们一般使用@Autowired注解去自动装配bean。而想要把一个类标识为可以用 @Autowired注解自动装配的bean，可以采用以下的注解实现：

1.@Component注解。通用的注解，可标注任意类为Spring组件。如果一个Bean不知道属于 哪一个层，可以使用@Component注解标注。

2.@Repository注解。对应持久层，即Dao层，主要用于数据库相关操作。

3.@Service注解。对应服务层，即Service层，主要涉及一些复杂的逻辑，需要用到Dao层 （注入）。

4.@Controller注解。对应Spring MVC的控制层，即Controller层，主要用于接受用户请求 并调用Service层的方法返回数据给前端页面。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring事务管理的方式有几种？

> 原文：[https://zwmst.com/1871.html](https://zwmst.com/1871.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:43:49+08:00"> 2021-08-15 </time> ](https://zwmst.com/1871.html)  1.编程式事务：在代码中硬编码（不推荐使用）。

2.声明式事务：在配置文件中配置（推荐使用），分为基于XML的声明式事务和基于注解的声 明式事务。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring事务中的隔离级别有哪几种？

> 原文：[https://zwmst.com/1873.html](https://zwmst.com/1873.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:44:03+08:00"> 2021-08-15 </time> ](https://zwmst.com/1873.html)  在TransactionDefinition接口中定义了五个表示隔离级别的常量：

ISOLATION_DEFAULT：使用后端数据库默认的隔离级别，Mysql默认采用的 REPEATABLE_READ隔离级别；Oracle默认采用的READ_COMMITTED隔离级别。 ISOLATION_READ_UNCOMMITTED：最低的隔离级别，允许读取尚未提交的数据变更， 可能会导致脏读、幻读或不可重复读。

ISOLATION_READ_COMMITTED：允许读取并发事务已经提交的数据，可以阻止脏读， 但是幻读或不可重复读仍有可能发生

ISOLATION_REPEATABLE_READ：对同一字段的多次读取结果都是一致的，除非数据是 被本身事务自己所修改，可以阻止脏读和不可重复读，但幻读仍有可能发生。

ISOLATION_SERIALIZABLE：最高的隔离级别，完全服从ACID的隔离级别。所有的事务依 次逐个执行，这样事务之间就完全不可能产生干扰，也就是说，该级别可以防止脏读、不可重 复读以及幻读。但是这将严重影响程序的性能。通常情况下也不会用到该级别。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring事务中有哪几种事务传播行为？

> 原文：[https://zwmst.com/1875.html](https://zwmst.com/1875.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:44:15+08:00"> 2021-08-15 </time> ](https://zwmst.com/1875.html)  在TransactionDefinition接口中定义了八个表示事务传播行为的常量。

支持当前事务的情况：

PROPAGATION_REQUIRED：如果当前存在事务，则加入该事务；如果当前没有事务，则 创建一个新的事务。

PROPAGATION_SUPPORTS： 如果当前存在事务，则加入该事务；如果当前没有事务，则 以非事务的方式继续运行。

PROPAGATION_MANDATORY： 如果当前存在事务，则加入该事务；如果当前没有事务， 则抛出异常。（mandatory：强制性）。

不支持当前事务的情况：

PROPAGATION_REQUIRES_NEW： 创建一个新的事务，如果当前存在事务，则把当前事 务挂起。

PROPAGATION_NOT_SUPPORTED： 以非事务方式运行，如果当前存在事务，则把当前 事务挂起。

PROPAGATION_NEVER： 以非事务方式运行，如果当前存在事务，则抛出异常。

其他情况：

PROPAGATION_NESTED： 如果当前存在事务，则创建一个事务作为当前事务的嵌套事务 来运行；如果当前没有事务，则该取值等价于PROPAGATION_REQUIRED。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring 事务底层原理

> 原文：[https://zwmst.com/1877.html](https://zwmst.com/1877.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:44:28+08:00"> 2021-08-15 </time> ](https://zwmst.com/1877.html)  划分处理单元——IoC

由于spring解决的问题是对单个数据库进行局部事务处理的，具体的实现首先用spring中的 IoC划分了事务处理单元。并且将对事务的各种配置放到了ioc容器中（设置事务管理器，设置 事务的传播特性及隔离机制）。

AOP拦截需要进行事务处理的类

Spring事务处理模块是通过AOP功能来实现声明式事务处理的，具体操作（比如事务实行的配 置和读取，事务对象的抽象），用TransactionProxyFactoryBean接口来使用AOP功能，生 成proxy代理对象，通过TransactionInterceptor完成对代理方法的拦截，将事务处理的功能 编织到拦截的方法中。读取ioc容器事务配置属性，转化为spring事务处理需要的内部数据结 构（TransactionAttributeSourceAdvisor），转化为TransactionAttribute表示的数据对 象。

对事务处理实现（事务的生成、提交、回滚、挂起）

spring委托给具体的事务处理器实现。实现了一个抽象和适配。适配的具体事务处理器： DataSource数据源支持、hibernate数据源事务处理支持、JDO数据源事务处理支持，JPA、 JTA数据源事务处理支持。这些支持都是通过设计PlatformTransactionManager、 AbstractPlatforTransaction一系列事务处理的支持。 为常用数据源支持提供了一系列的 TransactionManager。

总结

PlatformTransactionManager实现了TransactionInterception接口，让其与 TransactionProxyFactoryBean结合起来，形成一个Spring声明式事务处理的设计体系。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# BeanFactory和ApplicationContext有什么区别？

> 原文：[https://zwmst.com/1879.html](https://zwmst.com/1879.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:44:40+08:00"> 2021-08-15 </time> ](https://zwmst.com/1879.html)  ApplicationContext提供了一种解决文档信息的方法，一种加载文件资源的方式(如图片)，他 们可以向监听他们的beans发送消息。另外，容器或者容器中beans的操作，这些必须以bean 工厂的编程方式处理的操作可以在应用上下文中以声明的方式处理。应用上下文实现了 MessageSource，该接口用于获取本地消息，实际的实现是可选的。

相同点：两者都是通过xml配置文件加载bean，ApplicationContext和BeanFacotry相比， 提供了更多的扩展功能。

不同点：BeanFactory是延迟加载，如果Bean的某一个属性没有注入，BeanFacotry加载 后，直至第一次使用调用getBean方法才会抛出异常；而ApplicationContext则在初始化自身 是检验，这样有利于检查所依赖属性是否注入；所以通常情况下我们选择使用 ApplicationContext。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Resource 是如何被查找、加载的？

> 原文：[https://zwmst.com/1881.html](https://zwmst.com/1881.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:44:52+08:00"> 2021-08-15 </time> ](https://zwmst.com/1881.html)  Resource 接口是 Spring 资源访问策略的抽象，它本身并不提供任何资源访问实现，具体的资 源访问由该接口的实现类完成——每个实现类代表一种资源访问策略。 Spring 为 Resource 接口提供了如下实现类：

UrlResource：访问网络资源的实现类。ClassPathResource：访问类加载路径里资源的实现 类。FileSystemResource：访问文件系统里资源的实现类。ServletContextResource：访 问相对于 ServletContext 路径里的资源的实现类：InputStreamResource：访问输入流资源 的实现类。ByteArrayResource：访问字节数组资源的实现类。 这些 Resource 实现类，针 对不同的的底层资源，提供了相应的资源访问逻辑，并提供便捷的包装，以利于客户端程序的 资源访问。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 解释自动装配的各种模式？

> 原文：[https://zwmst.com/1883.html](https://zwmst.com/1883.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:45:04+08:00"> 2021-08-15 </time> ](https://zwmst.com/1883.html)  自动装配提供五种不同的模式供Spring容器用来自动装配beans之间的依赖注入:

no：默认的方式是不进行自动装配，通过手工设置ref 属性来进行装配bean。

byName：通过参数名自动装配，Spring容器查找beans的属性，这些beans在XML配置文件 中被设置为byName。之后容器试图匹配、装配和该bean的属性具有相同名字的bean。

byType：通过参数的数据类型自动自动装配，Spring容器查找beans的属性，这些beans在 XML配置文件中被设置为byType。之后容器试图匹配和装配和该bean的属性类型一样的 bean。如果有多个bean符合条件，则抛出错误。

constructor：这个同byType类似，不过是应用于构造函数的参数。如果在BeanFactory中不 是恰好有一个bean与构造函数参数相同类型，则抛出一个严重的错误。

autodetect：如果有默认的构造方法，通过 construct的方式自动装配，否则使用 byType的 方式自动装配。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 有哪些不同类型的IOC(依赖注入)？

> 原文：[https://zwmst.com/1885.html](https://zwmst.com/1885.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:45:17+08:00"> 2021-08-15 </time> ](https://zwmst.com/1885.html)  构造器依赖注入：构造器依赖注入在容器触发构造器的时候完成，该构造器有一系列的参数， 每个参数代表注入的对象。

Setter方法依赖注入：首先容器会触发一个无参构造函数或无参静态工厂方法实例化对象，之 后容器调用bean中的setter方法完成Setter方法依赖注入。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring AOP 实现原理

> 原文：[https://zwmst.com/1887.html](https://zwmst.com/1887.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:45:34+08:00"> 2021-08-15 </time> ](https://zwmst.com/1887.html)  实现AOP的技术，主要分为两大类：

一是采用动态代理技术，利用截取消息的方式，对该消息进行装饰，以取代原有对象行为的执 行；二是采用静态织入的方式，引入特定的语法创建“方面”，从而使得编译器可以在编译期间 织入有关“方面”的代码。

Spring AOP 的实现原理其实很简单：AOP 框架负责动态地生成 AOP 代理类，这个代理类的 方法则由 Advice和回调目标对象的方法所组成, 并将该对象可作为目标对象使用。AOP 代理包 含了目标对象的全部方法，但AOP代理中的方法与目标对象的方法存在差异，AOP方法在特定 切入点添加了增强处理，并回调了目标对象的方法。

Spring AOP使用动态代理技术在运行期织入增强代码。使用两种代理机制：基于JDK的动态代 理（JDK本身只提供接口的代理）和基于CGlib的动态代理。

(1) JDK的动态代理

JDK的动态代理主要涉及java.lang.reflect包中的两个类：Proxy和InvocationHandler。其 中InvocationHandler只是一个接口，可以通过实现该接口定义横切逻辑，并通过反射机制调 用目标类的代码，动态的将横切逻辑与业务逻辑织在一起。而Proxy利用InvocationHandler 动态创建一个符合某一接口的实例，生成目标类的代理对象。 其代理对象必须是某个接口的实现, 它是通过在运行期间创建一个接口的实现类来完成对目标 对象的代理.只能实现接口的类生成代理，而不能针对类。

(2)CGLib

CGLib采用底层的字节码技术，为一个类创建子类，并在子类中采用方法拦截的技术拦截所有 父类的调用方法，并顺势织入横切逻辑.它运行期间生成的代理对象是目标类的扩展子类.所以 无法通知final、private的方法,因为它们不能被覆写.是针对类实现代理,主要是为指定的类生 成一个子类，覆盖其中方法。 在spring中默认。况下使用JDK动态代理实现AOP,如果proxy-target-class设置为true或者 使用了优化策略那么会使用CGLIB来创建动态代理.Spring AOP在这两种方式的实现上基本 一样．以JDK代理为例，会使用JdkDynamicAopProxy来创建代理，在invoke()方法首先需 要织入到当前类的增强器封装到拦截器链中，然后递归的调用这些拦截器完成功能的织入，最 终返回代理对象。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# ApplicationContext通常的实现是什么?

> 原文：[https://zwmst.com/1889.html](https://zwmst.com/1889.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:45:50+08:00"> 2021-08-15 </time> ](https://zwmst.com/1889.html)  *   FileSystemXmlApplicationContext ：此容器从一个XML文件中加载beans的定义， XML Bean 配置文件的全路径名必须提供给它的构造函数。
*   ClassPathXmlApplicationContext：此容器也从一个XML文件中加载beans的定义， 这里，你需要正确设置classpath因为这个容器将在classpath里找bean配置。
*   WebXmlApplicationContext：此容器加载一个XML文件，此文件定义了一个WEB应 用的所有bean。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Bean 工厂和 Application contexts 有什么区别？

> 原文：[https://zwmst.com/1891.html](https://zwmst.com/1891.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-08-15T16:46:00+08:00"> 2021-08-15 </time> ](https://zwmst.com/1891.html)  Application contexts提供一种方法处理文本消息，一个通常的做法是加载文件资源（比如镜 像），它们可以向注册为监听器的bean发布事件。另外，在容器或容器内的对象上执行的那些 不得不由bean工厂以程序化方式处理的操作，可以在Application contexts中以声明的方式处 理。Application contexts实现了MessageSource接口，该接口的实现以可插拔的方式提供 获取本地化消息的方法。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 213.Spring

> 原文：[https://zwmst.com/3375.html](https://zwmst.com/3375.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T10:18:49+08:00"> 2021-09-18 </time> ](https://zwmst.com/3375.html)  它是一个全面的、企业应用开发一站式的解决方案，贯穿表现层、业务层、持久层。但是 Spring仍然可以和其他的框架无缝整合。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 214.Spring 特点

> 原文：[https://zwmst.com/3377.html](https://zwmst.com/3377.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T10:20:54+08:00"> 2021-09-18 </time> ](https://zwmst.com/3377.html)  1.  轻量级
2.  控制反转
3.  面向切面
4.  容器
5.  框架集合

![](img/450fd2e6522acd7c99ebc56f6c159a00.png)*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 215.Spring 核心组件

> 原文：[https://zwmst.com/3381.html](https://zwmst.com/3381.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T10:24:04+08:00"> 2021-09-18 </time> ](https://zwmst.com/3381.html)  ![](img/8b0194ba98c8ab60cfa0e7859a691e66.png)*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 216.Spring 常用模块

> 原文：[https://zwmst.com/3385.html](https://zwmst.com/3385.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T10:25:37+08:00"> 2021-09-18 </time> ](https://zwmst.com/3385.html)  ![](img/fb3033642948d87cf29656199be5689f.png)*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 217.Spring 主要包

> 原文：[https://zwmst.com/3388.html](https://zwmst.com/3388.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T10:27:52+08:00"> 2021-09-18 </time> ](https://zwmst.com/3388.html)  ![](img/4724b68066a640da6d7c7c2c8a064b0b.png)*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 218.Spring 常用注解

> 原文：[https://zwmst.com/3392.html](https://zwmst.com/3392.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:18:41+08:00"> 2021-09-18 </time> ](https://zwmst.com/3392.html)  bean 注入与装配的的方式有很多种，可以通过 xml，get set 方式，构造函数或者注解等。简单易用的方式就是使用 Spring 的注解了，Spring 提供了大量的注解方式。
![](img/9e86c1f5cbd7b494e407bc25f6e3cc2f.png)*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 219.Spring 第三方结合

> 原文：[https://zwmst.com/3395.html](https://zwmst.com/3395.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:20:38+08:00"> 2021-09-18 </time> ](https://zwmst.com/3395.html)  ![](img/f000d031637bd3b85997c041f30e9b55.png)*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 220.Spring IOC 原理

> 原文：[https://zwmst.com/3398.html](https://zwmst.com/3398.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:28:48+08:00"> 2021-09-18 </time> ](https://zwmst.com/3398.html)  Spring 通过一个配置文件描述 Bean 及 Bean 之间的依赖关系，利用 Java 语言的反射功能实例化Bean 并建立 Bean 之间的依赖关系。 Spring 的 IoC 容器在完成这些底层工作的基础上，还提供了 Bean 实例缓存、生命周期管理、 Bean 实例代理、事件发布、资源装载等高级服务。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 221.Spring 容器高层视图

> 原文：[https://zwmst.com/3400.html](https://zwmst.com/3400.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:31:41+08:00"> 2021-09-18 </time> ](https://zwmst.com/3400.html)  Spring 启动时读取应用程序提供的 Bean 配置信息，并在 Spring 容器中生成一份相应的 Bean 配置注册表，然后根据这张注册表实例化 Bean，装配好 Bean 之间的依赖关系，为上层应用提供准备就绪的运行环境。其中 Bean 缓存池为 HashMap 实现
![](img/1da2f52b4f47372b4f40779fc4517ed2.png)*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 222.BeanFactory-框架基础设施

> 原文：[https://zwmst.com/3404.html](https://zwmst.com/3404.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:35:21+08:00"> 2021-09-18 </time> ](https://zwmst.com/3404.html)  BeanFactory 是 Spring 框架的基础设施，面向 Spring 本身；ApplicationContext 面向使用Spring 框架的开发者，几乎所有的应用场合我们都直接使用 ApplicationContext 而非底层的 BeanFactory。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 223.BeanDefinitionRegistry 注册表

> 原文：[https://zwmst.com/3407.html](https://zwmst.com/3407.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:36:28+08:00"> 2021-09-18 </time> ](https://zwmst.com/3407.html)  Spring 配置文件中每一个节点元素在 Spring 容器里都通过一个 BeanDefinition 对象表示，它描述了 Bean 的配置信息。而 BeanDefinitionRegistry 接口提供了向容器手工注册BeanDefinition 对象的方法。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 224.BeanFactory 顶层接口

> 原文：[https://zwmst.com/3409.html](https://zwmst.com/3409.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:37:52+08:00"> 2021-09-18 </time> ](https://zwmst.com/3409.html)  位于类结构树的顶端 ，它最主要的方法就是 getBean(String beanName)，该方法从容器中返回特定名称的 Bean，BeanFactory 的功能通过其他的接口得到不断扩展：*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 225.ListableBeanFactory

> 原文：[https://zwmst.com/3411.html](https://zwmst.com/3411.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:38:36+08:00"> 2021-09-18 </time> ](https://zwmst.com/3411.html)  该接口定义了访问容器中 Bean 基本信息的若干方法，如查看 Bean 的个数、获取某一类型Bean 的配置名、查看容器中是否包括某一 Bean 等方法；*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 226.HierarchicalBeanFactory 父子级联

> 原文：[https://zwmst.com/3413.html](https://zwmst.com/3413.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:39:55+08:00"> 2021-09-18 </time> ](https://zwmst.com/3413.html)  父子级联 IoC 容器的接口，子容器可以通过接口方法访问父容器； 通过HierarchicalBeanFactory 接口， **Spring 的 IoC 容器可以建立父子层级关联的容器体系**，子容器可以访问父容器中的 Bean，但父容器不能访问子容器的 Bean。Spring 使用父子容器实现了很多功能，比如**在 Spring MVC 中，展现层 Bean 位于一个子容器中，而业务层和持久层的 Bean 位于父容器中。这样，展现层 Bean 就可以引用业务层和持久层的 Bean，而业务层和持久层的 Bean 则看不到展现层的 Bean**。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 227.ConfigurableBeanFactory

> 原文：[https://zwmst.com/3420.html](https://zwmst.com/3420.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:44:57+08:00"> 2021-09-18 </time> ](https://zwmst.com/3420.html)  是一个重要的接口，增强了 IoC 容器的可定制性，它定义了设置类装载器、属性编辑器、容器初始化后置处理器等方法；*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 228.AutowireCapableBeanFactory 自动装配

> 原文：[https://zwmst.com/3422.html](https://zwmst.com/3422.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:45:37+08:00"> 2021-09-18 </time> ](https://zwmst.com/3422.html)  定义了将容器中的 Bean 按某种规则（如按名字匹配、按类型匹配等）进行自动装配的方法；*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 229.SingletonBeanRegistry 运行期间注册单例 Bean

> 原文：[https://zwmst.com/3424.html](https://zwmst.com/3424.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:46:32+08:00"> 2021-09-18 </time> ](https://zwmst.com/3424.html)  定义了允许在运行期间向容器注册单实例 Bean 的方法；对于单实例（ singleton）的 Bean 来说，BeanFactory 会缓存 Bean 实例，所以第二次使用 getBean() 获取 Bean 时将直接从IoC 容器的缓存中获取 Bean 实例。Spring 在DefaultSingletonBeanRegistry 类中提供了一个用于缓存单实例 Bean 的缓存器，它是一个用 HashMap 实现的缓存器，单实例的 Bean 以beanName 为键保存在这个 HashMap 中。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 230.依赖日志框框

> 原文：[https://zwmst.com/3427.html](https://zwmst.com/3427.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:47:33+08:00"> 2021-09-18 </time> ](https://zwmst.com/3427.html)  **在初始化 BeanFactory 时，必须为其提供一种日志框架**，比如使用 Log4J， 即在类路径下提供 Log4J 配置文件，这样启动 Spring 容器才不会报错。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 231.ApplicationContext 面向开发应用

> 原文：[https://zwmst.com/3429.html](https://zwmst.com/3429.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:50:13+08:00"> 2021-09-18 </time> ](https://zwmst.com/3429.html)  ApplicationContext 由 BeanFactory 派 生 而 来 ， 提 供 了 更 多 面 向 实 际 应 用 的 功 能 。

ApplicationContext 继承了 HierarchicalBeanFactory 和 ListableBeanFactory 接口，在此基础上，还通过多个其他的接口扩展了 BeanFactory 的功能：![](img/aa4e78ed795bcf97e33fe68706b52d2e.png)

1.  ClassPathXmlApplicationContext：默认从类路径加载配置文件
2.  FileSystemXmlApplicationContext：默认从文件系统中装载配置文件
3.  ApplicationEventPublisher：让容器拥有发布应用上下文事件的功能，包括容器启动事件、关闭事件等。
4.  MessageSource：为应用提供 i18n 国际化消息访问的功能；
5.  ResourcePatternResolver ： 所 有 ApplicationContext 实现类都实现了类似于PathMatchingResourcePatternResolver 的功能，可以通过带前缀的 Ant 风格的资源文件路径装载 Spring 的配置文件。
6.  LifeCycle：该接口是 Spring 2.0 加入的，该接口提供了 start()和 stop()两个方法，主要用于控制异步处理过程。在具体使用时，该接口同时被 ApplicationContext 实现及具体Bean 实现， ApplicationContext 会将 start/stop 的信息传递给容器中所有实现了该接口的 Bean，以达到管理和控制 JMX、任务调度等目的。
7.  ConfigurableApplicationContext 扩展于 ApplicationContext，**它新增加了两个主要的方法： refresh()和 close()，让 ApplicationContext 具有启动、刷新和关闭应用上下文的能力**。在应用上下文关闭的情况下调用 refresh()即可启动应用上下文，在已经启动的状态下，调用 refresh()则清除缓存并重新装载配置信息，而调用 close()则可关闭应用上下文。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 232.WebApplication 体系架构

> 原文：[https://zwmst.com/3432.html](https://zwmst.com/3432.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:52:14+08:00"> 2021-09-18 </time> ](https://zwmst.com/3432.html)  WebApplicationContext 是专门为 Web 应用准备的，它允许从相对于 Web 根目录的路径中装载配置文件完成初始化工作。从 WebApplicationContext 中可以获得ServletContext 的引用，**整个 Web 应用上下文对象将作为属性放置到 ServletContext 中**，以便 Web 应用环境可以访问 Spring 应用上下文。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 233.Spring Bean 作用域

> 原文：[https://zwmst.com/3434.html](https://zwmst.com/3434.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:53:30+08:00"> 2021-09-18 </time> ](https://zwmst.com/3434.html)  Spring 3 中为 Bean 定义了 5 中作用域，分别为：

1.  singleton（单例）
2.  prototype（原型）
3.  request
4.  session
5.  global session*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 234.singleton：单例模式（多线程下不安全）

> 原文：[https://zwmst.com/3436.html](https://zwmst.com/3436.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:54:51+08:00"> 2021-09-18 </time> ](https://zwmst.com/3436.html)  singleton：单例模式，Spring IoC 容器中只会存在一个共享的 Bean 实例，无论有多少个Bean 引用它，始终指向同一对象。**该模式在多线程下是不安全的**。Singleton 作用域是Spring 中的缺省作用域，也可以显示的将 Bean 定义为 singleton 模式，配置为：

```
<bean id="userDao" class="com.ioc.UserDaoImpl" scope="singleton"/>
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 235.prototype:原型模式每次使用时创建

> 原文：[https://zwmst.com/3438.html](https://zwmst.com/3438.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-18T14:56:16+08:00"> 2021-09-18 </time> ](https://zwmst.com/3438.html)  prototype:原型模式，**每次通过 Spring 容器获取 prototype 定义的 bean 时，容器都将创建一个新的 Bean 实例，每个 Bean 实例都有自己的属性和状态**，而 singleton 全局只有一个对象。根据经验，**对有状态的bean使用prototype作用域，而对无状态的bean使用singleton作用域**。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 236.Request：一次 request 一个实例

> 原文：[https://zwmst.com/3443.html](https://zwmst.com/3443.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:17:52+08:00"> 2021-09-19 </time> ](https://zwmst.com/3443.html)  request：**在一次 Http 请求中，容器会返回该 Bean 的同一实例**。而对不同的 Http 请求则会产生新的 Bean，而且**该 bean 仅在当前 Http Request 内有效** Http 请求结束，该 bean实例也将会被销毁。

```
<bean id="loginAction" class="com.cnblogs.Login" scope="request"/>
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 237.session

> 原文：[https://zwmst.com/3445.html](https://zwmst.com/3445.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:19:37+08:00"> 2021-09-19 </time> ](https://zwmst.com/3445.html)  session：在一次 Http Session 中，容器会返回该 Bean 的同一实例。而对不同的 Session 请求则会创建新的实例，该 bean 实例仅在当前 Session 内有效。同 Http 请求相同，每一次session 请求创建新的实例，而不同的实例之间不共享属性，且实例仅在自己的 session 请求内有效，请求结束，则实例将被销毁。

```
<bean id="userPreference" class="com.ioc.UserPreference" scope="session"/>
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 238.global Session

> 原文：[https://zwmst.com/3447.html](https://zwmst.com/3447.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:22:18+08:00"> 2021-09-19 </time> ](https://zwmst.com/3447.html)  global Session：在一个全局的 Http Session 中，容器会返回该 Bean 的同一个实例，仅在使用 portlet context 时有效。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 239.Spring Bean 生命周期-实例化

> 原文：[https://zwmst.com/3449.html](https://zwmst.com/3449.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:23:25+08:00"> 2021-09-19 </time> ](https://zwmst.com/3449.html)  实例化一个 Bean，也就是我们常说的 new。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 240.Spring Bean 生命周期-IOC 依赖注入

> 原文：[https://zwmst.com/3451.html](https://zwmst.com/3451.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:27:51+08:00"> 2021-09-19 </time> ](https://zwmst.com/3451.html)  按照 Spring 上下文对实例化的 Bean 进行配置，也就是 IOC 注入。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 241.Spring Bean 生命周期-setBeanName 实现

> 原文：[https://zwmst.com/3453.html](https://zwmst.com/3453.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:39:57+08:00"> 2021-09-19 </time> ](https://zwmst.com/3453.html)  如果这个 Bean 已经实现了 BeanNameAware 接口，会调用它实现的 setBeanName(String)方法，此处传递的就是 Spring 配置文件中 Bean 的 id 值*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 242.Spring Bean 生命周期-BeanFactoryAware 实现

> 原文：[https://zwmst.com/3456.html](https://zwmst.com/3456.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:41:47+08:00"> 2021-09-19 </time> ](https://zwmst.com/3456.html)  如果这个 Bean 已经实现了 BeanFactoryAware 接口，会调用它实现的 setBeanFactory，setBeanFactory(BeanFactory)传递的是 Spring 工厂自身（可以用这个方式来获取其它 Bean，只需在 Spring 配置文件中配置一个普通的 Bean 就可以）。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 243.Spring Bean 生命周期-ApplicationContextAware 实现

> 原文：[https://zwmst.com/3458.html](https://zwmst.com/3458.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:42:42+08:00"> 2021-09-19 </time> ](https://zwmst.com/3458.html)  如果这个 Bean 已经实现了 ApplicationContextAware 接口，会调用setApplicationContext(ApplicationContext)方法，传入 Spring 上下文（同样这个方式也可以实现步骤 4 的内容，但比 4 更好，因为 ApplicationContext 是 BeanFactory 的子接口，有更多的实现方法）*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 244.postProcessBeforeInitialization 接口实现-初始化预处理

> 原文：[https://zwmst.com/3463.html](https://zwmst.com/3463.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:45:52+08:00"> 2021-09-19 </time> ](https://zwmst.com/3463.html)  如果这个 Bean 关联了 BeanPostProcessor 接口，将会调用postProcessBeforeInitialization(Object obj, String s)方法，BeanPostProcessor 经常被用作是 Bean 内容的更改，并且由于这个是在 Bean 初始化结束时调用那个的方法，也可以被应用于内存或缓存技术。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 245.init-method

> 原文：[https://zwmst.com/3468.html](https://zwmst.com/3468.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:48:39+08:00"> 2021-09-19 </time> ](https://zwmst.com/3468.html)  如果 Bean 在 Spring 配置文件中配置了 init-method 属性会自动调用其配置的初始化方法。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 246.postProcessAfterInitialization

> 原文：[https://zwmst.com/3470.html](https://zwmst.com/3470.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:50:17+08:00"> 2021-09-19 </time> ](https://zwmst.com/3470.html)  如果这个 Bean 关联了 BeanPostProcessor 接口，将会调用postProcessAfterInitialization(Object obj, String s)方法。

注：以上工作完成以后就可以应用这个 Bean 了，那这个 Bean 是一个 Singleton 的，所以一般情况下我们调用同一个 id 的 Bean 会是在内容地址相同的实例，当然在 Spring 配置文件中也可以配置非 Singleton。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 247.Destroy 过期自动清理阶段

> 原文：[https://zwmst.com/3472.html](https://zwmst.com/3472.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:52:27+08:00"> 2021-09-19 </time> ](https://zwmst.com/3472.html)  当 Bean 不再需要时，会经过清理阶段，如果 Bean 实现了DisposableBean 这个接口，会调用那个其实现的 destroy()方法；*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 248.destroy-method 自配置清理

> 原文：[https://zwmst.com/3474.html](https://zwmst.com/3474.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:53:26+08:00"> 2021-09-19 </time> ](https://zwmst.com/3474.html)  最后，如果这个 Bean 的 Spring 配置中配置了 destroy-method 属性，会自动调用其配置的销毁方法。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 249\. bean 标签

> 原文：[https://zwmst.com/3477.html](https://zwmst.com/3477.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:55:36+08:00"> 2021-09-19 </time> ](https://zwmst.com/3477.html)  bean 标签有两个重要的属性（init-method 和 destroy-method）。用它们你可以自己定制初始化和注销方法。它们也有相应的注解（@PostConstruct 和@PreDestroy）。

```
<bean id="" class="" init-method="初始化方法" destroy-method="销毁方法">
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 250.Spring 依赖注入-构造器注入

> 原文：[https://zwmst.com/3479.html](https://zwmst.com/3479.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:56:44+08:00"> 2021-09-19 </time> ](https://zwmst.com/3479.html)  ```
/*带参数，方便利用构造器进行注入*/ 
 public CatDaoImpl(String message){ 
 this. message = message; 
 } 
<bean id="CatDaoImpl" class="com.CatDaoImpl"> 
<constructor-arg value=" message "></constructor-arg> 
</bean>
 public class Id { 
 private int id; 
 public int getId() { return id; } 
 public void setId(int id) { this.id = id; } 
} 
<bean id="id" class="com.id "> <property name="id" value="123"></property> </bean> 
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 251.静态工厂注入

> 原文：[https://zwmst.com/3482.html](https://zwmst.com/3482.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:58:10+08:00"> 2021-09-19 </time> ](https://zwmst.com/3482.html)  静态工厂顾名思义，就是通过调用静态工厂的方法来获取自己需要的对象，为了让 spring 管理所有对象，我们不能直接通过"工程类.静态方法()"来获取对象，而是依然通过 spring 注入的形式获取：

```
public class DaoFactory { //静态工厂 
 public static final FactoryDao getStaticFactoryDaoImpl(){ 
 return new StaticFacotryDaoImpl(); 
 } 
} 
public class SpringAction { 
 private FactoryDao staticFactoryDao; //注入对象
 //注入对象的 set 方法 
 public void setStaticFactoryDao(FactoryDao staticFactoryDao) { 
 this.staticFactoryDao = staticFactoryDao; 
 } 
} 
//factory-method="getStaticFactoryDaoImpl"指定调用哪个工厂方法
 <bean name="springAction" class=" SpringAction" > 
 <!--使用静态工厂的方法注入对象,对应下面的配置文件--> 
 <property name="staticFactoryDao" ref="staticFactoryDao"></property> 
 </bean> 
 <!--此处获取对象的方式是从工厂类中获取静态方法--> 
<bean name="staticFactoryDao" class="DaoFactory" 
factory-method="getStaticFactoryDaoImpl"></bean>
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 252.实例工厂

> 原文：[https://zwmst.com/3484.html](https://zwmst.com/3484.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T19:59:28+08:00"> 2021-09-19 </time> ](https://zwmst.com/3484.html)  实例工厂的意思是获取对象实例的方法不是静态的，所以你需要首先 new 工厂类，再调用普通的实例方法：

```
public class DaoFactory { //实例工厂 
 public FactoryDao getFactoryDaoImpl(){ 
 return new FactoryDaoImpl();
  } 
} 
public class SpringAction { 
 private FactoryDao factoryDao; //注入对象 
 public void setFactoryDao(FactoryDao factoryDao) { 
 this.factoryDao = factoryDao; 
 } 
} 
 <bean name="springAction" class="SpringAction"> 
 <!--使用实例工厂的方法注入对象,对应下面的配置文件--> 
 <property name="factoryDao" ref="factoryDao"></property> 
 </bean> 
 <!--此处获取对象的方式是从工厂类中获取实例方法--> 
<bean name="daoFactory" class="com.DaoFactory"></bean> 
<bean name="factoryDao" factory-bean="daoFactory"
factory-method="getFactoryDaoImpl"></bean> 
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 253.setter 方法注入

> 原文：[https://zwmst.com/3489.html](https://zwmst.com/3489.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T20:02:01+08:00"> 2021-09-19 </time> ](https://zwmst.com/3489.html)  ```
 public class Id {
 private int id;
 public int getId() { return id; }
 public void setId(int id) { this.id = id; }
} 
<bean id="id" class="com.id "> <property name="id" value="123"></property> </bean>
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 254.5 种不同方式的自动装配

> 原文：[https://zwmst.com/3491.html](https://zwmst.com/3491.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T20:34:53+08:00"> 2021-09-19 </time> ](https://zwmst.com/3491.html)  Spring 装配包括**手动装配和自动装配**，手动装配是有基于 xml 装配、构造方法、setter 方法等自动装配有五种自动装配的方式，可以用来指导 Spring 容器用自动装配方式来进行依赖注入。

1.  no：默认的方式是不进行自动装配，通过显式设置 ref 属性来进行装配。
2.  byName：通过参数名 自动装配，Spring 容器在配置文件中发现 bean 的 autowire 属性被设置成 byname，之后容器试图匹配、装配和该 bean 的属性具有相同名字的 bean。
3.  byType：通过参数类型自动装配，Spring 容器在配置文件中发现 bean 的 autowire 属性被设置成 byType，之后容器试图匹配、装配和该 bean 的属性具有相同类型的 bean。如果有多个 bean 符合条件，则抛出错误。
4.  constructor：这个方式类似于 byType， 但是要提供给构造器参数，如果没有确定的带参数的构造器参数类型，将会抛出异常。
5.  autodetect：首先尝试使用 constructor 来自动装配，如果无法工作，则使用 byType 方式。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 255.Spring APO 原理概念

> 原文：[https://zwmst.com/3493.html](https://zwmst.com/3493.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T20:37:28+08:00"> 2021-09-19 </time> ](https://zwmst.com/3493.html)  "横切"的技术，剖解开封装的对象内部，并将那些影响了多个类的公共行为封装到一个可重用模块，并将其命名为"Aspect"，即切面。所谓"切面"，简单说就是那些与业务无关，却为业务模块所共同调用的逻辑或责任封装起来，便于减少系统的重复代码，降低模块之间的耦合度，并有利于未来的可操作性和可维护性。

使用"横切"技术，AOP 把软件系统分为两个部分：**核心关注点和横切关注点**。业务处理的主要流程是核心关注点，与之关系不大的部分是横切关注点。横切关注点的一个特点是，他们经常发生在核心关注点的多处，而各处基本相似，比如权限认证、日志、事物。AOP 的作用在于分离系统中的各种关注点，将核心关注点和横切关注点分离开来。

AOP 主要应用场景有：

1.  Authentication 权限
2.  Caching 缓存
3.  Context passing 内容传递
4.  Error handling 错误处理
5.  Lazy loading 懒加载
6.  Debugging 调试
7.  logging, tracing, profiling and monitoring 记录跟踪 优化 校准
8.  Performance optimization 性能优化
9.  Persistence 持久化
10.  Resource pooling 资源池
11.  Synchronization 同步
12.  Transactions 事务*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 256.AOP 核心概念

> 原文：[https://zwmst.com/3495.html](https://zwmst.com/3495.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T20:38:58+08:00"> 2021-09-19 </time> ](https://zwmst.com/3495.html)  1.  切面（aspect）：类是对物体特征的抽象，切面就是对横切关注点的抽象
2.  横切关注点：对哪些方法进行拦截，拦截后怎么处理，这些关注点称之为横切关注点。
3.  连接点（joinpoint）：被拦截到的点，因为 Spring 只支持方法类型的连接点，所以在 Spring中连接点指的就是被拦截到的方法，实际上连接点还可以是字段或者构造器。
4.  切入点（pointcut）：对连接点进行拦截的定义
5.  通知（advice）：所谓通知指的就是指拦截到连接点之后要执行的代码，通知分为前置、后置、异常、最终、环绕通知五类。
6.  目标对象：代理的目标对象
7.  织入（weave）：将切面应用到目标对象并导致代理对象创建的过程。
8.  引入（introduction）：在不修改代码的前提下，引入可以在运行期为类动态地添加一些方法或字段。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 257.AOP 两种代理方式

> 原文：[https://zwmst.com/3499.html](https://zwmst.com/3499.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T20:40:33+08:00"> 2021-09-19 </time> ](https://zwmst.com/3499.html)  Spring 提供了两种方式来生成代理对象: JDKProxy 和 Cglib，具体使用哪种方式生成由AopProxyFactory 根据 AdvisedSupport 对象的配置来决定。**默认的策略是如果目标类是接口，则使用 JDK 动态代理技术，否则使用 Cglib 来生成代理**。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 258.JDK 动态接口代

> 原文：[https://zwmst.com/3502.html](https://zwmst.com/3502.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T20:42:18+08:00"> 2021-09-19 </time> ](https://zwmst.com/3502.html)  JDK 动态代理主要涉及到 java.lang.reflect 包中的两个类：**Proxy** 和 **InvocationHandler**。
**InvocationHandler是一个接口，通过实现该接口定义横切逻辑，并通过反射机制调用目标类的代码，动态将横切逻辑和业务逻辑编制在一起。Proxy 利用 InvocationHandler 动态创建一个符合某一接口的实例，生成目标类的代理对象**。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 259.CGLib 动态代理

> 原文：[https://zwmst.com/3504.html](https://zwmst.com/3504.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T20:43:32+08:00"> 2021-09-19 </time> ](https://zwmst.com/3504.html)  CGLib 全称为 Code Generation Library，是一个强大的高性能，**高质量的代码生成类库，可以在运行期扩展 Java 类与实现 Java 接口**，CGLib 封装了 asm，可以再运行期动态生成新的 class。和 JDK 动态代理相比较：JDK 创建代理有一个限制，就是只能为接口创建代理实例，而对于没有通过接口定义业务方法的类，则可以通过 CGLib 创建动态代理。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 260.实现原理

> 原文：[https://zwmst.com/3506.html](https://zwmst.com/3506.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T20:44:19+08:00"> 2021-09-19 </time> ](https://zwmst.com/3506.html)  ```
@Aspect
public class TransactionDemo {
 @Pointcut(value="execution(* com.yangxin.core.service.*.*.*(..))")
 public void point(){
 }
 @Before(value="point()")
 public void before(){
 System.out.println("transaction begin");
 }
 @AfterReturning(value = "point()")
 public void after(){
 System.out.println("transaction commit");
 }
 @Around("point()")
 public void around(ProceedingJoinPoint joinPoint) throws Throwable{
 System.out.println("transaction begin");
 joinPoint.proceed();
 System.out.println("transaction commit");
 }
}
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 261.Spring MVC 原理

> 原文：[https://zwmst.com/3508.html](https://zwmst.com/3508.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T20:45:39+08:00"> 2021-09-19 </time> ](https://zwmst.com/3508.html)  Spring 的模型-视图-控制器（MVC）框架是围绕一个DispatcherServlet 来设计的，这个 Servlet会把请求分发给各个处理器，并支持可配置的处理器映射、视图渲染、本地化、时区与主题渲染等，甚至还能支持文件上传。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 262.MVC 流程

> 原文：[https://zwmst.com/3510.html](https://zwmst.com/3510.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T20:48:56+08:00"> 2021-09-19 </time> ](https://zwmst.com/3510.html)  ### Http 请求到 DispatcherServlet

1.  客户端请求提交到 DispatcherServlet。

    ### HandlerMapping 寻找处理器

2.  由 DispatcherServlet 控制器查询一个或多个 HandlerMapping，找到处理请求的Controller。

    ### 调用处理器 Controller

3.  DispatcherServlet 将请求提交到 Controller。

    ### Controller 调用业务逻辑处理后，返回 ModelAndView

4.  调用业务处理和返回结果：Controller 调用业务逻辑处理后，返回 ModelAndView。

    ### DispatcherServlet 查询 ModelAndView

5.  处理视图映射并返回模型： DispatcherServlet 查询一个或多个 ViewResoler 视图解析器，找到 ModelAndView 指定的视图。

    ### ModelAndView 反馈浏览器 HTTP

6.  Http 响应：视图负责将结果显示到客户端。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 263.MVC 常用注解

> 原文：[https://zwmst.com/3512.html](https://zwmst.com/3512.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T20:50:34+08:00"> 2021-09-19 </time> ](https://zwmst.com/3512.html)  ![](img/df74f6febe0414774a9b7600ce177e92.png)*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 264.Spring Boot 原理

> 原文：[https://zwmst.com/3515.html](https://zwmst.com/3515.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T20:51:53+08:00"> 2021-09-19 </time> ](https://zwmst.com/3515.html)  Spring Boot 是由 Pivotal 团队提供的全新框架，其设计目的是用来简化新 Spring 应用的初始搭建以及开发过程。该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置。通过这种方式，Spring Boot 致力于在蓬勃发展的快速应用开发领域(rapid application development)成为领导者。其特点如下：

1.  创建独立的 Spring 应用程序
2.  嵌入的 Tomcat，无需部署 WAR 文件
3.  简化 Maven 配置
4.  自动配置 Spring
5.  提供生产就绪型功能，如指标，健康检查和外部配置
6.  绝对没有代码生成和对 XML 没有要求配置 [1]*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 265.事务

> 原文：[https://zwmst.com/3517.html](https://zwmst.com/3517.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T20:53:51+08:00"> 2021-09-19 </time> ](https://zwmst.com/3517.html)  事务是计算机应用中不可或缺的组件模型，它保证了用户操作的原子性 ( Atomicity )、一致性( Consistency )、隔离性 ( Isolation ) 和持久性 ( Durabilily )。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 266.本地事务

> 原文：[https://zwmst.com/3520.html](https://zwmst.com/3520.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T20:55:55+08:00"> 2021-09-19 </time> ](https://zwmst.com/3520.html)  紧密依赖于底层资源管理器（例如数据库连接 )，**事务处理局限在当前事务资源内**。此种事务处理方式不存在对应用服务器的依赖，因而部署灵活却无法支持多数据源的分布式事务。在数据库连接中使用本地事务示例如下：

```
 public void transferAccount() { 
Connection conn = null; 
Statement stmt = null; 
try{ 
conn = getDataSource().getConnection(); 
// 将自动提交设置为 false，若设置为 true 则数据库将会把每一次数据更新认定为一个事务并自动提交
conn.setAutoCommit(false);
stmt = conn.createStatement(); 
// 将 A 账户中的金额减少 500
stmt.execute("update t_account set amount = amount - 500 where account_id = 'A'");
// 将 B 账户中的金额增加 500 
stmt.execute("update t_account set amount = amount + 500 where account_id = 'B'");
// 提交事务
 conn.commit();
 // 事务提交：转账的两步操作同时成功
} catch(SQLException sqle){ 
// 发生异常，回滚在本事务中的操做
 conn.rollback();
// 事务回滚：转账的两步操作完全撤销
 stmt.close(); 
 conn.close(); 
} 
}
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 267.分布式事务

> 原文：[https://zwmst.com/3522.html](https://zwmst.com/3522.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T20:57:41+08:00"> 2021-09-19 </time> ](https://zwmst.com/3522.html)  Java 事务编程接口（JTA：Java Transaction API）和 Java 事务服务 (JTS；Java Transaction Service) 为 J2EE 平台提供了分布式事务服务。分布式事务（Distributed Transaction）包括事务管理器（Transaction Manager）和一个或多个支持 XA 协议的资源管理器 ( Resource Manager )。我们可以将资源管理器看做任意类型的持久化数据存储；事务管理器承担着所有事务参与单元的协调与控制。

```
public void transferAccount() { 
UserTransaction userTx = null; 
Connection connA = null; Statement stmtA = null; 
Connection connB = null; Statement stmtB = null; 
try{ 
// 获得 Transaction 管理对象
userTx = (UserTransaction)getContext().lookup("java:comp/UserTransaction"); 
connA = getDataSourceA().getConnection();// 从数据库 A 中取得数据库连接
connB = getDataSourceB().getConnection();// 从数据库 B 中取得数据库连接
userTx.begin(); // 启动事务
stmtA = connA.createStatement();// 将 A 账户中的金额减少 500 
stmtA.execute("update t_account set amount = amount - 500 where account_id = 'A'");
// 将 B 账户中的金额增加 500 
stmtB = connB.createStatement(); 
stmtB.execute("update t_account set amount = amount + 500 where account_id = 'B'");
userTx.commit();// 提交事务
// 事务提交：转账的两步操作同时成功（数据库 A 和数据库 B 中的数据被同时更新）
} catch(SQLException sqle){ 
// 发生异常，回滚在本事务中的操纵
 userTx.rollback();// 事务回滚：数据库 A 和数据库 B 中的数据更新被同时撤销
} catch(Exception ne){ } 
}
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 268.两阶段提交

> 原文：[https://zwmst.com/3524.html](https://zwmst.com/3524.html)

   [ *Spring* ](https://zwmst.com/spring)*[ <time datetime="2021-09-19T21:00:05+08:00"> 2021-09-19 </time> ](https://zwmst.com/3524.html)  两阶段提交主要保证了分布式事务的原子性：即所有结点要么全做要么全不做，所谓的两个阶段是指：**第一阶段：准备阶段；第二阶段：提交阶段**。

1.  准备阶段
    事务协调者(事务管理器)给每个参与者(资源管理器)发送 Prepare 消息，每个参与者要么直接返回失败(如权限验证失败)，**要么在本地执行事务，写本地的 redo 和 undo 日志，但不提交**，到达一种“万事俱备，只欠东风”的状态。

2.  提交阶段：
    如果协调者收到了参与者的失败消息或者超时，直接给每个参与者发送回滚(Rollback)消息；否则，发送提交(Commit)消息；参与者根据协调者的指令执行提交或者回滚操作，释放所有事务处理过程中使用的锁资源。(注意:**必须在最后阶段释放锁资源**)

将提交分成两阶段进行的目的很明确，就是尽可能晚地提交事务，让事务在提交前尽可能地完成
所有能完成的工作。*
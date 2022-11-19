<!--yml
category: Java
date: 2022-11-19 13:21:56
-->

# Spring面试指南一（zthinker）

> 来源：[https://zthinker.com/archives/spring-interview-1](https://zthinker.com/archives/spring-interview-1)

[Java内存管理面试指南一](https://zthinker.com/archives/java-memory-interview-1)
[Java基础面试指南一](https://zthinker.com/archives/java-basic-interview-1)
[Java基础面试指南二](https://zthinker.com/archives/java-basic-interview-2)
[Java基础面试指南三](https://zthinker.com/archives/java-basic-interview-3)
[Java基础面试指南四](https://zthinker.com/archives/java-basic-interview-4)
[Java线程面试指南一](https://zthinker.com/archives/java-thread-interview-1)
[Java线程面试指南二](https://zthinker.com/archives/java-thread-interview-2)
[Redis面试指南一](https://zthinker.com/archives/redis-interview-1)
[Kafka面试指南一](https://zthinker.com/archives/kafka-interview-1)
[Spring面试指南一](https://zthinker.com/archives/spring-interview-1)
[SpringBoot面试指南一](https://zthinker.com/archives/springboot-interview-1)
[微服务面试指南一](https://zthinker.com/archives/microservice-interview-1)

Spring Framework是一个开源Java平台。它为任何类型的部署平台上的基于Java的现代企业应用程序提供了全面的编程和配置模型。Spring框架最初由Rod Johnson编写,并于2003年6月根据Apache 2.0许可证首次发布。

Spring是用于企业Java的开源开发框架。Spring Framework的核心功能可用于开发任何Java应用程序,但是在Java EE平台之上有一些用于构建Web应用程序的扩展。Spring框架旨在通过启用基于POJO的编程模型来使J2EE开发更易于使用并促进良好的编程实践。

Spring框架建立在两个设计概念之上:依赖注入和面向切面的编程。

**Spring框架的一些功能包括:**

*   轻巧,使用框架进行开发的开销很小。
*   依赖注入或控制反转以编写彼此独立的组件,spring容器负责将它们连接在一起以完成我们的工作。
*   Spring IoC容器管理Spring Bean生命周期和项目特定的配置,例如JNDI查找。
*   Spring MVC框架可用于创建Web应用程序以及能够返回XML和JSON响应的静态Web服务。
*   通过注释或通过spring bean配置文件,只需很少的配置即可支持事务管理,JDBC操作,文件上传,异常处理等。

**使用Spring Framework的一些优点是:**

*   为了减少应用程序不同组件之间的直接依赖关系,通常Spring IoC容器负责初始化资源或bean,并将它们作为依赖关系注入。
*   在Spring框架中编写单元测试用例很容易,因为我们的业务逻辑与实际的资源实现类没有直接的依赖关系。我们可以轻松地编写测试配置,并为测试目的注入Mock Bean。
*   减少样板代码的数量,例如初始化对象,打开/关闭资源。我非常喜欢JdbcTemplate类,因为它有助于我们删除JDBC编程附带的所有样板代码。
*   Spring框架分为几个模块,它有助于我们保持应用程序的轻量级。例如,如果我们不需要Spring事务管理功能,则无需在项目中添加该依赖项。
*   Spring框架支持大多数Java EE功能,甚至更多。它总是在新技术之上,例如,有一个Android的Spring项目可以帮助我们为本地android应用程序编写更好的代码。这使spring框架成为一个完整的软件包,我们不需要为不同的需求而使用不同的框架。

以下是spring框架的模块:

*   核心模块
*   Bean模块
*   上下文模块
*   表达语言模块
*   JDBC模块
*   ORM模块
*   OXM模块
*   Java Messaging Service(JMS)模块
*   事务模块
*   Web模块
*   Web-Servlet模块
*   Web-Struts模块
*   Web-Portlet模块

我们可以使用基于Spring XML以及基于注释的配置来在Spring应用程序中实现DI。

BeanFactory是基本容器,而ApplicationContext是高级容器。ApplicationContext扩展了BeanFactory接口。与BeanFactory相比,ApplicationContext提供了更多功能,例如与spring AOP集成,用于i18n的消息资源处理等。

Bean Factory是spring框架的核心,它是一个轻量级容器,用于加载Bean定义并管理您的Bean。使用XML文件配置Bean,并管理单例定义的Bean。它还负责生命周期方法并注入依赖项。它还删除了临时的单例模式和工厂。

需要Spring框架,因为它是–

*   Very Light Weight Container
*   Framework
*   IOC
*   AOP

这是一个非常重要的模块,并提供各种必要的服务,例如EJB集成,远程处理,JNDI访问和调度。它将spring转换为框架。它还通过应用生命周期事件来扩展BeanFactory的概念,为国际化消息和验证提供支持。

自动装配用于在协作bean之间建立关系。Spring容器可以自动解析合作者的bean。

自动装配有五种不同的模式:

**NO:**无自动接线

**byName**:可以通过属性名称完成自动装配

**byType**:属性类型为自动装配

**构造函数:**类似于byType,它的属性在构造函数中

**自动检测:** 允许Spring从byType或构造函数中选择自动装配

Bean生命周期有两种重要的方法:

将bean装入容器时调用安装程序

将bean卸载到容器中时调用拆解

以下是侦听器的不同事件类型:

*   ContextClosedEvent –上下文关闭时调用此事件。
*   ContextRefreshedEvent –初始化或刷新上下文时调用此事件
*   RequestHandledEvent –当Web上下文处理请求时调用此事件

可以在应用程序中引入切面的点称为Joinpoint。这一点可能是修改字段,调用方法甚至引发异常。此时,可以添加新方面的代码以向应用程序引入新行为。

此时可以将Aspect代码插入正常的应用程序流程中以更改当前行为。

Spring AOP中有5种建议。

1.  Before Advice
2.  After Advice
3.  After Returning Advice
4.  Throws Advice
5.  Around Advice

一些重要的Spring Framework模块是:

Spring Context –用于依赖注入。

Spring AOP –用于面向切面的编程。

Spring DAO –使用DAO模式进行数据库操作

Spring JDBC –用于JDBC和DataSource支持。

Spring ORM –对ORM工具的支持,例如Hibernate

Spring Web Module –用于创建Web应用程序。

Spring MVC –用于创建Web应用程序,Web服务等的Model-View-Controller实现。

**Aspect:** Aspect是实现跨领域关注点的类,例如事务管理。Aspects可以是配置的普通类,然后在Spring Bean配置文件中进行配置,或者我们可以使用Spring AspectJ支持使用@Aspect批注将类声明为Aspect。

**Advice:** Advice是针对特定联接点采取的操作。就编程而言,它们是在应用程序中达到具有匹配切入点的特定连接点时执行的方法。您可以将Advice视为Spring拦截器或Servlet过滤器。

**切入点(Pointcut)**:切入点是与连接点匹配的正则表达式,用于确定是否需要执行建议。Pointcut使用与联接点匹配的不同种类的表达式。Spring框架使用AspectJ切入点表达语言来确定将在其中应用建议方法的连接点。

**JointPoint:** JointPoint是应用程序中的特定点,例如方法执行,异常处理,更改对象变量值等。在Spring AOP中,连接点始终是方法的执行。

**Advice Arguments:** 我们可以在Advice方法中传递参数。我们可以在切入点中使用args()表达式,以将其应用于与参数模式匹配的任何方法。如果使用此选项,则需要在确定参数类型的建议方法中使用相同的名称。

Spring Bean定义了五个作用域。

**单例:**将为每个容器创建一个bean实例。这是spring bean的默认范围。在使用此范围时,请确保spring bean没有共享的实例变量,否则可能会导致数据不一致问题,因为它不是线程安全的。

**Prototype**:每次请求bean时都会创建一个新实例。

**Request:**这与Prototype范围相同,但是应用于Web应用程序。将为每个HTTP请求创建一个新的bean实例。

**会话:**容器将为每个HTTP会话创建一个新bean。

**Global-session**:这用于为Portlet应用程序创建全局会话Bean。

Spring MVC Framework提供了以下方法来帮助我们实现可靠的异常处理。

**基于Controller** –我们可以在控制器类中定义异常处理程序方法。我们所需要做的就是使用@ExceptionHandler注释对这些方法进行注释。

**全局异常处理程序** –异常处理是一个跨领域的问题,Spring提供了@ControllerAdvice批注,我们可以将其与任何类一起使用以定义我们的全局异常处理程序。

**HandlerExceptionResolver实现** –对于一般的异常,大多数时候我们提供静态页面。Spring Framework提供了HandlerExceptionResolver接口,我们可以实现该接口来创建全局异常处理程序。这种定义全局异常处理程序的其他方法背后的原因是,Spring框架还提供了默认实现类,我们可以在我们的Spring bean配置文件中定义这些默认实现类,以获得Spring框架异常处理的好处。
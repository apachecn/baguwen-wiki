<!--yml
category: Java
date: 2022-11-19 13:21:59
-->

# Spring boot面试指南一（zthinker）

> 来源：[https://zthinker.com/archives/springboot-interview-1](https://zthinker.com/archives/springboot-interview-1)

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
13.  [系统设计面试指南一](https://zthinker.com/archives/8-things-you-need-to-know-before-system-design-interviews)

Spring Boot是一个开放源代码的轻量级框架,用于开发基于Java的应用程序。它建立在Spring之上的。它是由Pivotal团队开发和维护的。它主要用于Web和命令行应用程序。它会自动配置所有功能,您只需单击一下即可运行该应用程序。

Spring框架是用于构建应用程序的最广泛使用的 Java框架。spring框架的主要特征是依赖注入。通过允许我们开发松耦合应用程序,它可以使事情变得更简单。

**Spring Boot**是Spring框架的模块。Spring Boot的主要功能是自动配置。它会根据该要求自动配置一个类。Spring Boot使得创建独立的基于Spring的独立应用程序变得很容易。

主要区别在于:spring框架为开发应用程序使用了几种配置。Spring Boot允许使用预定义的类路径进行自动配置。

*   主要功能是自动配置
*   Spring Boot CLI
*   Starter POMs
*   Actuator
*   Spring initializer
*   Type safe configuration
*   YAML支持
*   基于微服务的架构
*   它包括嵌入式Tomcat服务器
*   更好的Spring Boot安全性
*   Admin Support
*   Logging files
*   Spring Applications

**Java最新版本**

Spring Boot 2.X将不再支持Java 7或更低版​​本,最低要求是Java 8。

*   Java 8+
*   Spring Framework 5.2.4+

**构建工具:**

*   Gradle 5.x和6.x以上版本(也支持4.4 +)
*   Maven 3.3及以上

**嵌入式servlet容器:**

*   Servlet 3.x +兼容容器
*   Tomcat 9.0- Servlet v4.0 +
*   Jetty9.4-servletv3.1
*   Underflow 2.0-servletv 4.0

*   Spring Boot Auto Configuration
*   Spring Boot CLI
*   Spring Boot Starter POMs
*   Spring Boot Actuator

Spring Boot模块提供了许多启动器依赖项。这里,一些最常用的是:

*   Data JPA Starter
*   Test starter
*   Security Starter
*   Web starter
*   Web Services Starter
*   Mail starter
*   Thymeleaf starter

Actuator是Spring Boot的子项目。它提供了多个端点来监视和管理您的应用程序。它通过提供内置端点来实现,但是您也可以构建自己的端点。还提供了访问生产就绪REST点并从Web提取所有信息的简便方法。通过Actuator,只需极少的配置即可轻松地将您的应用程序与任何外部系统集成。

在现有的POM.XML文件中检查以下Maven依赖关系:

```
<dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-actuator</artifactId>
</dependency> 
```

Spring Boot CLI是用于Spring Boot应用程序的命令行界面工具。它使用Groovy脚本,它是用于创建/管理应用程序的强大工具。

*   -run command
*   -test command
*   -grab command
*   -jar command
*   -war command
*   -install command
*   -uninstall command
*   –init command
*   -shell command
*   -help command

一些常见的Spring Boot注释是:

**@SpringBootApplication**

*   @SpringBootconfiguration
*   @ComponentScan
*   @enableAutoconfiguration

**@importAutoConfiguration**

**@AutoConfigureBefore或After或Order**

**条件注释**

*   @ConditionalOnBean和@ConditionalOnMissingBean
*   @ConditionalOnNotWebApplication和@ConditionalOnWebApplication
*   @ConditionalOnProperty
*   @ConditionalOnResource
*   @ ConditionalOnExpression
*   @ConditionalOnCloudPlatform

**/beans:** 返回应用程序中所有spring bean的完整列表

**/dump**执行线程Dump

**/env**返回当前环境中的属性列表

**/health**:有关您的应用程序健康信息

**/trace**跟踪日志

**/info** 显示任意应用程序信息

**/auditevents**审计当前应用程序中的事件信息

**/mappings**显示所有@RequestMapping路径的列表。

**/metrics**显示指标信息,例如:JVM,系统CPU,openfiles

Spring Boot使用一些宽松的规则将环境属性绑定到@configuartionproperties bean,因此环境属性名称和bean属性名称之间不需要完全匹配。

在Spring Boot中,首先在resources文件夹下创建一个名为static的文件夹。您可以将静态内容放入该文件夹。

例如,路径interviewgigapp.js将资源\static\JS\interviewgigapp.js

您可以使用以下代码引用它

```
<script src =”/js/interviewgigapp.js”> </script> 
```

自动配置是一项重要功能,它可以基于类路径上的依赖关系(例如jar,bean,属性等)自动配置应用程序,而无需开发人员进行任何操作。Spring Boot自动配置会尝试根据添加的jar依赖关系自动配置Spring应用程序。

要注册自动配置类,我们必须在META-INF/spring.factories文件中的EnableAutoConfiguration键下列出其全限定名称:

```
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.zthinker.autoconfigure.CustomAutoConfiguration 
```

如果我们使用Maven构建项目,则应将该文件放置在资源/ META-INF目录中,该目录最终将在打包阶段中提到的位置。

您可以在命令提示符下将JAR文件作为JAR文件运行spring boot应用程序,而无需设置Web服务器。但是要运行WAR文件,您需要设置一个具有servlet容器的Web服务器,例如Tomcat,underflow或Jetty,然后在其中部署WAR文件。

它是Spring Boot团队构建的Maven插件,可简化应用程序的打包。它提供了一些命令,使您可以将代码打包为半开或运行应用程序。该插件提供了使用Spring Boot应用程序的几个目标:

**spring-boot:repackage:** 创建一个可自动执行的jar或war文件。它可以替换常规工件,或者可以使用单独的分类器附加到构建生命周期。

**spring-boot:run:** 运行带有多个选项的Spring Boot应用程序以将参数传递给它。

**spring-boot:启动和停止:** 将您的Spring Boot应用程序集成到集成测试阶段,以便该应用程序在启动之前启动。

**spring-boot:build-info:** 生成供执行器使用的构建信息。

将以下属性添加到属性(或.yml)文件中:

server.http2.enabled = true。

这是一个Spring Boot工具,可以非常轻松地引导Boot或Spring Applications。

入门程序仅仅是Gradle或Maven模块,其唯一目的是提供所有必要的依赖关系以“入门”特定功能。Spring Boot Starters使引导过程变得更加轻松和快捷。启动器为您带来了必需的Maven依赖关系以及一些预定义的配置位。

*   Spring Boot的主要目的是降低LOC。
*   它提供了许多默认配置,有助于更快地引导Spring应用程序。
*   它主要用于创建 stand loan applications。
*   不需要XML配置
*   易于创建Spring应用程序。
*   它带有嵌入式TOMCAT或Jetty服务器
*   它提供了很多插件。
*   它提供了CLI应用程序。

它用于管理依赖关系并自动配置,而无需您为任何依赖关系指定版本。当我们更新Spring Boot版本时,Spring将以一致的方式自动升级所有依赖项。

Thymeleaf是用于创建Web应用程序的基于Java的库之一。它提供了在Web应用程序中提供XHTML/HTML5的支持。它是spring框架的强大模板处理引擎。

它提供了非常有用的工具集合,极大地改善了开发经验。如自动保存等。

Spring Data JPA使实现基于JPA的存储库和构建使用数据访问技术的Spring供电的应用程序变得容易。

H2是完全用Java创建的开源RDBM(理性数据库管理)系统。它可以嵌入在Java应用程序中,也可以在客户端服务器模式下运行。或它是可以在内存中运行的轻量级数据库。

**@SpringBootApplication** 批注是以下三个spring批注的组合,并且仅用一行代码即可提供全部三个功能。

**@configuration或@springBootConfiguration(在版本2中):** 指示类提供了Spring Boot应用程序@configuration。

**@componentScan:** 它与Spring XMLs context:component-scan元素并行提供支持。

**@enableAutoconfiguration:** 用于启用spring boot的自动配置功能。

我们可以通过在application.properties文件中指定日志级别来控制Spring Boot的日志记录。当该文件存在于类路径中时,Spring Boot会加载该文件,并且可用于配置Spring Boot和应用程序代码。

Spring Boot使用Commons Logging进行所有内部日志记录,您可以通过在application.properties文件中添加以下行来更改日志级别:

logging.level.org.springframework =debug

logging.level.com.demo =info

*   Spring Boot是基于Java的应用程序框架。
*   它避免了编写大量样板代码,注释和XML配置。
*   为了减少开发,单元测试和集成测试的时间,请提供一些默认设置。
*   自动配置,无需手动配置。
*   易于使用,但功能强大的数据库事务管理功能
*   为了提高生产力
*   简化依赖管理
*   它包括嵌入式servlet容器。
*   它允许admin支持

首先,使用–debug开关启动应用程序。

接下来,在application.properties文件中设置logging.level.root = debug属性。

最后,在提供的日志配置文件中设置root logger的日志记录级别。

*   打开 cmd或shell窗口,并使用java -jar,如下所示
*   java -jar my project-0.0.1-SNAPSHOT.jar
*   要停止使用ctrl + C
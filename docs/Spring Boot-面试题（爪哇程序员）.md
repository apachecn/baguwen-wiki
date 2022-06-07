<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是springboot

> 原文：[https://zwmst.com/1894.html](https://zwmst.com/1894.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:48:24+08:00"> 2021-08-15 </time> ](https://zwmst.com/1894.html)  用来简化spring应用的初始搭建以及开发过程 使用特定的方式来进行配置（properties或yml 文件）

创建独立的spring引用程序 main方法运行

嵌入的Tomcat 无需部署war文件

简化maven配置

自动配置spring添加对应功能starter自动化配置

spring boot来简化spring应用开发，约定大于配置，去繁从简，just run就能创建一个独立的，产品级别的应用*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring Boot 有哪些优点？

> 原文：[https://zwmst.com/1896.html](https://zwmst.com/1896.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:48:34+08:00"> 2021-08-15 </time> ](https://zwmst.com/1896.html)  Spring Boot 的优点有：

1、减少开发，测试时间和努力。

2、使用 JavaConfig 有助于避免使用 XML。

3、避免大量的 Maven 导入和各种版本冲突。

4、提供意见发展方法。

5、通过提供默认值快速开始开发。

6、没有单独的 Web 服务器需要。这意味着你不再需要启动 Tomcat，Glassfish或其他任何 东西。

7、需要更少的配置 因为没有 web.xml 文件。只需添加用@ Configuration 注释的类，然后 添加用@Bean 注释的方法，Spring 将自动加载对象并像以前一样对其进行管理。您甚至可以 将@Autowired 添加到 bean 方法中，以使 Spring 自动装入需要的依赖关系中。

8、基于环境的配置 使用这些属性，您可以将您正在使用的环境传递到应用程序：Dspring.profiles.active = {enviornment}。在加载主应用程序属性文件后，Spring 将在 （application{environment} .properties）中加载后续的应用程序属性文件。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 创建一个 Spring Boot Project 的最简单的方法是什么？

> 原文：[https://zwmst.com/1898.html](https://zwmst.com/1898.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:48:46+08:00"> 2021-08-15 </time> ](https://zwmst.com/1898.html)  Spring Initializr是启动 Spring Boot Projects 的一个很好的工具。

![image-20210813203406199](img/48715026902ef4c96fcfe3de62489b09.png)

就像上图中所展示的一样，我们需要做一下几步：

登录 Spring Initializr，按照以下方式进行选择：

选择 com.in28minutes.springboot 为组

选择 studet-services 为组件

选择下面的依赖项 Web Actuator DevTools

点击生 GenerateProject

将项目导入 Eclipse。文件 – 导入 – 现有的 Maven 项目*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring 和 SpringBoot 有什么不同？

> 原文：[https://zwmst.com/1900.html](https://zwmst.com/1900.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:48:57+08:00"> 2021-08-15 </time> ](https://zwmst.com/1900.html)  Spring 框架提供多种特性使得 web 应用开发变得更简便，包括依赖注入、数据绑定、切面编 程、数据存取等等。

随着时间推移，Spring 生态变得越来越复杂了，并且应用程序所必须的配置文件也令人觉得 可怕。这就是 Spirng Boot 派上用场的地方了 – 它使得 Spring 的配置变得更轻而易举。

实际上，Spring 是 unopinionated（予以配置项多，倾向性弱） 的，Spring Boot 在平台和 库的做法中更 opinionated ，使得我们更容易上手。

这里有两条 SpringBoot 带来的好处：

*   根据 classpath 中的 artifacts 的自动化配置应用程序

*   提供非功能性特性例如安全和健康检查给到生产环境中的应用程序*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 如何重新加载 Spring Boot 上的更改，而无需重新启动服务器？

> 原文：[https://zwmst.com/1902.html](https://zwmst.com/1902.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:49:09+08:00"> 2021-08-15 </time> ](https://zwmst.com/1902.html)  这可以使用 DEV 工具来实现。通过这种依赖关系，您可以节省任何更改，嵌入式tomcat 将重 新启动。Spring Boot 有一个开发工具（DevTools）模块，它有助于提高开发人员的生产 力。Java 开发人员面临的一个主要挑战是将文件更改自动部署到服务器并自动重启服务器。开 发人员可以重新加载 Spring Boot 上的更改，而无需重新启动服务器。这将消除每次手动部署 更改的需要。Spring Boot 在发布它的第一个版本时没有这个功能。这是开发人员最需要的功 能。DevTools 模块完全满足开发人员的需求。该模块将在生产环境中被禁用。它还提供 H2 数据库控制台以更好地测试应用程序。

```
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-devtools</artifactId>
  <optional>true</optional>
</dependency>
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring Boot 中的监视器是什么？

> 原文：[https://zwmst.com/1904.html](https://zwmst.com/1904.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:49:20+08:00"> 2021-08-15 </time> ](https://zwmst.com/1904.html)  Spring boot actuator 是 spring 启动框架中的重要功能之一。Spring boot 监视器可帮助您 访问生产环境中正在运行的应用程序的当前状态。有几个指标必须在生产环境中进行检查和监 控。即使一些外部应用程序可能正在使用这些服务来向相关人员触发警报消息。监视器模块公 开了一组可直接作为 HTTP URL 访问的REST 端点来检查状态。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 如何在 Spring Boot 中禁用 Actuator 端点安全性？

> 原文：[https://zwmst.com/1906.html](https://zwmst.com/1906.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:49:37+08:00"> 2021-08-15 </time> ](https://zwmst.com/1906.html)  默认情况下，所有敏感的 HTTP 端点都是安全的，只有具有 ACTUATOR 角色的用户才能访问 它们。安全性是使用标准的 HttpServletRequest.isUserInRole 方法实施的。 我们可以使用 来禁用安全性。只有在执行机构端点在防火墙后访问时，才建议禁用安全性。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 怎么使用 Maven 来构建一个 SpringBoot 程序？

> 原文：[https://zwmst.com/1908.html](https://zwmst.com/1908.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:49:48+08:00"> 2021-08-15 </time> ](https://zwmst.com/1908.html)  就像引入其他库一样，我们可以在 Maven 工程中加入 SpringBoot 依赖。然而，最好是从 spring-boot-starter-parent 项目中继承以及声明依赖到 Spring Boot starters。这样做可以 使我们的项目可以重用 SpringBoot 的默认配置。

继承 spring-boot-starter-parent 项目依赖很简单 – 我们只需要在 pom.xml 中定义一个 parent 节点：

```
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.1.1.RELEASE</version>
</parent>
```

我们可以在 Maven central 中找到 spring-boot-starter-parent 的最新版本。

使用 starter 父项目依赖很方便，但并非总是可行。例如，如果我们公司都要求项目继承标准 POM，我们就不能依赖 SpringBoot starter 了。

这种情况，我们可以通过对 POM 元素的依赖管理来处理：

```
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-dependencies</artifactId>
      <version>2.1.1.RELEASE</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring Initializr 是创建 Spring Boot Projects 的唯一方法吗？

> 原文：[https://zwmst.com/1910.html](https://zwmst.com/1910.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:50:02+08:00"> 2021-08-15 </time> ](https://zwmst.com/1910.html)  不是的。

Spring Initiatlizr 让创建 Spring Boot 项目变的很容易，但是，你也可以通过设置一个 maven 项目并添加正确的依赖项来开始一个项目。

在我们的 Spring 课程中，我们使用两种方法来创建项目。

第一种方法是 start.spring.io 。

另外一种方法是在项目的标题为“Basic Web Application”处进行手动设置。

手动设置一个 maven 项目

这里有几个重要的步骤：

*   在 Eclipse 中，使用文件 – 新建 Maven 项目来创建一个新项目

*   添加依赖项。

*   添加 maven 插件。

*   添加 Spring Boot 应用程序类。

到这里，准备工作已经做好！*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 为什么我们需要 spring-boot-maven-plugin?

> 原文：[https://zwmst.com/1912.html](https://zwmst.com/1912.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:50:19+08:00"> 2021-08-15 </time> ](https://zwmst.com/1912.html)  spring-boot-maven-plugin 提供了一些像 jar 一样打包或者运行应用程序的命令。

*   spring-boot:run 运行你的 SpringBooty 应用程序。
*   spring-boot：repackage 重新打包你的 jar 包或者是 war 包使其可执行
*   spring-boot：start 和 spring-boot：stop 管理 Spring Boot 应用程序的生命周期 （也可以说是为了集成测试）。
*   spring-boot:build-info 生成执行器可以使用的构造信息。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是嵌入式服务器？我们为什么要使用嵌入式服务器呢?

> 原文：[https://zwmst.com/1914.html](https://zwmst.com/1914.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:50:30+08:00"> 2021-08-15 </time> ](https://zwmst.com/1914.html)  思考一下在你的虚拟机上部署应用程序需要些什么。

第一步： 安装 Java

第二部： 安装 Web 或者是应用程序的服务器（Tomat/Wbesphere/Weblogic 等等）

第三部： 部署应用程序 war 包

如果我们想简化这些步骤，应该如何做呢？

让我们来思考如何使服务器成为应用程序的一部分？

你只需要一个安装了 Java 的虚拟机，就可以直接在上面部署应用程序了， 是不是很爽？

这个想法是嵌入式服务器的起源。

当我们创建一个可以部署的应用程序的时候，我们将会把服务器（例如，tomcat）嵌入到可部 署的服务器中。

例如，对于一个 Spring Boot 应用程序来说，你可以生成一个包含 Embedded Tomcat 的应 用程序 jar。你就可以想运行正常 Java 应用程序一样来运行 web 应用程序了。

嵌入式服务器就是我们的可执行单元包含服务器的二进制文件（例如，tomcat.jar）。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 如何在 Spring Boot 中添加通用的 JS 代码？

> 原文：[https://zwmst.com/1916.html](https://zwmst.com/1916.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:50:42+08:00"> 2021-08-15 </time> ](https://zwmst.com/1916.html)  在源文件夹下，创建一个名为 static 的文件夹。然后，你可以把你的静态的内容放在这里面。 例如，myapp.js 的路径是 resources\static\js\myapp.js

你可以参考它在 jsp 中的使用方法：

![image-20210813203850149](img/2dd8c5c20f8afdf3d15d5835a92da18a.png)

错误：HAL browser gives me unauthorized error – Full authenticaition is required to access this resource.

该如何来修复这个错误呢？

![image-20210813203857201](img/6c7beaac656d89fe3764b0019676b95d.png)

两种方法：

方法 1：关闭安全验证 application.properties

```
management.security.enabled:FALSE
```

方法二：在日志中搜索密码并传递至请求标头中*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 如何使用 Spring Boot 部署到不同的服务器？

> 原文：[https://zwmst.com/1918.html](https://zwmst.com/1918.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:50:55+08:00"> 2021-08-15 </time> ](https://zwmst.com/1918.html)  你需要做下面两个步骤：

*   在一个项目中生成一个 war 文件。
*   将它部署到你最喜欢的服务器（websphere 或者 Weblogic 或者 Tomcat and so on）。

第一步：这本入门指南应该有所帮助：

[https://spring.io/guides/gs/convert-jar-to-war/](https://spring.io/guides/gs/convert-jar-to-war/)

第二步：取决于你的服务器。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 如何使用配置文件通过 Spring Boot 配置特定环境的配置？

> 原文：[https://zwmst.com/1920.html](https://zwmst.com/1920.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:51:07+08:00"> 2021-08-15 </time> ](https://zwmst.com/1920.html)  配置文件不是设别环境的关键。

在下面的例子中，我们将会用到两个配置文件

*   dev
*   prod

缺省的应用程序配置在 application.properties 中。让我们来看下面的例子：

application.properties

```
basic.value= true
    basic.message= Dynamic Message 
    basic.number= 100
```

我们想要为 dev 文件自定义 application.properties 属性。我们需要创建一个名为 application-dev.properties 的文件，并且重写我们想要自定义的属性。

application-dev.properties

```
basic.message: Dynamic Message in DEV
```

一旦你特定配置了配置文件，你需要在环境中设定一个活动的配置文件。

有多种方法可以做到这一点：

*   在 VM 参数中使用 Dspring.profiles.active=prod
*   在 application.properties 中使用 spring.profiles.active=prod*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是Swagger？你用Spring Boot实现了吗？

> 原文：[https://zwmst.com/1922.html](https://zwmst.com/1922.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:51:18+08:00"> 2021-08-15 </time> ](https://zwmst.com/1922.html)  Swagger 广泛用于可视化 API，使用 Swagger UI 为前端开发人员提供在线沙箱。Swagger 是用于生成 RESTful Web 服务的可视化表示的工具，规范和完整框架实现。它使文档能够以 与服务器相同的速度更新。当通过 Swagger 正确定义时，消费者可以使用最少量的实现逻辑 来理解远程服务并与其进行交互。因此，Swagger消除了调用服务时的猜测。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 如何实现Spring Boot应用程序的安全性？

> 原文：[https://zwmst.com/1924.html](https://zwmst.com/1924.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:51:29+08:00"> 2021-08-15 </time> ](https://zwmst.com/1924.html)  为了实现Spring Boot的安全性，使用spring-boot-starter-security依赖项，并且必须添加 安全配置。它只需要很少代码。配置类将必须扩展WebSecurityConfigurerAdapter并覆盖其 方法。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 比较一下Spring Security和Shiro各自的优缺点？

> 原文：[https://zwmst.com/1926.html](https://zwmst.com/1926.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:51:39+08:00"> 2021-08-15 </time> ](https://zwmst.com/1926.html)  由于Spring Boot官方提供了大量的非常方便的开箱即用的Starter，包括Spring Security的 Starter，使得在SpringBoot中使用Spring Security变得更加容易，甚至只需要添加一个一来 就可以保护所有接口，所以如果是SpringBoot项目，一般选择Spring Security。当然这只是 一个建议的组合，单纯从技术上来说，无论怎么组合，都是没有问题的。

Shiro和Spring Security相比，主要有如下特点：

Spring Security是一个重量级的安全管理框架；Shiro则是一个轻量级的安全管理框架； Spring Security概念复杂，配置繁琐；Shiro概念简单、配置简单； Spring Security功能强大；Shiro功能简单*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring Boot中如何解决跨域问题？

> 原文：[https://zwmst.com/1928.html](https://zwmst.com/1928.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:51:50+08:00"> 2021-08-15 </time> ](https://zwmst.com/1928.html)  跨域可以在前端通过JSONP来解决，但是JSONP只可以发送GET请求，无法发送其他类型的请 求，在RESTful风格的应用中，就显得非常鸡肋，因此推荐在后端通过（CORS，Crossorigin resource sharing）来解决跨域问题。这种解决方案并非Spring Boot特有的，在传统 的SSM框架中，就可以通过CORS来解决跨域问题，只不过之前我们是在XML文件中配置 CORS，现在可以通过实现WebMvcConfigurer接口然后重addCorsMappings方法解决跨 域问题。

```
@Configuration
public class CorsConfig implements WebMvcConfigurer {

  @Override
  public void addCorsMappings(CorsRegistry registry) {
    registry.addMapping("/**").allowedOrigins("*").allowCredentials(true).allowedMethods("GET", "POST", "PUT", "DELETE", "OPTIONS").maxAge(3600);

  }

}
```

项目中前后端分离部署，所以需要解决跨域的问题。

我们使用cookie存放用户登录的信息，在spring拦截器进行权限控制，当权限不符合时，直接 返回给用户固定的json结果。

当用户登录以后，正常使用；当用户退出登录状态时或者token过期时，由于拦截器和跨域的 顺序有问题，出现了跨域的现象。

我们知道一个http请求，先走filter，到达servlet后才进行拦截器的处理，如果我们把cors放在filter里，就可以优先于权限拦截器执行。

```
@Configuration
public class CorsConfig {
    @Bean
    public CorsFilter corsFilter() {
      CorsConfiguration corsConfiguration = new CorsConfiguration();
      corsConfiguration.addAllowedOrigin("*");
      corsConfiguration.addAllowedHeader("*");
      corsConfiguration.addAllowedMethod("*");
      corsConfiguration.setAllowCredentials(true);
      UrlBasedCorsConfigurationSource urlBasedCorsConfigurationSource = new UrlBasedCorsConfigurationSource();
      urlBasedCorsConfigurationSource.registerCorsConfiguration("/**", corsConfiguration);
      return new CorsFilter(urlBasedCorsConfigurationSource);
    }
}
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Spring Boot的核心注解是哪些？他由哪几个注解组成的？

> 原文：[https://zwmst.com/1930.html](https://zwmst.com/1930.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:52:02+08:00"> 2021-08-15 </time> ](https://zwmst.com/1930.html)  启动类上面的注解是@SpringBootApplication，他也是SpringBoot的核心注解，主要组合 包含了以下3个注解：

@SpringBootConfiguration：组合了@Configuration注解，实现配置文件的功能；

@EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项，如 关闭数据源自动配置的功能：@SpringBootApplication(exclude= {DataSourceAutoConfiguration.class})；

@ComponentScan：Spring组件扫描。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 保护SpringBoot应用有哪些方法？

> 原文：[https://zwmst.com/1932.html](https://zwmst.com/1932.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:52:13+08:00"> 2021-08-15 </time> ](https://zwmst.com/1932.html)  在生产中使用HTTPS

使用Snyk检查你的依赖关系

升级到最新版本

启用CSRF保护

使用内容安全策略防止XSS攻击*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# SpringBoot 2.X有哪些新特性？与1.X有什么区别？

> 原文：[https://zwmst.com/1934.html](https://zwmst.com/1934.html)

   [ *Spring Boot* ](https://zwmst.com/spring-boot)*[ <time datetime="2021-08-15T16:52:28+08:00"> 2021-08-15 </time> ](https://zwmst.com/1934.html)  配置变更

JDK版本升级

第三方类库升级

响应式Spring编程支持

HTTP/2支持

配置属性绑定

更多改进与加强*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Servlet的生命周期？

> 原文：[https://zwmst.com/1428.html](https://zwmst.com/1428.html)

—根据Servlet的配置参数1来决定实例化时机，没有配置该参数项或者为负数，则第一次访 问的时候才会被实例化并调用init () 函数，如果为0或者正整数，则服务器启动的时候就会被 加载，加载顺序由小到达。Servlet 通过调用 init () 方法进行初始化。

—客户端请求到达后，Servlet 调用 service() 方法来处理客户端的请求。

—服务器关闭，或者Servlet长时间没有使用，Servlet 通过调用 destroy() 方法终止（结 束）。

—最后，Servlet 是由 JVM 的垃圾回收器进行垃圾回收的。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Servlet和JSP的区别？

> 原文：[https://zwmst.com/1430.html](https://zwmst.com/1430.html)

Servlet是服务器端的程序，动态生成html页面发送到客户端，但是这样程序里会有很多 out.println(),java与html语言混在一起很乱，造成编写逻辑控制的后台工程师和设计前端网 页的前端工程师彼此很难独立开展工作，所以后来sun公司推出了JSP，其实JSP就是Servlet， 每次运行的时候JSP都首先被编译成servlet文件，然后再被编译成.class文件运行。有了jsp，在MVC项目中servlet不再负责动态生成页面，转而去负责控制程序逻辑的作用，控制jsp与 javabean之间的流转。其实对jsp也有封装的模板工具velocity和freemarker。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Servlet的基本架构

> 原文：[https://zwmst.com/1432.html](https://zwmst.com/1432.html)

```
public class ServletName extends HttpServlet {
    public void doPost(HttpServletRequest request, HttpServletResponse response) 
        throws ServletException, IOException {

    }

    public void doGet(HttpServletRequest request, HttpServletResponse response) 
        throws ServletException, IOException {

    }
}
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么情况下调用doGet()和doPost()？

> 原文：[https://zwmst.com/1434.html](https://zwmst.com/1434.html)

JSP页面中的form标签里的method属性为get时调用doGet()，为post时调用doPost()；超链接跳转页面时调用doGet()*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 页面间对象传递的方法

> 原文：[https://zwmst.com/1436.html](https://zwmst.com/1436.html)

request，session，application，cookie等*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 四种会话跟踪技术

> 原文：[https://zwmst.com/1438.html](https://zwmst.com/1438.html)

会话作用域ServletsJSP 页面描述

1）page否是代表与一个页面相关的对象和属性。一个页面由一个编译好的 Java servlet 类 （可以带有任何的 include 指令，但是没有 include 动作）表示。这既包括 servlet 又包括被 编译成 servlet 的 JSP 页面

2）request是是代表与 Web 客户机发出的一个请求相关的对象和属性。一个请求可能跨越多 个页面，涉及多个 Web 组件（由于 forward 指令和 include 动作的关系）

3）session是是代表与用于某个 Web 客户机的一个用户体验相关的对象和属性。一个 Web 会 话可以也经常会跨越多个客户机请求

4）application是是代表与整个 Web 应用程序相关的对象和属性。这实质上是跨越整个 Web 应用程序，包括多个页面、请求和会话的一个全局作用域*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Request对象的主要方法

> 原文：[https://zwmst.com/1440.html](https://zwmst.com/1440.html)

setAttribute(String name,Object)：设置名字为name的request的参数值

getAttribute(String name)：返回由name指定的属性值

getAttributeNames()：返回request对象所有属性的名字集合，结果是一个枚举的实例

getCookies()：返回客户端的所有Cookie对象，结果是一个Cookie数组

getCharacterEncoding()：返回请求中的字符编码方式

getContentLength()：返回请求的Body的长度

getHeader(String name)：获得HTTP协议定义的文件头信息

getHeaders(String name)：返回指定名字的request Header的所有值，结果是一个枚举的 实例

getHeaderNames()：返回所以request Header的名字，结果是一个枚举的实例

getInputStream()：返回请求的输入流，用于获得请求中的数据

getMethod()：获得客户端向服务器端传送数据的方法

getParameter(String name)：获得客户端传送给服务器端的有name指定的参数值

getParameterNames()：获得客户端传送给服务器端的所有参数的名字，结果是一个枚举的 实例

getParameterValues(String name)：获得有name指定的参数的所有值

getProtocol()：获取客户端向服务器端传送数据所依据的协议名称

getQueryString()：获得查询字符串

getRequestURI()：获取发出请求字符串的客户端地址

getRemoteAddr()：获取客户端的IP地址

getRemoteHost()：获取客户端的名字

getSession([Boolean create])：返回和请求相关Session

getServerName()：获取服务器的名字

getServletPath()：获取客户端所请求的脚本文件的路径

getServerPort()：获取服务器的端口号

removeAttribute(String name)：删除请求中的一个属性*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 如何配置Servlet的初始化参数？

> 原文：[https://zwmst.com/1442.html](https://zwmst.com/1442.html)

在web.xml中该Servlet的定义标记中，比如：

```
 <servlet>
     <servlet-name>TimeServlet</servlet-name>
     <servlet-class>
         com.allanlxf.servlet.basic.TimeServlet
     </servlet-class>
     <init-param>
         <param-name>user</param-name>
         <param-value>username</param-value>
     </init-param>
     <init-param>
         <param-name>blog</param-name>
         <param-value>http://。。。</param-value>
     </init-param>
 </servlet>
```

配置了两个初始化参数user和blog它们的值分别为**username**和http://。。。， 这样以后要修改用户名和博客的地址不需要修改Servlet代码，只需修改配置文件即可。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 如何读取Servlet的初始化参数？

> 原文：[https://zwmst.com/1444.html](https://zwmst.com/1444.html)

ServletConfig中定义了如下的方法用来读取初始化参数的信息： public String getInitParameter(String name)

参数：初始化参数的名称。

返回：初始化参数的值，如果没有配置，返回null。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# init(ServletConfig)方法执行次数

> 原文：[https://zwmst.com/1446.html](https://zwmst.com/1446.html)

该方法执行在单线程的环境下，因此开发者不用考虑线程安全的问题。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# init(ServletConfig)方法与异常

> 原文：[https://zwmst.com/1448.html](https://zwmst.com/1448.html)

该方法在执行过程中可以抛出ServletException来通知Web服务器Servlet实例初始化失败。 一旦ServletException抛出，Web服务器不会将客户端请求交给该Servlet实例来处理，而是 报告初始化失败异常信息给客户端，该Servlet实例将被从内存中销毁。如果在来新的请求， Web服务器会创建新的Servlet实例，并执行新实例的初始化操作*
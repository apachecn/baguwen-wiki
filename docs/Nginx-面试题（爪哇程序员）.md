<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 请解释一下什么是 Nginx ？

> 原文：[https://zwmst.com/1482.html](https://zwmst.com/1482.html)

Nginx ，是一个 Web 服务器和反向代理服务器，用于 HTTP、HTTPS、SMTP、POP3 和 IMAP 协议。

目前使用的最多的 Web 服务器或者代理服务器，像淘宝、新浪、网易、迅雷等都在使用。

Nginx 的主要功能如下：

作为 http server (代替 Apache ，对 PHP 需要 FastCGI 处理器支持)

FastCGI：Nginx 本身不支持 PHP 等语言，但是它可以通过 FastCGI 来将请求扔给某些语言 或框架处理。

反向代理服务器

实现负载均衡

虚拟主机*


# 为什么要用Nginx？

> 原文：[https://zwmst.com/1484.html](https://zwmst.com/1484.html)

跨平台、配置简单、方向代理、高并发连接：处理2-3万并发连接数，官方监测能支持5万并 发，内存消耗小：开启10个nginx才占150M内存 ，nginx处理静态文件好，耗费内存少，

而且Nginx内置的健康检查功能：如果有一个服务器宕机，会做一个健康检查，再发送的请求 就不会发送到宕机的服务器了。重新将请求提交到其他的节点上。

使用Nginx的话还能：

节省宽带：支持GZIP压缩，可以添加浏览器本地缓存

稳定性高：宕机的概率非常小

接收用户请求是异步的*


# Nginx怎么处理请求的？

> 原文：[https://zwmst.com/1486.html](https://zwmst.com/1486.html)

nginx接收一个请求后，首先由listen和server_name指令匹配server模块，再匹配 server模块里的location，location就是实际地址

```
server { # 第一个Server区块开始，表示一个独立的虚拟主机站点
    listen 80; # 提供服务的端口，默认80

    server_name localhost; # 提供服务的域名主机名

    location / { # 第一个location区块开始 
        root html; # 站点的根目录，相当于Nginx的安装目录
        index index.html; # 默认的首页文件，多个用空格分开
    }
}
```*


# Nginx的优缺点？

> 原文：[https://zwmst.com/1488.html](https://zwmst.com/1488.html)

优点：

占内存小，可实现高并发连接，处理响应快

可实现http服务器、虚拟主机、方向代理、负载均衡 Nginx配置简单

可以不暴露正式的服务器IP地址

缺点：

动态处理差：nginx处理静态文件好,耗费内存少，但是处理动态页面则很鸡肋，现在一般前端 用nginx作为反向代理抗住压力，*


# Nginx应用场景？

> 原文：[https://zwmst.com/1490.html](https://zwmst.com/1490.html)

http服务器。Nginx是一个http服务可以独立提供http服务。可以做网页静态服务器。

虚拟主机。可以实现在一台服务器虚拟出多个网站，例如个人网站使用的虚拟机。

反向代理，负载均衡。当网站的访问量达到一定程度后，单台服务器不能满足用户的请求时， 需要用多台服务器集群可以使用nginx做反向代理。并且多台服务器可以平均分担负载，不会 应为某台服务器负载高宕机而某台服务器闲置的情况。

nginx 中也可以配置安全管理、比如可以使用Nginx搭建API接口网关,对每个接口服务进行拦截。*


# 使用“反向代理服务器”的优点是什么?

> 原文：[https://zwmst.com/1492.html](https://zwmst.com/1492.html)

反向代理服务器可以隐藏源服务器的存在和特征。它充当互联网云和web服务器之间的中间层。这对于安全方面来说是很好的，特别是当您使用web托管服务时。*


# 列举Nginx服务器的最佳用途。

> 原文：[https://zwmst.com/1494.html](https://zwmst.com/1494.html)

Nginx服务器的最佳用法是在网络上部署动态HTTP内容，使用SCGI、WSGI应用程序服务 器、用于脚本的FastCGI处理程序。它还可以作为负载均衡器。*


# 请解释Nginx如何处理HTTP请求。

> 原文：[https://zwmst.com/1496.html](https://zwmst.com/1496.html)

Nginx使用反应器模式。主事件循环等待操作系统发出准备事件的信号，这样数据就可以从套 接字读取，在该实例中读取到缓冲区并进行处理。单个线程可以提供数万个并发连接。*


# 在Nginx中，如何使用未定义的服务器名称来阻止处理请求?

> 原文：[https://zwmst.com/1498.html](https://zwmst.com/1498.html)

只需将请求删除的服务器就可以定义为：

```
Server {
    listen 80; 
    server_name “ “ ; 
    return 444;
}
```

这里，服务器名被保留为一个空字符串，它将在没有“主机”头字段的情况下匹配请求，而一个 特殊的Nginx的非标准代码444被返回，从而终止连接。*


# 在Nginx中如何在URL中保留双斜线?

> 原文：[https://zwmst.com/1500.html](https://zwmst.com/1500.html)

要在URL中保留双斜线，就必须使用merge_slashes_off；语法:merge_slashes [on/off] ； 默认值: merge_slashes on ；环境: http，server*


# ngx_http_upstream_module的作用是什么?

> 原文：[https://zwmst.com/1502.html](https://zwmst.com/1502.html)

ngx_http_upstream_module用于定义可通过fastcgi传递、proxy传递、uwsgi传递、 memcached传递和scgi传递指令来引用的服务器组。*


# fastcgi 与 cgi 的区别？

> 原文：[https://zwmst.com/1504.html](https://zwmst.com/1504.html)

1）cgi

web 服务器会根据请求的内容，然后会 fork 一个新进程来运行外部 c 程序（或 perl 脚 本…）， 这个进程会把处理完的数据返回给 web 服务器，最后 web 服务器把内容发送给用 户，刚才 fork 的进程也随之退出。

如果下次用户还请求改动态脚本，那么 web 服务器又再次 fork 一个新进程，周而复始的进行。

2）fastcgi

web 服务器收到一个请求时，他不会重新 fork 一个进程（因为这个进程在 web 服务器启动时 就开启了，而且不会退出），web 服务器直接把内容传递给这个进程（进程间通信，但 fastcgi 使用了别的方式，tcp 方式通信），这个进程收到请求后进行处理，把结果返回给 web 服务器，最后自己接着等待下一个请求的到来，而不是退出。

综上，差别在于是否重复 fork 进程，处理请求。*


# Nginx 常用命令？

> 原文：[https://zwmst.com/1506.html](https://zwmst.com/1506.html)

启动 nginx 。

停止 nginx -s stop 或 nginx -s quit 。

重载配置 ./sbin/nginx -s reload(平滑重启) 或 service nginx reload 。

重载指定配置文件 .nginx -c /usr/local/nginx/conf/nginx.conf 。

查看 nginx 版本 nginx -v 。

检查配置文件是否正确 nginx -t 。

显示帮助信息 nginx -h 。*


# Nginx 常用配置？

> 原文：[https://zwmst.com/1508.html](https://zwmst.com/1508.html)

```
worker_processes 8; # 工作进程个数
worker_connections 65535; # 每个工作进程能并发处理（发起）的最大连接数（包含所有 连接数）
error_log /data/logs/nginx/error.log; # 错误日志打印地址
access_log /data/logs/nginx/access.log; # 进入日志打印地址
log_format main '$remote_addr"$request" ''$status $upstream_addr
"$request_time"'; # 进入日志格式

## 如果未使用 fastcgi 功能的，可以无视
fastcgi_connect_timeout=300; # 连接到后端 fastcgi 超时时间
fastcgi_send_timeout=300; # 向 fastcgi 请求超时时间(这个指定值已经完成两次握手
后向fastcgi传送请求的超时时间)
fastcgi_rend_timeout=300; # 接收 fastcgi 应答超时时间，同理也是2次握手后
fastcgi_buffer_size=64k; # 读取 fastcgi 应答第一部分需要多大缓冲区，该值表示使用 1个64kb的缓冲区读取应答第一部分(应答头),可以设置为fastcgi_buffers选项缓冲区大小 
fastcgi_buffers 4 64k; # 指定本地需要多少和多大的缓冲区来缓冲fastcgi应答请求，假 设一个php或java脚本所产生页面大小为256kb,那么会为其分配4个64kb的缓冲来缓存 
fastcgi_cache TEST; # 开启fastcgi缓存并为其指定为TEST名称，降低cpu负载,防止502 错误发生

listen 80; # 监听端口
server_name rrc.test.jiedaibao.com; # 允许域名 
root /data/release/rrc/web; # 项目根目录
index index.php index.html index.htm; # 访问根文件
```*


# 请陈述stub_status和sub_filter指令的作用是什么?

> 原文：[https://zwmst.com/1510.html](https://zwmst.com/1510.html)

（1）Stub_status指令：该指令用于了解Nginx当前状态的当前状态，如当前的活动连接，接 受和处理当前读/写/等待连接的总数 ；

（2）Sub_filter指令：它用于搜索和替换响应中的内容，并快速修复陈旧的数据*


# 301.主从 Reactor 多线程模型

> 原文：[https://zwmst.com/3609.html](https://zwmst.com/3609.html)

服务端用于接收客户端连接的不再是个 1 个单独的 NIO 线程，而是一个独立的 NIO 线程池。Acceptor 接收到客户端 TCP 连接请求处理完成后（可能包含接入认证等），将新创建的SocketChannel 注册到 IO 线程池（sub reactor 线程池）的某个 IO 线程上，由它负责SocketChannel 的读写和编解码工作。Acceptor 线程池仅仅只用于客户端的登陆、握手和安全认证，一旦链路建立成功，就将链路注册到后端 subReactor 线程池的 IO 线程上，由 IO 线程负责后续的 IO 操作*


# 1202.请解释一下什么是 Nginx?

> 原文：[https://zwmst.com/5709.html](https://zwmst.com/5709.html)

Nginx 是一个 web 服务器和反向代理服务器，用于 HTTP、HTTPS、SMTP、POP3和 IMAP 协议。*


# 1203.请列举 Nginx 的一些特性。

> 原文：[https://zwmst.com/5712.html](https://zwmst.com/5712.html)

Nginx 服务器的特性包括：
反向代理/L7 负载均衡器
嵌入式 Perl 解释器
动态二进制升级
可用于重新编写 URL，具有非常好的 PCRE 支持*


# 1204.请解释 Nginx 如何处理 HTTP 请求。

> 原文：[https://zwmst.com/5714.html](https://zwmst.com/5714.html)

Nginx 使用反应器模式。主事件循环等待操作系统发出准备事件的信号，这样数据就可以从套接字读取，在该实例中读取到缓冲区并进行处理。单个线程可以提供数万个并发连接。*


# 1205.在 Nginx 中，如何使用未定义的服务器名称来阻止处理请求?

> 原文：[https://zwmst.com/5716.html](https://zwmst.com/5716.html)

只需将请求删除的服务器就可以定义为：

```
Server {listen 80;server_name “ “ ;return 444;}
```

这里，服务器名被保留为一个空字符串，它将在没有“主机”头字段的情况下
匹配请求，而一个特殊的 Nginx 的非标准代码 444 被返回，从而终止连接。*


# 1206\. 使用“反向代理服务器”的优点是什么?

> 原文：[https://zwmst.com/5718.html](https://zwmst.com/5718.html)

反向代理服务器可以隐藏源服务器的存在和特征。它充当互联网云和 web 服务器之间的中间层。这对于安全方面来说是很好的，特别是当您使用 web 托管服务时。*


# 1208.请解释 Nginx 服务器上的 Master 和 Worker 进程分别是什么?

> 原文：[https://zwmst.com/5722.html](https://zwmst.com/5722.html)

Master 进程：读取及评估配置和维持
Worker 进程：处理请求*


# 1209.请解释你如何通过不同于 80 的端口开启 Nginx?

> 原文：[https://zwmst.com/5724.html](https://zwmst.com/5724.html)

为了通过一个不同的端口开启 Nginx，你必须进入/etc/Nginx/sitesenabled/，如果这是默认文件，那么你必须打开名为“default”的文件。编辑文件，并放置在你想要的端口：Like server { listen 81; }*


# 1210.请解释是否有可能将 Nginx 的错误替换为 502 错误、503?

> 原文：[https://zwmst.com/5726.html](https://zwmst.com/5726.html)

502 =错误网关
503 =服务器超载
有可能，但是您可以确保 fastcgi_intercept_errors 被设置为 ON，并使用错误页面指令。
Location / {fastcgi_pass 127.0.01:9001;fastcgi_intercept_errors on;error_page 502 =503/error_page.html;#…}*


# 1211.在 Nginx 中，解释如何在 URL 中保留双斜线?

> 原文：[https://zwmst.com/5728.html](https://zwmst.com/5728.html)

要在 URL 中保留双斜线，就必须使用 merge_slashes_off;
语法:merge_slashes [on/off]
默认值: merge_slashes on
环境: http，server*


# 1212.请解释 ngx_http_upstream_module 的作用是什么?

> 原文：[https://zwmst.com/5730.html](https://zwmst.com/5730.html)

ngx_http_upstream_module 用于定义可通过 fastcgi 传递、proxy 传递、uwsgi传递、memcached 传递和 scgi 传递指令来引用的服务器组。*


# 1213.请解释什么是 C10K 问题?

> 原文：[https://zwmst.com/5732.html](https://zwmst.com/5732.html)

C10K 问题是指无法同时处理大量客户端(10,000)的网络套接字。*


# 1214.请陈述 stub_status 和 sub_filter 指令的作用是什么?

> 原文：[https://zwmst.com/5734.html](https://zwmst.com/5734.html)

Stub_status 指令：该指令用于了解 Nginx 当前状态的当前状态，如当前的活动连接，接受和处理当前读/写/等待连接的总数
Sub_filter 指令：它用于搜索和替换响应中的内容，并快速修复陈旧的数据*


# 1216.、解释如何在 Nginx 中获得当前的时间

> 原文：[https://zwmst.com/5737.html](https://zwmst.com/5737.html)

要获得 Nginx 的当前时间，必须使用 SSI 模块、$date_gmt 和$date_local 的变量。

```
Proxy_set_header THE-TIME $date_gmt;
```*


# 1217.用 Nginx 服务器解释-s 的目的是什么?

> 原文：[https://zwmst.com/5739.html](https://zwmst.com/5739.html)

用于运行 Nginx -s 参数的可执行文件。*


# 1218.解释如何在 Nginx 服务器上添加模块

> 原文：[https://zwmst.com/5741.html](https://zwmst.com/5741.html)

在编译过程中，必须选择 Nginx 模块，因为 Nginx 不支持模块的运行时间选择*
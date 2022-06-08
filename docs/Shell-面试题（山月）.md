# shell 中 ${} 与 $() 各是什么意思

> 原文：[https://q.shanyue.tech/base/linux/130.html](https://q.shanyue.tech/base/linux/130.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 130(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/130)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

*   `${}` 变量
*   `$()` 命令

# 如何判断端口是否可达

> 原文：[https://q.shanyue.tech/base/linux/146.html](https://q.shanyue.tech/base/linux/146.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 146(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/146)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

使用 `nc`，`-z` 指测试接口连通性

```
nc -vz localhost 443 
```

# 如何禁止服务器被 ping

> 原文：[https://q.shanyue.tech/base/linux/163.html](https://q.shanyue.tech/base/linux/163.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 163(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/163)

Author

回答者: [iSenninha(opens new window)](https://github.com/iSenninha)

> echo "1" > /proc/sys/net/ipv4/icmp_echo_ignore_all

[How do I disable ping responses from my system? (opens new window)](https://access.redhat.com/articles/7134#:~:text=To%20configure%20a%20Red%20Hat,command%20as%20the%20root%20user.&text=To%20make%20the%20changes%20persistent,to%20ICMP%20(ping)%20net.)

# 在服务器内如何得知自己的公网 IP

> 原文：[https://q.shanyue.tech/base/linux/172.html](https://q.shanyue.tech/base/linux/172.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 172(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/172)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

有现成的公网 IP 服务提供，根据 TCP 连接获得真实 IP 地址

```
$ curl ifconfig.me 
```

# ssh 如何设置 IP whiteList

> 原文：[https://q.shanyue.tech/base/linux/180.html](https://q.shanyue.tech/base/linux/180.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 180(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/180)

# 如何判断文件中的换行符是 LF 还是 CRLF

> 原文：[https://q.shanyue.tech/base/linux/200.html](https://q.shanyue.tech/base/linux/200.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 200(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/200)

# 如何查看 node_modules(某一文件夹) 的体积有多大

> 原文：[https://q.shanyue.tech/base/linux/278.html](https://q.shanyue.tech/base/linux/278.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 278(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/278)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

`du` (disk usage) 命令可以查看磁盘的使用情况，从它可以看出来文件及目录的大小

```
# -d 搜索深度，0 指当前目录
# -h 以可读性的方式显示大小
$ du -hd 0 node_modules
132M    node_modules 
```

同理，可以使用以下命令查看 `node_modules` 下每个目录所占的大小

```
$ du -hd 1 node_modules 
```

# 服务器的平均负载如何计算

> 原文：[https://q.shanyue.tech/base/linux/299.html](https://q.shanyue.tech/base/linux/299.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 299(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/299)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

`load average` 指单位时间内运行态进程及不可中断进程的平均进程数，运行态进程指正在使用或者 等待使用 CPU 的进程，不可中断进程指正等待一些 IO 操作的进程。可使用 `uptime` 查看此指标。

```
$ uptime
 16:48:09 up 2 days, 23:43,  2 users,  load average: 0.01, 0.21, 0.20 
```

# 多服务器的系统时间不一致如何解决

> 原文：[https://q.shanyue.tech/base/linux/304.html](https://q.shanyue.tech/base/linux/304.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 304(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/304)

Author

回答者: [vincent-sk(opens new window)](https://github.com/vincent-sk)

ntp 服务

# 什么是 CPU 缓存，如何查看缓存命中率

> 原文：[https://q.shanyue.tech/base/linux/414.html](https://q.shanyue.tech/base/linux/414.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 414(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/414)

Author

回答者: [edisonwd(opens new window)](https://github.com/edisonwd)

CPU 缓存介于 CPU 和内存之间，缓存的是热点的内存数据。这些缓存按照大小不同分为 L1、L2、L3 等三级缓存，其中 L1 和 L2 在同一个 cpu 核中， 而在同一个 CPU 插槽中的多个核共享一个 L3 缓存。

缓存命中率，即直接通过缓存获取数据的请求次数，占所有数据请求次数的百分比。当可以直接通过缓存获取到需要的数据，则命中缓存；否则需要从磁盘等地方读取获取数据。缓存命中率越高，表示直接从缓存获取数据的次数越多，程序执行效率越高。 使用 cachestat 可以查看整个个操作系统缓存的读写命中情况： cachestat 安装方式： `sudo apt install perf-tools-unstable`

下面以 1 秒间隔输出三组缓存信息：

```
$ sudo cachestat 1
Counting cache functions... Output every 1 seconds.
    HITS   MISSES  DIRTIES    RATIO   BUFFERS_MB   CACHE_MB
    1989        0       13   100.0%          501       2600
   12969        0     1412   100.0%          501       2600
   16798        0     2803   100.0%          501       2600 
```

从结果可以看到，HITS 是缓存命中的次数；MISSES 是缓存未命中的次数；DIRTIES 是表示新增到缓存中的脏页数；BUFFERS_MB 表示 Buffers 的大小，单位为 MB；CACHED_MB 表示 Cache 的大小，单位为 MB。

# 什么是 exit code

> 原文：[https://q.shanyue.tech/base/linux/424.html](https://q.shanyue.tech/base/linux/424.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 424(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/424)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

`exit code` 代表一个进程的返回码，通过系统调用 `exit_group` 来触发。在 `POSIX` 中，`0` 代表正常的返回码，`1-255` 代表异常返回码，一般主动抛出的错误码都是 `1`。

这里有一张关于异常码的附表 [Appendix E. Exit Codes With Special Meanings(opens new window)](http://www.tldp.org/LDP/abs/html/exitcodes.html)。

异常码在操作系统中随处可见，以下是一个关于 `cat` 命令的异常以及它的 `exit code`，并使用 `strace` 追踪系统调用。

```
$ cat a
cat: a: No such file or directory

# 使用 strace 查看 cat 的系统调用
# -e 只显示 write 与 exit_group 的系统调用
$ strace -e write,exit_group cat a
write(2, "cat: ", 5cat: )                    = 5
write(2, "a", 1a)                        = 1
write(2, ": No such file or directory", 27: No such file or directory) = 27
write(2, "\n", 1
)                       = 1
exit_group(1)                           = ?
+++ exited with 1 +++ 
```

从系统调用的最后一行可以看出，该进行的 `exit code` 是 1，并把错误信息输出到 `stderr` (标准错误的 fd 为 2) 中

## 如何查看 exit code

从 `strace` 中可以来判断进程的 `exit code`，但是不够方便过于冗余，特别身处 shell 编程环境中。

**有一种简单的方法，通过 `echo $?` 来确认返回码**

```
$ cat a
cat: a: No such file or directory

$ echo $?
1 
```

# 什么是 coredump，如何配置与分析

> 原文：[https://q.shanyue.tech/base/linux/425.html](https://q.shanyue.tech/base/linux/425.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 425(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/425)

# shell

# source 与 sh 执行脚本时有何区别

> 原文：[https://q.shanyue.tech/base/shell/316.html](https://q.shanyue.tech/base/shell/316.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 316(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/316)

Author

回答者: [Asarua(opens new window)](https://github.com/Asarua)

source 执行是在当前环境下执行 sh 执行会新开一个子运行环境，结束后子脚本中的变量无法访问 因此当配置.zshrc 这种文件时，通常会 source 一下

# npm 执行命令传递参数时，为何需要双横线

> 原文：[https://q.shanyue.tech/base/shell/719.html](https://q.shanyue.tech/base/shell/719.html)

更多描述

如在`npm script` 中有以下命令：

```
{
  "start": "serve"
} 
```

其中 `serve` 可通过 `--port` 指定端口号：

```
$ npm start -- --port 8080

# 而在 yarn 时无需传递参数
$ yarn start --port 8080 
```

那为什么 npm 执行命令传递参数时，为何需要双横线

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 719(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/719)

Author

回答者: [iceycc(opens new window)](https://github.com/iceycc)

https://github.com/npm/npm/pull/5518 npm 脚本执行时会开启一个 shell，执行后面指定的脚本命令或文件， -- 是为了给后面 shell 脚本命令传递参数，类似 node 环境的 process.argv 的吧。
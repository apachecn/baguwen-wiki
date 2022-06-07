<!--yml
category: DevOps
date: 0001-01-01 00:00:00
-->

# Docker 面试题（爪哇程序员）

# 什么是Docker

> 原文：[https://zwmst.com/1097.html](https://zwmst.com/1097.html)

Docker是一个容器化平台，它以容器的形式将您的应用程序及其所有依赖项打包在一起，以确 保您的应用程序在任何环境中无缝运行。


# Docker与虚拟机有何不同

> 原文：[https://zwmst.com/1099.html](https://zwmst.com/1099.html)

Docker不是虚拟化方法。它依赖于实际实现基于容器的虚拟化或操作系统级虚拟化的其他工 具。为此，Docker最初使用LXC驱动程序，然后移动到libcontainer现在重命名为runc。

Docker主要专注于在应用程序容器内自动部署应用程序。应用程序容器旨在打包和运行单个服 务，而系统容器则设计为运行多个进程，如虚拟机。因此，Docker被视为容器化系统上的容器 管理或应用程序部署工具。

A 容器不需要引导操作系统内核，因此可以在不到一秒的时间内创建容器。此功能使基于容器 的虚拟化比其他虚拟化方法更加独特和可取。

B 由于基于容器的虚拟化为主机增加了很少或没有开销，因此基于容器的虚拟化具有接近本机 的性能。

C 对于基于容器的虚拟化，与其他虚拟化不同，不需要其他软件。

D 主机上的所有容器共享主机的调度程序，从而节省了额外资源的需求。

E 与虚拟机映像相比，容器状态（Docker或LXC映像）的大小很小，因此容器映像很容易分 发。

F 容器中的资源管理是通过cgroup实现的。Cgroups不允许容器消耗比分配给它们更多的资 源。虽然主机的所有资源都在虚拟机中可见，但无法使用。这可以通过在容器和主机上同时运 行top或htop来实现。所有环境的输出看起来都很相似。


# 什么是Docker镜像

> 原文：[https://zwmst.com/1101.html](https://zwmst.com/1101.html)

Docker镜像是Docker容器的源代码，Docker镜像用于创建容器。使用build命令创建镜像。


# 什么是Docker容器

> 原文：[https://zwmst.com/1103.html](https://zwmst.com/1103.html)

Docker容器包括应用程序及其所有依赖项，作为操作系统的独立进程运行。


# Docker容器有几种状态

> 原文：[https://zwmst.com/1105.html](https://zwmst.com/1105.html)

四种状态：运行、已暂停、重新启动、已退出。


# DockerFile中最常见的指定是什么?

> 原文：[https://zwmst.com/1107.html](https://zwmst.com/1107.html)

| 指令 | 备注 |
| --- | --- |
| FROM | 指定基础镜像 |
| LABEL | 功能为镜像指定标签 |
| RUN | 运行指定命令 |
| CMD | 容器启动时要运行的命令 |


# DockerFile中的命令COPY和ADD命令有什么区别？

> 原文：[https://zwmst.com/1109.html](https://zwmst.com/1109.html)

COPY和ADD的区别时COPY的SRC只能是本地文件，其他用法一致。


# Docker的常用命令？

> 原文：[https://zwmst.com/1111.html](https://zwmst.com/1111.html)

| 命令 | 备注 |
| --- | --- |
| docker pull | 拉去或更新指定的镜像 |
| docker push | 将镜像推送到远程仓库 |
| docker rm | 删除容器 |
| docker rmi | 删除镜像 |
| docker images | 列出所有镜像 |
| docker ps | 列出所有容器 |


# 容器与主机之间的数据拷贝命令？

> 原文：[https://zwmst.com/1113.html](https://zwmst.com/1113.html)

Docker cp命令用于穷奇与主机之间的数据拷贝

*   主机到哦容器：docker cp /www 96f7f14e99ab:/www/
*   容器到主机：docker cp 96f7f14e99ab:/www /tmp


# 启动nginx容器（随机端口映射），并挂载本地文件目录到容器html的命令？

> 原文：[https://zwmst.com/1115.html](https://zwmst.com/1115.html)

```
Docker run -d -p --name nginx2 -v /home/nginx:/usr/share/nginx/html nginx
```


# 如何使用 Docker 技术创建与环境无关的容器系统？

> 原文：[https://zwmst.com/1117.html](https://zwmst.com/1117.html)

Docker 技术有三中主要的技术途径辅助完成此需求：

*   存储卷（Volumes）
*   环境变量（Environment variable）注入
*   只读（Read-only）文件系统


# 有什么方法确定一个 Docker 容器运行状态

> 原文：[https://zwmst.com/1119.html](https://zwmst.com/1119.html)

使用如下命令行命令确定一个 Docker 容器的运行状态

```
docker ps –a
```

这将列表形式输出运行在主机上的所有 Docker 容器及其运行状态。从这个列表中很容易找到 想要的容器及其运行状态。


# Docker Image 和 Docker Layer (层) 有什么不同

> 原文：[https://zwmst.com/1121.html](https://zwmst.com/1121.html)

Image ：一个 Docker Image 是由一系列 Docker 只读层（read-only Layer） 创建出来 的。

Layer： 在 Dockerfile 配置文件中完成的一条配置指令，即表示一个 Docker 层（Layer）。 如下 Dockerfile 文件包含 4 条指令，每条指令创建一个层（Layer）。

```
FROM ubuntu:15.04 
COPY . /app 
RUN make /app 
CMD python /app/app.py
```

重点，每层只对其前一层进行一（某）些进化。


# 如何停止所有正在运行的容器？

> 原文：[https://zwmst.com/1123.html](https://zwmst.com/1123.html)

使用docker kill $(sudo docker ps -q)


# 如何清理批量后台停止的容器？

> 原文：[https://zwmst.com/1125.html](https://zwmst.com/1125.html)

使用docker rm $（sudo docker ps -a -q）


# 如何临时退出一个正在交互的容器的终端，而不终止它？

> 原文：[https://zwmst.com/1127.html](https://zwmst.com/1127.html)

按Ctrl+p，后按Ctrl+q，如果按Ctrl+c会使容器内的应用进程终止，进而会使容器终止。


# Docker 群（Swarm）是什么

> 原文：[https://zwmst.com/1129.html](https://zwmst.com/1129.html)

Docker Swarm — Docker 群 — 是原生的 Docker 集群服务工具。它将一群 Docker 主机集 成为单一一个虚拟 Docker 主机。利用一个 Docker 守护进程，通过标准的 Docker API 和任 何完善的通讯工具，Docker Swarm 提供透明地将 Docker 主机扩散到多台主机上的服务。


# 在使用 Docker 技术的产品中如何监控其运行

> 原文：[https://zwmst.com/1131.html](https://zwmst.com/1131.html)

Docker 在产品中提供如 运行统计和 Docker 事件的工具。可以通过这些工具命令获取 Docker 运行状况的统计信息或报告。

Docker stats ： 通过指定的容器 id 获取其运行统计信息，可获得容器对 CPU，内存使用情况 等的统计信息，类似 Linux 系统中的 top 命令。 Docker events ：Docker 事件是一个命令，用于观察显示运行中的 Docker 一系列的行为活 动。

一般的 Docker 事件有：attach（关联），commit（提交），die（僵死），detach（取消 关联），rename（改名），destory（销毁）等。也可使用多个选项对事件记录筛选找到想要 的事件信息。


# 什么是孤儿卷及如何删除它？

> 原文：[https://zwmst.com/1133.html](https://zwmst.com/1133.html)

孤儿卷是未与任何容器关联的卷。在 Docker v1.9 之前的版本中，删除这些孤儿卷存在很大 问题。


# 在 Windows 系统上可以运行原生的 Docker 容器吗？

> 原文：[https://zwmst.com/1135.html](https://zwmst.com/1135.html)

在 ‘Windows Server 2016’ 系统上， 你可以运行 Windows 的原生容器， 微软推出其映像是 ‘Windows Nano Server’ ， 一个轻量级的运行在容器中的 Windows 原生系统。 您可以在其 中布署基于 .NET 的应用。

译注： 结合 Docker 的基本技术原理，参考后面的 问题 26 和 问题 27， 可推测， 微软在系统 内核上开发了对 Docker 的支持， 支持其闭源系统的容器化虚拟技术。但译者认为， Windows 系统本就是闭源紧耦合的系统， 好像你在本机上不装 .NET 组件，各应用能很好运 行似的。何必再弄个容器，浪费资源。这只是译者自己之孔见，想喷就喷！ 另： Windows Server 2016 版本之后的都可支持这种原生 Docker 技术，如 Windows Server 2018 版。


# 在 非 Linux 操作系统平台上如何运行 Docker ?

> 原文：[https://zwmst.com/1137.html](https://zwmst.com/1137.html)

容器化虚拟技术概念可能来源于，在 Linux 内核版本 2.6.24 上加入的对 命名空间（ namespace） 的技术支持特性。 容器化进程加入其进程 ID 到其创建的每个进程上并且对每 个进程中的系统级调用进行访问控制及审查。 其本身是由系统级调用 clone () 克隆出来的进 程， 允许其创建属于自己命名空间的进程实例，而区别于之前的，归属与整个本机系统的进程 实例。

如果上述在 Linux 系统内核上的技术实现成为可能， 那么明显的问题是如何在 非 Linux 系统 上运行容器化的 Docker 。过去， Mac 和 Windows 系统上运行 Docker 容器都使用 Linux 虚拟机（VMs） 技术， Docker 工具箱使用的容器运行在 Virtual Box 虚拟机上。 现在，最新 的情况是， Windows 平台上使用的是 Hyper-V 产品技术，Mac 平台上使用的是 Hypervisor.framework （框架）产品技术。


# 616.Docker概念

> 原文：[https://zwmst.com/4352.html](https://zwmst.com/4352.html)

| Docker 镜像(Images) | Docker 镜像是用于创建 Docker 容器的模板。 |
| --- | --- |
| Docker 容器(Container) | 容器是独立运行的一个或一组应用。 |
| Docker 客户端(Client) | Docker 客户端通过命令行或者其他工具使用 Docker API 与 Docker 的守护进程通信。 |
| Docker 主机(Host) | 一个物理或者虚拟的机器用于执行 Docker 守护进程和容器。 |
| Docker 仓库(Registry) | Docker 仓库用来保存镜像，可以理解为代码控制中的代码仓库。Docker Hub 提供了庞大的镜像集合供使用。 |
| Docker Machine | Docker Machine 是一个简化 Docker 安装的命令行工具，通过一个简单的命令行即可在相应的平台上安装 Docker，比如 VirtualBox、 Digital Ocean、Microsoft Azure。 |

Docker 的出现一定是因为目前的后端在开发和运维阶段确实需要一种虚拟化技术解决开发环境和生产环境环境一致的问题，通过 Docker 我们可以将程序运行的环境也纳入到版本控制中，排除因为环境造成不同运行结果的可能。但是上述需求虽然推动了虚拟化技术的产生，但是如果没有合适的底层技术支撑，那么我们仍然得不到一个完美的产品。本文剩下的内容会介绍几种 Docker 使用的核心技术，如果我们了解它们的使用方法和原理，就能清楚 Docker 的实现原理。Docker 使用客户端-服务器 (C/S) 架构模式，使用远程 API 来管理和创建 Docker 容器。Docker 容器通过Docker 镜像来创建。


# 617.Namespaces

> 原文：[https://zwmst.com/4354.html](https://zwmst.com/4354.html)

命名空间（namespaces）是 Linux 为我们提供的用于分离进程树、网络接口、挂载点以及进程间通信等资源的方法。在日常使用 Linux 或者 macOS 时，我们并没有运行多个完全分离的服务器的需要，但是如果我们在服务器上启动了多个服务，这些服务其实会相互影响的，每一个服务都能看到其他服务的进程，也可以访问宿主机器上的任意文件，这是很多时候我们都不愿意看到的，我们更希望运行在同一台机器上的不同服务能做到完全隔离，就像运行在多台不同的机器上一样。Linux 的命名空间机制提供了以下七种不同的命名空间，包括 CLONE_NEWCGROUP、CLONE_NEWIPC、CLONE_NEWNET、CLONE_NEWNS、CLONE_NEWPID、CLONE_NEWUSER 和 CLONE_NEWUTS，通过这七个选项我们能在创建新的进程时设置新进程应该在哪些资源上与宿主机器进行隔离。


# 618.进程(CLONE_NEWPID 实现的进程隔离)

> 原文：[https://zwmst.com/4356.html](https://zwmst.com/4356.html)

docker 创建新进程时传入 CLONE_NEWPID 实现的进程隔离，也就是使用 Linux 的命名空间实现进程的隔离，Docker 容器内部的任意进程都对宿主机器的进程一无所知。当我们每次运行docker run 或者 docker start 时，都会在创建一个用于设置进程间隔离的 Spec，同时会设置进程相关的命名空间，还会设置与用户、网络、IPC 以及 UTS 相关的命名空间，所有命名空间相关的设置 Spec 最后都会作为 Create 函数的入参在创建新的容器时进行设置。


# 619.Libnetwork 与网络隔离

> 原文：[https://zwmst.com/4358.html](https://zwmst.com/4358.html)

如果 Docker 的容器通过 Linux 的命名空间完成了与宿主机进程的网络隔离，但是却有没有办法通过宿主机的网络与整个互联网相连，就会产生很多限制，所以 Docker 虽然可以通过命名空间创建一个隔离的网络环境，但是 Docker 中的服务仍然需要与外界相连才能发挥作用。

Docker 整个网络部分的功能都是通过 Docker 拆分出来的 libnetwork 实现的，它提供了一个连接不同容器的实现，同时也能够为应用给出一个能够提供一致的编程接口和网络层抽象的容器网络模型。

libnetwork 中最重要的概念，容器网络模型由以下的几个主要组件组成，分别是 Sandbox、Endpoint 和 Network。在容器网络模型中，每一个容器内部都包含一个 Sandbox，其中存储着当前容器的网络栈配置，包括容器的接口、路由表和 DNS 设置，Linux 使用网络命名空间实现这个Sandbox，每一个 Sandbox 中都可能会有一个或多个 Endpoint，在 Linux 上就是一个虚拟的网卡veth，Sandbox 通过 Endpoint 加入到对应的网络中，这里的网络可能就是我们在上面提到的 Linux 网桥或者 VLAN。

每一个使用 docker run 启动的容器其实都具有单独的网络命名空间，Docker 为我们提供了四种不同的网络模式，Host、Container、None 和 Bridge 模式。

在这一部分，我们将介绍 Docker 默认的网络设置模式：网桥模式。在这种模式下，除了分配隔离的网络命名空间之外，Docker 还会为所有的容器设置 IP 地址。当 Docker 服务器在主机上启动之后会创建新的虚拟网桥 docker0，随后在该主机上启动的全部服务在默认情况下都与该网桥相连。在默认情况下，每一个容器在创建时都会创建一对虚拟网卡，两个虚拟网卡组成了数据的通道，其中一个会放在创建的容器中，会加入到名为 docker0 网桥中。


# 620.资源隔离与 CGroups

> 原文：[https://zwmst.com/4360.html](https://zwmst.com/4360.html)

Control Groups（简称 CGroups）能够隔离宿主机器上的物理资源，例如 CPU、内存、磁盘 I/O 和网络带宽。每一个 CGroup 都是一组被相同的标准和参数限制的进程，不同的 CGroup 之间是有层级关系的，也就是说它们之间可以从父类继承一些用于限制资源使用的标准和参数。


# 621.镜像与 UnionFS

> 原文：[https://zwmst.com/4362.html](https://zwmst.com/4362.html)

Linux 的命名空间和控制组分别解决了不同资源隔离的问题，前者解决了进程、网络以及文件系统的隔离，后者实现了 CPU、内存等资源的隔离，但是在 Docker 中还有另一个非常重要的问题需要解决 – 也就是镜像。

Docker 镜像其实本质就是一个压缩包，我们可以使用命令将一个 Docker 镜像中的文件导出，你可以看到这个镜像中的目录结构与 Linux 操作系统的根目录中的内容并没有太多的区别，可以说Docker 镜像就是一个文件。


# 622.存储驱动

> 原文：[https://zwmst.com/4364.html](https://zwmst.com/4364.html)

Docker 使用了一系列不同的存储驱动管理镜像内的文件系统并运行容器，这些存储驱动与Docker 卷（volume）有些不同，存储引擎管理着能够在多个容器之间共享的存储。

当镜像被 docker run 命令创建时就会在镜像的最上层添加一个可写的层，也就是容器层，所有对于运行时容器的修改其实都是对这个容器读写层的修改。


# 926.Dubbo 集群的负载均衡有哪些策略

> 原文：[https://zwmst.com/5125.html](https://zwmst.com/5125.html)

Dubbo 提供了常见的集群策略实现，并预扩展点予以自行实现。

1.  Random LoadBalance: 随机选取提供者策略，有利于动态调整提供者权重。截面碰撞率高，调用次数越多，分布越均匀；
2.  RoundRobin LoadBalance: 轮循选取提供者策略，平均分布，但是存在请求累积的问题；
3.  LeastActive LoadBalance: 最少活跃调用策略，解决慢提供者接收更少的请求；
4.  ConstantHash LoadBalance: 一致性 Hash 策略，使相同参数请求总是发到同一提供者，一台机器宕机，可以基于虚拟节点，分摊至其他提供者，避免引起提供者的剧烈变动；
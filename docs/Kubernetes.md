<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是Kubernetes？

> 原文：[https://zwmst.com/1241.html](https://zwmst.com/1241.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:51:08+08:00"> 2021-08-15 </time> ](https://zwmst.com/1241.html)  Kubernetes是一个开源容器管理工具，负责容器部署，容器扩缩容以及负载平衡。作为 Google的创意之作，它提供了出色的社区，并与所有云提供商合作。因此，我们可以说 Kubernetes不是一个容器化平台，而是一个多容器管理解决方案。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Kubernetes与Docker有什么关系？

> 原文：[https://zwmst.com/1243.html](https://zwmst.com/1243.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:51:33+08:00"> 2021-08-15 </time> ](https://zwmst.com/1243.html)  众所周知，Docker提供容器的生命周期管理，Docker镜像构建运行时容器。但是，由于这些 单独的容器必须通信，因此使用Kubernetes。因此，我们说Docker构建容器，这些容器通过 Kubernetes相互通信。因此，可以使用Kubernetes手动关联和编排在多个主机上运行的容器。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是Container Orchestration？

> 原文：[https://zwmst.com/1245.html](https://zwmst.com/1245.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:51:45+08:00"> 2021-08-15 </time> ](https://zwmst.com/1245.html)  考虑一个应用程序有5-6个微服务的场景。现在，这些微服务被放在单独的容器中，但如果没 有容器编排就无法进行通信。因此，由于编排意味着所有乐器在音乐中和谐共处，所以类似的 容器编排意味着各个容器中的所有服务协同工作以满足单个服务器的需求。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Kubernetes如何简化容器化部署？

> 原文：[https://zwmst.com/1247.html](https://zwmst.com/1247.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:51:58+08:00"> 2021-08-15 </time> ](https://zwmst.com/1247.html)  由于典型应用程序将具有跨多个主机运行的容器集群，因此所有这些容器都需要相互通信。因 此，要做到这一点，你需要一些能够负载平衡，扩展和监控容器的东西。由于Kubernetes与 云无关并且可以在任何公共/私有提供商上运行，因此必须是您简化容器化部署的选择。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是Google容器引擎？

> 原文：[https://zwmst.com/1249.html](https://zwmst.com/1249.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:52:09+08:00"> 2021-08-15 </time> ](https://zwmst.com/1249.html)  Google Container Engine（GKE）是Docker容器和集群的开源管理平台。这个基于 Kubernetes的引擎仅支持在Google的公共云服务中运行的群集。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是Heapster？

> 原文：[https://zwmst.com/1251.html](https://zwmst.com/1251.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:52:21+08:00"> 2021-08-15 </time> ](https://zwmst.com/1251.html)  Heapster是由每个节点上运行的Kubelet提供的集群范围的数据聚合器。此容器管理工具在 Kubernetes集群上本机支持，并作为pod运行，就像集群中的任何其他pod一样。因此，它基 本上发现集群中的所有节点，并通过机上Kubernetes代理查询集群中Kubernetes节点的使用 信息。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是Minikube？

> 原文：[https://zwmst.com/1253.html](https://zwmst.com/1253.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:52:31+08:00"> 2021-08-15 </time> ](https://zwmst.com/1253.html)  Minikube是一种工具，可以在本地轻松运行Kubernetes。这将在虚拟机中运行单节点 Kubernetes群集。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是Kubectl？

> 原文：[https://zwmst.com/1257.html](https://zwmst.com/1257.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:52:49+08:00"> 2021-08-15 </time> ](https://zwmst.com/1257.html)  Kubectl是一个平台，您可以使用该平台将命令传递给集群。因此，它基本上为CLI提供了针对 Kubernetes集群运行命令的方法，以及创建和管理Kubernetes组件的各种方法。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是Kubelet？

> 原文：[https://zwmst.com/1260.html](https://zwmst.com/1260.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:54:01+08:00"> 2021-08-15 </time> ](https://zwmst.com/1260.html)  这是一个代理服务，它在每个节点上运行，并使从服务器与主服务器通信。因此，Kubelet处 理PodSpec中提供给它的容器的描述，并确保PodSpec中描述的容器运行正常。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Kubernetes Architecture的不同组件有哪些？

> 原文：[https://zwmst.com/1262.html](https://zwmst.com/1262.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:54:12+08:00"> 2021-08-15 </time> ](https://zwmst.com/1262.html)  Kubernetes Architecture主要有两个组件 – 主节点和工作节点。如下图所示，master和 worker节点中包含许多内置组件。主节点具有kube-controller-manager，kubeapiserver，kube-scheduler等。而工作节点具有在每个节点上运行的kubelet和kubeproxy。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 你对Kube-proxy有什么了解？

> 原文：[https://zwmst.com/1264.html](https://zwmst.com/1264.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:54:24+08:00"> 2021-08-15 </time> ](https://zwmst.com/1264.html)  Kube-proxy可以在每个节点上运行，并且可以跨后端网络服务进行简单的TCP / UDP数据包 转发。基本上，它是一个网络代理，它反映了每个节点上Kubernetes API中配置的服务。因 此，Docker可链接的兼容环境变量提供由代理打开的群集IP和端口。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 您能否介绍一下Kubernetes中主节点的工作情况？

> 原文：[https://zwmst.com/1266.html](https://zwmst.com/1266.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:54:33+08:00"> 2021-08-15 </time> ](https://zwmst.com/1266.html)  Kubernetes master控制容器存在的节点和节点内部。现在，这些单独的容器包含在容器内部 和每个容器内部，您可以根据配置和要求拥有不同数量的容器。因此，如果必须部署pod，则 可以使用用户界面或命令行界面部署它们。然后，在节点上调度这些pod，并根据资源需求， 将pod分配给这些节点。kube-apiserver确保在Kubernetes节点和主组件之间建立通信。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# kube-apiserver和kube-scheduler的作用是什么？

> 原文：[https://zwmst.com/1268.html](https://zwmst.com/1268.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:54:48+08:00"> 2021-08-15 </time> ](https://zwmst.com/1268.html)  kube -apiserver遵循横向扩展架构，是主节点控制面板的前端。这将公开Kubernetes主节点 组件的所有API，并负责在Kubernetes节点和Kubernetes主组件之间建立通信。

kube-scheduler负责工作节点上工作负载的分配和管理。因此，它根据资源需求选择最合适 的节点来运行未调度的pod，并跟踪资源利用率。它确保不在已满的节点上调度工作负载。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 你能简要介绍一下Kubernetes控制管理器吗？

> 原文：[https://zwmst.com/1270.html](https://zwmst.com/1270.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:54:58+08:00"> 2021-08-15 </time> ](https://zwmst.com/1270.html)  多个控制器进程在主节点上运行，但是一起编译为单个进程运行，即Kubernetes控制器管理 器。因此，Controller Manager是一个嵌入控制器并执行命名空间创建和垃圾收集的守护程 序。它拥有责任并与API服务器通信以管理端点。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是etcd？

> 原文：[https://zwmst.com/1272.html](https://zwmst.com/1272.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:55:10+08:00"> 2021-08-15 </time> ](https://zwmst.com/1272.html)  etcd是用Go编程语言编写的，是一个分布式键值存储，用于协调分布式工作。因此，Etcd存 储Kubernetes集群的配置数据，表示在任何给定时间点的集群状态。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 你对Kubernetes的负载均衡器有什么了解？

> 原文：[https://zwmst.com/1274.html](https://zwmst.com/1274.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:55:21+08:00"> 2021-08-15 </time> ](https://zwmst.com/1274.html)  负载均衡器是暴露服务的最常见和标准方式之一。根据工作环境使用两种类型的负载均衡器， 即内部负载均衡器或外部负载均衡器。内部负载均衡器自动平衡负载并使用所需配置分配容 器，而外部负载均衡器将流量从外部负载引导至后端容器。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是Ingress网络，它是如何工作的？

> 原文：[https://zwmst.com/1276.html](https://zwmst.com/1276.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:55:31+08:00"> 2021-08-15 </time> ](https://zwmst.com/1276.html)  Ingress网络是一组规则，充当Kubernetes集群的入口点。这允许入站连接，可以将其配置为 通过可访问的URL，负载平衡流量或通过提供基于名称的虚拟主机从外部提供服务。因此， Ingress是一个API对象，通常通过HTTP管理集群中服务的外部访问，是暴露服务的最有效方 式。

现在，让我以一个例子向您解释Ingress网络的工作。

有2个节点具有带有Linux桥接器的pod和根网络命名空间。除此之外，还有一个名为 flannel0（网络插件）的新虚拟以太网设备被添加到根网络中。

现在，假设我们希望数据包从pod1流向pod 4。

因此，数据包将pod1的网络保留在eth0，并进入veth0的根网络。 然后它被传递给cbr0，这使得ARP请求找到目的地，并且发现该节点上没有人具有目的地IP地址。

因此，桥接器将数据包发送到flannel0，因为节点的路由表配置了flannel0。 现在，flannel守护程序与Kubernetes的API服务器通信，以了解所有pod IP及其各自的节 点，以创建pods IP到节点IP的映射。

网络插件将此数据包封装在UDP数据包中，其中额外的标头将源和目标IP更改为各自的节点， 并通过eth0发送此数据包。

现在，由于路由表已经知道如何在节点之间路由流量，因此它将数据包发送到目标节点2。 数据包到达node2的eth0并返回到flannel0以解封装并在根网络命名空间中将其发回。 同样，数据包被转发到Linux网桥以发出ARP请求以找出属于veth1的IP。 数据包最终穿过根网络并到达目标Pod4。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 您对云控制器管理器有何了解？

> 原文：[https://zwmst.com/1278.html](https://zwmst.com/1278.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:55:43+08:00"> 2021-08-15 </time> ](https://zwmst.com/1278.html)  Cloud Controller Manager负责持久存储，网络路由，从核心Kubernetes特定代码中抽象出 特定于云的代码，以及管理与底层云服务的通信。它可能会分成几个不同的容器，具体取决于 您运行的是哪个云平台，然后它可以使云供应商和Kubernetes代码在没有任何相互依赖的情 况下开发。因此，云供应商开发他们的代码并在运行Kubernetes时与Kubernetes云控制器管理器连接。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是Container资源监控？

> 原文：[https://zwmst.com/1280.html](https://zwmst.com/1280.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:55:55+08:00"> 2021-08-15 </time> ](https://zwmst.com/1280.html)  对于用户而言，了解应用程序的性能和所有不同抽象层的资源利用率非常重要，Kubernetes 通过在容器，pod，服务和整个集群等不同级别创建抽象来考虑集群的管理。现在，可以监视 每个级别，这只是容器资源监视。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Replica Set 和 Replication Controller之间有什么区别？

> 原文：[https://zwmst.com/1282.html](https://zwmst.com/1282.html)

   [ *Kubernetes* ](https://zwmst.com/kubernetes)*[ <time datetime="2021-08-15T10:56:05+08:00"> 2021-08-15 </time> ](https://zwmst.com/1282.html)  Replica Set 和 Replication Controller几乎完全相同。它们都确保在任何给定时间运行指定 数量的pod副本。不同之处在于复制pod使用的选择器。Replica Set使用基于集合的选择器， 而Replication Controller使用基于权限的选择器。

Equity-Based选择器：这种类型的选择器允许按标签键和值进行过滤。因此，在外行术语 中，基于Equity的选择器将仅查找与标签具有完全相同短语的pod。 示例：假设您的标签键表 示app = nginx，那么，使用此选择器，您只能查找标签应用程序等于nginx的那些pod。

Selector-Based选择器：此类型的选择器允许根据一组值过滤键。因此，换句话说，基于 Selector的选择器将查找已在集合中提及其标签的pod。 示例：假设您的标签键在（nginx， NPS，Apache）中显示应用程序。然后，使用此选择器，如果您的应用程序等于任何nginx， NPS或Apache，则选择器将其视为真实结果。*
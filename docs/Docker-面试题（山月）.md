<!--yml
category: Docker
date: 0001-01-01 00:00:00
-->

# Docker 面试题（山月）

# CoW 策略指什么，docker 中有哪些应用

> 原文：[https://q.shanyue.tech/devops/docker/42.html](https://q.shanyue.tech/devops/docker/42.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 42(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/42)

# docker 中如何查看某个容器消耗的内存和 CPU

> 原文：[https://q.shanyue.tech/devops/docker/43.html](https://q.shanyue.tech/devops/docker/43.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 43(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/43)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

```
$ docker stats postgres
CONTAINER ID        NAME                CPU %               MEM USAGE / LIMIT     MEM %               NET I/O             BLOCK I/O           PIDS
adb85849e229        postgres            0.00%               3.328MiB / 1.796GiB   0.18%               0B / 0B             874GB / 2.6GB       7 
```

# docker 中的网络隔离是如何实现的

> 原文：[https://q.shanyue.tech/devops/docker/47.html](https://q.shanyue.tech/devops/docker/47.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 47(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/47)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

参考: https://docs.docker.com/network/iptables/

# docker 中如何为每个容器的 cpu/memory 设限，原理是什么

> 原文：[https://q.shanyue.tech/devops/docker/126.html](https://q.shanyue.tech/devops/docker/126.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 126(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/126)

# 构建镜像时，那几个指令会增加镜像层数

> 原文：[https://q.shanyue.tech/devops/docker/129.html](https://q.shanyue.tech/devops/docker/129.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 129(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/129)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

`RUN`，`ADD`，`COPY`

# docker 如何隔离容器与宿主机的时间

> 原文：[https://q.shanyue.tech/devops/docker/131.html](https://q.shanyue.tech/devops/docker/131.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 131(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/131)

# 在 docker 的容器中，如何访问宿主机的 localhost

> 原文：[https://q.shanyue.tech/devops/docker/132.html](https://q.shanyue.tech/devops/docker/132.html)

更多描述

如在宿主机有一个 `mysql` 数据库，在容器中，如何连接数据库

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 132(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/132)

# 如何在 docker 中运行 docker

> 原文：[https://q.shanyue.tech/devops/docker/133.html](https://q.shanyue.tech/devops/docker/133.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 133(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/133)

# docker-compose 部署 docker 时，如何把宿主机的环境变量注入到容器中

> 原文：[https://q.shanyue.tech/devops/docker/144.html](https://q.shanyue.tech/devops/docker/144.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 144(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/144)
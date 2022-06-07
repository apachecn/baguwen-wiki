<!--yml
category: Jenkins
date: 0001-01-01 00:00:00
-->

# Jenkins 面试题（爪哇程序员）

# 什么是Jenkins？

> 原文：[https://zwmst.com/1219.html](https://zwmst.com/1219.html)

Jenkins是一个用Java编写的开源持续集成工具。它跟踪版本控制系统, 并在发生更改时启动和 监视构建系统。


# Maven, Ant和Jenkins有什么区别？

> 原文：[https://zwmst.com/1221.html](https://zwmst.com/1221.html)

最基本的区别是：

Maven和Ant是Build Technologies, 而Jenkins是持续集成工具。


# 在Jenkins中, 什么是持续集成？

> 原文：[https://zwmst.com/1225.html](https://zwmst.com/1225.html)

在软件开发中, 多个开发人员或团队在同一个Web应用程序的不同部分上工作, 因此你必须通过 集成所有模块来执行集成测试。为了做到这一点, 每天都要对每段代码进行自动化处理, 以便对 所有代码进行测试。此过程称为连续集成。


# Jenkins的优势是什么？

> 原文：[https://zwmst.com/1227.html](https://zwmst.com/1227.html)

Jenkins的优势包括：

*   在开发环境的早期阶段, 错误跟踪很容易。
*   提供大量的插件支持。
*   对代码的迭代改进。
*   构建失败会在集成阶段进行缓存。
*   对于每个代码提交更改, 都会生成一个自动生成报告通知。
*   为了将构建报告的成功或失败通知开发人员, 它与LDAP邮件服务器集成在一起。
*   实现持续集成的敏捷开发和测试驱动的开发。
*   通过简单的步骤, 即可自动完成maven发布项目。


# 可以使用哪些命令手动启动Jenkins？

> 原文：[https://zwmst.com/1229.html](https://zwmst.com/1229.html)

你可以使用以下任何命令来手动启动Jenkins：

*   (Jenkins_url)/ restart：强制重启, 而无需等待构建完成。
*   (Jenkin_url)/ safeRestart：允许所有正在运行的构建完成。


# 如何在Jenkins中创建备份和复制文件？

> 原文：[https://zwmst.com/1231.html](https://zwmst.com/1231.html)

如果要创建Jenkins设置的备份, 只需复制将Jenkins的所有设置, 构建工件和日志保存在其主目 录中的目录。你还可以复制作业目录以克隆或复制作业或重命名目录。


# 如何通过Jenkins克隆Git存储库？

> 原文：[https://zwmst.com/1233.html](https://zwmst.com/1233.html)

如果要通过Jenkins克隆Git存储库, 则必须输入Jenkins系统的电子邮件和用户名。切换到作业 目录并为此执行” git config”命令。


# 什么是jenkinsfile?为什么使用jenkinsfile

> 原文：[https://zwmst.com/1235.html](https://zwmst.com/1235.html)

Jenkinsfile是一个文本文件，其中包含Jenkins Pipeline的定义，并已签入源代码管理 虽然用于定义管道的脚本语法和jenkinsfile类似，但通常认为在项目中定义管道Jenkinsfile并 检查源代码管理是最佳实践

为所有分支和请求自动创建一个管道构建过程

管道上的代码审查/迭代

审核追踪管道


# 什么是Blue Ocean

> 原文：[https://zwmst.com/1238.html](https://zwmst.com/1238.html)

Blue Ocean是pipeline的可视化UI。同时他兼容经典的自由模式的job。Jenkins Pipeline从 头开始设计，但仍与自由式作业兼容，Blue Ocean减少了经典模式下的混乱并为团队中的每个 成员增加了清晰度。Blue Ocean的主要特点包括：

连续交付（CD）管道的复杂可视化，可以让您快速直观地理解管道状态。 管道编辑器 – 通过引导用户通过直观和可视化的过程来创建管道，从而使管道的创建变得平易近人。

个性化以适应团队中每个成员的基于角色的需求。

在需要干预和/或出现问题时确定精确度。Blue Ocean显示的标注了关键步骤，促进异常处理和提高生产力。
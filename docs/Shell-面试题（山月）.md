<!--yml
category: 工具
date: 0001-01-01 00:00:00
-->

# Shell 面试题（山月）

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


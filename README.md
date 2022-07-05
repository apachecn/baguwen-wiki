# ApacheCN 八股文知识库

> 协议：[CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/)
> 
> 收割 SB 的人会被 SB 们封神，试图唤醒 SB 的人是 SB 眼中的 SB。——SB 第三定律

* [在线阅读](https://bgww.apachecn.org)
* [在线阅读（Gitee）](https://apachecn.gitee.io/doc-template/)
* [ApacheCN 学习资源](http://docs.apachecn.org/)
* [ApacheCN 翻译校对兼职群 713436582](https://jq.qq.com/?_wv=1027&k=VSNtgpjb)

## 贡献指南

请通过 ISSUE 提交想要收录的文章，负责人看到后就会处理。

## 写在前面

IT八股文是中国特色的东西之一，不用怀疑，北美、欧洲和土澳还是东南亚，没有任何一家公司面试考这个东西。它们习惯于考察系统架构设计，似乎更关心更大的架构而不是细节。也就是一个组件怎么在项目中使用，而不是它是怎么做出来的。

如果你跟我一样很幸运，没怎么背八股文就进入了IT行业，你会发现这些东西对编程，哦不，对于日常工作根本没啥卵用。很简单，如果你知道了 HTTP2 支持长连接，你会把许多数据塞进一个请求里面给前端吗？如果你又发现了当前使用的 HTTP 库不支持长连接（大多数库都是这样，标准和实现不完全统一），你会写个连接池来复用它吗？很遗憾，你还是跟大多数人一样，该怎么发请求就怎么发，因为这个对于整个项目毫无影响。

我之前对于八股文一向是逃避。现在我反思了自己的错误，有了新的认识。如果你不喜欢一个东西，最好的方式不是逃避，而是扛旗反旗，KILL THE GAME！虽然八股文对编程没啥卵用，不过另一方面，背八股文也不需要懂编程，这个就是问题的突破口。

敏捷宣言提倡了代码优先于文档。同样，放在面试中，就是算法题优先于八股文。因为，员工入职之后总是要写代码的，只会背八股文创造不了产出。那么，我们就可以把东西都放到台面上来，把八股文总结得足够详细，忽悠转行的人，培训班的人都来背八股文。等到我们培养了一大堆只会背八股文而不会干实事的人，公司必然会调整面试策略向算法题倾斜。

这算是劳方和资方得博弈，我相信一个两个人做不到，但我们作为 Github 百强社区，一定可以做到。KILL THE GAME！

## 联系方式

### 负责人

* [飞龙](https://github.com/wizardforcel): 562826179

### 其他

*   在我们的 [apachecn/baguwen-wiki](https://github.com/apachecn/baguwen-wiki) github 上提 issue.
*   发邮件到 Email: `apachecn@163.com`.
*   在我们的 [组织学习交流群](https://www.apachecn.org/#/docs/join) 中联系群主/管理员即可.

## 下载

### Docker

```
docker pull apachecn0/baguwen-wiki
docker run -tid -p <port>:80 apachecn0/baguwen-wiki
# 访问 http://localhost:{port} 查看文档
```

### PYPI

```
pip install baguwen-wiki
baguwen-wiki <port>
# 访问 http://localhost:{port} 查看文档
```

### NPM

```
npm install -g baguwen-wiki
baguwen-wiki <port>
# 访问 http://localhost:{port} 查看文档
```

## 赞助我们

![](http://data.apachecn.org/img/about/donate.jpg)

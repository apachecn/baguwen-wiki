<!--yml
category: 数据库
date: 0001-01-01 00:00:00
-->

# GraphQL 面试题（山月）

# graphql 的引进有什么风险，以及性能问题

> 原文：[https://q.shanyue.tech/server/graphql/53.html](https://q.shanyue.tech/server/graphql/53.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 53(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/53)

# 当编辑 graphql 的 query 时，如何在编辑器中自动补全

> 原文：[https://q.shanyue.tech/server/graphql/188.html](https://q.shanyue.tech/server/graphql/188.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 188(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/188)

# apollo-client 与 react-apollo 在前端应用中扮演什么角色

> 原文：[https://q.shanyue.tech/server/graphql/423.html](https://q.shanyue.tech/server/graphql/423.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 423(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/423)

# 如何给 graphql 设计合理的 Rate Limit

> 原文：[https://q.shanyue.tech/server/graphql/439.html](https://q.shanyue.tech/server/graphql/439.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 439(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/439)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

对于 Rest API 而言可根据特定的 API 来进行*限流(Rate Limit)*设计

然而，GraphQL 只有一个 API，无法根据此来限流，一般情况下根据 `Field` 来进行限流，为了更好地设计及声明限流条件，可自定义 `Directive`，如下所示

```
type Query {
  todos: [Todo!]! @rateLimit(window: "1s", max: 100)
} 
```

可参考以下两个 npm package

*   [graphql-rate-limit(opens new window)](https://github.com/teamplanes/graphql-rate-limit)
*   [graphql-rate-limit-directive(opens new window)](https://github.com/ravangen/graphql-rate-limit)
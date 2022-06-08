<!--yml
category: 前端
date: 0001-01-01 00:00:00
-->

# TypeScript 面试题（山月）

# 在 Typescript 中如何实现类型标记 Pick 与 Omit

> 原文：[https://q.shanyue.tech/fe/ts/695.html](https://q.shanyue.tech/fe/ts/695.html)

更多描述

有以下测试用例

```
interface User {
  id: number;
  age: number;
  name: string;
}

// 相当于: type PickUser = { age: number; name: string; }
type OmitUser = Omit<User, "id">;

// 相当于: type PickUser = { id: number; age: number; }
type PickUser = Pick<User, "id" | "age">; 
```

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 695(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/695)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

```
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};

type Exclude<T, U> = T extends U ? never : T;

type Omit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>; 
```

```
interface User {
  id: number;
  age: number;
  name: string;
}

// 相当于: type PickUser = { age: number; name: string; }
type OmitUser = Omit<User, "id">;

// 相当于: type PickUser = { id: number; age: number; }
type PickUser = Pick<User, "id" | "age">; 
```

Author

回答者: [Asarua(opens new window)](https://github.com/Asarua)

```
type MyPick<O extends object, K extends keyof O> = {
  [P in K]: O[P];
};

type MyOmit<O extends object, K extends keyof O> = MyPick<
  O,
  Exclude<keyof O, K>
>;

type MyOmit2<O extends object, K extends keyof O> = {
  [P in Exclude<keyof O, K>]: O[P];
}; 
```

# 什么是协变与逆变

> 原文：[https://q.shanyue.tech/fe/ts/713.html](https://q.shanyue.tech/fe/ts/713.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 713(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/713)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

> 协变与逆变(Covariance and contravariance )是在计算机科学中，描述具有父/子型别关系的多个型别通过型别构造器、构造出的多个复杂型别之间是否有父/子型别关系的用语。

Author

回答者: [Carrie999(opens new window)](https://github.com/Carrie999)

https://github.com/sl1673495/blogs/issues/54

Author

回答者: [Carrie999(opens new window)](https://github.com/Carrie999)

https://www.zhihu.com/question/38861374

# 在 ts 中如何实现 Partial

> 原文：[https://q.shanyue.tech/fe/ts/714.html](https://q.shanyue.tech/fe/ts/714.html)

更多描述

实现 `Partial`，使得 Object 所有的属性变为可选属性。

> PS: `Partial` 已经在 TS 中原生实现，见文档: [https://www.typescriptlang.org/docs/handbook/utility-types.html#partialtype(opens new window)](https://www.typescriptlang.org/docs/handbook/utility-types.html#partialtype)

```
type User = {
  id: number;
  age: number;
  name: string;
};

// Output:
// type PartialUser = {
//   id?: number | undefined;
//   age?: number | undefined;
//   name?: string | undefined;
// }
type PartialUser = Partial<User>; 
```

以下是使用案例

```
interface Todo {
  title: string;
  description: string;
}

function updateTodo(todo: Todo, fieldsToUpdate: Partial<Todo>) {
  return { ...todo, ...fieldsToUpdate };
}

const todo1 = {
  title: "organize desk",
  description: "clear clutter",
};

const todo2 = updateTodo(todo1, {
  description: "throw out trash",
}); 
```

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 714(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/714)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

```
type Partial<T> = {
  [P in keyof T]?: T[P];
}; 
```

# 在 ts 中什么是 infer，并实现 Parameters 与 ReturnType

> 原文：[https://q.shanyue.tech/fe/ts/715.html](https://q.shanyue.tech/fe/ts/715.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 715(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/715)

Author

回答者: [heretic-G(opens new window)](https://github.com/heretic-G)

```
type Parameters<T extends (...args: any[]) => unknown> = T extends (
  ...args: infer R
) => unknown
  ? R
  : never; 
```

Author

回答者: [zhimazz(opens new window)](https://github.com/zhimazz)

Parameters 是啥

Author

回答者: [Asarua(opens new window)](https://github.com/Asarua)

> Parameters 是啥

取得某个函数的参数类型的高级类型

Author

回答者: [iceycc(opens new window)](https://github.com/iceycc)

Parameters <t>的作用是用于获得函数的参数类型组成的元组类型。</t>

```
type Parameters<T extends (...args: any) => any> = T extends (
  ...args: infer P
) => any
  ? P
  : never; 
```

```
type A = Parameters<() => void>; // []
type B = Parameters<typeof Array.isArray>; // [any]
type C = Parameters<typeof parseInt>; // [string, (number | undefined)?]
type D = Parameters<typeof Math.max>; // number[] 
```

# typescript 中 interface 与 type 有何区别

> 原文：[https://q.shanyue.tech/fe/ts/730.html](https://q.shanyue.tech/fe/ts/730.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 730(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/730)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

https://stackoverflow.com/questions/37233735/interfaces-vs-types-in-typescript

Author

回答者: [illumi520(opens new window)](https://github.com/illumi520)

interface 是接口，type 是类型，本身就是两个概念。只是碰巧表现上比较相似。 希望定义一个变量类型，就用 type，如果希望是能够继承并约束的，就用 interface。 如果你不知道该用哪个，说明你只是想定义一个类型而非接口，所以应该用 type。

# 请简述 typescript 中的 infer

> 原文：[https://q.shanyue.tech/fe/ts/731.html](https://q.shanyue.tech/fe/ts/731.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 731(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/731)

Author

回答者: [okbug(opens new window)](https://github.com/okbug)

和 returnType 有点关联，做返回值推断的
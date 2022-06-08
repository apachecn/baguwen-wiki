<!--yml
category: 前端
date: 0001-01-01 00:00:00
-->

# React 面试题（山月）

# 当新入职一家公司时，如何快速搭建开发环境并让应用跑起来

> 原文：[https://q.shanyue.tech/fe/react/9.html](https://q.shanyue.tech/fe/react/9.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 9(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/9)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

新人入职新上手项目，如何把它跑起来，这是所有人都会碰到的问题：所有人都是从新手开始的。

有可能你会脱口而出：`npm run dev/npm start`，但实际工作中，处处藏坑，往往没这么简单。

1.  查看是否有 `CI/CD`，如果有跟着 `CI/CD` 部署的脚本跑命令
2.  查看是否有 `dockerfile`，如果有跟着 `dockerfile` 跑命令
3.  查看 npm scripts 中是否有 dev/start，尝试 `npm run dev/npm start`
4.  查看是否有文档，如果有跟着文档走。为啥要把文档放到最后一个？原因你懂的

但即便是十分谨慎，也有可能遇到以下几个叫苦不迭、浪费了一下午时间的坑:

1.  前端有可能在**本地环境启动时需要依赖前端构建时所产生的文件**，所以有时需要**先正常部署一遍，再试着按照本地环境启动 (即需要先 `npm run build` 一下，再 `npm run dev/npm start`)**。(比如，一次我们的项目 npm run dev 时需要 webpack DllPlugin 构建后的东西）
2.  别忘了设置环境变量或者配置文件 (.env/consul/k8s-configmap)

因此，设置一个少的 script，可以很好地避免后人踩坑，更重要的是，可以避免后人骂你，

此时可设置 script hooks，如 `prepare`、`postinstall` 自动执行脚本，来完善该项目的基础设施

```
{
  "scripts": {
    "start": "npm run dev",
    "config": "node assets && node config",
    "build": "webpack",
    // 设置一个钩子，在 npm install 后自动执行，此处有可能不是必须的
    "prepare": "npm run build",
    "dev": "webpack-dev-server --inline --progress"
  }
} 
```

## npm run dev 与 npm start 的区别

对于一个**纯生成静态页面打包**的前端项目而言，它们是没有多少区别的：生产环境的部署只依赖于构建生成的资源，更不依赖 npm scripts。可见 [如何部署前端项目(opens new window)](https://shanyue.tech/frontend-engineering/docker.html)。

使用 `create-react-app` 生成的项目，它的 npm script 中只有 `npm start`

```
{
  "start": "react-scripts start",
  "build": "react-scripts build",
  "test": "react-scripts test",
  "eject": "react-scripts eject"
} 
```

使用 `vuepress` 生成的项目，它的 npm script 中只有 `npm run dev`

```
{
  "dev": "vuepress dev",
  "build": "vuepress build"
} 
```

在一个**面向服务端**的项目中，如 `next`、`nuxt` 与 `nest`。dev 与 start 的区别趋于明显，一个为生产环境，一个为开发环境

*   dev: 在开发环境启动项目，一般带有 watch 选项，监听文件变化而重启服务，此时会耗费大量的 CPU 性能，不宜放在生产环境
*   start: 在生产环境启动项目

在 `nest` 项目中进行配置

```
{
  "start": "nest start",
  "dev": "nest start --watch"
} 
```

Author

回答者: [xwxgjs(opens new window)](https://github.com/xwxgjs)

我的意见和楼上相反，应该先大概看一遍文档…… 文档中会描述本地环境的配置方法

```
查看是否有 CI/CD，如果有跟着 CI/CD 部署的脚本跑命令
查看是否有 dockerfile，如果有跟着 dockerfile 跑命令
查看 npm scripts 中是否有 dev/start，尝试 npm run dev/npm start 
```

大部分公司的开发环境都是本地环境，所以什么 CI/CD、Docker 可以先放到一边

npm run dev/npm start 这个是一般的约定，但不是所有的项目都是这样。所以需要先看 package.json 中的 script 来确定

### npm run dev 和 npm start 的区别？

1.  npm start 是 npm run start 的别名，支持 prestart 和 poststart 钩子

Author

回答者: [linlai163(opens new window)](https://github.com/linlai163)

> 我的意见和楼上相反，应该先大概看一遍文档…… 文档中会描述本地环境的配置方法
> 
> ```
> 查看是否有 CI/CD，如果有跟着 CI/CD 部署的脚本跑命令
> 查看是否有 dockerfile，如果有跟着 dockerfile 跑命令
> 查看 npm scripts 中是否有 dev/start，尝试 npm run dev/npm start 
> ```
> 
> 大部分公司的开发环境都是本地环境，所以什么 CI/CD、Docker 可以先放到一边
> 
> npm run dev/npm start 这个是一般的约定，但不是所有的项目都是这样。所以需要先看 package.json 中的 script 来确定
> 
> ### npm run dev 和 npm start 的区别？
> 
> 1.  npm start 是 npm run start 的别名，支持 prestart 和 poststart 钩子

你是真没吃过文档的亏。。。管他什么公司，文档都有坑。

# 了解 React 中的 ErrorBoundary 吗，它有那些使用场景

> 原文：[https://q.shanyue.tech/fe/react/11.html](https://q.shanyue.tech/fe/react/11.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 11(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/11)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

待答

Author

回答者: [hackftz(opens new window)](https://github.com/hackftz)

从其他文章里看到的 避免错误渲染白屏做异常中间处理的嵌套组件 class ErrorBoundary extends Component { static getDerivedStateFromError() { return { hasError: true }; } state = { hasError: false, }; componentDidCatch(error, info) { // reportError(error, info); } render() { const { hasError } = this.state; const { children } = this.props; if (hasError) { return

系统异常，请稍后再试; } return children; } } function render(Component, props) { const rootElement = document.getElementById("root"); ReactDOM.render( <errorboundary><Component {...props} /></errorboundary> , rootElement ); }

作者：蚂蚁保险体验技术 链接：https://juejin.im/post/5de91d0f51882512400acafd 来源：掘金 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

Author

回答者: [BertieGo(opens new window)](https://github.com/BertieGo)

是 react 内的一个钩子，用于在组件内发生了 js 错误时候的错误处理。 使用场景是在发生 js 报错的时候不至于说白屏，可以转去别的页面提示用户这里报了错，转用别的去到去继续操作。

Author

回答者: [baihech(opens new window)](https://github.com/baihech)

这不就是 try catch 么。。。

Author

回答者: [baihech(opens new window)](https://github.com/baihech)

错误不抛出，交给 catch 处理，然鹅并不能预先知道错误类型。。。

Author

回答者: [libin1991(opens new window)](https://github.com/libin1991)

[前端防御性编程(opens new window)](https://juejin.im/post/5de91d0f51882512400acafd#heading-9)

Author

回答者: [into-piece(opens new window)](https://github.com/into-piece)

了解，在推出之前报错会直接白屏，总是需要我们前端进行手动 try catch，react16 新增了两个生命周期 componentdidcatch 和 static getDerivedStateFromError 从框架级别让我们更方便捕捉异常并显示备用 ui。其实就是在整个 workloop 外面包一层 try catch，报错时候遍历父组件找到这两个生命周期并把堆栈信息塞给生命周期进行判断。

Author

回答者: [into-piece(opens new window)](https://github.com/into-piece)

顺带一句 suspense 的原理好像也是这个

# 有没有使用过 react hooks，它带来了那些便利

> 原文：[https://q.shanyue.tech/fe/react/14.html](https://q.shanyue.tech/fe/react/14.html)

更多描述

有没有使用过 react hooks，它有哪些优缺点？

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 14(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/14)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

依我的看法，`React hooks` 主要解决了状态以及副作用难以复用的场景，除此之外，他对我最大的好处就是在 `Console` 中不会看到重重叠叠相同名字的组件了(HOC)。

目前使用感觉最爽的两个 hook，都是关于请求的。一个是 `apollo-client` 的 `useQuery`，一个是 [swr(opens new window)](https://github.com/zeit/swr)。

Author

回答者: [libin1991(opens new window)](https://github.com/libin1991)

1.HOC 嵌套地狱 2.this 3.逻辑复用 3.tree-shaking

Author

回答者: [JeffWong16(opens new window)](https://github.com/JeffWong16)

个人最喜欢的两个点 1， 再也不用操心讨厌的 this 的问题 2，逻辑复用更加方便，代码逻辑更加清晰

Author

回答者: [Muralitob(opens new window)](https://github.com/Muralitob)

不用去写生命周期了

# 如何使用 react hooks 实现一个计数器的组件

> 原文：[https://q.shanyue.tech/fe/react/15.html](https://q.shanyue.tech/fe/react/15.html)

更多描述

如何使用 react hooks 实现最简单一个计数器的组件

为了保证最最简单化，不需要暂停与开始状态

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 15(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/15)

Author

回答者: [Hack-Jay(opens new window)](https://github.com/Hack-Jay)

```
import React, { useState, useEffect } from 'react'
import useCountDown from './useCountDown'

const useCountDown = (num) => {
    const [seconds, setSecond] = useState(num)

    useEffect(() => {
        setTimeout(() => {
            if (seconds > 0) {
                setSecond(c => c - 1);
            }
        }, 1000);
    }, [seconds]);

    return [seconds, setSecond]
}

// use it
const Demo = () => {
    const [seconds, setSecond] = useCountDown(0)
    return (
             <Button
                disable={seconds !== 0}
                onClick={() => setSecond(59)}
            >
                {seconds > 0 ? `${seconds}s后可点击` : '点击开始倒计时'}
            </Button>
        )
} 
```

Author

回答者: [bWhirring(opens new window)](https://github.com/bWhirring)

```
import React, { useEffect, useState } from "react";

function App() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    setInterval(() => {
      setCount((count) => count + 1);
    }, 1000);
  }, []);

  return <h1>{count}</h1>;
} 
```

Author

回答者: [shaul-xu(opens new window)](https://github.com/shaul-xu)

```
import React, { useEffect, useState } from "react";

function App() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    const timer = setInterval(() => {
      setCount((count) => count + 1);
    }, 1000);

    return () => {
      clearInterval(timer);
    };
  }, []);

  return <h1>{count}</h1>;
} 
```

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

代码见 [如何使用 React Hooks 实现计数器组件 - codesandbox(opens new window)](https://codesandbox.io/s/shiyong-react-hooks-ruheshixianyigejishuqi-counter-tc5u1?file=/src/App.js)

可使用 `setTimeout` 与 `setInterval` 实现。

其中，使用 setTimeout 实现时，当页面处于不可见 (`document.hidden = false`) 状态时，将可能会停止计时，建议使用 `setInterval` 实现

```
import { useEffect, useState } from "react";
import "./styles.css";

function CounterWithTimeout() {
  const [count, setCount] = useState(0);
  useEffect(() =>
    setTimeout(() => {
      setCount(count + 1);
    }, 1000)
  );
  return <h1>{count}</h1>;
}

function CounterWithInterval() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    const timer = setInterval(() => {
      setCount((count) => count + 1);
    }, 1000);

    return () => {
      clearInterval(timer);
    };
  }, []);

  return <h1>{count}</h1>;
}

export default function App() {
  return (
    <div>
      <CounterWithTimeout />
      <CounterWithInterval />
    </div>
  );
} 
```

# React 中，cloneElement 与 createElement 各是什么，有什么区别

> 原文：[https://q.shanyue.tech/fe/react/22.html](https://q.shanyue.tech/fe/react/22.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 22(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/22)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

```
React.cloneElement(element, [props], [...children]);

React.createElement(type, [props], [...children]); 
```

直接上 API，很容易得出结论：首参不一样。这也是他们的最大区别：

1.  `cloneElement`，根据 Element 生成新的 Element
2.  `createElement`，根据 Type 生成新的 Element

然而，此时估计还是云里雾里，含糊不清，需要弄清它，首先要明白俩概念

1.  Type
2.  Element

## React.cloneElement 的使用场景

# 使用 react 实现一个通用的 message 组件

> 原文：[https://q.shanyue.tech/fe/react/39.html](https://q.shanyue.tech/fe/react/39.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 39(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/39)

# 如何使用 react hooks 实现 useFetch 请求数据

> 原文：[https://q.shanyue.tech/fe/react/67.html](https://q.shanyue.tech/fe/react/67.html)

更多描述

比如设计成 `useFetch` 这种形式，它的 API 应该如何设计

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 67(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/67)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

可以参考 [How to fetch data with React Hooks?(opens new window)](https://www.robinwieruch.de/react-hooks-fetch-data)

# react 如何使用 render prop component 请求数据

> 原文：[https://q.shanyue.tech/fe/react/68.html](https://q.shanyue.tech/fe/react/68.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 68(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/68)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

参考: [https://www.robinwieruch.de/react-fetching-data#how-to-fetch-data-in-render-props(opens new window)](https://www.robinwieruch.de/react-fetching-data#how-to-fetch-data-in-render-props)

# React Portal 有哪些使用场景

> 原文：[https://q.shanyue.tech/fe/react/69.html](https://q.shanyue.tech/fe/react/69.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 69(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/69)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

> Portals provide a first-class way to render children into a DOM node that exists outside the DOM hierarchy of the parent component.

在以前， `react` 中所有的组件都会位于 `#app` 下，而使用 `Portals` 提供了一种脱离 `#app` 的组件。

因此 `Portals` 适合脱离文档流(out of flow) 的组件，特别是 `position: absolute` 与 `position: fixed` 的组件。比如模态框，通知，警告，goTop 等。

以下是官方一个模态框的示例，可以在以下地址中测试效果 [https://codepen.io/gaearon/pen/jGBWpE?editors=1010(opens new window)](https://codepen.io/gaearon/pen/jGBWpE?editors=1010)

```
<html>
  <body>
    <div id="app"></div>
    <div id="modal"></div>
    <div id="gotop"></div>
    <div id="alert"></div>
  </body>
</html> 
```

```
const modalRoot = document.getElementById("modal");

class Modal extends React.Component {
  constructor(props) {
    super(props);
    this.el = document.createElement("div");
  }

  componentDidMount() {
    modalRoot.appendChild(this.el);
  }

  componentWillUnmount() {
    modalRoot.removeChild(this.el);
  }

  render() {
    return ReactDOM.createPortal(this.props.children, this.el);
  }
} 
```

# 什么是 virtual DOM，它的引入带了什么好处

> 原文：[https://q.shanyue.tech/fe/react/70.html](https://q.shanyue.tech/fe/react/70.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 70(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/70)

Author

回答者: [libin1991(opens new window)](https://github.com/libin1991)

*   虚拟 DOM 最大的优势在于抽象了原本的渲染过程，实现了跨平台的能力，而不仅仅局限于浏览器的 DOM，可以是安卓和 IOS 的原生组件，可以是近期很火热的小程序，也可以是各种 GUI。

*   vdom 把渲染过程抽象化了，从而使得组件的抽象能力也得到提升，并且可以适配 DOM 以外的渲染目标。

*   Virtual DOM 在牺牲(牺牲很关键)部分性能的前提下，增加了可维护性，这也是很多框架的通性。 实现了对 DOM 的集中化操作，在数据改变时先对虚拟 DOM 进行修改，再反映到真实的 DOM 中，用最小的代价来更新 DOM，提高效率(提升效率要想想是跟哪个阶段比提升了效率，别只记住了这一条)。

*   打开了函数式 UI 编程的大门。

*   可以渲染到 DOM 以外的端，使得框架跨平台，比如 ReactNative，React VR 等。

*   可以更好的实现 SSR，同构渲染等。这条其实是跟上面一条差不多的。

*   组件的高度抽象化。

> 虚拟 DOM 的缺点

*   首次渲染大量 DOM 时，由于多了一层虚拟 DOM 的计算，会比 innerHTML 插入慢。
*   虚拟 DOM 需要在内存中的维护一份 DOM 的副本(更上面一条其实也差不多，上面一条是从速度上，这条是空间上)。
*   如果虚拟 DOM 大量更改，这是合适的。但是单一的，频繁的更新的话，虚拟 DOM 将会花费更多的时间处理计算的工作。所以，如果你有一个 DOM 节点相对较少页面，用虚拟 DOM，它实际上有可能会更慢。但对于大多数单页面应用，这应该都会更快。

Author

回答者: [eEmpty(opens new window)](https://github.com/eEmpty)

同意楼上

Author

回答者: [into-piece(opens new window)](https://github.com/into-piece)

react 初次 render 或协调后所生成的一个对象，react16 前是通过组件递归遍历而来，react16 是以 fiber 为节点构建成的单链表结构树，其作为真实 dom 的映射。 优点：大大地提高了开发效率，解放生产力，通过计算这两棵树之间的差别来判断如何有效率的更新。 缺点：初次需要构建遍历深层次的组件树，耗费性能，所以有普遍首屏渲染慢的问题。

# react 与 vue 数组中 key 的作用是什么

> 原文：[https://q.shanyue.tech/fe/react/72.html](https://q.shanyue.tech/fe/react/72.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 72(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/72)

Author

回答者: [su-imagine(opens new window)](https://github.com/su-imagine)

diff 算法需要比对虚拟 dom 的修改，然后异步的渲染到页面中，当出现大量相同的标签时，vnode 会首先判断 key 和标签名是否一致，如果一致再去判断子节点一致，使用 key 可以帮助 diff 算法提升判断的速度，在页面重新渲染时更快消耗更少

# react 中 ref 是干什么用的，有哪些使用场景

> 原文：[https://q.shanyue.tech/fe/react/93.html](https://q.shanyue.tech/fe/react/93.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 93(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/93)

Author

回答者: [senbochen(opens new window)](https://github.com/senbochen)

**取得深层次的 dom 的结构。进行操作；我用过的主要是对表格滚动条的操作**

Author

回答者: [libin1991(opens new window)](https://github.com/libin1991)

操作原生 JS 的桥梁

# 如何使用 react/vue 实现一个 message API

> 原文：[https://q.shanyue.tech/fe/react/101.html](https://q.shanyue.tech/fe/react/101.html)

更多描述

可以实现如下 API

`message.info()` `message.success()`

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 101(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/101)

Author

回答者: [allan-hx(opens new window)](https://github.com/allan-hx)

```
import React from 'react';
import ReactDOM from 'react-dom';
// info组件
import Info from 'info';
// success组件
import Success from 'success';

function createMessage(message, Com) {

  let el = document.createElement('div');

  document.body.appendChild(el);

  const component = React.createElement(Com, {
    message
  });

  ReactDOM.render(component, el);
}

const message = {
  info(message) {
    return createMessage(message, Info);
  },
  success(message) {
    return createMessage(message, Success);
  },
};

export default message; 
```

主要实现思路就是创建一个 div 到 body 下，然后利用 ReactDOM.render 将组件渲染到这个容器下，这只是一个简单的实现，没实现关闭和多次调用

Author

回答者: [wizzeng(opens new window)](https://github.com/wizzeng)

Vue 实现也是差不多，可以先写好一个 render 函数，作用是把某一 HTML 片段挂载到 #root 下 / 从 #root 删除该片段。然后写一个 Vue 插件，就是一个暴露了包含 install 方法的模块，install 方法中将 设置 Vue.prototype.$message = message 对象。最后使用 Vue.use 全局注册这个插件即可。

Author

回答者: [guanwanxiao(opens new window)](https://github.com/guanwanxiao)

```
// alert.js
import Alert from './alert.vue'
import Vue from 'vue'
// 创建构造器
const InstanceAlert = Vue.extend(Alert)

export default class Message {
  deaultOptions = {
    el: document.createElement('div')
    propsData: {
      title: '标题'
    }
  }
  instance = {}
  constructor (options) {
    options = Object.assign({},options,this.deaultOptions)
    this.instance = new InstanceAlert(options)
  }
  show() {
    document.body.appendChild(this.instance.$el)

  }
  hide() {
    document.body.removeChild(this.instance.$el)
  }
} 
```

```
// alert.vue
<template>
  <div id="alert-mount">
    这里是{{ title }}
  </div>
</template>

<script>
  export default {
    props:{
      title:{
        type:String,
        default:""
      }
    }
  }
</script> 
```

Author

回答者: [Drowned-fish(opens new window)](https://github.com/Drowned-fish)

用 createPortal 会好点，符合 createPortal 的使用场景并且如果 message 复杂点 createElement 就用不了

# react hooks 中如何模拟 componentDidMount

> 原文：[https://q.shanyue.tech/fe/react/143.html](https://q.shanyue.tech/fe/react/143.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 143(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/143)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

在 `useEffect`，把第二个参数即依赖的状态，设置为 `[]`

```
useEffect(callback, []); 
```

# 如果使用 SSR，可以在 created/componentWillMount 中访问 localStorage 吗

> 原文：[https://q.shanyue.tech/fe/react/147.html](https://q.shanyue.tech/fe/react/147.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 147(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/147)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

不可以，created/componentWillMount 时，还未挂载，代码仍然在服务器中执行，此时没有浏览器环境，因此此时访问 localStorage 将会报错

Author

回答者: [thunderqin(opens new window)](https://github.com/thunderqin)

我试了 可以啊 这是时候只是找不到实体 DOM 但是具备 js 的执行环境了

# react hooks 如何替代或部分替代 redux 功能

> 原文：[https://q.shanyue.tech/fe/react/152.html](https://q.shanyue.tech/fe/react/152.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 152(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/152)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

我们把全局 store 分为两块

1.  从服务器端来，如各种 `model`，此时可以使用 `swr` 直接替代。或者封装一个 `useModel`，如 `useUser`，`usePermission`
2.  客户端全局 store，此时可以使用 `useReducer` 和 `useContext` 来替代

Author

回答者: [into-piece(opens new window)](https://github.com/into-piece)

useReducer+useContext

# 如何实现一个 react hook，你有没有自己写过一个

> 原文：[https://q.shanyue.tech/fe/react/153.html](https://q.shanyue.tech/fe/react/153.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 153(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/153)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

可以参考官方文档 [https://reactjs.org/docs/hooks-custom.html(opens new window)](https://reactjs.org/docs/hooks-custom.html)

自定义一个 `hook` 仅仅是一个以 `use` 打头，组合 `useState` 和 `useEffect` 或者其它 `hooks` 的一个普通函数

Author

回答者: [into-piece(opens new window)](https://github.com/into-piece)

各种优秀实现=》https://github.com/streamich/react-use

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

> 各种优秀实现=》https://github.com/streamich/react-use

这个厉害！

# 在 react/vue 中数组是否可以以在数组中的次序为 key

> 原文：[https://q.shanyue.tech/fe/react/155.html](https://q.shanyue.tech/fe/react/155.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 155(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/155)

Author

回答者: [into-piece(opens new window)](https://github.com/into-piece)

不可，key 应为唯一标示，在数组变更时插入或删除后，index 无法确保始终指向对应的序列

# React 中 fiber 是用来做什么的

> 原文：[https://q.shanyue.tech/fe/react/165.html](https://q.shanyue.tech/fe/react/165.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 165(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/165)

Author

回答者: [yuzeyang97(opens new window)](https://github.com/yuzeyang97)

因为 JavaScript 单线程的特点，每个同步任务不能耗时太长，不然就会让程序不会对其他输入作出相应，React 的更新过程就是犯了这个禁忌，而 React Fiber 就是要改变现状。 而可以通过分片来破解 JavaScript 中同步操作时间过长的问题。

把一个耗时长的任务分成很多小片，每一个小片的运行时间很短，虽然总时间依然很长，但是在每个小片执行完之后，都给其他任务一个执行的机会，这样唯一的线程就不会被独占，其他任务依然有运行的机会。

React Fiber 把更新过程碎片化，每执行完一段更新过程，就把控制权交还给 React 负责任务协调的模块，看看有没有其他紧急任务要做，如果没有就继续去更新，如果有紧急任务，那就去做紧急任务。

维护每一个分片的数据结构，就是 Fiber。

Author

回答者: [Feahter(opens new window)](https://github.com/Feahter)

React Fiber 是对核心算法的一次重新实现 Fiber reconciler 从 v16.x 开始底层使用 Fiber reconciler 替换 stack reconciler. 已知： stack reconciler 处理大状态时由于计算和组件树遍历的消耗容易出现渲染线程挂起，进而页面掉帧。（根本原因是渲染/更新过程一旦开始无法中断，持续占用主线程，主线程忙于执行 JS）

求： 建立一种能解决主线程占用问题，且具有长远意义的机制 解： 把渲染/更新过程拆分为小块任务，通过合理的调度机制来控制时间（更细粒度、更强的控制力）

子问题： 1.拆什么？什么不能拆？ 把渲染/更新过程分为 2 个阶段（diff + patch）： diff~~render/reconciliation (对比 prevInstance 和 nextInstance 的状态，找出差异及其对应的 DOM change。) patch~~commit (把本次更新中的所有 DOM change 应用到 DOM 树，是一连串的 DOM 操作。) render/reconciliation 阶段的工作（diff）可以拆分，commit 阶段的工作（patch）不可拆分.

2.怎么拆？ Fiber 的拆分单位是 fiber（fiber tree 上的一个节点），实际上就是按虚拟 DOM 节点拆，因为 fiber tree 是根据 vDOM tree 构造出来的，树结构一模一样，只是节点携带的信息有差异。

3.如何调度任务？ 分 2 部分： ￼ 工作循环 ￼ 优先级机制 工作循环是基本的任务调度机制，工作循环中每次处理一个任务（工作单元），处理完毕有一次喘息的机会，此时通过 shouldYield 函数（idleDeadline.timeRemaining()）判读时间是否用完，用完则把时间还给主线程等待下次 requestIdleCallback 的唤起，否则继续执行任务。 优先级机制用来处理突发事件与优化次序。 有如下策略： ￼ 到 commit 阶段了，提高优先级 ￼ 高优任务做一半出错了，给降一下优先级 ￼ 抽空关注一下低优任务，别给饿死了 ￼ 如果对应 DOM 节点此刻不可见，给降到最低优先级 是工作循环的辅助机制。

4.如何中断/断点恢复？ 中断：检查当前正在处理的工作单元，保存当前成果（firstEffect, lastEffect），修改 tag 标记一下，迅速收尾并再开一个 requestIdleCallback，下次有机会再做 断点恢复：下次再处理到该工作单元时，看 tag 是被打断的任务，接着做未完成的部分或者重做 自然中断（时间耗尽），或优先级中断（高优任务中断），原理相同。

5.如何收集任务结果？ 每个节点更新结束时向上归并 effect list 来收集任务结果，reconciliation 结束后，根节点的 effect list 里记录了包括 DOM change 在内的所有 side effect。

requestIdleCallback 让开发者在主事件循环中执行后台或低优先级的任务,不会对动画和用户交互等关键事件产生影响。

fiber 架构：

*   循环条件：利用 requestIdeCallback 空闲时间递减.
*   遍历过程：利用链表，找孩子找兄弟找父亲.

# React hooks 中 useCallback 的使用场景是什么

> 原文：[https://q.shanyue.tech/fe/react/212.html](https://q.shanyue.tech/fe/react/212.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 212(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/212)

Author

回答者: [newwangyiyang(opens new window)](https://github.com/newwangyiyang)

能想到的只有两个场景

1.  作为 props 传递的函数，集合 memo 一起使用；
2.  作为更新触发的依赖项 主要目的是为了避免高昂的计算和不必要的重复渲染

# useEffect 中如何使用 async/await

> 原文：[https://q.shanyue.tech/fe/react/236.html](https://q.shanyue.tech/fe/react/236.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 236(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/236)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

```
function useEffect(effect: EffectCallback, deps?: DependencyList): void;
type EffectCallback = () => void | (() => void | undefined); 
```

根据文档及 ts 的提示来看，`useEffect` 的回调参数返回的是一个清除副作用的 `clean-up` 函数。因此无法返回 `Promise`，更无法使用 `async/await`

```
useEffect(() => {
  const subscription = props.source.subscribe();
  return () => {
    // Clean up the subscription
    subscription.unsubscribe();
  };
}); 
```

**此时可以选择再包装一层 async 函数，置于 useEffect 的回调函数中，变相使用 async/await**

```
async function fetchMyAPI() {
  let response = await fetch("api/data");
  response = await res.json();
  dataSet(response);
}

useEffect(() => {
  fetchMyAPI();
}, []); 
```

Author

回答者: [jkLennon(opens new window)](https://github.com/jkLennon)

useEffect(() => { (async function anyNameFunction() { await loadContent(); })(); }, []);

# react hooks 的原理是什么

> 原文：[https://q.shanyue.tech/fe/react/273.html](https://q.shanyue.tech/fe/react/273.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 273(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/273)

Author

回答者: [newwangyiyang(opens new window)](https://github.com/newwangyiyang)

闭包 ➕ 链表

Author

回答者: [EricWong1994(opens new window)](https://github.com/EricWong1994)

这也太短了吧。。具体点呢

# redux 解决什么问题，还有什么其他方案

> 原文：[https://q.shanyue.tech/fe/react/279.html](https://q.shanyue.tech/fe/react/279.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 279(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/279)

Author

回答者: [newwangyiyang(opens new window)](https://github.com/newwangyiyang)

1.  mobx
2.  useContext ➕ useReducer

# 为什么不能在表达式里面定义 react hooks

> 原文：[https://q.shanyue.tech/fe/react/280.html](https://q.shanyue.tech/fe/react/280.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 280(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/280)

Author

回答者: [Kffhi(opens new window)](https://github.com/Kffhi)

https://zh-hans.reactjs.org/docs/hooks-rules.html#explanation

# redux 和 mobx 有什么不同

> 原文：[https://q.shanyue.tech/fe/react/372.html](https://q.shanyue.tech/fe/react/372.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 372(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/372)

# 关于 React hooks 的 caputre value，以下输出多少

> 原文：[https://q.shanyue.tech/fe/react/373.html](https://q.shanyue.tech/fe/react/373.html)

更多描述

```
function App() {
  const [count, setCount] = useState(0);
  const incr = () => {
    setTimeout(() => {
      setCount(count + 1);
    }, 3000);
  };
  return <h1 onClick={incr}>{count}</h1>;
} 
```

当连续点击 10 次时，会输出多少

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 373(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/373)

Author

回答者: [zckpp(opens new window)](https://github.com/zckpp)

应该是 1 吧，在 state 被 update 之前 count 一直还是 0

Author

回答者: [jkLennon(opens new window)](https://github.com/jkLennon)

连续点击 10 次是在 3s 内完成，那传给 setTimeout 的 count 都为 0，输出应该都是 1

Author

回答者: [cloudXA(opens new window)](https://github.com/cloudXA)

验证一下 https://codesandbox.io/s/sharp-dawn-5e5hp?file=/src/capture.js

# 在 React 项目中 immutable 是优化性能的

> 原文：[https://q.shanyue.tech/fe/react/374.html](https://q.shanyue.tech/fe/react/374.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 374(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/374)

# 在 redux 中如何发送请求

> 原文：[https://q.shanyue.tech/fe/react/376.html](https://q.shanyue.tech/fe/react/376.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 376(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/376)

Author

回答者: [selecaing(opens new window)](https://github.com/selecaing)

使用 redux-thunk 中间件 就能够在 redux 中发送请求

# 在 redux 中如何写一个记录状态变更的日志插件

> 原文：[https://q.shanyue.tech/fe/react/380.html](https://q.shanyue.tech/fe/react/380.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 380(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/380)

# React 在 setState 时发生了什么

> 原文：[https://q.shanyue.tech/fe/react/383.html](https://q.shanyue.tech/fe/react/383.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 383(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/383)

Author

回答者: [hqylss111(opens new window)](https://github.com/hqylss111)

react16 1.setstae 以后会把 update 队列加入到 mount 里面 如果他在生命周期里面 其实他是进行批量去更新的 如果他是在生命周期里面去 set 其实数据同步的。如果想要拿到最新的就需要脱离 react 生命周期，和 react 事件流 比如在 setTimeout 里面 set 值 他拿到的数据就是最新的。

Author

回答者: [hqylss111(opens new window)](https://github.com/hqylss111)

例如下面代码 `class App extends React.Component { state = { val: 0 } componentDidMount() { setTimeout(() => { // 第一次调用 this.setState({ val: this.state.val + 1 }); console.log('first setState', this.state);

```
 // 第二次调用
  this.setState({ val: this.state.val + 1 });
  console.log('second setState', this.state);
}); 
```

} render() { return

val: { this.state.val }} }

class App extends React.Component { state = { val: 0 } componentDidMount() { // 第一次调用 this.setState({ val: this.state.val + 1 }); console.log('first setState', this.state);

```
 // 第二次调用
 this.setState({ val: this.state.val + 1 });
 console.log('second setState', this.state);

 this.setState({ val: this.state.val + 1 }); 
```

} render() { return

val: { this.state.val }}` 第一个 app 是 12 第二个是 00 1 验证了我上面说的

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

1.  当每次 setState 时，组件会重新渲染
2.  当在函数式组件中 setState 时，如果两次设置的 state 相同时，组件将不会重新渲染
3.  当在事件处理函数中，多次调用 setState，React 将会批量进行渲染
4.  当在事件处理函数外，多次调用 setState，React 将不会重新渲染
5.  在 React18 之后，同一函数多次调用 setState，React 都将会批量进行渲染

Author

回答者: [hqylss111(opens new window)](https://github.com/hqylss111)

在 React18 之后，同一函数多次调用 setState，React 都将会重新渲染 为什么会这样修改那？ 目的是什么那？ 批量修改不是性能更好嘛？

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

@hqylss111 口误了，其实是都会批量渲染，可以看看我的示例: https://codesandbox.io/s/react18-state-pilianggengxin-75ktu

# 如何设计一个 UI 组件库

> 原文：[https://q.shanyue.tech/fe/react/385.html](https://q.shanyue.tech/fe/react/385.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 385(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/385)

# React 中的 dom diff 算法如何从 O(n3) 优化到 O(n) 的

> 原文：[https://q.shanyue.tech/fe/react/410.html](https://q.shanyue.tech/fe/react/410.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 410(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/410)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

> 参考官方文档: [协调的设计动机(opens new window)](https://zh-hans.reactjs.org/docs/reconciliation.html#motivation)
> 
> 此算法有一些通用的解决方案，即生成将一棵树转换成另一棵树的最小操作次数。然而，即使使用最优的算法，该算法的复杂程度仍为 O(n 3 )，其中 n 是树中元素的数量。
> 
> 如果在 React 中使用该算法，那么展示 1000 个元素则需要 10 亿次的比较。这个开销实在是太过高昂。于是 React 在以下两个假设的基础之上提出了一套 O(n) 的启发式算法：
> 
> 1.  两个不同类型的元素会产生出不同的树；
> 2.  开发者可以通过设置 key 属性，来告知渲染哪些子元素在不同的渲染下可以保存不变；
> 
> 在实践中，我们发现以上假设在几乎所有实用的场景下都成立。

# 在 React 应用中如何排查性能问题

> 原文：[https://q.shanyue.tech/fe/react/411.html](https://q.shanyue.tech/fe/react/411.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 411(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/411)

# React 17.0 有什么变化

> 原文：[https://q.shanyue.tech/fe/react/415.html](https://q.shanyue.tech/fe/react/415.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 415(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/415)

# 现代框架如 React、Vue 相比原生开发有什么优势

> 原文：[https://q.shanyue.tech/fe/react/460.html](https://q.shanyue.tech/fe/react/460.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 460(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/460)

Author

回答者: [illumi520(opens new window)](https://github.com/illumi520)

render（UI）

Author

回答者: [jkLennon(opens new window)](https://github.com/jkLennon)

react、vue： 1、一套代码维护 Android 和 ios 两个平台，减少开发成本 2、相同功能可以使用组件复用 3、两个平台可以同时更新，原生代码更新时需要审核

# React/Vue 中的 router 实现原理如何

> 原文：[https://q.shanyue.tech/fe/react/463.html](https://q.shanyue.tech/fe/react/463.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 463(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/463)

Author

回答者: [buzuosheng(opens new window)](https://github.com/buzuosheng)

前端路由实现的本质是**监听 url 变化**，实现方式有两种：Hash 模式和 History 模式，无需刷新页面就能重新加载相应的页面。 Hash url 的格式为`www.a.com/#/`，当#后的哈希值发生变化时，通过 hashchange 事件监听，然后页面跳转。 History url 通过`history.pushState`和`history.replaceState`改变 url。 两种模式的区别：

*   hash 只能改变#后的值，而 history 模式可以随意设置同源 url；
*   hash 只能添加字符串类的数据，而 history 可以通过 API 添加多种类型的数据；
*   hash 的历史记录只显示之前的`www.a.com`而不会显示 hash 值，而 history 的每条记录都会进入到历史记录；
*   hash 无需后端配置且兼容性好，而 history 需要配置`index.html`用于匹配不到资源的情况。

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

前端路由有两种实现方式:

## history API

*   通过 `history.pushState()` 跳转路由
*   通过 `popstate event` 监听路由变化，但无法监听到 `history.pushState()` 时的路由变化

## hash

*   通过 `location.hash` 跳转路由
*   通过 `hashchange event` 监听路由变化

# 在 SSR 项目中如何判断当前环境时服务器端还是浏览器端

> 原文：[https://q.shanyue.tech/fe/react/474.html](https://q.shanyue.tech/fe/react/474.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 474(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/474)

Author

回答者: [listenecho(opens new window)](https://github.com/listenecho)

1.  SSR 渲染的时候，服务端与客户端走不同的 webpack 打包配置。 那么就可以在打包的时候写入区分环境的环境变量。
2.  服务器端是没有 window document 等浏览器宿主环境对象的，可以通过 类型检测 这些对象 来区分。

```
 ::: tip Author
回答者: [shfshanyue](https://github.com/shfshanyue)
:::

``` js
const isServer = typeof window === 'undefined' 
```

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

> 1.  SSR 渲染的时候，服务端与客户端走不同的 webpack 打包配置。 那么就可以在打包的时候写入区分环境的环境变量。
> 2.  服务器端是没有 window document 等浏览器宿主环境对象的，可以通过 类型检测 这些对象 来区分。

一般就是通过第二条来区分了

# React.setState 是同步还是异步的

> 原文：[https://q.shanyue.tech/fe/react/506.html](https://q.shanyue.tech/fe/react/506.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 506(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/506)

Author

回答者: [buzuosheng(opens new window)](https://github.com/buzuosheng)

setState 并不能保证是同步的，在生命周期函数和合成事件中是异步的，在原生事件和 setTimeout 中是同步的。

# 什么是服务器渲染 (SSR)

> 原文：[https://q.shanyue.tech/fe/react/507.html](https://q.shanyue.tech/fe/react/507.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 507(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/507)

Author

回答者: [buzuosheng(opens new window)](https://github.com/buzuosheng)

服务端渲染 SSR：在服务端将请求的所有资源生成 HTML，客户端收到后可以直接渲染。

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

1.  `renderToString`
2.  `hydrate`

Author

回答者: [haotie1990(opens new window)](https://github.com/haotie1990)

服务器渲染 (SSR)：将同一个组件渲染为服务器端的 HTML 字符串，将它们直接发送到浏览器，最后将这些静态标记"激活"为客户端上完全可交互的应用程序。这个过程可以成为服务端渲染。

优势：

*   更好的 SEO

*   更快的内容到达时间 (time-to-content)

[Vue.js 服务器端渲染指南(opens new window)](https://ssr.vuejs.org/zh/)

# 在 React 中如何实现代码分割 (code splitting)

> 原文：[https://q.shanyue.tech/fe/react/508.html](https://q.shanyue.tech/fe/react/508.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 508(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/508)

Author

回答者: [haotie1990(opens new window)](https://github.com/haotie1990)

[https://zh-hans.reactjs.org/docs/code-splitting.html(opens new window)](https://zh-hans.reactjs.org/docs/code-splitting.html)

# 在 React 中如何做好性能优化

> 原文：[https://q.shanyue.tech/fe/react/510.html](https://q.shanyue.tech/fe/react/510.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 510(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/510)

Author

回答者: [buzuosheng(opens new window)](https://github.com/buzuosheng)

*   代码分割
*   React.memo()、shouldComponentUpdate()等防止不必要的渲染
*   Fragments 避免额外标记
*   错误边界避免组件在出错时破坏整个应用

# 在 React 中发现状态更新时卡顿，此时应该如何定位及优化

> 原文：[https://q.shanyue.tech/fe/react/511.html](https://q.shanyue.tech/fe/react/511.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 511(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/511)

# 当多次重复点击按钮时，以下三个 Heading 是如何渲染的

> 原文：[https://q.shanyue.tech/fe/react/512.html](https://q.shanyue.tech/fe/react/512.html)

更多描述

```
import React, { memo, useMemo, useState } from "react";

const Heading = memo(({ style, title }) => {
  console.log("Rendered:", title);

  return <h1 style={style}>{title}</h1>;
});

export default function App() {
  const [count, setCount] = useState(0);

  const normalStyle = {
    backgroundColor: "teal",
    color: "white",
  };

  const memoizedStyle = useMemo(() => {
    return {
      backgroundColor: "red",
      color: "white",
    };
  }, []);

  return (
    <>
      <button
        onClick={() => {
          setCount(count + 1);
        }}
      >
        Increment {count}
      </button>
      <Heading style={memoizedStyle} title="Memoized" />
      <Heading style={normalStyle} title="Normal" />
      <Heading title="React.memo Normal" />
    </>
  );
} 
```

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 512(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/512)

Author

回答者: [buzuosheng(opens new window)](https://github.com/buzuosheng)

"Memoized"只在第一次渲染时打印一次，后续点击不刷新。 "Normal"会在每次渲染时打印。 "React.memo Normal”只会在第一次渲染时打印一次。

使用`useMemo`时，依赖数组为 null，这意味着只会在首次渲染时，对 memoizedStyle 进行一次计算，后续不再计算。 在渲染`<heading></heading>组件时，React.memo 会先判断前后状态

```
memoizedStyle === memoizedStyle; //true 
```

由于状态始终是一个对象，自身始终是与自身相等的，所以不会导致重新渲染。

没有使用`useMemo`时，每次点击，对`<Heading />`组件传入属性，React.memo 判断

```
 {
    backgroundColor: "teal",
    color: "white",
  } ===  {
    backgroundColor: "teal",
    color: "white",
  }  // false 
```

每次都会传入一个新的对象，由于 React.memo 对 prop 进行浅比较，两个对象总是不相等的。 如果需要进行深比较，可以对 React.memo 传入一个深比较函数作为第二个参数。

"React.memo Normal”的参数是字符串，相比对象的比较简单了很多，所以不会导致重新渲染。

# Javascript 数组中有那些方法可以改变自身，那些不可以

> 原文：[https://q.shanyue.tech/fe/react/553.html](https://q.shanyue.tech/fe/react/553.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 553(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/553)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

不可改变自身的 Array API

*   Array.prototype.map

Author

回答者: [Kiera569(opens new window)](https://github.com/Kiera569)

不改变原数组的方法：concat/join/reduce/map/forEach/filter/slice/findIndex

改变原数组的方法：push/unshift/pop/shift/sort/splice/reverse

# 关于 setState 以下代码的输出

> 原文：[https://q.shanyue.tech/fe/react/566.html](https://q.shanyue.tech/fe/react/566.html)

更多描述

代码如下所示，每次切换 TODO 状态时，通过手动修改 `todo.status` 再 setTodo，此时是否会修改成功

> 代码见 [setState - codesandbox(opens new window)](https://codesandbox.io/s/setstate-r7qof?file=/src/App.js)

```
import { useState } from "react";

export default function App() {
  const [todo, setTodo] = useState({ id: 1, status: "TODO" });
  return (
    <div className="App">
      <button
        onClick={() => {
          todo.status = !todo.status;
          setTodo(todo);
        }}
      >
        Toggle Status
      </button>
      <h1>{todo.status}</h1>
    </div>
  );
} 
```

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 566(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/566)

Author

回答者: [hellolukeding(opens new window)](https://github.com/hellolukeding)

state 是只读的

# React 中什么是合成事件

> 原文：[https://q.shanyue.tech/fe/react/606.html](https://q.shanyue.tech/fe/react/606.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 606(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/606)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

1.  提供统一的 API，抹平各大浏览器差异
2.  所有事件绑定在 React Root Element 进行事件委托

# 前端项目中有哪些副作用

> 原文：[https://q.shanyue.tech/fe/react/608.html](https://q.shanyue.tech/fe/react/608.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 608(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/608)

# React/Vue 中受控组件与不受控组件的区别

> 原文：[https://q.shanyue.tech/fe/react/609.html](https://q.shanyue.tech/fe/react/609.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 609(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/609)

# React 中监听 input 的 onChange 事件的原生事件是什么

> 原文：[https://q.shanyue.tech/fe/react/611.html](https://q.shanyue.tech/fe/react/611.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 611(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/611)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

[React 中 onChange 的原生事件是什么？(opens new window)](https://codesandbox.io/s/input-onchange-1ybhw?file=/src/App.js)

```
import "./styles.css";

export default function App() {
  return (
    <div className="App">
      <input
        onChange={(e) => {
          console.log("Event: ", e);
          console.log("NativeEvent: ", e.nativeEvent);
          console.log("CurrentTarget: ", e.nativeEvent.currentTarget);
          console.log("NativeEvent Type: ", e.nativeEvent.type);
        }}
      />
    </div>
  );
} 
```

# 在 React hooks 中如何模拟 forceUpdate

> 原文：[https://q.shanyue.tech/fe/react/616.html](https://q.shanyue.tech/fe/react/616.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 616(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/616)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

```
const [ignored, forceUpdate] = useReducer((x) => x + 1, 0);

function handleClick() {
  forceUpdate();
} 
```

# React/Vue 中兄弟组件如何进行通信

> 原文：[https://q.shanyue.tech/fe/react/629.html](https://q.shanyue.tech/fe/react/629.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 629(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/629)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

> [见代码：React 中兄弟组件如何通信 - CodeSandbox(opens new window)](https://codesandbox.io/s/react-xiongdizujiantongxin-f2jf6)

兄弟组件可通过 prop 与回调函数式的 prop 进行通信

```
import { useState } from "react";
import "./styles.css";

function One({ count, setCount }) {
  return (
    <div style={{ border: "1px solid red" }}>
      <h2>Conponent One</h2>
      <button onClick={() => setCount(count + 1)}>Click</button>
      <div>{count}</div>
    </div>
  );
}

function Two({ count, setCount }) {
  return (
    <div style={{ border: "1px solid red" }}>
      <h2>Conponent Two</h2>
      <button onClick={() => setCount(count + 1)}>Click</button>
      <div>{count}</div>
    </div>
  );
}

export default function App() {
  const [count, setCount] = useState(0);
  return (
    <div className="App">
      <One count={count} setCount={(c) => setCount(c)} />
      <Two count={count} setCount={(c) => setCount(c)} />
    </div>
  );
} 
```

# React.memo 中是如何实现性能优化的

> 原文：[https://q.shanyue.tech/fe/react/630.html](https://q.shanyue.tech/fe/react/630.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 630(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/630)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

当 React 中一个组件进行更新时，它的所有子组件都会进行重新渲染，即便子组件的 props 并未发生任何改变。

`React.memo` 对子组件默认使用浅比较对比前后两次 props 的变更，若未发生变更则不会重新渲染，因此提高了性能。

可参考以下两个示例，加深理解:

1.  [React.memo 和性能优化(opens new window)](https://codesandbox.io/s/zujianxiasuoyouzizujianhuifashengchongxinxuanran-bv70e)。当某个组件状态更新时，它的所有子组件树将会重新渲染。
2.  [React.memo 和 React.useMemo 是如何优化性能的(opens new window)](https://codesandbox.io/s/reactmemo-and-reactusememo-79txp)

# immer 的原理是什么，为什么它的性能更高

> 原文：[https://q.shanyue.tech/fe/react/632.html](https://q.shanyue.tech/fe/react/632.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 632(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/632)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

```
const state = {
  user: { id: 3 },
  role: { name: "admin" },
};

const proxyState = new Proxy(state, {
  get(target, prop) {
    return target[prop];
  },
}); 
```

```
//=> True
state !== proxyState;

//=> True
state.user === proxyState.user; 
```

# React.useMemo 与 React.useCallback 是如何进行性能优化的

> 原文：[https://q.shanyue.tech/fe/react/633.html](https://q.shanyue.tech/fe/react/633.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 633(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/633)

Author

回答者: [Muralitob(opens new window)](https://github.com/Muralitob)

通过传入的依赖（浅比较）来确定是否返回新的值还是以前的值

# 同一页面三个组件请求同一个 API 发送了三次请求，如何优化

> 原文：[https://q.shanyue.tech/fe/react/642.html](https://q.shanyue.tech/fe/react/642.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 642(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/642)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

```
const fetchUser = (id) => {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log("Fetch: ", id);
      resolve(id);
    }, 5000);
  });
};

const cache = {};
const cacheFetchUser = (id) => {
  if (cache[id]) {
    return cache[id];
  }
  cache[id] = fetchUser(id);
  return cache[id];
}; 
```

```
cacheFetchUser(3).then((id) => console.log(id))
cacheFetchUser(3).then((id) => console.log(id))
cacheFetchUser(3).then((id) => console.log(id))

// Fetch:  3
​// 3
​// 3
​// 3 
```

# 如何优化 React 项目的性能

> 原文：[https://q.shanyue.tech/fe/react/645.html](https://q.shanyue.tech/fe/react/645.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 645(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/645)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

1.  避免不必要的渲染，shouldComponentUpdate、React.memo、React.useMemo、React.useCallback。
2.  代码分割，React.lazy 动态加载组件
3.  使用 `react-query`，对请求响应进行缓存、重发等，避免多次请求，减少网络 IO 消耗及优化渲染次数
4.  使用 `useDebounce`，对值及事件处理函数进行防抖，避免状态频繁变动，优化渲染次数
5.  使用 `useImmer`

# useLayoutEffect 和 useEffect 有什么区别

> 原文：[https://q.shanyue.tech/fe/react/671.html](https://q.shanyue.tech/fe/react/671.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 671(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/671)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

TODO

Author

回答者: [illumi520(opens new window)](https://github.com/illumi520)

dom 时间，一个是之前，一个是之后

Author

回答者: [luoheix(opens new window)](https://github.com/luoheix)

可以参考：[useEffect 和 useLayoutEffect 的区别 - 掘金(opens new window)](https://juejin.cn/post/6844904008402862094) 和 [useEffect 和 useLayoutEffect 到底有什么区别？(opens new window)](https://github.com/yaofly2012/note/issues/149#issuecomment-660593917) 这两篇文章

*   useLayoutEffect 和 componentDidMount 和 componentDidUpdate 触发时机一致（都在在 DOM 修改后且浏览器渲染之前）；
*   useLayoutEffect 要比 useEffect 更早的触发执行；
*   useLayoutEffect 会阻塞浏览器渲染，切记执行同步的耗时操作

# 在 React Hooks 中实现 usePreviouseValue 取上次渲染的值

> 原文：[https://q.shanyue.tech/fe/react/677.html](https://q.shanyue.tech/fe/react/677.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 677(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/677)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

TODO

# 在虚拟 DOM 中进行 diff 算法时，介绍当根据 key 对数组进行重用时的算法

> 原文：[https://q.shanyue.tech/fe/react/721.html](https://q.shanyue.tech/fe/react/721.html)

更多描述

如以下示例，当从上方五个 div 变为下方五个 div 时，由于 diff 算法，无需重复构建 DOM 创建五个新的 div 标签。

请写出此时重用的算法，并给出时间复杂度

```
<div key="1">Demo 1</div>
<div key="2">Demo 2</div>
<div key="3">Demo 3</div>
<div key="4">Demo 4</div>
<div key="5">Demo 5</div>

<div key="4">Demo 4</div>
<div key="5">Demo 5</div>
<div key="2">Demo 2</div>
<div key="1">Demo 1</div>
<div key="3">Demo 3</div> 
```

```
function updateChildren(element, oldVnodes, newVnodes) {} 
```

## 可参考

1.  [编辑距离(opens new window)](https://leetcode-cn.com/problems/edit-distance/)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 721(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/721)

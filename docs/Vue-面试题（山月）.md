# vue3.0 中为什么要使用 Proxy，它相比以前的实现方式有什么改进

> 原文：[https://q.shanyue.tech/fe/vue/12.html](https://q.shanyue.tech/fe/vue/12.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 12(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/12)

Author

回答者: [xiaoai7904(opens new window)](https://github.com/xiaoai7904)

简单描述就是: 性能更好，解决无法监听数组变化问题

Author

回答者: [konglingwen94(opens new window)](https://github.com/konglingwen94)

1.  可以提高实例初始化启动速度，优化数据响应式系统，由全部监听改为惰性监听（lazy by default)。
2.  数据响应式系统全语言特性支持，添加数组索引修改监听，对象的属性增加和删除。

Author

回答者: [hefeng1208(opens new window)](https://github.com/hefeng1208)

1.  Vue2.x 通过给每个对象添加`getter setter`属性去改变对象,实现对数据的观测,Vue3.x 通过 Proxy 代理目标对象,且一开始只代理最外层对象,嵌套对象`lazy by default` ,性能会更好
2.  支持数组索引修改,对象属性的增加,删除

# react 与 vue 数组中 key 的作用是什么

> 原文：[https://q.shanyue.tech/fe/vue/72.html](https://q.shanyue.tech/fe/vue/72.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 72(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/72)

Author

回答者: [su-imagine(opens new window)](https://github.com/su-imagine)

diff 算法需要比对虚拟 dom 的修改，然后异步的渲染到页面中，当出现大量相同的标签时，vnode 会首先判断 key 和标签名是否一致，如果一致再去判断子节点一致，使用 key 可以帮助 diff 算法提升判断的速度，在页面重新渲染时更快消耗更少

# vue 中 v-if 和 v-show 的区别是什么

> 原文：[https://q.shanyue.tech/fe/vue/90.html](https://q.shanyue.tech/fe/vue/90.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 90(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/90)

Author

回答者: [zhaofeihao(opens new window)](https://github.com/zhaofeihao)

> v-show always compiles and renders everything - it simply adds the "display: none" style to the element. It has a higher initial load cost, but toggling is very cheap. Incomparison, v-if is truely conditional: it is lazy, so if its initial condition is false, it won't even do anything. This can be good for initial load time. When the condition is true, v-if will then compile and render its content. Toggling a v-if block actually tearsdown everything inside it, e.g. Components inside v-if are acually destroyed and re-created when toggled, so toggling a huge v-if block can be more expensive than v-show.

v-show 总是会进行编译和渲染的工作 - 它只是简单的在元素上添加了 `display: none;` 的样式。v-show 具有较高的初始化性能成本上的消耗，但是使得转换状态变得很容易。 相比之下，v-if 才是真正「有条件」的：它的加载是惰性的，因此，若它的初始条件是 false，它就不会做任何事情。这对于初始加载时间来说是有益的，当条件为 true 时，v-if 才会编译并渲染其内容。切换 v-if 下的块儿内容实际上时销毁了其内部的所有元素，比如说处于 v-if 下的组件实际上在切换状态时会被销毁并重新生成，因此，切换一个较大 v-if 块儿时会比 v-show 消耗的性能多。

# vue 中 computed 的原理是什么

> 原文：[https://q.shanyue.tech/fe/vue/91.html](https://q.shanyue.tech/fe/vue/91.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 91(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/91)

Author

回答者: [wython(opens new window)](https://github.com/wython)

要讲清楚，computed 原理，首先得讲 vue 响应式原理，因为 computed 的实现是基于 Watcher 对象的。 那么 vue 的响应式原理是什么呢，众所周知，vue 是基于 Object.defineProperty 实现监听的。在 vue 初始化数据 data 和 computed 数据过程中。会涉及到以下几个对象：

1.  Observe 对象
2.  Dep 对象
3.  Watch 对象 Observe 对象是在 data 执行响应式时候调用，因为 computed 属性基于响应式属性，所以其不需要创建 Observe 对象。 Dep 对象主要功能是做依赖收集，有个属性维护多个 Watch 对象，当更新时候循环调用每个 Watch 执行更新。 Watch 对象主要是用于更新，而且是收集的重点对象。

这里谈到 computed 计算属性，首先要知道，其有两种定义方式，一种是方法，另一种是 get，set 属性。而且，其内部监听的对象必须是已经定义响应式的属性，比如 data 的属性 vuex 的属性。

vue 在创建 computed 属性时候，会循环所有计算属性，每一个计算属性会创建一个 watch，并且在通过 defineProperty 定义监听，在 get 中，计算属性工作是做依赖收集，在 set 中，计算属性重要工作是重新执行计算方法，这里需要多补充一句，因为 computed 是懒执行，也就是说第一次初始化之后，变不会执行计算，下一次变更执行重新计算是在 set 中。

另一个补充点是依赖收集的时机，computed 收集时机和 data 一样，是在组件挂载前，但是其收集对象是自己属性对应的 watch，而 data 本身所有数据对应一个 watch。

以下附计算属性源码验证说法：

```
function initComputed(vm: Component, computed: Object) {
  // $flow-disable-line
  const watchers = (vm._computedWatchers = Object.create(null));
  // computed properties are just getters during SSR
  const isSSR = isServerRendering();

  for (const key in computed) {
    const userDef = computed[key];
    const getter = typeof userDef === "function" ? userDef : userDef.get;
    if (process.env.NODE_ENV !== "production" && getter == null) {
      warn(`Getter is missing for computed property "${key}".`, vm);
    }

    if (!isSSR) {
      // create internal watcher for the computed property.
      watchers[key] = new Watcher(
        vm,
        getter || noop,
        noop,
        computedWatcherOptions
      );
    }

    // component-defined computed properties are already defined on the
    // component prototype. We only need to define computed properties defined
    // at instantiation here.
    if (!(key in vm)) {
      defineComputed(vm, key, userDef);
    } else if (process.env.NODE_ENV !== "production") {
      if (key in vm.$data) {
        warn(`The computed property "${key}" is already defined in data.`, vm);
      } else if (vm.$options.props && key in vm.$options.props) {
        warn(
          `The computed property "${key}" is already defined as a prop.`,
          vm
        );
      }
    }
  }
} 
```

可以看到，在执行 new Watcher 之前，会对计算属性做判断，判断其是否为函数，如果不是则取 getter。这是因为计算属性有两种定义方式。之后第二步是执行 deineCoumputed。这一步只是简单的调用 defineProterty 我就不贴代码了。

关于计算属性的 getter 和 setter 定义如下： 重点关注 get 的懒加载部分，和 Watcher 的定义

```
function createComputedGetter(key) {
  return function computedGetter() {
    const watcher = this._computedWatchers && this._computedWatchers[key];
    if (watcher) {
      if (watcher.dirty) {
        watcher.evaluate();
      }
      if (Dep.target) {
        watcher.depend();
      }
      return watcher.value;
    }
  };
}

function createGetterInvoker(fn) {
  return function computedGetter() {
    return fn.call(this, this);
  };
} 
```

# vue-loader 的实现原理是什么

> 原文：[https://q.shanyue.tech/fe/vue/92.html](https://q.shanyue.tech/fe/vue/92.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 92(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/92)

Author

回答者: [hwb2017(opens new window)](https://github.com/hwb2017)

vue-loader 会把 sfc 中的内容拆分为 template，script，style 三个“虚拟模块”，然后分别匹配 webpack 配置中对应的 rules，比如 script 模块会匹配所有跟处理 JavaScript 或 TypeScript 相关的 loader。

template 中的内容会通过 vue compiler 转换为 render 函数后合并到 script “虚拟模块”中。

scoped style 会经过 vue-loader/style-post-loader 的处理，成为只匹配特定元素的私有样式。

参考 [vue-loader README(opens new window)](https://github.com/vuejs/vue-loader/blob/master/README.md)

# 如何使用 react/vue 实现一个 message API

> 原文：[https://q.shanyue.tech/fe/vue/101.html](https://q.shanyue.tech/fe/vue/101.html)

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

# 如果使用 SSR，可以在 created/componentWillMount 中访问 localStorage 吗

> 原文：[https://q.shanyue.tech/fe/vue/147.html](https://q.shanyue.tech/fe/vue/147.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 147(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/147)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

不可以，created/componentWillMount 时，还未挂载，代码仍然在服务器中执行，此时没有浏览器环境，因此此时访问 localStorage 将会报错

Author

回答者: [thunderqin(opens new window)](https://github.com/thunderqin)

我试了 可以啊 这是时候只是找不到实体 DOM 但是具备 js 的执行环境了

# 在 react/vue 中数组是否可以以在数组中的次序为 key

> 原文：[https://q.shanyue.tech/fe/vue/155.html](https://q.shanyue.tech/fe/vue/155.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 155(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/155)

Author

回答者: [into-piece(opens new window)](https://github.com/into-piece)

不可，key 应为唯一标示，在数组变更时插入或删除后，index 无法确保始终指向对应的序列

# 如何设计一个 UI 组件库

> 原文：[https://q.shanyue.tech/fe/vue/385.html](https://q.shanyue.tech/fe/vue/385.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 385(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/385)

# vue3 中，如何监听数组的变化

> 原文：[https://q.shanyue.tech/fe/vue/457.html](https://q.shanyue.tech/fe/vue/457.html)

更多描述

比如深层数组如何监听

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 457(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/457)

Author

回答者: [18sby(opens new window)](https://github.com/18sby)

不需要额外监听，因为 Proxy 代理后的数据，数组的修改也是可以监听到的，reactive 之后直接修改即可。

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

TODO

Author

回答者: [illumi520(opens new window)](https://github.com/illumi520)

let list = [] const listProxy = new Proxy(list, { set(target, property, value) { console.log('set', property, value) //property 指下标 value 值 target[property] = value return true //表示设置成功 } })

listProxy.push(100)

# Vue 中 nextTick 的实现原理是什么

> 原文：[https://q.shanyue.tech/fe/vue/458.html](https://q.shanyue.tech/fe/vue/458.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 458(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/458)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

*   Promise
*   MutationObserver
*   setImmediate
*   setTimeout

# 现代框架如 React、Vue 相比原生开发有什么优势

> 原文：[https://q.shanyue.tech/fe/vue/460.html](https://q.shanyue.tech/fe/vue/460.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 460(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/460)

Author

回答者: [illumi520(opens new window)](https://github.com/illumi520)

render（UI）

Author

回答者: [jkLennon(opens new window)](https://github.com/jkLennon)

react、vue： 1、一套代码维护 Android 和 ios 两个平台，减少开发成本 2、相同功能可以使用组件复用 3、两个平台可以同时更新，原生代码更新时需要审核

# React/Vue 中的 router 实现原理如何

> 原文：[https://q.shanyue.tech/fe/vue/463.html](https://q.shanyue.tech/fe/vue/463.html)

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

# 前端项目中有哪些副作用

> 原文：[https://q.shanyue.tech/fe/vue/608.html](https://q.shanyue.tech/fe/vue/608.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 608(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/608)

# React/Vue 中受控组件与不受控组件的区别

> 原文：[https://q.shanyue.tech/fe/vue/609.html](https://q.shanyue.tech/fe/vue/609.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 609(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/609)

# React/Vue 中兄弟组件如何进行通信

> 原文：[https://q.shanyue.tech/fe/vue/629.html](https://q.shanyue.tech/fe/vue/629.html)

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

# 在虚拟 DOM 中进行 diff 算法时，介绍当根据 key 对数组进行重用时的算法

> 原文：[https://q.shanyue.tech/fe/vue/721.html](https://q.shanyue.tech/fe/vue/721.html)

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
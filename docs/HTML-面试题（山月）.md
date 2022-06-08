# html

# 网站开发中，如何实现图片的懒加载

> 原文：[https://q.shanyue.tech/fe/html/1.html](https://q.shanyue.tech/fe/html/1.html)

更多描述

网站开发中，如何实现图片的懒加载，随着 web 技术的发展，他有没有一些更好的方案

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 1(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/1)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

懒加载，顾名思义，在当前网页，滑动页面到能看到图片的时候再加载图片

故问题拆分成两个：

1.  如何判断图片出现在了当前视口 （即如何判断我们能够看到图片）
2.  如何控制图片的加载

## 方案一: 位置计算 + 滚动事件 (Scroll) + DataSet API

### 如何判断图片出现在了当前视口

`clientTop`，`offsetTop`，`clientHeight` 以及 `scrollTop` 各种关于图片的高度作比对

这些高度都代表了什么意思？

这我以前有可能是知道的，那时候我比较单纯，喜欢死磕。我现在想通了，背不过的东西就不要背了

**所以它有一个问题：复杂琐碎不好理解！**

仅仅知道它静态的高度还不够，我们还需要知道动态的

**如何动态？监听 `window.scroll` 事件**

### 如何控制图片的加载

```
<img data-src="shanyue.jpg" /> 
```

首先设置一个临时 Data 属性 `data-src`，控制加载时使用 `src` 代替 `data-src`，可利用 DataSet API 实现

```
img.src = img.datset.src 
```

## 方案二: getBoundingClientRect API + Scroll with Throttle + DataSet API

改进一下

### 如何判断图片出现在了当前视口

引入一个新的 API， **`Element.getBoundingClientRect()` 方法返回元素的大小及其相对于视口的位置。**

![getBoundingClientRect示例图](img/5356f85f1789c7fdfae64d54d99f9d00.png)

那如何判断图片出现在了当前视口呢，根据示例图示意，代码如下，这个就比较好理解了，就可以很容易地背会(就可以愉快地去面试了)。

```
// clientHeight 代表当前视口的高度
img.getBoundingClientRect().top < document.documentElement.clientHeight; 
```

**监听 `window.scroll` 事件也优化一下**

加个节流器，提高性能。工作中一般使用 `lodash.throttle` 就可以了，万能的 `lodash` 啊！

```
_.throttle(func, [(wait = 0)], [(options = {})]); 
```

参考 [什么是防抖和节流，他们的应用场景有哪些(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/3)，或者[前端面试题(opens new window)](https://q.shanyue.tech/fe/js/3.html)

## 方案三: IntersectionObserver API + DataSet API

再改进一下

### 如何判断图片出现在了当前视口

**方案二使用的方法是: `window.scroll` 监听 `Element.getBoundingClientRect()` 并使用 `_.throttle` 节流**

**一系列组合动作太复杂了，于是浏览器出了一个三合一事件: `IntersectionObserver` API，一个能够监听元素是否到了当前视口的事件，一步到位！**

事件回调的参数是 [IntersectionObserverEntry(opens new window)](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserverEntry) 的集合，代表关于是否在可见视口的一系列值

其中，`entry.isIntersecting` 代表目标元素可见

```
const observer = new IntersectionObserver((changes) => {
  // changes: 目标元素集合
  changes.forEach((change) => {
    // intersectionRatio
    if (change.isIntersecting) {
      const img = change.target;
      img.src = img.dataset.src;
      observer.unobserve(img);
    }
  });
});

observer.observe(img); 
```

**当然，`IntersectionObserver` 除了给图片做懒加载外，还可以对单页应用资源做预加载。**

如在 `next.js v9` 中，会对视口内的资源做预加载，可以参考 [next 9 production optimizations(opens new window)](https://nextjs.org/blog/next-9#production-optimizations)

```
<Link href="/about">  <a>关于山月</a>  </Link> 
```

## 方案四: LazyLoading 属性

浏览器觉得懒加载这事可以交给自己做，你们开发者加个属性就好了。实在是...！

```
<img src="shanyue.jpg" loading="lazy" /> 
```

不过目前浏览器兼容性不太好，关于 `loading` 属性的文章也可以查看 [Native image lazy-loading for the web!(opens new window)](https://addyosmani.com/blog/lazy-loading/)

Author

回答者: [hanhang123(opens new window)](https://github.com/hanhang123)

intersectionObserver

Author

回答者: [AgnesWY(opens new window)](https://github.com/AgnesWY)

比较单纯，喜欢死磕。我现在想通了，背不过的东西就不要背了！！！

Author

回答者: [Kiera569(opens new window)](https://github.com/Kiera569)

那时候我比较单纯，喜欢死磕。我现在想通了，背不过的东西就不要背了

Author

回答者: [haiifeng(opens new window)](https://github.com/haiifeng)

那时候我比较单纯，喜欢死磕。我现在想通了，背不过的东西就不要背了

Author

回答者: [hwb2017(opens new window)](https://github.com/hwb2017)

方案二的简单 Demo:

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>图片懒加载</title>
    <style> img {
        width: 100%;
        height: 600px;
      } </style>
  </head>
  <body>
    <img
      src="https://cdn.pixabay.com/photo/2021/08/24/15/38/sand-6570980_960_720.jpg"
      alt="1"
    />
    <img
      src="https://cdn.pixabay.com/photo/2013/02/21/19/06/drink-84533_960_720.jpg"
      alt="2"
    />
    <img
      data-src="https://cdn.pixabay.com/photo/2014/12/15/17/16/boardwalk-569314_960_720.jpg"
      alt="3"
    />
    <img
      data-src="https://cdn.pixabay.com/photo/2013/07/18/20/26/sea-164989_960_720.jpg"
      alt="4"
    />
    <img
      data-src="https://cdn.pixabay.com/photo/2015/04/23/22/00/tree-736885_960_720.jpg"
      alt="5"
    />
    <img
      data-src="https://cdn.pixabay.com/photo/2017/03/26/21/54/yoga-2176668_960_720.jpg"
      alt="6"
    />
    <img
      data-src="https://cdn.pixabay.com/photo/2015/03/17/14/05/sparkler-677774_960_720.jpg"
      alt="7"
    />
    <script src="https://cdn.bootcdn.net/ajax/libs/lodash.js/4.17.20/lodash.js"></script>
    <script> const images = document.querySelectorAll("img");
      const lazyLoad = () => {
        images.forEach((item) => {
          // 触发条件为img元素的CSSOM对象到视口顶部的距离 < 100px + 视口高度，+100px为了提前触发图片加载
          if (
            item.getBoundingClientRect().top <
            document.documentElement.clientHeight + 100
          ) {
            if ("src" in item.dataset) {
              item.src = item.dataset.src;
            }
          }
        });
      };
      document.addEventListener("scroll", _.throttle(lazyLoad, 200)); </script>
  </body>
</html> 
```

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

@hwb2017 可以在 codepen 里写一下，然后附个地址

Author

回答者: [hwb2017(opens new window)](https://github.com/hwb2017)

方案二的 Demo(CodePen) https://codepen.io/hwb2017/pen/BaZKeLa

Author

回答者: [Ha0ran2001(opens new window)](https://github.com/Ha0ran2001)

在 react hook 中要怎么应用？看到这篇文章https://juejin.cn/post/6844903768966856717，但是改成 useRef 不行，hook 不能在循环中使用

Author

回答者: [liucan233(opens new window)](https://github.com/liucan233)

方案一的实现[demo(opens new window)](https://codesandbox.io/s/manual-image-lazy-6zzhr?file=/index.html)，ScrollListener 类用于监听和处理滚动，在 Controller（实现 onEnterViewport 方法）元素出现在视窗内时调用 controller.onEnterViewport()，最后移除 controller。

```
<!DOCTYPE html>
<html lang="zh-CN">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>offsetTop计算实现图片懒加载</title>
    <style> body {
        margin: 0;
      }
      .img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        object-position: center;
      }

      .wrap {
        margin: 10px;
        display: inline-block;
        width: 480px;
        height: 270px;
      }

      .container {
        width: 100vw;
        height: 100vh;
        overflow: auto;
      }

      h1 {
        text-align: center;
      }

      .main {
        margin: 0;
        width: 2000px;
      } </style>
  </head>

  <body>
    <section class="container">
      <h1>请滚动页面查看效果</h1>
      <div class="main"></div>
    </section>
  </body>
  <script defer> "use strict";

    // 图片url列表
    const images = [
      "https://h2.ioliu.cn/bing/Latern2022_ZH-CN0112710917_640x480.jpg?imageslim",
      "https://h2.ioliu.cn/bing/MaldivesHeart_ZH-CN0032539727_640x480.jpg?imageslim",
      "https://h2.ioliu.cn/bing/FaceOff_ZH-CN9969100257_640x480.jpg?imageslim",
      "https://h2.ioliu.cn/bing/DarwinsArch_ZH-CN9740478501_640x480.jpg?imageslim",
      "https://h2.ioliu.cn/bing/TeaGardensMunnar_ZH-CN9587720369_640x480.jpg?imageslim",
      "https://h2.ioliu.cn/bing/SnowyBern_ZH-CN5472524801_640x480.jpg?imageslim",
      "https://h2.ioliu.cn/bing/SevenSistersCliffs_ZH-CN5362127173_640x480.jpg?imageslim",
      "https://h2.ioliu.cn/bing/SpeloncatoSnow_ZH-CN8115437163_640x480.jpg?imageslim",
      "https://h2.ioliu.cn/bing/WinterludeIce_ZH-CN7868524911_640x480.jpg?imageslim",
      "https://h2.ioliu.cn/bing/Oymyakon_ZH-CN7758768574_640x480.jpg?imageslim",
      "https://h2.ioliu.cn/bing/MexicoMonarchs_ZH-CN7526758236_640x480.jpg?imageslim",
      "https://h2.ioliu.cn/bing/WinterOlymics_ZH-CN7384614076_640x480.jpg?imageslim",
      "233",
    ];

    // 未加载时默认url
    const defaultUrl =
      "data:image/svg+xml;base64,PHN2ZyB0PSIxNjQ0ODk5MzI0NDgwIiBjbGFzcz0iaWNvbiIgdmlld0JveD0iMCAwIDEwMjQgMTAyNCIgdmVyc2lvbj0iMS4xIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHAtaWQ9IjIwOTMiIHdpZHRoPSIyMDAiIGhlaWdodD0iMjAwIj48cGF0aCBkPSJNODc0LjEgODEzLjc1SDE0OS45Yy0yMi4yMiAwLTQwLjIzLTE4LjAxLTQwLjIzLTQwLjIzVjI1MC40OWMwLTIyLjIyIDE4LjAxLTQwLjIzIDQwLjIzLTQwLjIzaDcyNC4yYzIyLjIyIDAgNDAuMjMgMTguMDEgNDAuMjMgNDAuMjN2NTIzLjAzYzAgMjIuMjEtMTguMDIgNDAuMjMtNDAuMjMgNDAuMjN6TTI4MC42NiAzMTAuODRjLTM4Ljg5IDAtNzAuNDEgMzEuNTItNzAuNDEgNzAuNDFzMzEuNTIgNzAuNDEgNzAuNDEgNzAuNDEgNzAuNDEtMzEuNTIgNzAuNDEtNzAuNDEtMzEuNTItNzAuNDEtNzAuNDEtNzAuNDF6IG01MTIuOTcgMTAwLjU4YzAtMjIuMjItMTguMDEtNDAuMjMtNDAuMjMtNDAuMjNoLTQwLjIzYy02Ni42NiAwLTEyMC43IDU0LjA0LTEyMC43IDEyMC43djQwLjIzYzAgMzMuMzMtMjcuMDIgNjAuMzUtNjAuMzUgNjAuMzUtMTguMjkgMC0zNC40Ny04LjMxLTQ1LjU0LTIxLjE1LTAuMDUtMC4wNi0wLjI1LTAuMjgtMC4yOS0wLjMzLTIyLjA5LTI0LjA1LTU5Ljc3LTM4Ljg2LTk0Ljk4LTM4Ljg2LTAuNDQgMC0wLjg0IDAuMTItMS4yOCAwLjEzbC0wLjA2LTAuMDZjLTg4LjI2IDAuNzMtMTU5LjU5IDcyLjQ0LTE1OS41OSAxNjAuODYgMCAyMi4yMiAxOC4wMSA0MC4yMyA0MC4yMyA0MC4yM0g3NTMuNGMyMi4yMiAwIDQwLjIzLTE4LjAxIDQwLjIzLTQwLjIzVjQxMS40MnoiIHAtaWQ9IjIwOTQiIGZpbGw9IiNjZGNkY2QiPjwvcGF0aD48L3N2Zz4=";

    // 加载错误时代替
    const errorUrl =
      "data:image/svg+xml;base64,PHN2ZyB0PSIxNjQ0ODk5ODEzMDQ1IiBjbGFzcz0iaWNvbiIgdmlld0JveD0iMCAwIDEwMjQgMTAyNCIgdmVyc2lvbj0iMS4xIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHAtaWQ9IjQ0OTEiIHdpZHRoPSIyMDAiIGhlaWdodD0iMjAwIj48cGF0aCBkPSJNNjQuMzgzMjM0IDUxMkM2NC4zODMyMzQgMjY0Ljc4NzgyOSAyNjQuNzg3ODI5IDY0LjM4MzIzNCA1MTIgNjQuMzgzMjM0IDc1OS4yMTIxNzEgNjQuMzgzMjM0IDk1OS42MTY3NjYgMjY0Ljc4NzgyOSA5NTkuNjE2NzY2IDUxMiA5NTkuNjE2NzY2IDc1OS4yMTIxNzEgNzU5LjIxMjE3MSA5NTkuNjE2NzY2IDUxMiA5NTkuNjE2NzY2IDI2NC43ODc4MjkgOTU5LjYxNjc2NiA2NC4zODMyMzQgNzU5LjIxMjE3MSA2NC4zODMyMzQgNTEyWk00NzQuMjMyMzc5IDc3MS4yNDUxMjRDNDc2LjQwODcxOCA3OTcuMzU1NTEyIDQ5MC41NTEzNzIgODEwLjQxMjEyMyA1MTYuNjYzMTc2IDgxMC40MTIxMjMgNTQyLjc3MzU2NCA4MTAuNDEyMTIzIDU1Ni45MTc2MzUgNzk3LjM1NTUxMiA1NTkuMDkyNTU2IDc3MS4yNDUxMjQgNTU2LjkxNzYzNSA3NDUuMTMzMzE5IDU0Mi43NzM1NjQgNzMwLjk5MDY2NiA1MTYuNjYzMTc2IDcyOC44MTQzMjcgNDkwLjU1MTM3MiA3MzAuOTkwNjY2IDQ3Ni40MDg3MTggNzQ1LjEzMzMxOSA0NzQuMjMyMzc5IDc3MS4yNDUxMjRaTTQ4MC43NTk5NzcgNjExLjMxNDc0OEM0ODAuNzU5OTc3IDYzNy40MjY1NTQgNDkyLjcyNzcxIDY1MC40ODE3NDcgNTE2LjY2MzE3NiA2NTAuNDgxNzQ3IDU0MC41OTcyMjYgNjUwLjQ4MTc0NyA1NTIuNTY0OTYgNjM3LjQyNjU1NCA1NTIuNTY0OTYgNjExLjMxNDc0OEw1NTIuNTY0OTYgMjQ5LjAyNDYxOEM1NTIuNTY0OTYgMjIyLjkxNDIzMSA1NDAuNTk3MjI2IDIwOS44NTc2MTkgNTE2LjY2MzE3NiAyMDkuODU3NjE5IDQ5Mi43Mjc3MSAyMDkuODU3NjE5IDQ4MC43NTk5NzcgMjIyLjkxNDIzMSA0ODAuNzU5OTc3IDI0OS4wMjQ2MThMNDgwLjc1OTk3NyA2MTEuMzE0NzQ4WiIgcC1pZD0iNDQ5MiIgZmlsbD0iI2NkY2RjZCI+PC9wYXRoPjwvc3ZnPg==";

    // 滚动监听和防抖
    class ScrollListener {
      entries = [];
      taskId = 0;

      constructor() {
        document.addEventListener("scroll", this.scrollDebounce.bind(this), {
          capture: true,
          passive: true,
        });
      }

      isInViewport(controller) {
        let offsetTop = 0,
          offsetLeft = 0,
          el = controller.el,
          scrollTop = 0,
          scrollLeft = 0,
          html = document.documentElement;
        while (el && el !== html) {
          offsetTop = offsetTop + el.offsetTop;
          offsetLeft = offsetLeft + el.offsetLeft;
          el = el.offsetParent;
        }

        el = controller.el;
        while (el) {
          scrollTop += el.scrollTop;
          scrollLeft += el.scrollLeft;
          el = el.parentElement;
        }
        offsetTop -= scrollTop;
        offsetLeft -= scrollLeft;

        el = controller.el;
        return (
          offsetTop < html.scrollTop + innerHeight &&
          offsetTop + el.clientHeight > html.scrollTop &&
          offsetLeft < html.scrollLeft + innerWidth &&
          offsetLeft + el.clientWidth > html.scrollLeft
        );
      }

      scrollDebounce() {
        if (this.taskId) {
          clearTimeout(this.taskId);
        }
        this.taskId = setTimeout(this.handleScroll.bind(this), 200);
      }

      addController(controller) {
        this.entries.push(controller);
        this.scrollDebounce();
      }

      handleScroll() {
        this.entries = this.entries.filter((controller) => {
          return !controller.blob;
        });
        this.entries.forEach((controller) => {
          if (this.isInViewport(controller)) {
            controller.onEnterViewport();
          }
        });
      }
    }

    // 图片控制对象
    class ImageController {
      img = "";
      blob = null;
      el = null;
      wrap = null;
      constructor(
        url = "",
        parent = document.body,
        className = "wrap",
        el = document.createElement("img")
      ) {
        el.src = defaultUrl;
        el.classList.add("img");

        this.el = el;
        this.img = url;

        this.wrap = document.createElement("div");
        this.wrap.classList.add(className);
        this.wrap.append(el);
        parent.append(this.wrap);
      }

      showImage() {
        const target = this;
        this.fetchImage().then(() => {
          target.el.src = this.blob;
        });
      }

      showLoading() {
        this.el.src = defaultUrl;
      }

      showError() {
        this.el.src = errorUrl;
      }

      onEnterViewport() {
        this.showImage();
      }

      async fetchImage() {
        if (typeof fetch !== "function") {
          this.thowError();
          throw new Error("浏览器不支持fetch接口");
        }

        // 如果已经加载过，直接返回
        if (!this.blob) {
          const target = this;
          return fetch(this.img)
            .then((res) => {
              if (res.status > 199 && res.status < 300) return res.blob();
              else return Promise.reject();
            })
            .then((blob) => {
              if (/image/.test(blob.type)) return URL.createObjectURL(blob);
              else return Promise.reject();
            })
            .then((url) => {
              target.blob = url;
            })
            .catch(() => {
              target.showError();
              throw new Error("URL不正确或MIME类型不正确");
            });
        }
      }
    }

    const scrollListener = new ScrollListener(),
      main = document.getElementsByClassName("main")[0],
      imageControllers = images.map((url) => {
        const controller = new ImageController(url, main);
        scrollListener.addController(controller);
      }); </script>
</html> 
```

Author

回答者: [LMW-lmw(opens new window)](https://github.com/LMW-lmw)

方案二有那么一点点抖动，这里重新实现了一下

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style> * {
        margin: 0px;
        padding: 0px;
      }

      body {
        margin: 0px;
        padding: 0px;
      }

      img {
        display: block;
      } </style>
  </head>

  <body>
    <div class="demo">
      <img
        data-src="https://cdn.pixabay.com/photo/2021/08/24/15/38/sand-6570980_960_720.jpg"
        alt="1"
      />
      <img
        data-src="https://cdn.pixabay.com/photo/2013/02/21/19/06/drink-84533_960_720.jpg"
        alt="2"
      />
      <img
        data-src="https://cdn.pixabay.com/photo/2013/07/18/20/26/sea-164989_960_720.jpg"
        alt="3"
      />
      <img
        data-src="https://cdn.pixabay.com/photo/2015/04/23/22/00/tree-736885_960_720.jpg"
        alt="4"
      />
      <img
        data-src="https://cdn.pixabay.com/photo/2017/03/26/21/54/yoga-2176668_960_720.jpg"
        alt="5"
      />
    </div>
  </body>
  <script> const demo = document.querySelectorAll("img");
    function lazy() {
      for (let elem of demo) {
        if (
          elem.getBoundingClientRect().top <
          document.documentElement.clientHeight
        ) {
          if (elem.dataset.src && elem.src == "") {
            elem.src = elem.dataset.src;
          }
        }
      }
    }
    function throttle(t, fn) {
      let time;
      return function () {
        if (!time) {
          time = setTimeout(() => {
            time = null;
            fn();
          }, t);
        }
      };
    }
    lazy();
    window.addEventListener("scroll", throttle(500, lazy)); </script>
</html> 
```

# 浏览器中如何实现剪切板复制内容的功能

> 原文：[https://q.shanyue.tech/fe/html/20.html](https://q.shanyue.tech/fe/html/20.html)

更多描述

在一些博客系统，如掘金的博客中，可以复制代码，它是如何实现的

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 20(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/20)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

它一般可以使用第三方库 [clipboard-copy(opens new window)](https://github.com/feross/clipboard-copy/blob/master/index.js) 来实现，源码很简单，可以读一读

目前最为推荐的方式是使用 `Clipboard API` 进行实现

```
navigator.clipboard.writeText(text); 
```

而对于一些不支持 `Clipboard API` 的浏览器，使用以下 API 进行复制

1.  选中: `Selection API`
2.  复制: `document.execCommand` (已被废弃)

## 选中: Selection API/Range API

选中主要利用了 [Selection API(opens new window)](https://developer.mozilla.org/en-US/docs/Web/API/Selection) 与 Range API

选中的代码如下

```
const selection = window.getSelection();
const range = document.createRange();

// RangeAPI: 制造区域
range.selectNodeContents(element);

// Selection: 选中区域
selection.addRange(range);

selectedText = selection.toString(); 
```

取消选中的代码如下

```
window.getSelection().removeAllRanges(); 
```

它有现成的第三方库可以使用: [select.js(opens new window)](https://github.com/zenorocha/select)

## 复制: execCommand

复制就比较简单了，`execCommand`

```
document.execCommand("copy"); 
```

# localhost:3000 与 localhost:5000 的 cookie 信息是否共享

> 原文：[https://q.shanyue.tech/fe/html/127.html](https://q.shanyue.tech/fe/html/127.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 127(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/127)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

共享

Author

回答者: [zhangwen9229(opens new window)](https://github.com/zhangwen9229)

根据同源策略，cookie 是区分端口的，但是浏览器实现来说，“cookie 区分域，而不区分端口，也就是说，同一个 ip 下的多个端口下的 cookie 是共享的！

Author

回答者: [fariellany(opens new window)](https://github.com/fariellany)

貌似 不考虑 domian 设置 path 默认为/的话

https://xxxx.com 和http://xxxx.com 协议不同其他相同的 cookie 也是共享的

Author

回答者: [hao0906(opens new window)](https://github.com/hao0906)

默认 domain 为 localhost path 为/ 存储的 cookie 没有端口信息 共享

Author

回答者: [Telanx(opens new window)](https://github.com/Telanx)

@[fariellany(opens new window)](https://github.com/fariellany) `Set-Cookie: id=a3fWa; Expires=Thu, 21 Oct 2021 07:28:00 GMT; Secure; HttpOnly` 补充一点,不同协议 http 和 https，也可以共享 但是带有 Secure 属性的不能被 http 共享 带有 HttpOnly 属性的 cookie 无法被 document.cookie 访问

# 什么是 CSRF 攻击

> 原文：[https://q.shanyue.tech/fe/html/160.html](https://q.shanyue.tech/fe/html/160.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 160(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/160)

Author

回答者: [DoubleRayWang(opens new window)](https://github.com/DoubleRayWang)

跨站请求伪造（英语：Cross-site request forgery），也被称为 one-click attack 或者 session riding，通常缩写为 CSRF 或者 XSRF， 是一种挟制用户在当前已登录的 Web 应用程序上执行非本意的操作的攻击方法。跟跨网站脚本（XSS）相比，XSS 利用的是用户对指定网站的信任，CSRF 利用的是网站对用户网页浏览器的信任。

来源：[维基百科(opens new window)](https://zh.wikipedia.org/wiki/%E8%B7%A8%E7%AB%99%E8%AF%B7%E6%B1%82%E4%BC%AA%E9%80%A0)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

CSRF (Cross-site request forgery)，跨站请求伪造，又称为 `one-click attack`，顾名思义，通过恶意引导用户一次点击劫持 cookie 进行攻击。

1.  使用 JSON API。当进行 CSRF 攻击时，请求体通过 `<form>` 构建，请求头为 `application/www-form-urlencoded`。它难以发送 JSON 数据被服务器所理解。
2.  CSRF Token。生成一个随机的 token，切勿放在 cookie 中，每次请求手动携带该 token 进行校验。
3.  SameSite Cookie。设置为 Lax 或者 Strict，禁止发送第三方 Cookie。

> 参考以下链接：
> 
> 1.  [理解 CSRF(opens new window)](https://github.com/pillarjs/understanding-csrf/blob/master/README_zh.md)
> 2.  [Cross-Site Request Forgery Prevention Cheat Sheet(opens new window)](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html)

# 在浏览器中如何监听剪切板中内容

> 原文：[https://q.shanyue.tech/fe/html/315.html](https://q.shanyue.tech/fe/html/315.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 315(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/315)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

通过 `Clipboard API` 可以获取剪切板中内容，但需要获取到 `clipboard-read` 的权限，以下是关于读取剪贴板内容的代码：

```
// 是否能够有读取剪贴板的权限
// result.state == "granted" || result.state == "prompt"
const result = await navigator.permissions.query({ name: "clipboard-read" });

// 获取剪贴板内容
const text = await navigator.clipboard.readText(); 
```

> 注: 该方法在 `devtools` 中不生效

相关问题: [【Q019】如何实现选中复制的功能(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/20)

# 如何把 json 数据转化为 demo.json 并下载文件

> 原文：[https://q.shanyue.tech/fe/html/352.html](https://q.shanyue.tech/fe/html/352.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 352(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/352)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

json 视为字符串，可以利用 `DataURL` 进行下载

`Text -> DataURL`

除了使用 DataURL，还可以转化为 Object URL 进行下载

`Text -> Blob -> Object URL`

可以把以下代码直接粘贴到控制台下载文件

```
function download(url, name) {
  const a = document.createElement("a");
  a.download = name;
  a.rel = "noopener";
  a.href = url;
  // 触发模拟点击
  a.dispatchEvent(new MouseEvent("click"));
  // 或者 a.click()
}

const json = {
  a: 3,
  b: 4,
  c: 5,
};
const str = JSON.stringify(json, null, 2);

// 方案一：Text -> DataURL
const dataUrl = `data:,${str}`;
download(dataUrl, "demo.json");

// 方案二：Text -> Blob -> ObjectURL
const url = URL.createObjectURL(new Blob(str.split("")));
download(url, "demo1.json"); 
```

## 总结

1.  模拟下载，可以通过新建一个 `<a href="url" download><a>` 标签并设置 `url` 及 `download` 属性来下载
2.  可以通过把 `json` 转化为 `dataurl` 来构造 URL
3.  可以通过把 `json` 转换为 `Blob` 再转化为 `ObjectURL` 来构造 URL

Author

回答者: [fariellany(opens new window)](https://github.com/fariellany)

这里 为啥要 split 下呢 const url = URL.createObjectURL(new Blob(str.split(''))) 我看 mdn 上面只需要 const url = URL.createObjectURL(new Blob([str], { type: 'application/json' })) 是有其他的含义吗 虽然都能实现下载的功能？

Author

回答者: [amandaQYQ(opens new window)](https://github.com/amandaQYQ)

> 这里 为啥要 split 下呢 const url = URL.createObjectURL(new Blob(str.split(''))) 我看 mdn 上面只需要 const url = URL.createObjectURL(new Blob([str], { type: 'application/json' })) 是有其他的含义吗 虽然都能实现下载的功能？

因为需要 Blob 的 API 是 var aBlob = new Blob( **array**, options );

Author

回答者: [xinconan(opens new window)](https://github.com/xinconan)

方法一有 2 个缺点：
1、无法保留缩进
2、字符串里面的空格会被删除

# 简单介绍 requestIdleCallback 及使用场景

> 原文：[https://q.shanyue.tech/fe/html/379.html](https://q.shanyue.tech/fe/html/379.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 379(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/379)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

`requestIdleCallback` 维护一个队列，将在浏览器空闲时间内执行。它属于 [Background Tasks API(opens new window)](https://developer.mozilla.org/zh-CN/docs/Web/API/Background_Tasks_API)，你可以使用 `setTimeout` 来模拟实现

```
window.requestIdleCallback =
  window.requestIdleCallback ||
  function (handler) {
    let startTime = Date.now();

    return setTimeout(function () {
      handler({
        didTimeout: false,
        timeRemaining: function () {
          return Math.max(0, 50.0 - (Date.now() - startTime));
        },
      });
    }, 1);
  }; 
```

以上实现过于复杂以及细节化，也可以像 [swr(opens new window)](https://github.com/vercel/swr) 一样做一个简单的模拟实现，以下代码见 [https://github.com/vercel/swr/blob/8670be8072b0c223bc1c040deccd2e69e8978aad/src/use-swr.ts#L33(opens new window)](https://github.com/vercel/swr/blob/8670be8072b0c223bc1c040deccd2e69e8978aad/src/use-swr.ts#L33)

```
const rIC = window["requestIdleCallback"] || ((f) => setTimeout(f, 1)); 
```

在 `rIC` 中执行任务时需要注意以下几点：

1.  执行重计算而非紧急任务
2.  空闲回调执行时间应该小于 50ms，最好更少
3.  空闲回调中不要操作 DOM，因为它本来就是利用的重排重绘后的间隙空闲时间，重新操作 DOM 又会造成重排重绘

React 的时间分片便是基于类似 `rIC` 而实现，然而因为 `rIC` 的兼容性及 50ms 流畅问题，React 自制了一个实现: [scheduler(opens new window)](https://github.com/facebook/react/tree/master/packages/scheduler)

[use-swr(opens new window)](https://github.com/vercel/swr) 中进行资源的 `revalidate` 时，也是通过 `rIC` 来提高性能

## 参考

**强烈推荐 MDN 与 w3c 上的两篇介绍**

*   [Background Tasks API - MDN(opens new window)](https://developer.mozilla.org/zh-CN/docs/Web/API/Background_Tasks_API)
*   [requestIdleCallback - W3C(opens new window)](https://w3c.github.io/requestidlecallback/#idle-periods)

# 如何计算白屏时间和首屏时间

> 原文：[https://q.shanyue.tech/fe/html/469.html](https://q.shanyue.tech/fe/html/469.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 469(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/469)

Author

回答者: [hhhpw(opens new window)](https://github.com/hhhpw)

白屏时间: window.performance.timing.domLoading - window.performance.timing.navigationStart

首屏时间: window.performance.timing.domInteractive - window.performace.timing.navigationStart

Author

回答者: [wuyuehui(opens new window)](https://github.com/wuyuehui)

首屏时间: window.performance.timing.domInteractive - window.performace.timing.navigationStart

window.performace.timing.navigationStart

performace -> performance 少了个 n

# 什么是重排重绘，如何减少重拍重绘

> 原文：[https://q.shanyue.tech/fe/html/472.html](https://q.shanyue.tech/fe/html/472.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 472(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/472)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

重排和重绘是关键渲染路径中的两步，可以参考另一个问题: [什么是关键渲染路径(opens new window)](https://q.shanyue.tech/fe/%E5%89%8D%E7%AB%AF%E5%B7%A5%E7%A8%8B%E5%8C%96/391.html)

*   重排(Reflow)：元素的位置发生变动时发生重排，也叫回流。此时在关键渲染路径中的 Layout 阶段，计算每一个元素在设备视口内的确切位置和大小。当一个元素位置发生变化时，其父元素及其后边的元素位置都可能发生变化，代价极高 ![](img/fcfbaab610489b45da813990cd63baf2.png)

*   重绘(Repaint): 元素的样式发生变动，但是位置没有改变。此时在关键渲染路径中的 Paint 阶段，将渲染树中的每个节点转换成屏幕上的实际像素，这一步通常称为绘制或栅格化 ![](img/47577d983717aa410e736436fd5c1be8.png)

另外，重排必定会造成重绘。以下是避免过多重拍重绘的方法

1.  使用 `DocumentFragment` 进行 DOM 操作，不过现在原生操作很少也基本上用不到
2.  CSS 样式尽量批量修改
3.  避免使用 table 布局
4.  为元素提前设置好高宽，不因多次渲染改变位置

# HTML 中的 input 标签有哪些 type

> 原文：[https://q.shanyue.tech/fe/html/477.html](https://q.shanyue.tech/fe/html/477.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 477(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/477)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

## button

没有默认行为的按钮，上面显示 value 属性的值，默认为空。

```
<input type="button" name="button" /> 
```

## checkbox

复选框，可设为选中或未选中。

```
<input type="checkbox" name="checkbox" /> 
```

## color

用于指定颜色的控件；在支持的浏览器中，激活时会打开取色器。

```
<input type="color" name="color" /> 
```

## date

输入日期的控件（年、月、日，不包括时间）。在支持的浏览器激活时打开日期选择器或年月日的数字滚轮。

```
<input type="date" name="date" /> 
```

## datetime-local

输入日期和时间的控件，不包括时区。在支持的浏览器激活时打开日期选择器或年月日的数字滚轮。

```
<input type="datetime-local" name="datetime-local" /> 
```

## email

编辑邮箱地址的区域。类似  text  输入，但在支持的浏览器和带有动态键盘的设备上会有确认参数和相应的键盘。

```
<input type="email" name="email" /> 
```

## file

让用户选择文件的控件。使用 accept 属性规定控件能选择的文件类型。

```
<input type="file" accept="image/*, text/*" name="file" /> 
```

## hidden

不显示的控件，其值仍会提交到服务器。举个例子，右边就是一个隐形的控件。

## image

带图像的  submit 按钮。显示的图像由 src  属性规定。如果 src 缺失，alt 属性就会显示。

```
<input type="image" name="image" src="" alt="image input" /> 
```

## month

输入年和月的控件，没有时区。

```
<input type="month" name="month" /> 
```

## number

用于输入数字的控件。如果支持的话，会显示滚动按钮并提供缺省验证（即只能输入数字）。拥有动态键盘的设备上会显示数字键盘。

```
<input type="number" name="number" /> 
```

## password

单行的文本区域，其值会被遮盖。如果站点不安全，会警告用户。

```
<input type="password" name="password" /> 
```

## radio

单选按钮，允许在多个拥有相同 name 值的选项中选中其中一个。

```
<input type="radio" name="radio" /> 
```

## range

此控件用于输入不需要精确的数字。控件是一个范围组件，默认值为正中间的值。同时使用 htmlattrdefmin    和 htmlattrdefmax 来规定值的范围。

```
<input type="range" name="range" min="0" max="25" /> 
```

## reset

此按钮将表单的所有内容重置为默认值。不推荐。

```
<input type="reset" name="reset" /> 
```

## search

用于搜索字符串的单行文字区域。输入文本中的换行会被自动去除。在支持的浏览器中可能有一个删除按钮，用于清除整个区域。拥有动态键盘的设备上的回车图标会变成搜索图标。

```
<input type="search" name="search" /> 
```

## submit

用于提交表单的按钮。

```
<input type="submit" name="submit" /> 
```

## tel

用于输入电话号码的控件。拥有动态键盘的设备上会显示电话数字键盘。

```
<input type="tel" name="tel" /> 
```

## text

默认值。单行的文本区域，输入中的换行会被自动去除。

```
<input type="text" name="text" /> 
```

## time

用于输入时间的控件，不包括时区。

```
<input type="time" name="time" /> 
```

## url

用于输入 URL 的控件。类似 text  输入，但有验证参数，在支持动态键盘的设备上有相应的键盘。

```
<input type="url" name="url" /> 
```

## week

用于输入以年和周数组成的日期，不带时区。

```
<input type="week" name="week" /> 
```

# 什么是 Data URL

> 原文：[https://q.shanyue.tech/fe/html/478.html](https://q.shanyue.tech/fe/html/478.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 478(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/478)

Author

回答者: [buzuosheng(opens new window)](https://github.com/buzuosheng)

Data URL 是将图片转换为 base64 直接嵌入到了网页中，使用`<img src="data:[MIME type];base64"/>`这种方式引用图片，不需要再发请求获取图片。 使用 Data URL 也有一些缺点：

*   base64 编码后的图片会比原来的体积大三分之一左右。
*   Data URL 形式的图片不会缓存下来，每次访问页面都要被下载一次。可以将 Data URL 写入到 CSS 文件中随着 CSS 被缓存下来。

Author

回答者: [haotie1990(opens new window)](https://github.com/haotie1990)

[Data URLs(opens new window)](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics_of_HTTP/Data_URIs)

Author

回答者: [hsq777(opens new window)](https://github.com/hsq777)

Data URL 是前缀为`data:`协议的 URL； 它允许内容创建者向文档中嵌入小文件，比如图片等。 Data URL 由四部分组成：

*   前缀`data:`
*   指示数据类型的 MIME 类型。例如`image/jpeg`表示 JPEG 图像文件；如果此部分被省略，则默认值为`text/plain;charset=US-SACII`
*   如果为非文本数据，则可选 base64 做标记
*   数据

```
data:[mediatype][;base63], data 
```

# 什么是 HTML 的实体编码 (HTML Entity Encode)

> 原文：[https://q.shanyue.tech/fe/html/480.html](https://q.shanyue.tech/fe/html/480.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 480(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/480)

Author

回答者: [kglive(opens new window)](https://github.com/kglive)

*   不可分的空格:＆nbsp;
*   <(小于符号):＆lt;
*   (大于符号):＆gt;
*   ＆(与符号):＆amp;
*   ″(双引号):＆quot;
*   '(单引号):'＆apos;
*   ……

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

HTML 实体是一段以连字号（&）开头、以分号（;）结尾的字符串。用以显示不可见字符及保留字符 (如 HTML 标签)

在前端，一般为了避免 XSS 攻击，会将 `<>` 编码为 `&lt;` 与 `&gt;`，这些就是 HTML 实体编码。

在 [whatwg(opens new window)](https://html.spec.whatwg.org/multipage/named-characters.html#named-character-references) 中可查看实体编码数据。

在 HTML 转义时，仅仅只需要对六个字符进行编码: `&`, `<`, `>`, `"`, `'`, ```。可使用 [he(opens new window)](https://npm.devtool.tech/he) 这个库进行编码及转义

```
// 实体编码
> he.encode('<img src=""></img>')
< "&#x3C;img src=&#x22;&#x22;&#x3E;&#x3C;/img&#x3E;"

// 转义
> he.escape('<img src=""></img>')
< "&lt;img src=&quot;&quot;&gt;&lt;/img&gt;" 
```

# textarea 如何禁止拉伸

> 原文：[https://q.shanyue.tech/fe/html/484.html](https://q.shanyue.tech/fe/html/484.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 484(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/484)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

使用 CSS 样式可以避免拉伸

```
textarea {
  resize: none;
} 
```

# 在 Canvas 中如何处理跨域的图片

> 原文：[https://q.shanyue.tech/fe/html/485.html](https://q.shanyue.tech/fe/html/485.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 485(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/485)

Author

回答者: [hhhpw(opens new window)](https://github.com/hhhpw)

img.setAttribute("crossOrigin", "anonymous");

# 如何取消请求的发送

> 原文：[https://q.shanyue.tech/fe/html/502.html](https://q.shanyue.tech/fe/html/502.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 502(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/502)

Author

回答者: [evle(opens new window)](https://github.com/evle)

根据发送网络请求的 API 不同，取消方法不同

*   xhr
*   fetch
*   axios

如果使用`XMLHttpRequest`发送请求可以使用`XMLHttpRequest.abort()`

如果使用`fetch`发送请求可以使用`AbortController`

```
const controller = new AbortController();
const signal = controller.signal;
fetch('https://somewhere', { signal })
controller.abort() 
```

如果使用`axios`，取消原理同 fetch

```
var CancelToken = axios.CancelToken;
var source = CancelToken.source();

axios.get('/https://somewhere', {
  cancelToken: source.token
}

source.cancel() 
```

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

## 001 XHR 使用 `xhr.abort()`

```
const xhr = new XMLHttpRequest(),
  method = "GET",
  url = "https://developer.mozilla.org/";
xhr.open(method, url, true);

xhr.send();

// 取消发送请求
xhr.abort(); 
```

## 002 fetch 使用 `AbortController`

> `AbortController` 文档见 [AbortSignal - MDN(opens new window)](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal)，它不仅可以取消 Fetch 请求发送，同样也可以取消事件的监听(通过 `addEventListener` 的第三个参数 `signal` 控制)

1.  发送请求时使用一个 `signal` 选项控制 fetch 请求
2.  `control.abort()` 用以取消请求发送
3.  取消请求发送之后会得到异常 `AbortError`

```
const controller = new AbortController()
const signal = controller.signal

const downloadBtn = document.querySelector('.download');
const abortBtn = document.querySelector('.abort');

downloadBtn.addEventListener('click', fetchVideo);

// 点击取消按钮时，取消请求的发送
abortBtn.addEventListener('click', function() {
  controller.abort();
  console.log('Download aborted');
});

function fetchVideo() {
  ...
  fetch(url, {signal}).then(function(response) {
    ...
  }).catch(function(e) {
   // 请求被取消之后将会得到一个 AbortError
    reports.textContent = 'Download error: ' + e.message;
  })
} 
```

### 003 Axios: `xhr` 与 `http/https`

`Axios` 中通过 `cancelToken` 取消请求发送

```
const CancelToken = axios.CancelToken;
const source = CancelToken.source();

axios
  .get("/user/12345", {
    cancelToken: source.token,
  })
  .catch(function (thrown) {
    if (axios.isCancel(thrown)) {
      console.log("Request canceled", thrown.message);
    } else {
      // handle error
    }
  });

axios.post(
  "/user/12345",
  {
    name: "new name",
  },
  {
    cancelToken: source.token,
  }
);

// cancel the request (the message parameter is optional)
source.cancel("Operation canceled by the user."); 
```

而其中的原理可分为两部分

*   浏览器端: 基于 XHR，`xhr.abort()`，见源码[axios/lib/adapters/xhr.js(opens new window)](https://github.com/axios/axios/blob/v0.21.1/lib/adapters/xhr.js#L165)
*   Node 端: 基于 http/https/follow-redirects，使用 `request.abort()`，见源码[axios/lib/adapters/http.js(opens new window)](https://github.com/axios/axios/blob/v0.21.1/lib/adapters/http.js#L289)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

@evle 可以使用 js 代码高亮一下，其实 CancelToken 的底部原理是基于 xhr 的

# HTML 标签有哪些行内元素

> 原文：[https://q.shanyue.tech/fe/html/529.html](https://q.shanyue.tech/fe/html/529.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 529(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/529)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

常见的标签有以下几种，可参考 [inline element(opens new window)](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements)

*   a
*   img
*   picture
*   span
*   input
*   textarea
*   select
*   label

# HTML 中有哪些语义化标签

> 原文：[https://q.shanyue.tech/fe/html/543.html](https://q.shanyue.tech/fe/html/543.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 543(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/543)

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

> 见文档 [HTML Elements - MDN(opens new window)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

*   header
*   footer
*   main
*   aside
*   article
*   section
*   address
*   summary/details
*   menu
*   h1/h2/h3/h4/h5/h6
*   img
*   p
*   strong/italic

# 什么是 URL 编码 (URL Encode)

> 原文：[https://q.shanyue.tech/fe/html/598.html](https://q.shanyue.tech/fe/html/598.html)

Issue

欢迎在 Gtihub Issue 中回答此问题: [Issue 598(opens new window)](https://github.com/shfshanyue/Daily-Question/issues/598)

Author

回答者: [haotie1990(opens new window)](https://github.com/haotie1990)

encodeURI 用来编码**URI**，其不会编码保留字符：;,/?😡&=+$

encodeURIComponent 用来编码 URI**参数**，除了字符：A-Z a-z 0-9 - _ . ! ~ * ' ( )，都将会转义

Author

回答者: [shfshanyue(opens new window)](https://github.com/shfshanyue)

TODO
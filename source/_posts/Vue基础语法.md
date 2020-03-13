---
title: Vue基础语法
date: 2020-03-06 12:59:55
categories:
- 前端
tags:
- Vue
keywords:
comments:
---


<center> 
<img src="https://i.loli.net/2020/03/06/DBnjol4tUpivVON.jpg" style="zoom:80%;" />


Vue 的简介和一些基本语法
</center>
<!-- more -->

# Vue 简介


## Vue 简单认识

- [Vue 官网](https://cn.vuejs.org/v2/guide/)

- Vue（读音 /vjuː/，类似于 view）是一个渐进式的框架，什么是渐进式？ 
  -   渐进式意味着你可以将 Vue 作为应用的一部分嵌入其中，带来更丰富的交互体验
  -   或者如果你希望将更多的业务逻辑使用Vue实现，那么Vue的核心库以及其生态系统（比如：Core+Vue-router+Vuex）也可以满足你各种各样的需求

- Vue 有很多特点和Web开发中常见的高级功能
  -   解耦视图和数据
  -   可复用的组件
  -   前端路由技术
  -   状态管理
  -   虚拟DOM

## Vue 安装

安装Vue的方式有很多：

### 方式一：直接CDN引入

你可以选择引入开发环境版本还是生产环境版本

```javascript
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

### 方式二：下载和引入

- 开发环境：https://vuejs.org/js/vue.js
- 生产环境：https://vuejs.org/js/vue.min.js

### 方式三：NPM 安装

```shell
npm install vue<a name="YFJI3"></a>
```

## Vue 初体验

### Hello World

```html
<div class="div">{{message}}</div>
<script src="./js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.div',
    data: {
      message: 'Hello Vue!'
    }
  });
</script>
```

### 展示列表

```html
<div class="div">
  <ul>
  <li v-for="item in NBAStars">{{item}}</li>
</ul>
</div>
<script src="./js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.div',
    data: {
      NBAStars: ['林书豪', '杜兰特', '詹姆斯', '欧文', '库里']
    }
  });
</script>
```


### 计数器

```html
<div class="div">
  <h2>当前计数：{{counter}}</h2>
  <button @click='increment'>+</button>
  <button @click='decrement'>-</button>
</div>
<script src="./js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.div',
    data: {
      counter: 0
    },
    methods: {
      increment: function() {
        this.counter++
      },
      decrement: function() {
        this.counter--
      }
    }
  })
</script>
```

## Vue 中的 MVVM

### 什么是MVVM

[MVVM框架理解及其原理实现](https://segmentfault.com/a/1190000015895017)

![](https://i.loli.net/2020/03/06/KeslVLEkiv3zqNJ.png)

<img src="https://i.loli.net/2020/03/06/7MmG3LKhQYBOZn2.png" alt="MVVM实例" style="zoom: 50%;" />

- View 层：视图层，在前端开发中，通常就是 DOM 层，主要的作用是给用户展示各种信息
- Model 层：数据层，数据可能是我们固定的死数据，更多的是来自我们服务器，从网络上请求下来的数据
- VueModel 层：视图模型层，视图模型层是 View 和 Model 沟通的桥梁，一方面实现了 Data Binding（数据绑定），将 Model 的改变实时的反应到 View 中，另一方面它实现了 DOM Listener（DOM监听），当 DOM 发生一些事件（点击、滚动、touch 等）时，可以监听到，并在需要的情况下改变对应的 Data

### MVC 和 MVVM 的区别

[MVC 和 MVVM 的区别](https://www.jianshu.com/p/b0aab1ffad93)

- MVC

![](https://i.loli.net/2020/03/06/Ew2Xbm8LdVxvl57.png)

- MVVM

![](https://i.loli.net/2020/03/06/63j9OPAkTyeCbGY.png)


### Vue 的生命周期

<img src="https://i.loli.net/2020/03/06/U1wRBiGFyEZTLe4.png" alt="Vue生命周期" style="zoom: 33%;" />


# Vue 基础语法


## 插值语法

插值：将值插入到模板的内容中

### Mustache

```html
<div class="div">
  <!-- 插到标签中 -->
  <h2>Hello {{name}}</h2>
  <!-- 使用了两个Mustach -->
  <h2>{{firstName}} {{lastName}}</h2>
  <!-- 也可以是表达式 -->
  <h2>{{counter*2}}</h2>
</div>
<script src="./js/vue.js"></script>

<script>
  const app = new Vue({
    el: '.div',
    data: {
      name: 'VueJS',
      firstName: 'Yuanyang',
      lastName: 'Liao',
      counter: 100
    }
  });
</script>
```


### v-once

在某些情况下，我们可能不希望界面中 Mustach 中的值随意的跟随改变，就可以使用一个 Vue 的指令：`v-once`

- 该指令后面不需要跟任何表达式
- 该指令表示元素和组件只渲染一次，不会随着数据的改变而改变

```html
<div class="app">
  <h2>{{message}}</h2>
  <h2 v-once>{{message}}</h2> <!-- 只会渲染一次 -->
</div>
<script src="./js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      message: 'Liao'
    }
  })
</script>
```



### v-html

某些情况下，我们从服务器请求到的数据本身就是一个 HTML 代码，如果我们直接通过 `{ { } }` 来输出，会将 HTML 代码也一起输出，但如果希望按照 HTML 格式进行解析，并且显示对应的内容，可以使用 `v-html` 指令

`v-html` 指令后面往往会跟上一个 string 类型，会将 string 的 html 解析出来并且进行渲染!



### v-text

- v-text 作用和 Mustache 比较相似，都是用于将数据显示在界面中
- v-text 通常情况下，接受一个 string 类型
- v-text 会覆盖原来的内容 不够灵活



### v-pre

`v-pre` 用于跳过这个元素和它子元素的编译过程，显示原本的 Mustache 语法，将代码原封不动的解析出来



### v-cloak

将未解析出来的代码块进行隐藏，但基本不会用到




## 绑定属性 v-bind

### v-bind 基本使用

Mustache 指令主要作用是将值插入到我们模板的内容当中，但是，除了内容需要动态来决定外，某些属性我们也希望动态来绑定，比如：

- 动态绑定 a 元素的 href 属性
- 动态绑定 img 元素的 src 属性

这时，可以使用 `v-bind` 指令来动态绑定属性，`v-bind` 用于绑定一个或多个属性值，或者向另一个组件传递 props值



### v-bind 语法糖

v-bind 有一个对应的语法糖（简写方式），在开发中，通常会使用语法糖的形式，因为这样更加简洁简写方式如下：

```html
<div class="app">
  <img :src="imgSrc" alt=""><br>
  <a :href="aHref">Vue.js官网</a>
</div>
```

即省略 v-bind，直接写 `:`



### v-bind 动态绑定 class

很多时候，我们希望动态的来切换 class，比如：

- 当数据为某个状态时，字体显示红色
- 当数据另一个状态时，字体显示黑色

绑定 class 有两种方式：

- 对象语法
- 数组语法

1. 对象语法

对象语法的含义是：class 后面跟的是一个对象对象语法有下面这些用法：

```html
用法一：直接通过{}绑定一个类
<h2 :class="{'active': isActive}">Hello World</h2>

用法二：也可以通过判断，传入多个值
<h2 :class="{'active': isActive, 'line': isLine}">Hello World</h2>

用法三：和普通的类同时存在，并不冲突
注：如果isActive和isLine都为true，那么会有title/active/line三个类
<h2 class="title" :class="{'active': isActive, 'line': isLine}">Hello World</h2>

用法四：如果过于复杂，可以放在一个methods或者computed中
注：classes是一个计算属性
<h2 class="title" :class="classes">Hello World</h2>
```

有时候，如果 `v-bind:class="{active:isActive,line:isLine}"` 中 class 的项太多，可以定义一个方法，将其放到 methods 中：

```html
<div class="app">
  <!-- <h2 class="title" v-bind:class="{active:isActive,line:isLine}">{{message}}</h2> -->
  <h2 class="title" v-bind:class="getCLasses()">{{message}}</h2>
  <button v-on:click="btnClick">改变颜色</button>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      message: 'YuanyangLiao',
      isActive: true,
      isLine: true
    },
    methods: {
      btnClick: function() {
        this.isActive = !this.isActive
      },
      getCLasses: function() {
        return {
          active: this.isActive,
          line: this.isLine
        }
      }
    }
  })
</script>
```

2. 数组语法

数组语法的含义是：class 后面跟的是一个数组数组语法有下面这些用法：

```html
用法一：直接通过{}绑定一个类
<h2 :class="['active']">Hello World</h2>

用法二：也可以传入多个值
<h2 :class=“[‘active’, 'line']">Hello World</h2>

用法三：和普通的类同时存在，并不冲突
注：会有title/active/line三个类
<h2 class="title" :class=“[‘active’, 'line']">Hello World</h2>

用法四：如果过于复杂，可以放在一个methods或者computed中
注：classes是一个计算属性
<h2 class="title" :class="classes">Hello World</h2>
```

```html
<div class="app">
  <h2 class="title" v-bind:class="[active,line]">{{message}}</h2>
  <h2 class="title" v-bind:class="getCLasses()">{{message}}</h2>
  <button v-on:click="btnClick">改变颜色</button>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      message: 'YuanyangLiao',
      active: 'active',
      line: true
    },
    methods: {
      btnClick: function() {
        this.isActive = !this.isActive
      },
      getCLasses: function() {
        return [this.active, this.line]
      }
    }
  })
</script>
```


### 案例：点击当前项变色

![图片.png](https://i.loli.net/2020/03/06/xp84R9IBlONhH1f.png)

### v-bind 动态绑定 style

我们可以利用 `v-bind:style` 来绑定一些 CSS 内联样式

在写CSS属性名的时候，比如 `font-size`，可以使用驼峰式 (camelCase) `fontSize`，或短横线分隔 (kebab-case，记得用单引号括起来) `'font-size'`

绑定class有两种方式：

- 对象语法
- 数组语法

1. 对象语法

style 后面跟的是一个对象类型

- 对象的 key 是 CSS 属性名称
- 对象的 value 是具体赋的值，值可以来自于 data 中的属性

```html
<div class="app">
  <!-- 50px 必须加上单引号 -->
  <h2 :style="{fontSize:'50px'}">{{message}}</h2>
  <!-- finalSize、finalColor当成一个变量使用 -->
  <h2 :style="{fontSize:finalSize + 'px',color:finalColor}">{{message}}</h2>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      message: 'YuanyangLiao',
      finalSize: 100,
      finalColor: 'skyblue',
    },
  })
</script>
```

2. 数组语法

style 后面跟的是一个数组类型

```html
<div class="app">
  <h2 :style="[baseStyles,baseStyles2]">{{message}}</h2>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      message: 'YuanyangLiao',
      baseStyles: {
        color: 'red'
      },
      baseStyles2: {
        fontSize: '50px'
      },
    },
  })
</script>
```

## 计算属性 computed

在模板中可以直接通过插值语法显示一些 data 中的数据，但是在某些情况下，可能需要对数据进行一些转化后再显示，或者需要将多个数据结合起来进行显示，这时可以使用计算属性 computed

### 计算属性 computed 的基本使用

比如：现在有 firstName 和 lastName 两个变量，需要显示完整的名称，可能直接使用空格将其隔开：

```html
<h2>{{firstName}} {{lastName}}</h2>
```

或者使用加号拼接：

```html
<h2>{{firstName + '' +lastName}}</h2>
```

但是如果多个地方都需要显示完整的名称，我们就需要写多个 `{{firstName}} {{lastName}}` 或 `{{firstName + '' +lastName}}` ，使代码看上去很不优雅

这时，可能想到，将`{{firstName + '' +lastName}}` 封装为一个函数，通过函数的方式调用，但其实最佳方案是使用计算属性：

```html
<div class="app">
  <!-- 方式1 -->
  <h2>{{firstName}} {{lastName}}</h2>
  <!-- 方式2 -->
  <h2>{{firstName + ' ' + lastName}}</h2>
  <!-- 方式3 -->
  <h2>{{getFullName()}}</h2>
  <!-- 方式4 -->
  <h2>{{fullName}}</h2>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      firstName: 'Yuanyang',
      lastName: 'Liao',
    },
    computed: {
      fullName() {
        return this.firstName + ' ' + this.lastName
      }
    },
    methods: {
      getFullName: function() {
        return this.firstName + ' ' + this.lastName
      }
    }
  })
</script>
```

计算属性中也可以进行一些更加复杂的操作，比如下面计算图书价格的例子：

```html
<div class="app">
  <h2>图书总价为：{{totalPrice}}</h2>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      books: [{
        id: 1001,
        name: '计算机操作原理',
        price: 108
      }, {
        id: 1002,
        name: 'JavaScript高级程序设计',
        price: 99
      }, {
        id: 1003,
        name: '计算机网络',
        price: 28
      }, {
        id: 1004,
        name: '数据结构',
        price: 46
      }, {
        id: 1005,
        name: 'C语言',
        price: 48
      }, ]
    },
    computed: {
      totalPrice: function() {
        let result = 0
        for (let i in this.books) {
          result += this.books[i].price
        }
        return result
      }
    },
  })
</script>
```

### 计算属性的 setter 和 getter

每个计算属性都包含一个 getter 和一个 setter，getter 用来读取值，setter 用来设置值（但 setter 不常用）

![图片.png](https://i.loli.net/2020/03/06/GCUjroHit2DJuYm.png)


### couputed 与 methods 的区别

我们可能会考虑这样的一个问题：   

- methods 和 computed 看起来都可以实现我们的功能，那么为什么还要多一个计算属性这个东西呢？
- 原因：计算属性会进行缓存，如果多次使用时，计算属性只会调用一次

**computed 区别于 methods 的核心**

在官方文档中，强调了computed 区别于 methods 最重要的两点

1. computed 是属性调用，而 methods 是函数调用
1. computed 带有缓存功能，而 methods 没有

- computed 定义的方法，我们是以属性访问的形式调用的，`{ {computedTest} }`，但是 methods 定义的方法，我们必须要加上`()`来调用，如"`{ { methodTest() } }`"
- 我们可以将同一函数定义为一个方法而不是一个计算属性，两种方式的最终结果确实是完全相同的然而，不同的是计算属性是基于它们的响应式依赖进行缓存的，只在相关响应式依赖发生改变时它们才会重新求值，这就意味着只要 text 还没有发生改变，多次访问 getText 计算属性会立即返回之前的计算结果，而不必再次执行函数，而方法只要页面中的属性发生改变就会重新执行
- 对于任何复杂逻辑，都应当使用计算属性
- computed 依赖于 data 中的数据，只有在它的相关依赖数据发生改变时才会重新求值


## 事件监听 v-on


### v-on 基本使用

在前端开发中，我们需要经常和用户进行交互，这个时候，就必须监听用户发生的事件，比如点击、拖拽、键盘事件等，在 Vue 中监听事件使用 v-on 指令

```html
<div class="app">
  <h2>{{counter}}</h2>
  <!-- 常规写法 -->
  <button v-on:click="increment">+</button>
  <!-- 语法糖形式 -->
  <button @click="decrement">-</button>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      counter: 0
    },
    methods: {
      increment() {
        this.counter++
      },
      decrement() {
        this.counter--
      }
    }
  })
</script>
```

当通过 methods 中定义方法，以 `@click` 调用时，需要注意参数问题：

- 如果该方法不需要额外参数，那么方法后的 () 可以不添加，但如果方法本身中有一个参数，那么会默认将原生事件 event 参数传递进去
- 如果需要同时传入某个参数，同时需要 event 时，可以通过 `$event` 传入事件

```html
<div class="app">
  <!-- 1.事件调用的方法没有参数：可以省略() -->
  <!-- <button @click="btnClick()">按钮1</button>
<button @click="btnClick">按钮2</button> -->

  <!-- 2.事件调用的方法有参数 -->
  <button @click="btnClick()">按钮1</button>
  <!-- undefined -->
  <button @click="btnClick(123)">按钮2</button>
  <!-- 123 -->
  <button @click="btnClick">按钮3</button>
  <!-- MouseEvent对象：vue会默认将浏览器产生的event对象作为参数传到方法中 -->

  <!-- 3.在事件定义时，即需要event对象，又需要其他参数 -->
  <button @click="btnClick(123,$event)">按钮</button>

</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      counter: 0
    },
    methods: {
      btnClick(event, num) {
        console.log(event, num);
      }
    }
  })
</script>
```

### v-on 修饰符

在某些情况下，我们拿到 event 的目的可能是进行一些事件处理，vue 提供了修饰符来帮助我们方便的处理一些事件：

- `.stop` ：调用 `event.stopPropagation()`
- `.prevent` ：调用 `event.preventDefault()`
- `.{keyCode | keyAlias}` ：只当事件是从特定键触发时才触发回调
- `.native` ：监听组件根元素的原生事件
- `.once` ：只触发一次回调

```html
<div class="app">
  <!-- 1 .stop:停止冒泡 -->
  <div @click="divClick">divdiv
    <button @click.stop="btnClick">按钮</button>
  </div>

  <!-- 2. .prevent:阻止默认行为 -->
  <form action="baidu" method="post">
    <input type="submit" value="提交" @click.prevent="submitClick">
  </form>

  <!-- 3. .enter:监听enter按键 -->
  <input type="text" @keyup.enter="enterClick">

  <!-- 4. .once:点击回调只会触发一次 -->
  <button @click.once="btnClick2">按钮2</button>

</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      counter: 0
    },
    methods: {
      btnClick() {
        console.log("btnClick...")
      },
      divClick() {
        console.log("divClick...")
      },
      submitClick() {
        console.log("submitClick...")
      },
      enterClick() {
        console.log("enterClick...")
      },
      btnClick2() {
        console.log("btnClick2...")
      }
    }
  })
</script>
```


## 条件和循环

### 条件判断

v-if、v-else-if、v-else 这三个指令与 JavaScript 的条件语句 if、else、else if 类似

vue 的条件指令可以根据表达式的值在 DOM 中渲染或销毁元素或组件

![图片.png](https://i.loli.net/2020/03/06/AnYpagPLfSZs2Nk.png)

**v-if **

v-if 后面的条件为 false 时，对应的元素以及其子元素不会渲染，也就是不会有对应的标签出现在 DOM 中

**v-show**

v-show 的用法和 v-if 非常相似，也用于决定一个元素是否渲染

**v-show 和 v-if 的区别**

- v-if 是真正的条件渲染，会确保在切换过程中，条件块内的事件和子组件被销毁和重建（组件被重建将会调用created）
- v-show 不论如何，都会被渲染在 DOM 中，当条件为真值时，将会修改条件的 css 样式
- v-if 有更高的切换开销，v-show 有更高的初始渲染开销
- v-if 是动态的向 DOM 树内添加或者删除 DOM 元素，v-show 是通过设置 DOM 元素的 display 样式属性控制显隐
- v-if 切换有一个局部编译/卸载的过程，切换过程中合适地销毁和重建内部的事件监听和子组件，v-show 只是简单的基于 css 切换
- v-if 是惰性的，如果初始条件为假，则什么也不做，只有在条件第一次变为真时才开始局部编译，v-show 是在任何条件下（首次条件是否为真）都被编译，然后被缓存，而且 DOM 元素保留
- v-if 有更高的切换消耗，v-show 有更高的初始渲染消耗
- v-if 适合运营条件不大可能改变，v-show适合频繁切换

**v-if 和 v-show 都可以决定一个元素是否渲染，那么开发中我们如何选择呢？**

v-if 当条件为 false 时，压根不会有对应的元素在 DOM 中v-show 当条件为 false 时，仅仅是将元素的 display 属性设置为 none 而已

结论：

- 当需要在显示与隐藏之间切换很频繁时，使用 v-show 
- 当只有一次切换时，通过使用 v-if

### 案例：切换用户账号

这里面的`key="username"`是在切换中清空输入框，不加的话只会切换，输入的内容不会清空

```html
<div class="app">
  <span v-if="isUser">
    <label for="username">用户账号</label>
    <input type="text" id="username" placeholder="用户账号" key="username">
  </span>
  <span v-else>
    <label for="email">用户邮箱</label>
    <input type="text" id="email" placeholder="用户邮箱" key="email">
  </span>
  <button @click="isUser = !isUser">切换类型</button>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      isUser: true
    }
  })
</script>
```


### 循环 v-for

当我们有一组数据需要进行渲染时，我们就可以使用 v-for 来完成

v-for 的语法类似于 JavaScript 中的 for 循环：`v-for="item in items"`

通过索引值修改数组中的元素不是响应式的，即数据修改了，但是界面不会更新


#### 遍历数组

```html
<div class="app">
  <ul>
    <!-- 1.遍历数组的值 -->
    <li v-for="item in NBAStars">{{item}}</li>
    <!-- 2.遍历数组的索引和值 -->
    <li v-for="(item,index) in NBAStars">{{index+1}}.{{item}}</li>
  </ul>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      NBAStars: ['林书豪', '杜兰特', '詹姆斯', '欧文', '库里']
    }
  })
</script>
```


#### 遍历对象

```html
<div class="app">
  <ul>
    <!-- 1.遍历对象的值 -->
    <li v-for="item in info">{{item}}</li><br>
    <!-- 2.遍历对象的键和值 -->
    <li v-for="(item,key) in info">{{key}} : {{item}}</li><br>
    <!-- 3.遍历对象的索引、键和值 -->
    <li v-for="(item,key,index) in info">{{index+1}}. {{key}} : {{item}}</li>
  </ul>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      info: {
        name: 'LiaoYuanyang',
        age: 18,
        gender: '男',
        height: 1.75
      }
    }
  })
</script>
```

![图片.png](https://i.loli.net/2020/03/06/3JOBrYow7jkxbHA.png)

#### 组件的 key 属性

官方推荐我们在使用 v-for 时，给对应的元素或组件添加上一个 `:key` 属性

为什么需要这个 key 属性呢，其实和 Vue 的虚拟 DOM 的 Diff 算法有关系，这里借用 React’s diff algorithm 中的一张图来简单说明一下：

![图片.png](https://i.loli.net/2020/03/06/5ajmSBLv9rT1g2l.png)

当某一层有很多相同的节点时，也就是列表节点时，我们希望插入一个新的节点

![图片.png](https://i.loli.net/2020/03/06/e7yd5S2Tjb1KXJa.png)

我们希望可以在 B 和 C 之间加一个 F，Diff 算法默认执行起来是这样的：即把 C 更新成 F，D 更新成 C，E 更新成 D，最后再插入 E：

![图片.png](https://i.loli.net/2020/03/06/XDf21J7MvYTnGlU.png)
是不是很没有效率？

所以我们需要使用 key 来给每个节点做一个唯一标识，Diff 算法就可以正确的识别此节点，找到正确的位置区插入新的节点，所以，key 的作用主要是为了高效的更新虚拟 DOM

![图片.png](https://i.loli.net/2020/03/06/P18Frwxb7lVnUDO.png)

```html
<li v-for="item in info" :key="item">{{item}}</li>
```

### 过滤器 filters



### 案例：图书购物车

![图片.png](https://i.loli.net/2020/03/06/ZSCwlJcNKVvkAhM.png)

index.html:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="./bootstrap-3.3.7-dist/css/bootstrap.min.css">
    <script src="jquery.min.js"></script>
    <script src="./bootstrap-3.3.7-dist/js/bootstrap.min.js"></script>
    <style>
        .app .table,
        .app .totalPrice {
            width: 800px;
            margin: 20px auto;
            padding: 20px;
        }
    </style>
</head>

<body>
    <div class="app">
        <div v-if="books.length">
            <table class="table table-hover">
                <thead>
                    <tr>
                        <th></th>
                        <th>书籍名称</th>
                        <th>出版日期</th>
                        <th>书本价格</th>
                        <th>购买数量</th>
                        <th>操作</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(item,index) in books">
                        <td>{{item.id}}</td>
                        <td>{{item.name}}</td>
                        <td>{{item.date}}</td>
                        <!-- <td>{{getFinallPrice(item.price)}}</td> -->
                        <td>{{item.price | showPrice}}</td>
                        <td>
                            <button type="button" class="btn btn-default" @click="decrement(index)" :disabled="item.count <=1">-</button>
                            <label>{{item.count}}</label>
                            <button type="button" class="btn btn-default" @click="increment(index)">+</button>
                        </td>
                        <td><button type="button" class="btn btn-warning" @click="removeClick(index)">移除</button></td>
                    </tr>
                </tbody>
            </table>
            <h2 class="totalPrice">总价格：{{totalPrice | showPrice}}</h2>
        </div>
        <h2 class="totalPrice" v-else>购物车为空！</h2>
    </div>
    <script src="../js/vue.js"></script>
    <script src="main.js"></script>
</body>
</html>
```

main.js:

```javascript
const app = new Vue({
    el: '.app',
    data: {
        books: [{
            id: 1001,
            name: '计算机操作原理',
            date: '2020-02-12',
            price: 108,
            count: 1
        }, {
            id: 1002,
            name: 'JavaScript高级程序设计',
            date: '2020-02-12',
            price: 99,
            count: 1
        }, {
            id: 1003,
            name: '计算机网络',
            date: '2020-02-12',
            price: 28,
            count: 1
        }, {
            id: 1004,
            name: '数据结构',
            date: '2020-02-12',
            price: 46,
            count: 1
        }, {
            id: 1005,
            name: 'C语言',
            date: '2020-02-12',
            price: 48,
            count: 1
        }]
    },
    methods: {
        // 普通方法处理价格
        getFinallPrice(price) {
            return '￥' + price.toFixed(2)
        },

        increment(index) {
            this.books[index].count++
        },
        decrement(index) {
            this.books[index].count--
        },
        removeClick(index) {
            this.books.splice(index, 1)
        },
    },
    computed: {
        totalPrice() {
            let totalPrice = 0
                // 方式一：for (let i in ...)
                /*  for (let i in this.books) {
                     totalPrice += this.books[i].price * this.books[i].count
                 } */
                // 方式二：for (let item of ...)
                /* for (let item of this.books) {
                    totalPrice += item.price * item.count
                } */
                // 方式三：高阶函数reduce：汇总数组内的元素
            this.books.reduce(function(preValue, book) {
                totalPrice += book.price * book.count
            }, 0)

            return totalPrice
        }
    },
    filters: {
        // 过滤器方法处理价格
        showPrice(price) {
            return '￥' + price.toFixed(2)
        }
    },
})
```


## 表单绑定 v-model


### v-model 基本使用

表单控件在实际开发中是非常常见的，特别是对于用户信息的提交，需要大量的表单，vue 中使用 v-model 指令来实现表单元素和数据的双向绑定

![图片.png](https://i.loli.net/2020/03/06/CDy6IJQ7ZVPj3dr.png)

案例解析：当我们在输入框输入内容时，因为 input 中的 v-model 绑定了 message，所以会实时将输入的内容传递给 message，message 发生改变，当 message 发生改变时，因为使用了 Mustache 语法，所以将 message 的值插入到 DOM 中，所以 DOM 会发生响应的改变，所以通过 v-model 实现了双向绑定


### v-model 原理

v-model 其实是一个语法糖，它的背后本质上是包含两个操作：

1. v-bind 绑定一个 value 属性
1. v-on 指令给当前元素绑定 input 事件

也就是说：

```html
<input type="text" v-model="message">
```

等同于：

```html
<input type="text" :value="message" @input="message = $event.target.value">
```


### v-model 结合 radio 使用

![图片.png](https://i.loli.net/2020/03/06/UotMTugHVZYkhXK.png)

```html
<div class="app">
  <label for="male">
    <input type="radio" v-model="gender" id="male" value="男">男
  </label>
  <label for="female">
    <input type="radio" v-model="gender" id="female" value="女">女
  </label>
  <h3>您选择的性别是：{{gender}}</h3>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      gender: '男'
    }
  });
</script>
```


### v-model 结合 checkbox 使用

- **checkbox 单选框**

![图片.png](https://i.loli.net/2020/03/06/9rjRgIlZ21OfJTP.png)

```html
<div class="app">
  <!-- checkbox单选框 -->
  <label for="licence">
    <input type="checkbox" v-model="isAgree" id="licence">同意协议
  </label>
  <h3>您的选择是：{{isAgree}}</h3>
  <button :disabled="!isAgree">下一步</button>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      isAgree: false
    }
  });
</script>
```

- **checkbox 多选框**

![图片.png](https://i.loli.net/2020/03/06/8zVeHDlvP7bFsYA.png)

```html
<div class="app">
  <h3>请选择您的爱好</h3>
  <label for="sing">
    <input type="checkbox" v-model="hobbies" id="sing" value="唱">唱
  </label>
  <label for="jump">
    <input type="checkbox" v-model="hobbies" id="jump" value="跳">跳
  </label>
  <label for="rap">
    <input type="checkbox" v-model="hobbies" id="rap" value="rap">rap
  </label>
  <label for="basketball">
    <input type="checkbox" v-model="hobbies" id="basketball" value="篮球">篮球
  </label>
  <h3>您的爱好是：{{hobbies}}</h3>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      hobbies: []
    }
  });
</script>
```



### v-model 结合 select 使用

![图片.png](https://i.loli.net/2020/03/06/OY5t6KmxJrwq9Fz.png)

```html
<div class="app">
  <!-- 选择一个值 -->
  <h3>请选择您喜欢的水果：</h3>
  <select name="" v-model="fruit">
    <option value="苹果">苹果</option>
    <option value="香蕉">香蕉</option>
    <option value="橘子">橘子</option>
    <option value="西瓜">西瓜</option>
    <option value="榴莲">榴莲</option>
  </select>
  <h3>您选择的水果是：{{fruit}}</h3>

  <!-- 选择多个值 -->
  <select name="" v-model="fruits" multiple>
    <option value="苹果">苹果</option>
    <option value="香蕉">香蕉</option>
    <option value="橘子">橘子</option>
    <option value="西瓜">西瓜</option>
    <option value="榴莲">榴莲</option>
  </select>
  <h3>您选择的水果是：{{fruits}}</h3>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      fruit: '苹果',
      fruits: []
    }
  });
</script>
```


### v-model 修饰符

- lazy 修饰符
  - 默认情况下，v-model 是在 input 事件中同步输入框的数据，也就是说，一旦有数据发生改变，对应的 data 中的数据就会自动发生改变
  - lazy 修饰符可以让数据在失去焦点或者回车时才会更新

- number 修饰符
  - 默认情况下，在输入框中无论输入的是字母还是数字，都会被当做字符串类型进行处理，但是如果我们希望处理的是数字类型，那么最好直接将内容当做数字处理
  - number 修饰符可以让在输入框中输入的内容自动转成数字类型

- trim 修饰符
  - 如果输入的内容首尾有很多空格，通常我们希望将其去除
  - trim 修饰符可以过滤内容左右两边的空格


```html
<div class="app">
  <!-- 1.lazy修饰符：失去焦点或按下回车才更新 -->
  <input type="text" v-model.lazy="name">
  <h2>{{name}}</h2>
  <!-- 2.number修饰符：将输入框中的内容自动转为number -->
  <input type="number" v-model.number="age">
  <h2>{{age}}---{{typeof age}}</h2>
  <!-- 3.trim修饰符：过滤内容左右两边的空格 -->
  <input type="text" v-model.trim="name">
  <h2>你输入的名字是:{{name}}</h2>
</div>
<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '.app',
    data: {
      name: 'YuanyangLiao',
      age: 18,
    }
  });
</script>
```

![图片.png](https://i.loli.net/2020/03/06/nCPOAEDif23rdwJ.png)
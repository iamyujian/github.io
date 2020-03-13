---
title: Vue router
date: 2020-03-13 22:53:40
categories:
- 前端
tags:
- Vue
- 前端
keywords:
comments:
---

<center>
<img src="https://i.loli.net/2020/03/06/DBnjol4tUpivVON.jpg" style="zoom:80%;" />


Vue router （路由）的使用
</center>
<!-- more -->



# Vue-router

## 认识路由

### 什么是路由

> 路由（routing）就是通过互联的网络把信息从源地址传输到目的地址的活动   — 维基百科


路由器提供了两种机制， 路由和转发

- 路由是决定数据包从来源到目的地的路径
- 转发将输入端的数据转移到合适的输出端

### 网站发展的几个阶段

#### 后端路由阶段 

**什么是后端路由**

早期的网站开发，整个 HTML 页面都是是由服务器来渲染的，服务器直接生产渲染好对应的 HTML 页面, 返回给客户端进行展示

但是, 服务器如何处理一个网站的诸多页面呢?

首先，一个页面会有自己对应的网址, 也就是 URL，客户端发生请求时，URL 会发送到服务器，服务器通过正则对该URL 进行匹配且最后交给 Controller 进行处理，Controller 进行各种处理后，最终生成 HTML 或者数据，返回给前端，这就完成了一个IO操作，这种操作, 就是后端路由

**后端路由的优点**

当页面中需要请求不同的路径内容时，交给服务器来进行处理, 服务器渲染好整个页面，并且将页面返回给客户端，这种情况下渲染好的页面，不需要单独加载任何的 js 和 css，可以直接交给浏览器展示，这样也有利于 SEO 的优化

**后端路由的缺点**

- 整个页面的模块都要由后端人员来编写和维护，工作量太大
- 前端开发人员如果要开发页面，需要通过 PHP 和 Java 等语言来编写页面代码，增加了额外的学习成本
- HTML 代码和数据以及对应的逻辑混在一起,，不利于编写和维护

#### 前端路由阶段

前端路由的核心：改变URL，但是页面不进行整体的刷新

##### 前后端分离阶段

随着 Ajax 的出现，有了前后端分离的开发模式：后端只提供 API 来返回数据，前端通过 Ajax 获取数据，并且可以通过 JavaScript 将数据渲染到页面中

优点：

- 前后端责任变得很清晰，后端专注于数据上, 前端专注于交互和可视化上
- 当移动端(iOS/Android)出现后，后端不需要进行任何处理， 依然使用之前的一套API即可

##### 单页面富应用阶段

单页面富应用，即单页Web应用（single page web application，SPA），就是只有一张 Web 页面的应用，是加载单个 HTML 页面并在用户与应用程序交互时动态更新该页面的 Web 应用程序

简单理解：就是在前后端分离的基础上加了一层前端路由

**SPA的特点**

- 速度：更好的用户体验，让用户在 web app 感受 native app 的速度和流畅
- ·MVVM：经典 MVVM 开发模式，前后端各负其责
- ·ajax：重前端，业务逻辑全部在本地操作，数据都需要通过AJAX同步、提交
- ·路由：在 URL 中采用 # 号来作为当前视图的地址，改变 # 号后的参数，页面并不会重载

**SPA 缺点**

- 首屏渲染等待时长： 必须得加载完毕，才能渲染出首屏
- seo不友好：爬虫只能拿到一个 div，认为页面是空的，不利于 seo
- 初次加载耗时多：为实现单页Web应用功能及显示效果，需要在加载页面的时候将 JavaScript、CSS 统一加载，部分页面可以在需要的时候加载，所以必须对 JavaScript 及 CSS 代码进行合并压缩处理，如果使用第三方库，建议使用一些大公司的 CDN，因此带宽的消耗是必然的

**SPA 优点**

- 良好的交互体验
  ：用户不需要重新刷新页面，获取数据也是通过 Ajax 异步获取，页面显示流畅
- 良好的前后端工作分离模式：单页 Web 应用可以和 RESTful 规约一起使用，通过 REST API 提供接口数据，并使用 Ajax 异步获取，这样有助于分离客户端和服务器端工作，更进一步，可以在客户端也可以分解为静态页面和页面交互两个部分
- 减轻服务器压力：服务器只用出数据就可以，不用管展示逻辑和页面合成，吞吐能力会提高几倍
- 共用一套后端程序代码：不用修改后端程序代码就可以同时用于 Web 界面、手机、平板等多种客户端

### 改变 URL，页面不刷新

#### URL 的 hash

URL 的 hash 也就是锚点(#)，本质上是改变 window.location 的 href 属性，可以通过直接赋值 location.hash 来改变 href，但是页面不发生刷新

![图片.png](https://i.loli.net/2020/03/09/TB28PpVIKmfjvg3.png)



#### HTML5 的 history 模式

history 接口是 HTML5 新增的，它有五种模式改变 URL 而不刷新页面（具体有点像浏览器的前进和后退）

- `history.pushState()`，相当于入栈的操作（出入栈相当于往一个杯子里加东西，只有一个出入口，后进的会在先进的上面），遵循后进先出的规则，会保存历史记录，可以返回

![图片.png](https://i.loli.net/2020/03/09/I2HEyRPNlBSoYzW.png)

- `history.replaceState()`，同 `pushState()` 不保存历史记录，不能返回
- `history.forward()` 可以前进到下一个记录的地址
- `history.back()`，相当于出栈的操作，遵循后进先出的规则，可以返回上一个记录的地址
- `history.go()` 功能等价于 `history.back` ，但是可以通过参数来进行具体的跳转

![图片.png](https://i.loli.net/2020/03/09/NT4C5Omlua6LqiU.png)



## Vue-router 基本使用

目前前端流行的三大框架，都有自己的路由实现：

- Angular：ngRouter
- React：ReactRouter
- Vue：vue-router

vue-router 是 Vue.js 官方的路由插件，它和 vue.js 是深度集成的，适合用于构建单页面富应用程序

vue-router 是基于路由和组件的，路由用于设定访问路径, 将路径和组件映射起来，在 vue-router 的单页面应用中, 页面路径的改变就是组件的切换

### 安装 vue-router

直接使用 npm 来安装路由即可

1. 安装 vue-router

```shell
npm install vue-router --save
```

2. 在模块化工程中使用

因为 vue-router 是一个插件，所以可以通过 `Vue.use()` 来安装路由功能

  1. 导入路由对象，并且调用 Vue.use(VueRouter)
  1. 创建路由实例，并且传入路由映射配置
  1. 在 Vue 实例中挂载创建的路由实例

### 使用 vue-router

1. 创建路由组件

- 创建 router 实例

<img src="https://i.loli.net/2020/03/09/trwjAfsD9CH4JIV.png" alt="img" style="zoom:67%;" />

- 挂载到 Vue 实例中

<img src="https://i.loli.net/2020/03/09/AGsDHka2nPRLv5f.png" alt="img" style="zoom:67%;" />



2. 配置路由映射: 组件和路径映射关系

- 新建两个组件

<img src="https://i.loli.net/2020/03/09/9cDpjsJ3t1EvC84.png" alt="img"  />

- 为组件配置路由映射关系

<img src="https://i.loli.net/2020/03/09/VC1RxqcaPSIBOjY.png" alt="img" style="zoom:67%;" />



3. 使用路由: 通过`<router-link>`和`<router-view>`

- `<router-link>`: 该标签是一个 vue-router 中已经内置的组件, 它默认会被渲染成一个 `<a>` 标签
- `<router-view>`: 该标签会根据当前的路径，动态渲染出不同的组件，放置的位置决定渲染的位置

<img src="https://i.loli.net/2020/03/09/XbofSjkwE5W76Fe.png" alt="img" style="zoom:67%;" />

最终效果如下：

<img src="https://i.loli.net/2020/03/09/5Nbf8EOn2xeGJwK.png" alt="img" style="zoom:67%;" />



### 细节处理

#### 路由的默认路径

默认情况下, 进入网站的首页，我们希望 `<router-view>` 渲染首页的内容，但是在上面的实现中，默认没有显示首页组件，必须让用户点击才可以

如何可以让路径默认跳到到首页，并且`<router-view>`渲染首页组件呢?

只需要多配置一个映射就可以了：

![图片.png](https://i.loli.net/2020/03/09/fWSOVEsakT1U2Cb.png)

我们在 routes 中又配置了一个映射：

- path：根路径 `/`
- redirect：重定向，也就是将根路径重定向到 `/home` 的路径下

这样，打开页面时，就会默认显示首页的内容了

#### HTML5 的 History 模式

前面说过改变路径的方式有两种：

- URL 的 hash
- HTML5 的 history

默认情况下，Vue 路径的改变使用的是 URL 的 hash，这样显示出的页面的地址中有一个 `#` 号，不太美观：

![图片.png](https://i.loli.net/2020/03/09/L2qsSMwQpOakzIK.png)

可以使用 HTML5 的 history 模式来进行改变，进行如下配置即可：

![图片.png](https://i.loli.net/2020/03/09/PI6d5uNkF8rnSQc.png)



![图片.png](https://i.loli.net/2020/03/09/ZPOdbyCv3j4XhMJ.png)

### router-link 补充

在前面的 `<router-link>` 中，我们只是使用了一个属性`:to`，用于指定跳转的路径

`<router-link>` 还有一些其他属性：

- tag：tag 可以指定 `<router-link>` 之后渲染成什么组件，默认是渲染为 `<a></a>` 标签

  我们可以使用 `tag="button"`、`tag="li"` 来改变

<img src="https://i.loli.net/2020/03/13/WTZzycJX5AvxlKG.png" alt="img" style="zoom:67%;" />

![图片.png](https://i.loli.net/2020/03/13/pWwKIosetLrPNBG.png)

- replace

  默认使用的是 HTML5 的 history 模式下的 pushState，可以通过浏览器进行返回和前进，如果想要禁用返回和前进，可以指定 replace 即可

```vue
<router-link to="/home" tag="button" replace>首页</router-link>
```

- active-class: 当`<router-link>`对应的路由匹配成功时，会自动给当前元素设置一个 `router-link-active` 的class

![img](https://i.loli.net/2020/03/13/X6UhO2ACutJjzEr.png)

设置 `active-class` 可以修改默认的名称：

```vue
<router-link to="/home" tag="button" active-class="active">首页</router-link>
```

![img](https://i.loli.net/2020/03/13/QBl7CiMpObc41zd.png)

在进行高亮显示的导航菜单或者底部 tabbar 时，会使用到该类，比如想设置按钮点击时变为红色：

<img src="https://i.loli.net/2020/03/13/Rrv7qxWVXlaTiLm.png" alt="img" style="zoom:67%;" />

![图片.png](https://i.loli.net/2020/03/13/8xyzG7oQFwEsqUh.png)

该 class 具体的名称也可以通过 router 实例的属性进行统一修改：

![图片.png](https://i.loli.net/2020/03/13/Iz6NlHTrqFePxLk.png)

但是通常不会修改类的属性, 会直接使用默认的 router-link-active 即可



### **路由代码跳转**

有时候，页面的跳转可能需要执行对应的 JavaScript 代码，这个时候，就可以使用第二种跳转方式了,比如，我们将代码修改如下：

<img src="https://i.loli.net/2020/03/13/WZrnv4Kji8omgzY.png" alt="img" style="zoom:67%;" />

`$router` 属性已经被 vue-router 嵌套进所有的组件中，可以在组件中直接使用

这里如果想禁用浏览器前进后退的功能的话，可以使用`this.$router.replace('/home')` 即可

### 动态路由

<a name="params"></a>

[参数传递](#canshu)

在某些情况下，一个页面的 path 路径可能是不确定的，比如我们进入用户界面时，希望是如下的路径：`/user/aaaa` 或 `/user/bbbb`，除了有前面的 `/user `之外，后面还跟上了用户的 ID

这种 path 和 Component 的匹配关系，称之为动态路由（也是路由传递数据的一种方式）

1. 在 `vue-router` 的路由路径中使用“动态路径参数”(dynamic segment) ：

<img src="https://i.loli.net/2020/03/13/Rl7cuvWTpJNUMBZ.png" alt="img" style="zoom:67%;" />

2. 在组件中手动绑定一个用户 ID：

<img src="https://i.loli.net/2020/03/13/1ih5ldmq7zZfAU2.png" alt="img" style="zoom:67%;" />

3. 更新 `User` 的模板，输出当前用户的 ID：

<img src="https://i.loli.net/2020/03/13/uSHeWkDx7R9Unpo.png" alt="img" style="zoom:67%;" />

4. 查看显示效果：

![图片.png](https://i.loli.net/2020/03/13/u7swmgkySfdYHEC.png)



### 路由的懒加载

#### 认识路由的懒加载

当打包构建应用时，Javascript 包会变得非常大，影响页面加载，如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就更加高效了

为了实现这种效果，我们可以使用路由的懒加载

路由懒加载的主要作用就是将路由对应的组件打包成一个个的 js 代码块，只有在这个路由被访问到的时候，才加载对应的组件

#### 懒加载的三种写法

1. 结合 Vue 的异步组件和 Webpack 的代码分析（早期的懒加载写法，能认识就行，不要求会写）

```javascript
const Home = resolve => { require.ensure(['../components/Home.vue'], () => { resolve(require('../components/Home.vue')) })};
```

2. AMD 写法

```javascript
const About = resolve => require(['../components/About.vue'], resolve);
```

3. 在ES6中，可以用更加简单的写法来组织 Vue 异步组件和 Webpack 的代码分割

```javascript
const Home = () => import('../components/Home.vue')
```

**路由懒加载的效果**

<img src="https://i.loli.net/2020/03/13/8dgnHwYQU4vDiPM.png" alt="img" style="zoom:67%;" />

## Vue-router 嵌套路由

嵌套路由是一个很常见的功能，比如在 home 页面中，我们希望通过 `/home/news` 和 `/home/message` 访问一些内容，一个路径映射一个组件，访问这两个路径也会分别渲染两个组件

路径和组件的关系如下:

<img src="https://i.loli.net/2020/03/13/32xXWELcQiNbaKo.png" alt="img" style="zoom: 80%;" />

实现嵌套路由有两个步骤：

1. 创建对应的子组件，并且在路由映射中配置对应的子路由

- 定义两个子组件

<img src="https://i.loli.net/2020/03/13/wS4HK7pOeREn2yk.png" alt="img" style="zoom:67%;" />

- 配置子组件的路由

<img src="https://i.loli.net/2020/03/13/7SMhQsHR8pVOTFY.png" alt="img" style="zoom:67%;" />

- 配置嵌套路由的默认路径

<img src="https://i.loli.net/2020/03/13/9fFGTNKd2akD47S.png" alt="img" style="zoom:67%;" />

2. 在父组件内部显示子组件

<img src="https://i.loli.net/2020/03/13/mxwQEecNFzuRqyj.png" alt="img" style="zoom:67%;" />

3. 查看显示效果

<img src="https://i.loli.net/2020/03/13/xu3IHwPfy12BLAX.png" alt="img" style="zoom:67%;" />

## Vue-router 参数传递



### 准备工作

为了演示传递参数，再创建一个组件，并且将其配置好

1. 创建新的组件 Profile.vue

<img src="https://i.loli.net/2020/03/13/A4qsbJXYlOfw3Qn.png" alt="img" style="zoom:67%;" />

2. 配置路由映射

<img src="https://i.loli.net/2020/03/13/daknbYPph8cAOE1.png" alt="img" style="zoom:67%;" />

3. 添加跳转的`<router-link>`

<img src="https://i.loli.net/2020/03/13/wKxQCzkt2filIoP.png" alt="img" style="zoom:67%;" />



### 传递参数的方式

传递参数主要有两种类型: params 和 query

如果数据简单且少使用 params ，如果数据较多就使用 query

- params 

  <a name="canshu"></a>

 [跳转到详细使用](#params)

  - 配置路由格式：`/router/:id`
  - 传递的方式：在 path 后面跟上对应的值
  - 传递后形成的路径：`/router/123`，`/router/abc`

- query
  - 配置路由格式：`/router`
  - 传递的方式：对象中使用 query 的 key 作为传递方式
  - 传递后形成的路径：`/router?id=123`，`/router?id=abc`

<img src="https://i.loli.net/2020/03/13/fOt1e3Y8DVrodxJ.png" alt="img" style="zoom:67%;" />

这里获取并打印这些数据：

<img src="https://i.loli.net/2020/03/13/o5Tp9QuYqf4jKGP.png" alt="img" style="zoom:67%;" />

<img src="https://i.loli.net/2020/03/13/9T4bD3urlFs8Q5N.png" alt="img" style="zoom:67%;" />

**获取参数**

获取参数是通过 _route_ 对象获取的，在使用了 _vue_−_router_ 的应用中，路由对象会被注入每个组件中，赋值为`_this_.route` ，并且当路由切换时，路由对象会被更新

**route 和 router 的区别**

- _$router_ 为 VueRouter 实例，想要导航到不同 URL，则使用 `router.push` 方法
- $route 为当前 router 跳转对象，是当前处于活跃的路由，里面可以获取 name、path、query、params 等

## Vue-router 导航守卫

在一个 SPA 应用中，如何改变网页的标题呢？

普通的修改方式：在每一个路由对应的组件 `.vue` 文件中，通过 mounted 声明周期函数，执行对应的代码进行修改

但是当页面比较多时，需要在多个页面执行类似的代码，所以这种方式不容易维护

更好的办法是使用导航守卫

### 什么是导航守卫

导航守卫主要用来监听路由的进入和离开，vue-router 提供了 beforeEach 和 afterEach 的钩子函数，它们会在路由即将改变前和改变后触发

### 导航守卫使用

我们可以利用 beforeEach 来完成标题的修改：

1. 在钩子当中利用 meta 来定义标题

<img src="https://i.loli.net/2020/03/13/PdjigxO2n3LSHYR.png" alt="img" style="zoom:67%;" />

2. 利用导航守卫，修改标题

<img src="https://i.loli.net/2020/03/13/fWqJmEc9y6SRbDr.png" alt="img" style="zoom:67%;" />

3. 查看修改效果

<img src="https://i.loli.net/2020/03/13/MC3eIhrTGstDBcq.png" alt="img" style="zoom:67%;" />



### 导航钩子的三个参数解析

- to: 即将要进入的目标的路由对象
- from: 当前导航即将要离开的路由对象
- next: 调用该方法后，才能进入下一个钩子



### 导航守卫补充

- 如果是后置钩子，也就是afterEach，不需要主动调用 next() 函数
- beforEach 必须要调用 next() 函数，不然就会终止，不会往下执行
- 上面使用的导航守卫，被称之为全局守卫，除此之外，还有路由独享的守卫、组件内的守卫



## keep-alive

keep-alive 是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染

router-view 也是一个组件，如果直接被包在 keep-alive 里面，所有路径匹配到的视图组件都会被缓存：

```vue
<keep-alive>
  <router-view>
    <!-- 所有路径匹配到的试图组件都会被缓存！ -->
  </router-view>
</keep-alive>
```

现在有这样一个需求：首页正正在显示的是被嵌套的消息路由，当我们点击其他页面，又重新点击首页时，让首页仍然显示被嵌套的消息路由

<img src="https://i.loli.net/2020/03/13/57zJr6jbOMS3maA.png" alt="img" style="zoom:67%;" />

1. 先取消嵌套路由的默认路径

<img src="https://i.loli.net/2020/03/13/2xtDMhkwX6lpyre.png" alt="img" style="zoom:67%;" />

2. 在 App.vue 中使用 `<keep-alive></keep-alive>` 包裹 `<router-view/>`

<img src="https://i.loli.net/2020/03/13/7IA2pdNK5FH63aC.png" alt="img" style="zoom:67%;" />

3. 在 Home.vue 中记录离开之前的路径

`activated`：当组件处于活跃的时候调用，只有在使用 keep-alive 的前提下才有作用

`deactivated`：当组件不是活跃的时候调用，同上

`beforeRouteLeave`：在离开之前调用

<img src="https://i.loli.net/2020/03/13/7VnspvNE5X68CBG.png" alt="img" style="zoom:67%;" />

keep-alive 还有两个非常重要的属性:

- include - 字符串或正则表达，只有匹配的组件会被缓存
- exclude - 字符串或正则表达式，任何匹配的组件都不会被缓存

让部分组件不缓存：

```vue
// 这里传的参数是组件里的 name 属性的值，如果需要传入多个组件的话，逗号后面不要留空格，不然会出现问题
<keep-alive exclude="Profile,User">
  <router-view/>
</keep-alive>
```
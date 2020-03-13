---
title: Vuex
date: 2020-03-13 23:10:55
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


Vuex 的使用
</center>
<!-- more -->



# Vuex

## 认识 Vuex

### 什么是 Vuex

> Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式


- Vuex 采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化
- Vuex 也集成到 Vue 的官方调试工具 devtools extension，提供了诸如零配置的 time-travel 调试、状态快照导入导出等高级调试功能

### 状态管理

#### 什么是状态管理

简单理解：把需要多个组件共享的变量全部存储在一个对象里面，然后将这个对象放在顶层的 Vue 实例中，让其他组件可以使用，共享这个对象中的所有变量属性，并且是响应式的

#### 管理什么状态

- 用户的登录状态、用户名称、头像、地理位置信息等
- 商品的收藏、购物车中的物品等

#### 单界面的状态管理

在单个组件中进行状态管理是一件非常简单的事情，如图：

<img src="https://i.loli.net/2020/03/13/LEUzYHMRiur4vPx.png" alt="img" style="zoom:67%;" />

- State：状态（姑且可以当做是 data 中的属性）
- View：视图层，可以针对 State 的变化，显示不同的信息
- Actions：用户的各种操作：点击、输入等，会导致状态的改变

**单界面状态管理的实现**

<img src="https://i.loli.net/2020/03/13/yW8UY3DTiEKesox.png" alt="img" style="zoom:67%;" />

在这个案例中：

- counter 需要某种方式被记录下来，也就是 State
- counter 目前的值需要被显示在界面中，也就是我们的 View
- 界面发生某些操作时（这里是用户的点击，也可以是用户的 input），需要去更新状态，也就是 Actions

#### 多界面状态管理

Vue 已经帮我们做好了单个界面的状态管理，但是如果是多个界面呢？

多个视图都依赖同一个状态（一个状态改了，多个界面需要进行更新）

全局单例模式（大管家）

现在要做的就是将共享的状态抽取出来，交给大管家统一进行管理，之后每个试图按照规定进行访问和修改等操作，这就是 Vuex 的基本思想

Vuex 状态管理图例

<img src="https://i.loli.net/2020/03/13/XQupl8njUPO2DMz.png" alt="img" style="zoom:67%;" />

### Vuex 的基本使用

**简单的案例**

还是实现一下之前简单的案例：

![img](https://i.loli.net/2020/03/13/1H984S5KBcMQ6pw.png)

首先，我们需要在某个地方存放我们的 Vuex 代码：

- 安装 Vuex：`npm i vuex --save`
- 创建一个文件夹 store，并且在其中创建一个 index.js 文件

<img src="https://i.loli.net/2020/03/13/y4T8OVvdRukJZWQ.png" alt="img" style="zoom:67%;" />

- 在 index.js 文件中写入如下代码

```javascript
import Vue from 'vue'
import Vuex from 'vuex'

vue.use(Vuex)

const store = Vuex.Store({
    state: {
        count: 0
    },
    mutations: {
        increment(state) {
            state.count++
        },
        decrement(state) {
            state.count--
        }
    }
})

export default store
```

**挂载到 Vue 实例中**

其次，我们让所有的 Vue 组件都可以使用这个 store 对象

来到 main.js 文件，导入 store 对象，并且放在 `new Vue` 中：

```javascript
import Vue from 'vue'
import App from './App'
import router from './router'
import store from './store'

Vue.config.productionTip = false

new Vue({
    el: '#app',
    router,
    store,
    render: h => h(App)
})
```

此后，在其他 Vue 组件中，可以通过 `this.$store` 的方式，获取到 store 对象

**使用 Vuex 的 count**

```vue
<template>
  <div class="test">
    <h2>当前计数：{{count}}</h2>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
  </div>
</template>

<script>
export default {
  name: 'Test',
  computed:{
    count(){
      return this.$store.state.count
    }
  },
  methods:{
    increment(){
      this.$store.commit('increment')
    },
    decrement(){
      this.$store.commit('decrement')
    }
  }
}
</script>
<style scoped>
</style>
```

这就是使用 Vuex 最简单的方式了：

1. 提取出一个公共的 store 对象，用于保存在多个组件中共享的状态
1. 将 store 对象放置在 new Vue 对象中，这样可以保证在所有的组件中都可以使用到
1. 在其他组件中使用 store 对象中保存的状态即可
  1. 通过 `this.$store.state.属性` 的方式来访问状态
  1. 通过 `this.$store.commit(‘Mutations中方法’)` 来修改状态

注意事项：

我们通过提交 Mutations 的方式，而非直接改变 `store.state.count` ，这是因为 Vuex 可以更明确的追踪状态的变化，如果是由多个组件修改同一个状态，可以知道是由哪个组件修改的什么状态，便于调试，所以不要直接改变 `store.state.count` 的值。


## Vuex 核心概念

### State 单一状态树

Vuex 提出使用单一状态树（Single Source of Truth），也可以翻译成单一数据源

如果状态信息是保存到多个 Store 对象中的，那么之后的管理和维护等等都会变得特别困难，所以 Vuex 使用了单一状态树来管理应用层级的全部状态

单一状态树能够让我们以最直接的方式找到某个状态的片段，而且在之后的维护和调试过程中，也可以非常方便的管理和维护

### Getters

有时候，我们需要从 store 中获取一些 state 变异后的状态，则可以使用 getters，相当于计算属性，一些复杂的计算和操作可以写到这里

#### Getters 基本使用

比如，现在 Store 中有这样的学生信息：

```javascript
const store = new Vuex.Store({
    state: {
        count: 0,
        students: [
            { id: 1001, name: 'lyy', age: 18 },
            { id: 1002, name: 'sss', age: 17 },
            { id: 1003, name: 'lin', age: 28 },
          	{ id: 1004, name: 'jack', age: 24 }
        ]
    }
})
```

现要求获取年龄小于20的学生个数，可以在 Store 中定义 getters：

```javascript
getters: {
  // 获取年龄小于20的学生人数
  getAgeLess20Count(state) { 
    return state.students.filter(s => s.age < 20).length
  }
}
```

之后，在各个组件中想要使用这个 getters，只需要：

```vue
<template>
  <div id="app">
    <h3>{{this.$store.getters.getAgeLess20Count}}</h3>
  </div>
</template>
```

#### Getters 作为参数

如果我们已经有了一个获取所有年龄小于20岁学生列表的 getters，那么可以这样来写：

```javascript
getters: {
  // 获取年龄小于20的学生
  getAgeLess20(state) {
    return state.students.filter(s => s.age < 20)
  },
  // 获取年龄小于20的学生人数
  getAgeLess20Count(state, getters) {
    return getters.getAgeLess20.length
  }
}
```

#### Getters 传递参数

getters 默认是不能传递参数的，如果希望传递参数，那么只能让 getters 本身返回另一个函数

比如上面的案例中，我们希望根据 ID 获取用户的信息：

```javascript
getters: {
  // 根据id查找学生
  getStuByID(state) {
    return id => state.students.find(s => s.id === id)
  }
}
```

在组件中使用：

```vue
<template>
  <div id="app">
    <h3>{{this.$store.getters.getStuByID(1002)}}</h3>
  </div>
</template>
```

![img](https://i.loli.net/2020/03/13/CumG8c9O3Nd6rwF.png)


### Mutations 状态更新

Vuex 的 store 状态的更新唯一方式：提交 Mutations

#### Mutations 组成

- 字符串的事件类型（type）
- 一个回调函数（handler），该回调函数的第一个参数就是 state

#### Mutations 的定义方式

```javascript
mutations: {
  increment(state) {
    state.count++
  },
    decrement(state) {
      state.count--
    }
}
```

**通过 Mutations 更新**

```javascript
methods:{
  increment(){
    this.$store.commit('increment')
  },
  decrement(){
    this.$store.commit('decrement')
  }
}
```



#### Mutations 传递参数

在通过 Mutations 更新数据的时候，有时候希望携带一些额外的参数，这种参数被称为 Mutations 的载荷(Payload)

比如之前的计数器案例，每次都是加减 1 ，现在想让加减的数字作为一个参数，传到 Mutations 的方法中：

![img](https://i.loli.net/2020/03/13/g6C89dPvYxSzKj1.png)

<img src="https://i.loli.net/2020/03/13/dl4mUAnkI17KZfR.png" alt="img" style="zoom:67%;" />

如果有很多参数需要传递，通常会以对象的形式传递，也就是 payload 是一个对象，再从对象中取出相关的信息

![img](https://i.loli.net/2020/03/13/Rwz8dtxIBO13GpL.png)



#### Mutations 提交风格

上面的通过 commit 进行提交是一种普通的方式

Vue 还提供了另外一种风格, 它是一个包含 type 属性的对象

![img](https://i.loli.net/2020/03/13/c9YCO2zZ5UNo7di.png)

Mutations 中的处理方式是将整个 commit 的对象作为 payload 使用, 所以代码没有改变, 依然如下:

![img](https://i.loli.net/2020/03/13/NkDG3pLngYU7zmM.png)



#### Mutations 响应规则

Vuex 的 store 中的 state 是响应式的， 当 state 中的数据发生改变时，Vue 组件会自动更新

这就要求我们必须遵守一些Vuex对应的规则：

- 提前在store中初始化好所需的属性
- 当给 state 中的对象添加新属性时，使用下面的方式：
  1. 使用 `Vue.set(obj, 'newProp', 123)`
  1. 用新对象给旧对象重新赋值

我们来看一个例子:

当我们点击更新信息时，界面并没有发生对应改变：

<img src="https://i.loli.net/2020/03/13/CLlSVqzUB6Ncvis.png" alt="img" style="zoom:67%;" />

以上代码给 state 中的对象添加新属性时，由于不是响应式添加，所以界面不会更新，要想让界面更新，可以使用一下方式：

```javascript
updateInfo(state, payload) {
  // state.info['height'] = payload.height
  // 方式一：Vue.set()
  // Vue.set(state.info, 'height', payload.height)
  // 方式二：给 info 赋值一个新的对象
  state.info = {...state.info, 'height': payload.height }
}
```

此时，点击修改信息按钮后，界面和 info 里面的信息都会更新：

<img src="https://i.loli.net/2020/03/13/184I9sQDoM2LPyn.png" alt="img" style="zoom:67%;" />

#### Mutations 常量类型

在 Mutations 中， 我们定义了很多事件类型（也就是其中的方法名称），当我们的项目不断增大时，会出现：

- Vuex 管理的状态越来越多，需要更新状态的情况越来越多
- Mutations 中的方法越来越多，使用者需要花费大量的经历去记住这些方法，甚至是多个文件间来回切换，查看方法名称，甚至出现写错的情况

如何避免上述的问题呢?

在各种 Flux 实现中，一种很常见的方案是：

- 使用常量替代 Mutations 事件的类型
- 将这些常量放在一个单独的文件中，方便管理以及让整个 app 所有的事件类型一目了然

具体操作：

1. 创建一个文件: mutations-types.js，并且在其中定义我们的常量

<img src="https://i.loli.net/2020/03/13/4vXykBfEaJ38o7g.png" alt="img" style="zoom:67%;" />

定义常量时，我们可以使用 ES2015 中的风格，使用一个常量来作为函数的名称

2. 使用定义的常量

<img src="https://i.loli.net/2020/03/13/i3DCo5GBan68pvF.png" alt="img" style="zoom:67%;" />

### Actions

通常情况下，Vuex 要求 Mutations 中的方法必须是同步方法，因为当我们使用 devtools 时，devtools 可以帮助我们捕捉 Mutations 的快照，但如果是异步操作, 那么 devtools 将不能很好的追踪这个操作什么时候会被完成

比如之前的代码，当执行修改信息操作时，devtools 中会有如下信息：

<img src="https://i.loli.net/2020/03/13/2YphSX8vNxuCBID.png" alt="img" style="zoom:67%;" />

但是，如果 Vuex 中的代码使用了异步函数：

```javascript
mutations: {
  [types.UPDATE_INFO](state, payload) {
    setTimeout(() => {
      state.info = {...state.info, 'height': payload.height }
    }, 1000);
  }
}
```

这时会发现 state 中的 info 数据一直没有被改变：

<img src="https://i.loli.net/2020/03/13/zhpNYUc5AqbnxH3.png" alt="img" style="zoom:67%;" />

这是因为 devtools 无法追踪到异步操作

虽然强调不要再 Mutations 中进行异步操作，但某些情况,，又确实希望在 Vuex 中进行一些异步操作，比如网络请求，这时可以使用 Action

Action 类似于 Mutations，是用来代替 Mutations 进行异步操作的

在 Action 中，可以将异步操作放在一个 Promise 中，并且在成功或者失败后，调用对应的 resolve 或 reject：

<img src="https://i.loli.net/2020/03/13/QJgie9pMPnVArNB.png" alt="img" style="zoom:67%;" />

<img src="https://i.loli.net/2020/03/13/8Jv9CRQPB3UtfWN.png" alt="img" style="zoom:67%;" />

这里的 context 可以当成 store 对象，也可以通过 payload 传递参数，这里的 context 可以使用对象的解构方式的写法

### Modules

#### Modules 基本使用

Modules 是模块的意思，为什么在Vuex中我们要使用模块呢?

Vue 使用单一状态树，意味着很多状态都会交给 Vuex 来管理，当应用变得非常复杂时，store 对象就有可能变得相当臃肿，为了解决这个问题，Vuex 允许我们将 store 分割成模块（Module）， 每个模块拥有自己的 state、mutations、actions、getters 等

我们按照什么样的方式来组织模块呢?

```javascript
const ModuleA = {
  state:{},
  mutations:{},
  // 这里的 context 指的是本模块内 mutations 里的内容
  actions:{},
  // 模块里的getters可以有第三个参数 rootState ,意思是可以拿到根模块中的数据
  getters:{}
}

const ModuleB = {
  state:{},
  mutations:{},
  actions:{},
  getters:{}
}

const store = new Vuex.Store({
  modules:{
    a:ModuleA,
    b:ModuleB
  }
})
// 拿取 state 里的数据的时候要.对应的模块来拿取，其它的使用方法都一样
$store.state.a // ModuleA 的状态
$store.state.b // ModuleB 的状态
```



#### Modules 中的 state

要想知道如何调用 Modules 中的 state，需要先了解一下 Modules 中的 module 真实位置

其实，在 store 实例的 modules  中定义的 a 和 b 会被放到 store 的 state 中：

<img src="https://i.loli.net/2020/03/13/sKY3aG1QjexPVW8.png" alt="img" style="zoom:67%;" />

在 devtools 中也能看到：

<img src="https://i.loli.net/2020/03/13/EnFIVujzs4dOp5G.png" alt="img" style="zoom:67%;" />

既然 Module 被放到了 store 的 state 中，那么在其他组件中就可以使用 `this.$store.state` 来调用了：

<img src="https://i.loli.net/2020/03/13/qnrO4cFvPpTQw67.png" alt="img" style="zoom:67%;" />



![img](https://i.loli.net/2020/03/13/LTV19fCshbJr7Uu.png)


#### Modules 中的 mutations

虽然 mutations 是定义在模块中的，但是在组件中提交时还是使用：`this.$store.commit`

<img src="https://i.loli.net/2020/03/13/seUWtcbKdgAnl7T.png" alt="img" style="zoom:67%;" />



<img src="https://i.loli.net/2020/03/13/d2QXuOomCGwRWYN.png" alt="img" style="zoom:67%;" />



#### Modules 中的 getters

<img src="https://i.loli.net/2020/03/13/RJ8lxjUZ7rusOza.png" alt="img" style="zoom:67%;" />

#### Modules 中的 actions

<img src="https://i.loli.net/2020/03/13/yrCh4xBpobeO1P9.png" alt="img" style="zoom:67%;" />

## 项目结构

当 Vuex 帮助我们管理过多的内容时，好的项目结构可以让我们的代码更加清晰：

这里建议：state 的内容可以写在 index 里，其它所有的都抽离成一个模块

<img src="https://i.loli.net/2020/03/13/u4OKgRhHza2oqAQ.png" alt="img" style="zoom:67%;" />
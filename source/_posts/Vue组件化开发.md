---
title: Vue组件化开发
date: 2020-03-08 01:19:34
categories:
- 前端
tags:
- Vue
keywords:
comments:
---



<center> 
<img src="https://i.loli.net/2020/03/06/DBnjol4tUpivVON.jpg" style="zoom:80%;" />


Vue 的组件化开发
</center>
<!-- more -->



# 组件化开发

## 认识组件化

- 人面对复杂问题的处理方式：任何一个人处理信息的逻辑能力都是有限的，但人有一种天生的能力，就是将问题进行拆解，如果将一个复杂的问题，拆分成很多个可以处理的小问题，再将其放在整体当中，会发现大的问题也会迎刃而解
- 组件化也是类似的思想：如果我们将一个页面中所有的处理逻辑全部放在一起，处理起来就会变得非常复杂，而且不利于后续的管理以及扩展，但如果将一个页面拆分成一个个小的功能块，每个功能块完成属于自己这部分独立的功能，那么之后整个页面的管理和维护就变得非常容易了


## Vue 组件化思想

组件化是 Vue.js 中的重要思想，它提供了一种抽象，让我们可以开发出一个个独立可复用的小组件来构造我们的应用

任何的应用都会被抽象成一颗组件树：

![](https://i.loli.net/2020/03/06/h9fNTv3ewWPd65Z.png)

有了组件化的思想，我们在之后的开发中就要充分的利用它，尽可能的将页面拆分成一个个小的、可复用的组件，这样让我们的代码更加方便组织和管理，并且扩展性也更强


## 注册组件

组件的使用分成三个步骤：

1. 创建组件构造器
1. 注册组件
1. 使用组件

![img](https://i.loli.net/2020/03/08/T9GC8oJAOIfV2iK.png)

注意：以上代码方式创建的组件是全局组件，即可以在多个 vue 的实例下使用，要改为局部组件，需要将注册方法写到具体的某个实例中


## 全局组件和局部组件

当我们通过调用 `Vue.component()` 注册组件时，组件的注册是全局的
，这意味着该组件可以在任意 Vue 实例下使用；如果我们注册的组件是挂载在某个实例中, 那么就是一个局部组件

![图片.png](https://i.loli.net/2020/03/06/5OAafPimuwCI3KJ.png)


## 父组件和子组件

组件和组件之间存在层级关系，而其中一种非常重要的关系就是父子组件的关系

<img src="https://i.loli.net/2020/03/08/5es2wZEdbjyclA9.png" alt="img" style="zoom:67%;" />

## 注册组件语法糖

在上面注册组件的方式，可能会有些繁琐，Vue为了简化这个过程，提供了注册的语法糖，主要是省去了调用`Vue.extend()` 的步骤，直接使用一个对象来代替

语法糖注册全局组件和局部组件：

```javascript
<div class="app">
  <my-cpn1></my-cpn1>
  <my-cpn2></my-cpn2>
  </div>
  <script src="../js/vue.js"></script>
  <script>
    // 1. 注册全局组件的语法糖
    Vue.component('my-cpn1', {
    template: `
      <div>
      <h2>组件标题1</h2>
      <p>组件1中的一个段落内容</p>
      </div>
      `
  })
  const app = new Vue({
    el: '.app',
    // 2. 注册局部组件的语法糖
    components: {
      'my-cpn2': {
        template: `
          <div>
          <h2>组件标题2</h2>
          <p>组件2中的一个段落内容</p>
          </div>
          `
      }
    }
  })
</script>
```


## 注册组件模板分离

即使用 script 标签或 template 标签将模板内容从注册时的 template 中抽离出来


### 使用 < script >  标签

![图片.png](https://i.loli.net/2020/03/06/om17vSMXQUedNyn.png)


### 使用 < template > 标签

这种方式更为简单常用

<img src="https://i.loli.net/2020/03/08/8OsQUP2TCo95uNi.png" alt="img" style="zoom:67%;" />




## 组件数据存放

组件是一个单独功能模块的封装，这个模块有属于自己的HTML模板，也应该有属性自己的数据 data，那么组件中的数据是保存在哪里呢？顶层的Vue实例中吗？

先来测试一下，组件中能不能直接访问 Vue 实例中的 data：

![图片.png](https://i.loli.net/2020/03/06/fqpMPuVxIyvHN8l.png)



通过以上代码发现，组件不能直接访问 Vue 实例中的 data，而且即使可以访问，如果将所有的数据都放在 Vue 实例中，Vue 实例就会变的非常臃肿

结论：Vue 组件应该有自己保存数据的地方

那么，组件自己的数据存放在哪里呢?

其实，组件对象也有一个 data 属性，只是这个 data 属性必须是一个函数，而且这个函数返回一个对象，对象内部保存着数据

![图片.png](https://i.loli.net/2020/03/06/Yv2mxTXqaQN4dcu.png)

**为什么 data 在组件中必须是一个函数呢?**

使用函数的话，每次使用组件的时候，每个组件都会创建自己的数据空间，组件之间的数据不会相互影响，如果是对象的话，每个组件调用的数据来自同一个对象，其中一个组件修改了数据的话，其他组件的数据也会跟着改变，这不是我们所期望的。

- 首先，如果不是一个函数，Vue直接就会报错
- 其次，Vue 让每个组件对象都返回一个新的对象，因为如果是同一个对象的，组件在多次使用后会相互影响

![img](https://i.loli.net/2020/03/08/Nh9IWzO327X6ig8.png)




## 父子组件通信

- 父传子：props
- 子传父：自定义事件

![图片.png](https://i.loli.net/2020/03/06/df93AsYLnqMuVJZ.png)


### 父传子 props

在组件中，使用选项 props 来声明需要从父级接收到的数据

**注意**：`<cpn :c-info="info"></cpn>`这里的`:`后面的参数是不支持驼峰命名的参数的，否者是没有效果的，如果是驼峰的可以`-`进行连接来进行替换

props 的值有两种方式：

1. 字符串数组，数组中的字符串就是传递时的名称

![img](https://i.loli.net/2020/03/08/tqcKNJFdzS2wa67.png)



2. 对象，对象可以设置传递时的类型，也可以设置默认值和类型等

![img](https://i.loli.net/2020/03/08/XZ2lhp3WfaKrwQU.png)



验证支持的数据类型：

![image-20200306230643611](https://i.loli.net/2020/03/06/roAk7gqnZtb93G5.png)



### 子传父 自定义事件

自定义事件流程：

1. 在子组件中，通过 `$emit()` 来触发事件
1. 在父组件中，通过 `v-on` 来监听子组件事件

<img src="https://i.loli.net/2020/03/08/JiMFbGXSWkxHEBg.png" alt="img" style="zoom:67%;" />


### 双向绑定

```html
<!-- 父组件模板 -->
<div class="app">
  <cpn :number1="num1" :number2="num2" @num1change="num1change" @num2change="num2change"></cpn>
</div>
<!-- 子组件模板 -->
<template id="cpn">
  <div>
    <h2>props:{{number1}}</h2>
    <h2>data:{{dnumber1}}</h2>
    <!-- <input type="text" v-model="dnumber1"> -->
    <input type="text" :value="dnumber1" @input="num1Input">
    <h2>props:{{number2}}</h2>
    <h2>data:{{dnumber2}}</h2>
    <!-- <input type="text" v-model="dnumber2"> -->
    <input type="text" :value="dnumber2" @input="num2Input">
  </div>
</template>
<script src="../js/vue.js"></script>
<script>
  // 父组件
  const app = new Vue({
    el: '.app',
    data: {
      num1: 1,
      num2: 0
    },
    methods: {
      num1change(value) {
        this.num1 = parseFloat(value)
      },
      num2change(value) {
        this.num2 = parseFloat(value)
      }
    },
    // 子组件
    components: {
      cpn: {
        template: '#cpn',
        // props中的数据只能父组件修改，通过使用标签动态绑定
        props: { // 父传子
          number1: Number,
          number2: Number
        },
        data() {
          return {
            dnumber1: this.number1,
            dnumber2: this.number2,
          }
        },
        methods: {
          num1Input(event) {
            // 将input中的vlaue赋值给dnumber1
            this.dnumber1 = event.target.value
            // 发射一个事件，让父组件可以修改值（子传父）
            this.$emit('num1change', this.dnumber1)
            // 修改dnumber2的值
            this.dnumber2 = this.dnumber1 * 100
            this.$emit('num2change', this.dnumber2)
          },
          num2Input(event) {
            this.dnumber2 = event.target.value
            this.$emit('num2change', this.dnumber2)
            this.dnumber1 = this.dnumber2 / 100
            this.$emit('num1change', this.dnumber1)
          }
        }
      }
    }
  })
</script>
```

图解关系：

![img](https://i.loli.net/2020/03/08/lVWK4gCyR8m6isN.png)


## 父子组件访问


### 父组件访问子组件

父组件访问子组件有两种方式：

- $children（不常用）
- $refs（常用）


#### $children

`this.$children` 是一个数组类型，它包含所有子组件对象，可以通过遍历，取出所有子组件的信息

![img](https://i.loli.net/2020/03/08/FR8otOAzQe6nIKj.png)

$children 的缺陷：通过 $children 访问子组件时，是一个数组类型，访问其中的子组件必须通过索引值，但是当子组件过多，我们需要拿到其中一个时，往往不能确定它的索引值，甚至还可能会发生变化

有时候，我们想明确获取其中一个特定的组件，这个时候就可以使用 $refs


#### $refs

$refs 和 ref 指令通常是一起使用的：

1. 首先，我们通过 ref 给某一个子组件绑定一个特定的 ID

```html
<cpn ref="child1"></cpn>
<cpn ref="child2"></cpn>
```

2. 其次，通过 `this.$refs.ID` 就可以访问到该组件了

```javascript
console.log(this.$refs.child1.name);
console.log(this.$refs.child2.name);
```


### 子组件访问父组件（不常用）

子组件访问父组件通过：$parent 如果是向访问根组件，通过：$root

![img](https://i.loli.net/2020/03/08/CkcXn63RUpETxAl.png)

注意：

- 尽管在 Vue 开发中，我们允许通过 $parent 来访问父组件，但是在真实开发中尽量不要这样做，因为这样耦合度太高了
- 子组件应该尽量避免直接访问父组件的数据，如果我们将子组件放在另外一个组件之内，很可能该父组件没有对应的属性，往往会引起问题
- 另外，通过 $parent 直接修改父组件的状态，那么父组件中的状态将变得飘忽不定，很不利于调试和维护
- 也不常用 $root 来访问根组件（即 vue 实例），因为根组件中一般只存放路由等重要数据，不存放其他信息


# 组件化高级


## 插槽 slot（Vue 2.6之前用法）


### 为什么使用 slot

slot 翻译为插槽，插槽的目的是让我们原来的设备具备更多的扩展性

组件的插槽，也是为了让我们封装的组件更加具有扩展性，让使用者可以决定组件内部的一些内容到底展示什么


### slot 基本使用

在子组件中，使用特殊的元素 `<slot>` 就可以为子组件开启一个插槽，该插槽插入什么内容取决于父组件如何使用

![图片.png](https://i.loli.net/2020/03/06/4ogGtJKVHEpPL5i.png)




### 具名插槽 slot

当子组件的功能复杂时，子组件的插槽可能并非是一个，比如我们封装一个导航栏的子组件，可能就需要三个插槽，分别代表左边、中间、右边

那么，外面在给插槽插入内容时，如何区分插入的是哪一个呢？这个时候，我们就需要给插槽起一个名字，这就是具名插槽<br />具名插槽的使用很简单，只要给 slot 元素一个 name 属性即可：`<slot name='myslot'></slot>`

![图片.png](https://i.loli.net/2020/03/06/hGv6DPNibTF1YLO.png)




### 编译作用域

- 父组件模板的所有东西，都会在父级作用域内编译
- 子组件模板的所有东西，都会在子级作用域内编译

![图片.png](https://i.loli.net/2020/03/06/gitPUB9xIM346jn.png)


### 作用域插槽

作用域插槽是 slot 一个比较难理解的点，一句话总结就是：

父组件替换插槽的标签，但是内容由子组件来提供

![img](https://i.loli.net/2020/03/08/oWRVxQagLO2uA1e.png)




## 插槽slot（Vue 2.6之后用法）

> 在 2.6.0 中，我们为具名插槽和作用域插槽引入了一个新的统一的语法 (即 `v-slot` 指令)。它取代了 `slot` 和 `slot-scope` 这两个目前已被废弃但未被移除且仍在[文档中](https://cn.vuejs.org/v2/guide/components-slots.html#%E5%BA%9F%E5%BC%83%E4%BA%86%E7%9A%84%E8%AF%AD%E6%B3%95)的特性。新语法的由来可查阅这份 [RFC](https://github.com/vuejs/rfcs/blob/master/active-rfcs/0001-new-slot-syntax.md)。


slot 有三种类型

- 默认插槽 default
- 具名插槽 name
- 作用域插槽 v-slot

在子组件中：

- 插槽用 `<slot>` 标签来确定渲染的位置，里面放的是父组件没传内容时的后备内容，一个不带 name 的 `<slot>` 出口会带有隐含的名字 default
- 具名插槽用 name 属性来表示插槽的名字
- 作用域插槽在作用域上绑定属性来将子组件的信息传给父组件使用

有时我们需要多个插槽。例如对于一个带有如下模板的 `<base-layout>` 组件：

```html
<div class="container">
  <header>
    <!-- 我们希望把页头放这里 -->
  </header>
  <main>
    <!-- 我们希望把主要内容放这里 -->
  </main>
  <footer>
    <!-- 我们希望把页脚放这里 -->
  </footer>
</div>
```

对于这样的情况，`<slot>` 元素有一个特殊的特性：`name`，这个特性可以用来定义额外的插槽：

```html
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>
```

一个不带 name 的 <slot> 出口会带有隐含的名字“default”。


### v-slot

- 具名插槽通过指令参数 `v-slot:插槽名` 的形式传入，可以简化为 `#插槽名`
- 作用域插槽通过 `v-slot:xxx="slotProps"` 的 slotProps 来获取子组件传出的属性

```html
//具名插槽的缩写
<template>
  <child>
   <!--默认插槽-->
   <template v-slot>  // v-slot:default
     <div>默认插槽</div>
   </template>
   <!--具名插槽-->
   <template #header>  // v-slot:header
     <div>具名插槽</div>
   </template>
   <!--作用域插槽-->
   <template #footer="slotProps">  //v-slot:footer
     <div>
      {{slotProps.testProps}}
     </div>
   </template>
  <child>
</template>
```

在向具名插槽提供内容的时候，我们可以在一个 `<template>` 元素上使用 `v-slot` 指令，并以 `v-slot` 的参数的形式提供其名称：

```html
<base-layout>
  <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>

  <p>A paragraph for the main content.</p>
  <p>And another one.</p>

  <template v-slot:footer>
    <p>Here's some contact info</p>
  </template>
</base-layout>
```

现在 `<template>` 元素中的所有内容都将会被传入相应的插槽。任何没有被包裹在带有 `v-slot`的 `<template>` 中的内容都会被视为默认插槽的内容

然而，如果你希望更明确一些，仍然可以在一个 `<template>` 中包裹默认插槽的内容：

```html
<base-layout>
  <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>

  <template v-slot:default>
    <p>A paragraph for the main content.</p>
    <p>And another one.</p>
  </template>

  <template v-slot:footer>
    <p>Here's some contact info</p>
  </template>
</base-layout>
```

任何一种写法都会渲染出：

```html
<div class="container">
  <header>
    <h1>Here might be a page title</h1>
  </header>
  <main>
    <p>A paragraph for the main content.</p>
    <p>And another one.</p>
  </main>
  <footer>
    <p>Here's some contact info</p>
  </footer>
</div>
```

注意 **v-slot 只能添加在  上** (只有一种例外情况)，这一点和已经废弃的 `slot` 特性)不同。

### v-slot 作用域插槽

有时让插槽内容能够访问子组件中才有的数据是很有用的，例如，设想一个带有如下模板的 `<current-user>` 组件：

```html
<span>
  <slot>{{ user.lastName }}</slot>
</span>
```

我们可能想换掉备用内容，用名而非姓来显示，如下：

```html
<current-user>
  {{ user.firstName }}
</current-user>
```

然而上述代码不会正常工作，因为只有 `<current-user>` 组件可以访问到 `user` 而我们提供的内容是在父级渲染的

为了让 `user` 在父级的插槽内容中可用，我们可以将 `user` 作为 `<slot>` 元素的一个特性绑定上去：

```html
<span>
  <slot v-bind:user="user">
    {{ user.lastName }}
  </slot>
</span>
```

绑定在 `<slot>` 元素上的特性被称为**插槽 prop**。现在在父级作用域中，我们可以使用带值的 `v-slot` 来定义我们提供的插槽 prop 的名字：

```html
<current-user>
  <template v-slot:default="slotProps">
    {{ slotProps.user.firstName }}
  </template>
</current-user>
```

在这个例子中，我们选择将包含所有插槽 prop 的对象命名为 slotProps，但你也可以使用任意你喜欢的名字


### 独占默认插槽的缩写语法

在上述情况下，当被提供的内容只有默认插槽时，组件的标签才可以被当作插槽的模板来使用，这样我们就可以把 v-slot 直接用在组件上：

```html
<current-user v-slot:default="slotProps">
 {{ slotProps.user.firstName }}
</current-user>
```

这种写法还可以更简单，就像假定未指明的内容对应默认插槽一样，不带参数的 v-slot 被假定对应默认插槽：

```html
<current-user v-slot="slotProps">
 {{ slotProps.user.firstName }}
</current-user>
```

注意默认插槽的缩写语法不能和具名插槽混用，因为它会导致作用域不明确：

```html
<!-- 无效，会导致警告 -->
<current-user v-slot="slotProps">
 {{ slotProps.user.firstName }}
 <template v-slot:other="otherSlotProps">
   slotProps is NOT available here
 </template>
</current-user>
```

只要出现多个插槽，请始终为所有的插槽使用完整的基于 <template> 的语法：

```html
<current-user>
 <template v-slot:default="slotProps">
   {{ slotProps.user.firstName }}
 </template>
 <template v-slot:other="otherSlotProps">
   ...
 </template>
</current-user>
```


### 解构插槽 Prop

作用域插槽的内部工作原理是将你的插槽内容包括在一个传入单个参数的函数里：

```html
function (slotProps) {
 // 插槽内容
}
```

这意味着 v-slot 的值实际上可以是任何能够作为函数定义中的参数的 JavaScript 表达式

所以在支持的环境下 (单文件组件或现代浏览器)，你也可以使用 ES2015 解构来传入具体的插槽 prop，如下：

```html
<current-user v-slot="{ user }">
 {{ user.firstName }}
</current-user>
```

这样可以使模板更简洁，尤其是在该插槽提供了多个 prop 的时候。它同样开启了 prop 重命名等其它可能，例如将 user 重命名为 person：

```html
<current-user v-slot="{ user: person }">
 {{ person.firstName }}
</current-user>
```

你甚至可以定义后备内容，用于插槽 prop 是 undefined 的情形：

```html
<current-user v-slot="{ user = { firstName: 'Guest' } }">
 {{ user.firstName }}
</current-user>
```

注意：

- 默认插槽名为default，可以省略default直接写v-slot。缩写为#时不能不写参数，写成#default（这点所有指令都一样，v-bind、v-on）
- 多个插槽混用时，v-slot不能省略default
- 只要出现多个插槽，请始终为所有的插槽使用完整的基于<template> 的语法


### 动态插槽名（ 2.6.0 新增）

动态指令参数也可以用在 v-slot 上，来定义动态的插槽名：

```html
<base-layout>
 <template v-slot:[dynamicSlotName]>
   ...
 </template>
</base-layout>
```


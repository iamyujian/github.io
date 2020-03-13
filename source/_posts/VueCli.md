---
title: VueCli
date: 2020-03-13 22:39:56
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


Vue Cli （脚手架）的使用
</center>
<!-- more -->



# Vue CLI



## 什么是 Vue CLI

如果你只是简单写几个 Vue 的 Demo 程序, 那么你不需要 Vue CLI如果你在开发大型项目, 那么你需要, 并且必然需要使用 Vue CLI

使用 Vue.js 开发大型应用时，我们需要考虑代码目录结构、项目结构和部署、热加载、代码单元测试等事情，如果每个项目都要手动完成这些工作，效率比较低，所以通常我们会使用一些脚手架工具来帮助完成这些事情

**CLI 是什么意思**

CLI 是 Command-Line Interface , 翻译为命令行界面, 俗称脚手架

Vue CLI 是一个官方发布的 vue.js 项目脚手架

使用 vue-cli 可以快速搭建 Vue 开发环境以及对应的 webpack 配置

Vue CLI 使用前提：

- Node
- webpack

## Vue CLI 的使用

### 安装 Vue 脚手架

```shell
npm install -g @vue/cli
```

注意：上面安装的是 Vue CLI3 以上的版本，如果需要想按照 Vue CLI2 的方式初始化项目，还需要拉取 2.x 的模板

### 拉取 2.x 模板（旧版本）

```shell
npm i @vue/cli-init -g
```

### 初始化项目

#### Vue CLI2 初始化项目

```shell
vue init webpack vuecli2test
```

**vue cli 2 项目详解**

![img](https://i.loli.net/2020/03/08/4YQETKHsGjcvdhJ.png)

**vue cli 2 目录详解**

<img src="https://i.loli.net/2020/03/08/6JHcwRa1sYW9rBU.png" alt="img" style="zoom:67%;" />

#### Vue CLI3 初始化项目

```shell
vue create vuecli3test
```

vue-cli 3 与 2 版本有很大区别：

- vue-cli 3 是基于 webpack 4 打造，vue-cli 2 还是 webapck 3
- vue-cli 3 的设计原则是“0配置”，移除了根目录下的 build 和 config 等的配置文件目录
- vue-cli 3 提供了 vue ui 命令，提供了可视化配置，更加人性化
- 移除了 static 文件夹，新增了 public 文件夹，并且 index.html 移动到 public 中

**vue cli 3 项目详解**

![图片1](https://i.loli.net/2020/03/08/rSTRPKo6E8Od54B.png)

<img src="https://i.loli.net/2020/03/08/v59h3Hz8lMICk7f.png" alt="img" style="zoom:67%;" />



**如何删除保存的配置单呢？**

<img src="https://i.loli.net/2020/03/08/PlOgVm6C2e4fZH3.png" alt="删除" style="zoom:67%;" />



**vue cli 3 目录详解**

<img src="https://i.loli.net/2020/03/08/s8uyMxXVG1WJQlp.png" alt="img" style="zoom:67%;" />

main.js 里的 `Vue.config.productionTip = false` 用来设置产品在构建的时候是否要显示提示信息，开发阶段一般设置为 `false`

### CLI 相关配置

#### Runtime-Compiler 和 Runtime-only 的区别

构建项目时：

![img](https://i.loli.net/2020/03/08/tswErpoXe7PzW91.png)

官方解释：

<img src="https://i.loli.net/2020/03/08/6DpNEat8uAm7HX2.png" alt="img" style="zoom:67%;" />

简单总结：

- 如果在之后的开发中，你依然使用 template，就需要选择 Runtime-Compiler
- 如果你之后的开发中，使用的是 .vue 文件开发，那么可以选择 Runtime-only

**render 和 template**

![img](https://i.loli.net/2020/03/08/4HFCxt91WEmJcQa.png)

**Vue 程序运行过程**

<img src="https://i.loli.net/2020/03/08/DYViX6tFPZl9vKA.png" alt="img" style="zoom:67%;" />**render 函数的使用**

<img src="https://i.loli.net/2020/03/08/EIVKMgqybhQGT8r.png" alt="img" style="zoom:67%;" />



#### npm run build

<img src="https://i.loli.net/2020/03/08/LnqV96wc3MYobhk.png" alt="img" style="zoom:67%;" />



#### npm run dev

<img src="https://i.loli.net/2020/03/08/KH81pw3gOWdzB64.png" alt="img" style="zoom:67%;" />



#### 配置文件去向

在 Vue CLI 3 中，webpack 等相关配置文件被隐藏起来了，如果想查看或修改相关配置，可以通过以下3种方式：

1. 从 UI 界面上修改

- 启动配置服务器：`vue ui`
- 进入 Vue 项目管理器，导入我们的项目：

<img src="https://i.loli.net/2020/03/08/SGPuoflaDrUjgQ2.png" alt="img" style="zoom:67%;" />



- 然后可以在配置中查看或修改我们的 webpack 等配置：

<img src="https://i.loli.net/2020/03/08/GmovU7cRCLKlsij.png" alt="img" style="zoom:67%;" />

2. 在 node_modules 中寻找

<img src="https://i.loli.net/2020/03/08/hHYlO8tTuNdfvxy.png" alt="img" style="zoom:67%;" />



3. 在项目中新建一个 vue.config.js 文件，将需要修改的配置代码写入其中

<img src="https://i.loli.net/2020/03/08/dMoz4aNZEBpWv28.png" alt="img" style="zoom:67%;" />

最终编译时会自动将我们添加的代码与隐藏的代码进行合并


---
title: art-template模板引擎
date: 2020-02-28 21:11:57
categories:
- 前端
tags:
- 前端
keywords:
comments:
---

<center>
<img src="https://i.loli.net/2020/02/28/5vBSzW3fjQnkLyu.png
" style="zoom: 130%;"/>

art-template 的使用方式
</center>
<!-- more -->

# 模板引擎art-template

## 安装

```shell
npm install art-template
# 该命令在哪执行就会把包下载到哪里，默认会下载到 node_modules 目录，不要修改里面的文件，也不支持改
```

[官方文档](https://aui.github.io/art-template/zh-cn/docs/installation.html)

## 模板继承

### extend

```html
<!-- index.html -->
{{extend './layout.html'}} --->显示所有 layout 页面中的内容
{{block 'head'}} ... {{/block}} ---> 重编这里面的内容
  
 <!-- layout.html -->
		内容
{{block 'head'}} 默认内容... {{/block}}
		内容
```

### include

```html
{{include './header.html'}} ---> 相当于PHP 中的 include
{{include './header.html' data}}
```

## 在浏览器中使用

```html
<!-- 注意：在浏览器中需要引用lib/template-web.js文件 
		强调：模板引擎不关心你的字符串内容，只关心自己能认识的模板标记语法，例如 {{}}(被称为 mustache 语法，八字胡)-->

<script src="../node_modules/art-template/lib/template-web.js"></script>
  <script type="text/template" id="tpl">
    大家好，我叫：{{ name }}
    我今年 {{ age }} 岁了
    我来自 {{ province }}
    我喜欢： {{each hobbies}} {{ $value }} {{/each}}
  </script>
  <script>
    var ret = template('tpl', {
      name: 'Tom',
      age: 23,
      province: '杭州市',
      hobbies: [
        '写代码',
        '唱歌',
        '打游戏'
      ]
    })
    console.log(ret);
  </script>1
```

## 在Node中使用

1. 安装文件
2. 在需要使用的文件模块中加载 `art-template`
3. 查文档，使用模板引擎的 API ( render 渲染)
4. 语法：`.render(渲染对象,替换对象)`

```javascript
var template = require('art-template')
var tplStr = `
大家好，我叫：{{ name }}
我今年 {{ age }} 岁了
我来自 {{ province }}
我喜欢： {{each hobbies}} {{ $value }} {{/each}}`
// tplStr 接受的是字符串类型
var ret = template.render(tplStr, {
  name: 'Tom',
  age: 23,
  province: '杭州市',
  hobbies: [
    '写代码',
    '唱歌',
    '打游戏'
  ]
})
//输出结果同上
console.log(ret);
```

## 在Express中使用

### 安装

```shell
npm install --save art-template
npm install --save express-art-template
```

### 使用

- 配置引擎
  - `.engine`配置使用`art-template`模板引擎
  - 第一个参数表示：当渲染以`.art`结尾的文件的时候，使用`art-template`模板引擎
  - `express-art-template`是专门用来在 `Express` 中把 `art-template`整合到`Express`中
  - 虽然外面这里不需要加载 `art-template`，但是也必须安装，原因在于`express-art-template`依赖了`art-template`
- 渲染
  - `Express`为 `Response`相应对象提供了一个方法：`render`
  - `render`方法默认是不可以使用，但是如果配置了模板引擎就可以使用了
  - 语法：`res.render('html模板名',{模板数据})`
  - 第一个参数不能写路径，默认会去项目中的 `views`目录查找该模板文件
  - 也就是说 `Express`有一个约定：开发人员把所有的视图文件都放到 `views`目录中
  - 修改默认的 `views`目录：`app.set('views',render函数的默认路径)`

```js
var express = require('express');
var app = express();

// 配置引擎
app.engine('art', require('express-art-template'));

//渲染
app.get('/', function (req, res) {  
  res.render('index.art', {})
})

app.listen(3000, function () {  
  console.log('running~')
})
```
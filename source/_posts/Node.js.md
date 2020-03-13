---
title: Node.js
date: 2020-02-28 18:54:22
categories:
- Node
tags:
- Node
keywords:
comments:
---


<center><img src="https://i.loli.net/2020/02/28/Vf9Pu8plSRAUHzN.png" style="zoom: 100%;"/> 

nodejs 学习文档</center>
<!-- more -->


# Node.js介绍

## node.js是什么

Node.js不是一门语言，不是库，不是框架，是一个`javascript`运行时环境，可以解析和执行`javascript`代码。是一个平台

- 浏览器中的`javascript`：
  - EcmaScript
  - BOM
  - DOM
- Node.js 中的`javascript`：
  - 没有`BOM`、`DOM`，服务端不处理页面(DOM)
  - `EcmaScript`
  - 在Node这个`javascript`执行环境中为`javascript`提供了一些服务器级别的`API`
    - 例如文件读写
    - 网络服务的构建
    - 网络通信
    - ……

- Node.js的特性：
  - `event-driven`事件驱动
  - `non-blocking I/O model` 非阻塞IO模型(异步)
  - `lightweight and efficient` 轻量和高效
- npm
  - npm是世界上最大的开源库生态系统
  - 绝大多数`javascript`相关的包都存放在了`npm`上，这样做的目的是为了让开发人员更方便的去下载使用
  - `npm install jquery`
- 构建在 Chrome 的 V8 引擎之上
  - 代码只是具有特定格式的字符串而已
  - 引擎可以认识它，可以帮你去解析和执行
  - Google Chrome 的 V8 引擎是目前公认的解析执行 javascript 代码最快的

## Node.js 能做什么

- Web服务器后台
- 命令行工具
- 对于前端工程师来讲，接触Node最多的是它的命令行工具
  - 自己写的很少，主要是使用别人第三方的
  - webpack
  - gulp
  - npm

## 一些资源

![image-20200202211841081.png](https://raw.githubusercontent.com/iamyujian/PicGo/master/img/image-20200202211841081.png)

## 能学习到什么

- B/S 编程模型
  - Browser - Server
  - back-end
  - 任何服务端技术这种BS编程模型都是一样，和语言无关
  - Node 只是作为我们学习BS模型的一个工具而已
- 模块化编程
- Node 常用 API
- 异步编程
- Express 开发框架
- Ecmascript 6
- ……

# node.js模块化开发

## 开发规范

- 文件操作中的相对路径可以省略 `./`，在模块加载中，相对路径中的`./`不能省略，如果省略了 `.` 则是磁盘根目录
- Nodejs 规定一个`JavaScript`文件就是一个模块，模块内部定义的变量和函数默认情况下在外部无法得到，只能得到输出结果，但是可以通过导出得到变量等数据
- 我们一个项目中有且只有一个`node_module`，放在项目根目录中
- 如果想要了解更多底层细节，可以自行参考：《深入浅出Node.js》中的模块系统章节

## 模块导出

- `exports`导出模块，是`module.exports`的引用（地址引用关系），导岀对象最终以 `module.exports` 为准，如果你实在分不清楚 `exports` 和 `module.exports` 的区别，可以忘记 exports 而只使用 `module.exports`

  - `module.exports`和`exports`的关系

    > 在 Node 中，每个模块内部都有一个自己的 module 对象，该 module 对象中，有一个成员叫：exports 也是一个对象，require 的得到的结果是 module.exports,默认在代码的最后一句：`return module.exports`
    >
    > `exports === module.exports`：exports 是 module.exports 的一个引用
    >
    > exports 的值的地址指向 module.exports 的值得指向，修改 exports 值会断开和 module.exports 的引用关系，反过来同理，但是最后 return 的是 module.exports 的值

  - 导出多个成员(必须在对象中)：

    ```js
    // 方式一：
    exports.a = 123
    exports.b = 'hello'
    
    // 方式二：
    module.exports = {
      add:function () {
        return x + y
      },
      str: 'hello'
    }
    ```

  - 导出单个成员(拿到的就是：函数、字符串)：

    ```js
    module.exports = 'hello'  //后面的会覆盖前面的
    ```


## 模块加载

[深入浅出 Node.js（三）：深入 Node.js 的模块机制](https://www.infoq.cn/article/nodejs-module-mechanism)

### 模块有路径但没有后缀时

```js
require('./find.js')
require('./find')
```
- 加载规则
1. `require` 方法根据模块路径查找模块，如果是完整路径，直接引入模块
2. 如果模块后缀省略，先找同名 JS 文件再找同名 JS 文件夹
3. 如果找到了同名文件夹，找文件夹中的 `index.js`
4. 如果文件夹中没有 `index.js` 就会去当前文件夹中的 `package.js` 文件中查找 `main` 选项中的入口文件
5. 如果找指定的入口文件不存在或者没有指定入口文件就会报错，模块没有被找到

### 模块没有路径且没有后缀时

```js
require('find')
```
- 加载规则
1. `Node.js`会假设它是系统模块
2. `Node.js`去当前文件所处目录中的`node_modules`文件夹中
3. 首先看是否有该名字的文件夹
4. 再找`package.json`文件中的`main`属性，然后加载成功
5. 如果 `package.json`文件不存在或者 `main` 指定的入口模块为空或没有
6. 则看该目录里面是否有`index.js`，有则默认加载
7. 没有则进入上一级目录中的`node_module`目录查找，如果没有，返回上上级，直到当前磁盘根目录还找不到
8. 报错：`can not find module xxx`

### 优先从缓存加载

>加载模块的时候，先看一下这个模块有没有别加载过，如果缓存里面有就直接拿，没有就从新加载
>

## 系统模块

Node运行环境提供的API.因为这些API都是以模块化的方式逬行开发的，所以我们又称Node运行环境提脚API为系统模块

![image-20200203191338074.png](https://raw.githubusercontent.com/iamyujian/PicGo/master/img/image-20200203191338074.png)

### 文件操作

 f: file 文件，s: system 系统，文件操作系统。

注意：**文件操作中的路径指的是：执行当前文件的命令工具所处的文件路径**

`const fs = require ('fs')`

- **读取文件内容**
- 语法：`fs.readFile ('文件路径'[,'文件编码'],callback);`
  
  - 读取的文件内容默认是二进制数据，可以加入第二个参数转，也可以转字符串：`toString()`

```javascript
//实例
//读取上—级css目录下中的base.css
fs.readFile('../css/base.css','utf-8' (err, doc) =>
//如果文件读取发生错误参数err的值为错误对象,否则err的值为null 
//doc參数为文件内容，失败则是 underfund 
if (err = null) {
//在控制台中输出文件内容
console.log(doc);
}
});
```

- **读取目录**

  `fs.readdir('文件路径', callback);`输出的是文件名称拼成的数组
  
- **写入文件内容**

  `fs. writeFile ('文件路径','数据',callback);`

```javascript
const content = '<h3> 正在使用 fs.writeFile 写入文件内容 </h3>';
fs.writeFile('./index.html', content, err => {
if (err != null) {
	console.log(err);
	return;
}
console .log("文件写入成功');
});
```

### 路径操作

> 使用 path 需要导入先 path 模块
> const path = require('path')

- 文件操作的相对路径
  - `./data/`：相对于当前目录
  - `data/a.txt`：相对于当前目录
  - `/data/a.txt`：绝对路径，当前文件模块所处磁盘根目录
  - `c:/xx/xx`：绝对路径

- **相对路径vs绝对路径**
  
  - 绝对路径：`path.join(__dirname, './public/')`
  - 大多数情况下使用绝对路径，因为相对路径有时候相对的是命令行工具的当前工作目录
  - 在读取文件或者设置文件路径时都会选择绝对路径
  - 使用`_dirname`获取当前文件所在的绝对路径
  
- 常用`path`方法

  - 获取目录中文件名部分，第二个参数隐藏文件后缀

    ```js
    path.basename('c:/a/b/c/index.js') // index.js
    path.basename('c:/a/b/c/index.js','.js') // index
    ```

  - 获取目录名

    ```js
    path.dirname('c:/a/b/c/index.js') // 'c:/a/b/c'
    ```

  - 获取文件后缀

    ```js
    path.extname('c:/a/b/c/index.js') // .js
    ```

  - 判断是否为绝对路径

    ```js
    path.isAbsolute('c:/a/b/c/index.js') // true
    ```

  - 解析路径，将一个路径转换为一个对象

    ```js
    path.parse('c:/a/b/c/index.js')
    /*
    {root: 'c:/'
     dir: 'c:/a/b/c'
     base: 'index.js'
     ext: '.js'
     name: 'index'
    }
    */
    ```

  - 路径拼接

    ```js
    path.join('itcast', 'a', 'b', 'c.css') // itcast\\a\\b\\c.css 
    // windows 中的路径使用反斜杠，反斜杠有转义的意思。所以使用两个
    ```

## Node 中的其他成员

> 在每个模块中，除了`require`、`exports`等模块相关 API 之外，还有两个特殊的成员，这两个成员是动态获取的路径，会随着文件的位置变化而变化

- `__dirname`：用来获取当前文件模块所属目录的绝对路径
- `__filename`：用来获取当前文件的绝对路径

## 第三方模块

- **什么是第三方模块**

  > 别人写好的、具有特定功能的，我们能直接使用的模块即第三方模块，由于第三方模块通常都是由多个文件组成并且被放置在一个文件夹中，所以又名包。

- **存在形式**

  - 以`js`文件的形式存在，提供实现项目具体功能的`API`接口。
  - 以命令行工具形式存在，辅助项目开发。

### npm

> `npm` (node package manager): node 的第三方模块管理工具
>
> [官方网站](npmjs.com)

- 常用命令

   - `npm install 模块名称 模块名称 模块名称`或者`npm i 模块名称…`：下载包

   - `npm install 模块名称@版本号`：下载固定版本的包

   - `--save`

      会在`package.json`文件中生成所安装模块的依赖信息`dependencies`，建议安装包时都加上来保存依赖项信息，简写`-S`

      npm 5 版本以后可以不用加，默认会生成依赖信息

   - `-g`：全局安装

   - `--save-dev`：表示安装的包不是必须安装的，会将包的依赖单独写在`devDependencies`中

   - 卸载

     `npm uninstall package 模块名称`：只删除，如果有依赖项会依然保存，uninstall 可以简写成 `un`

     `npm uninstall --save`：删除的时候把依赖也删除

   - 查看帮助

     `npm --help`：查看所有的命令

     `npm 命令 --help`：查看具体命令的使用帮助
   
   - 升级：`npm install --global npm`
   
   - 查看 npm 配置信息：`npm config list` 

### 替换 npm 下载地址

> npm 默认的下载地址在国外，国内下载速度慢
>
> 淘宝的开发团队把 npm 在国内做了一个备份，[网址](http://npm.taobao.org/)

- `nrm` (npm registry manager) : npm 下载地址切换工具（解决 npm 下载速度慢）

  使用步骤：

  1. 使用 `npm install nrm -g` 下载它
  2. 查询可用下载地址列表 `nrm ls`
  3. 切换 `npm` 下载地址 `nrm use` 下载地址名称 (推荐使用`taobao`)

- 使用 `cnpm`：

  1. `npm install cnpm -g`安装 cnpm

  2. 下载包时使用 cnpm 代替 npm

- 配置文件

  ```shell
  # 每次安装时在后面加入 --registry=https://registry.npm.taobao.org
  # 或在配置文件中加入，一劳永逸
  npm config set registry https://registry.npm.taobao.org
  ```

  

### nodemon

> `nodemon` 是一个命令行工具，用以辅助项目开发。在 Node.js 中，每次修改文件都要在命令行工具中重新执行该文件，非常繁琐。

使用步骤：

1. 下载： `npm install nodemon -g` 
2. 在命令行工具中用 nodemon 命令替代 node 命令执行文件
3. 终止使用 `Ctrl + c`

### Gulp

> 基于node平台开发的前端构建工具，将机械化操作编写成任务，想要执行机械化操作时执行一个命令任务就能自动执行了，用机器代替手工，提高开发效率。

- 安装：  `npm install gulp-cli -g`

- Gulp作用
  
  - 项目上线，HTML，CSS，JS文件压缩合并
  - 语法转换(es6、less…)
  - 公共文件抽离
- 修改文件浏览器自动刷新
  
- Gulp使用
  1. 使用 `npm install gulp` 下载 gulp 库文件
  2. 在项目更目录下建立 `gulpfile.js`文件
  3. 重构项目的文件夹结构 src 目录放置源代码文件 dist 目录放置构建后文件
  4. 在 `gulpfile.js` 文件中编写任务
  5. 在命令行工具中执行 gulp 文件

- gulp 中提供的方法
  - `gulp.src()`：获取任务要处理的文件
  - `gulp.dest()`：输出文件
  - `gulp.task()`：建立gulp任务
  - `gulp.watch()`：监控文件的变化
  
  通过命令行运行代码：`gulp first`
  
- gulp插件
  - `gulp-htmlmin`：HTML 文件压缩
  - `gulp-csso`：压缩 css
  - `gulp-babel`：JavaScript 语法转换
  - `gulp-less`：less语法转换
  - `gulp-uglify`：压缩混淆 JavaScript
  - `gulp-file-include`：公共文件包含
  - `browsersync`：浏览器实时同步

- gulp插件使用流程（配合npmjs.com 官网使用）

```js
//引用模块
const gulp = require('gulp');
const htmlmin = require('gulp-htmlmin');
const fileinclude = require('gulp-file-include');
const less = require('gulp-less');
const csso = require('gulp-csso');
const babel = require('gulp-babel');
const uglify = require('gulp-uglify');
// 建立任务
gulp.task('first', (done) => {
  console.log('第一个任务');
  // 获取要处理的文件
  gulp.src('./src/demo.js')
    .pipe(gulp.dest('./dist/css'));
  done();
});

// html任务
// 通过gulp插件压缩代码
gulp.task('htmlmin', (done) => {
  gulp.src('./src/*.html')

    //抽取html文件中的公共代码
    .pipe(fileinclude())

    // 通过gulp插件压缩代码
    .pipe(htmlmin({
      collapseWhitespace: true
    }))
    //输出到dist文件夹
    .pipe(gulp.dest('dist'));
  done();
});

// css任务
gulp.task('cssmin', (done) => {
  gulp.src('./src/css/a.less')
    //less转css
    .pipe(less())
    //压缩css代码
    .pipe(csso())
    //结果输出
    .pipe(gulp.dest('dist/css'))
  done();
});

//js任务
gulp.task('jsmin', (done) => {
  gulp.src('./src/demo.js')
    // 语法转换
    .pipe(babel({
      // @babel/env可以判断当前代码的运行环境，将代码转换成当前运行环境所支持的代码
      presets: ['@babel/env']
    }))
    // 压缩
    .pipe(uglify())
    // 结果输出
    .pipe(gulp.dest('dist/js'))
  done();
});

// 复制文件夹
gulp.task('copy', (done) => {
  gulp.src('./src/images/*')
    .pipe(gulp.dest('dist/images'));
    done();
});

// 构建任务,执行default时，依次执行任务
gulp.task('default', gulp.series('htmlmin', 'cssmin','jsmin','copy', done => done()));
```

### package.json文件

> - 包描述文件，记录了当前项目的信息，eg 项目名称、版本、作者、github地址、当前项目依赖了哪些第三方模块等，建议每一个项目都要有一个
> - 通过 `npm init -y`生成 ，`-y`代表生成默认信息，不加的话需要逐条手动填写信息
> - 通过`npm install`能把`package.json`中的`dependencies`中所有的依赖项都下载下来



```json
  文件会记录npm下载的模块
  
	"name": "demo",      ---项目名称
	"version": "1.0.0",  ---项目版本
	"description": "",   ---项目描述
	"main": "index.js",   ---主入口文件，主模块
 
   "scripts": {          
     "test": "echo \"Error: no test specified\" && exit 1" ---存储命令的别名，使用 npm+run+别名 使用
   },                  

   "keywords": [],     ---使用关键字描述项目
   "author": "",       ---项目作者
   "license": "ISC"      ---遵循的协议，默认isc：开放源代码

  "dependencies": {
     "csso": "^4.0.2"	---通过npm install下载的模块（项目依赖），还原使用npm install --production命令进行下载，不下载`devDependencies`中的依赖
   }
 	"devDependencies": {
     "gulp": "^3.9.1"	---通过 --save-dev下载的模块（开发依赖），可以使用npm install 命令进行下载
  }
```

![image-20200122130426646.png](https://raw.githubusercontent.com/iamyujian/PicGo/master/img/image-20200122130426646.png)
![image-20200122130538922.png](https://raw.githubusercontent.com/iamyujian/PicGo/master/img/image-20200122130538922.png)

通过命令`npm install`可以下载项目所需要的所有的依赖

`npm install --production` 下载项目运行所需要的依赖，而不下载开发依赖

### package-lock.json文件

> npm 版本 5 以前没有这个文件，5 后面版本会自动生成这个文件
>
> 当你安装包的时候，会自动更新这个文件
>
> 当下载模块后会自动生成，主要记录模块与模块之间的依赖关系，保存了所有包的信息，有这个文件重载 node_modules 时会更快
>
> 锁定包的版本号，防止自动升级到新版

```json
"dependencies": {
    "@babel/code-frame": {
      "version": "7.8.3", ---版本
      "resolved": "https://registry.npm.taobao.org/@babel/code-frame/download/@babel/code-frame-7.8.3.tgz", ---地址
      "integrity": "sha1-M+JZA9dIEYFTThLsCiXxa2/PQZ4=",
      "requires": {
        "@babel/highlight": "^7.8.3"
      }
    }
```

# 创建web服务器

## IP地址和端口号

- IP地址用来定位计算机
- 端口号来定位具体的应用程序
- 一切需要联网通信的软件都会占用一个端口号
- 端口号的范围从 0 - 65536 之间
- 在计算机中有一些默认端口号，最好不要去使用 eg：http 服务中的 80
- 我们在开发过程中使用一些简单好记的就可以了，例如3000，5000等没什么含义的
- 可以同时开启多个服务，但一定要确保不同服务端口号不一致才可以，在一台计算机中，同一个端口号同一时间只能被一个程序占用

## 建立服务器

- nodejs是基于事件驱动的语言，当客户端有请求的时候，这个请求在服务端是通过事件来触发的

- 在服务端默认发送的数据，其实是 utf8 编码的内容，但是浏览器不知道你是 utf8 编码内容，此时浏览器会按照当前操作系统的默认编码(gbk)去解析，所以中文就会乱码

  解决：`res.setHeader('Content-Type', 'text/plain; charset=utf-8')`，图片格式的内容不需要设置编码格式，会报错

- Content-Type：不同的资源对应的 Content-Type 是不一样的

   图片类型不需要指定编码，一般只为字符数据才指定编码格式
   
   类型选择对照表：https://tool.oschina.net/ --> HTTP Mine-type

``` javascript
//用于创建网站服务器的系统模块
const http = require('http')

// app对象就是网站服务器对象
const app = http.createServer()

// 通过on为网站服务器对象添加请求对象，请求名称为request，当有请求的时候，执行后面的事件处理函数,req中保存着请求相关的信息，通过res对象下的方法对客户端进行响应
app.on('request', (req,res) => {
  // req.method来获取请求方式
  //req.url 来获取请求地址，默认是 /

  //告诉浏览器编码格式
  res.setHeader('Content-Type', 'text/plain; charset=utf-8')

  //res.end后的响应内容只能是二进制数据或者字符串(JSON.stringifoy转换)
  res.end('<h2>hello user</h2>')
})

//网站服务器建立好后，必须要监听一个端口来对外进行服务
app.listen(3000);
console.log('网站服务器启动成功！')

//上面的简写方式
const http = require('http')
http
  .createServer(function (req, res) {
    res.end('hello')
  })
  .listen(3000, function () {
    console.log('running...');
  })
```
![image-20200122141535489.png](https://raw.githubusercontent.com/iamyujian/PicGo/master/img/image-20200122141535489.png)
![image-20200122141600511.png](https://raw.githubusercontent.com/iamyujian/PicGo/master/img/image-20200122141600511.png)

## url

> `url.parse(地址,true)`：解析地址中的内容，得到的是一个 url 对象
>
> true：将对象中的 query 的值(字符串)转换成对象
>
> pathname：路径中 ? 之前的路径内容

```JS
var url = require('url');
var a = url.parse('http://localhost:8080/one?a=index&t=article');
console.log(a);

//输出结果：
{ 
    protocol : 'http' ,
    auth : null ,
    host : 'localhost:8080' ,
    port : '8080' ,
    hostname : 'localhost' ,
    hash : null ,
    search : '?a=index&t=article',
    query : 'a=index&t=article',
    pathname : '/one',
    path : '/one?a=index&t=article',
    href : 'http://localhost:8080/one?a=index&t=article'
}
```

> `JSON.stringfy()`：将 JavaScript 对象转换为字符串，也可以将 JavaScript 数组转换为 JSON 字符串

> `req.method` 来获取请求方式
> `req.url` 来获取请求地址
> `req.headers` 获取请求报文（res.headers['accept']）
> `res.writeHead(200,'content-type': 'text/html;charset=utf8')` 编写响应报文的信息


## 重定向

> 如何通过服务器让客户端重定向？
>
> 1. 状态码设置成 302 (临时重定向)，301是永久重定向
> 2. 在响应头中通过 `Location` 告诉客户端往哪儿重定向
>
> 如果客户端发现收到服务器的响应的状态码是 302 就会自动去响应头中找 Location ，然后对该地址发起新的请求
>
> 服务端重定向只针对同步请求才有效，异步请求无效，这时候可以使用客户端跳转：`window.location.href = '/'`

```js
// 方法一：
res.statusCode = 302
res.setHeader('Location', '/')
// 方法二：
res.redirect('/')

```

## 案例：留言板

```js
const http = require('http')
const fs = require('fs')
const template = require('art-template')
const url = require('url')

var comments = [{
    name: '张三',
    message: '今天天气不错！',
    datatime: '2020-10-14'
  },
  {
    name: '李四',
    message: '今天天气不错！+1',
    datatime: '2020-10-14'
  },
  {
    name: '王五',
    message: '今天天气不错！+2',
    datatime: '2020-10-14'
  },
  {
    name: '钢蛋',
    message: '今天天气不错！+3',
    datatime: '2020-10-14'
  }
]

http
  .createServer(function (req, res) {
    // 得到路径对象
    let parseObj = url.parse(req.url, true)
    let pathname = parseObj.pathname
    if (pathname === '/' || pathname === '/index') {
      fs.readFile('./views/index.html', function (err, data) {
        if (err) {
          return res.end('404 Not Found')
        }
        // 渲染
        var htmlStr = template.render(data.toString(), {
          comments: comments
        })
        res.end(htmlStr)
      })
      // 设置请求资源文件路径，公开静态资源目录public
    } else if (pathname.indexOf('/public/') === 0) {
      fs.readFile('.' + pathname, function (err, data) {
        if (err) {
          return res.end('404 Not Found')
        }
        res.end(data)
      })
    } else if (pathname === '/post') {
      fs.readFile('./views/post.html', function (err, data) {
        if (err) {
          return res.end('404 Not Found')
        }
        res.end(data)
      })
    } else if (pathname === '/comment') {
        // 将当前时间日期添加到数据对象中，然后存储到数组中
        let comment = parseObj.query
        comment.datatime = '2019-11-2 15:11:12'
        comments.unshift(comment)
        // 重定向(设置状态码和响应头)
        res.statusCode = 302
        res.setHeader('Location', '/')
        res.end()
    } else {
      fs.readFile('./views/404.html', function (err, data) {
        if (err) {
          return res.end('404 Not Found')
        }
        res.end(data)
      })
    }
  })

  .listen(3000, function () {
    console.log('running...');
  })
```

# Express框架

> 原生的 http 在某些方面表现不足以应对我们的开发需求，所以我们就需要使用框架来加快我们的开发效率，框架的目的就是提高效率，让我们的代码更高度统一
>
> 在 Node 中，有很多 Web 开发框架，我们这里以学习 express 为主
>
> [官方网址](http://expressjs.com/)

## 安装

```shell
npm install express --save
```

## 使用

### hello world

```json
const express = require('express')

let app = express()

// 公开指定目录，可以通过 /public/xx 的方式访问 public 目录中的所有资源
app.use('/public/', express.static('./public/'))

// 基本路由，当服务器收到 get 请求 / 的时候，执行
app.get('/', function (req, res) {  
  res.send('hello world!')
})

// 基本路由，当服务器收到 post 请求 / 的时候，执行
app.post('/', function (req, res) {  
  res.send('hello world!')
})

app.listen(3000, function () {  
  console.log('running~');
})
```

### 接收表单数据

- `get`请求

  > express 内置了一个 API ，可以直接通过 `req.query`来获取

  ```js
  app.get('/comment',function (req, res) {
    // 获取 url 地址中传递的参数
    let comment = req.query
  }
  ```

- `post`请求

  > 在 Express 中没有内置获取表单 POST 请求体的 API ，这里我们需要使用一个第三方包：`body-parser`
  >
  > [官方文档](http://expressjs.com/en/resources/middleware/body-parser.html)

  - 安装

    ```shell
    npm install --save body-parser
    ```

  - 配置

    ```js
    var express = require('express')
    // 引包
    var bodyParser = require('body-parser')
    var app = express()
    
    // 配置 body-parser
    // 只要加入这个配置，则在 req 请求对象上会多出来一个属性：body，通过 req.body 来获取表单 POST 请求体数据了
    // parse application/x-www-form-urlencoded
    app.use(bodyParser.urlencoded({ extended: false }))
    app.use(bodyParser.json())
    // 第二种方式
    var jsonParser = bodyParser.json()
    var urlencodedParser = bodyParser.urlencoded({ extended: false })
    
    // 使用
    // POST /login gets urlencoded bodies
    app.post('/login', function (req, res) {
      res.send('welcome, ' + req.body.username)
    })
    // POST /api/users gets JSON bodies
        app.post('/api/users', jsonParser, function (req, res) {
        })    
    
    ```
### 路由处理

> 将所有路由代码单独写到一个文件中

```js
// 文件 router.js
const express = require('express')
// 创建一个路由容器
let router = express.Router()
// 把路由都挂载到 router 路由容器中
router.get('./student', function (req, res) {})
// 将 router 导出
module.exports = router

// 文件 app.js 挂载路由
const router = require('./router')
// 挂载 放到配置信息后面
app.use(router)
```

### session

> 在 Express 这个框架中，默认不支持 Session 和 Cookie，但是我们可以使用第三方中间件：`express-session`来解决。

- 安装：`npm install express-session`

- 使用：

  添加 Session 数据：`req.session.foo = 'bar'`
  
  访问 Session 数据：`req.session.foo`

  清除：`req.session.foo = null`,对象还在
  删除：`delete req.session.xxx`
  
  Session 数据是存储在内存中的，服务器重启后就会消失，真正的生产环境会进行持久化存储
  
  `secret`: 配置加密字符串，它会在原有加密基础之上和这个字符串拼起来其加密，目的是为了增加安全性，防止客户端恶意伪造
  
  `saveUninitialized`: 决定是否默认分配一把钥匙。默认为 true
  
  ```js
  const session = require('express-session')
  
  // 配置 session 
  app.use(session({
    secret: 'keyboard cat',
    resave: false,
    saveUninitialized: false 
  }))
  ```
  

### 中间件
当请求进来，会从第一个中间件开始进行匹配，如果匹配则进来，如果进入了却没有调用 next 则不会进行下一个
在 Express 中，对中间件有几种分类
1. 不关心请求路径和请求方法的中间件,也就是说任何请求都会进入这个中间件,中间件本身是一个方法，该方法接受三个参数

   - `Request` 请求对象
   - `Response` 响应对象
   - `next` 下一个中间件,不加这个会默认执行第一个，不会往下执行，加上会执行下一个中间件，next 可以进行匹配调用后面的，而不是一定是执行紧挨着的下一个

    ```js
    app.use(function (req, res, next) {
      console.log('1')
      next()
    })
    app.use(function (req, res, next) {
      console.log('2')
    })
    //1 2

    // next 传错误对象
     app.use(function (req, res, next) {
      console.log('1')
      next(err)
    })
    app.use(function (req, res, next) {
      console.log('2')
    })
    app.use(function (err, req, res, next) {  
      console.log('错误信息')
    }) 
    // 输出为：错误信息
    ```
2. 以 /xx 开头的路径中间件
   ```js
   // 以 /b 开头的路径都可以访问
   app.use('/b',function (req,res, next) {  
     console.log(req.url) // /b 后面的路径
   })
   ```
3. 严格匹配请求方法和请求路径的中间件
   ```js
   app.get('/', function (req, res, next) {  })
   ```




## 案例：留言板

  ```js
  const express = require('express')
  const bodyParser = require('body-parser')
  let app = express()
  
  var comments = [{
      name: '张三',
      message: '今天天气不错！',
      datatime: '2020-10-14'
    },
    {
      name: '李四',
      message: '今天天气不错！+1',
      datatime: '2020-10-14'
    },
    {
      name: '王五',
      message: '今天天气不错！+2',
      datatime: '2020-10-14'
    },
    {
      name: '钢蛋',
      message: '今天天气不错！+3',
      datatime: '2020-10-14'
    }
  ]
  
  // 配置模板引擎
  app.engine('html', require('express-art-template'))
  
  // 配置接受 post 请求体
  var jsonParser = bodyParser.json()
  var urlencodedParser = bodyParser.urlencoded({
    extended: false
  })
  
  // 开放文件资源
  app.use('/public/', express.static('./public/'))
  
  app.get('/', function (req, res) {
    res.render('index.html', {
      comments: comments
    })
  })
  
  app.get('/post', function (req, res) {
    res.render('post.html')
  })
  
  app.get('/index', function (req, res) {
    res.render('index.html')
  })
  
  // 接受 get 提交的请求
  // app.get('/comment',function (req, res) {
  //   // 获取 url 地址中传递的参数
  //   let comment = req.query
  //   comments.datatime = '2012-12-3'
  //   comments.unshift(comment)
  //   // 重定向
  //   res.redirect('/')
  // })
  
  // 接受 post 提交的请求
  app.post('/comment', urlencodedParser,function (req, res) {
    // 获取 请求体中的数据
    let comment = req.body
    comments.datatime = '2012-12-3'
    comments.unshift(comment)
    // 重定向
    res.redirect('/')
  })
  
  app.listen(3000, function () {
    console.log('running!');
  })
  ```

## 案例：crud

> 实现文件的增删改查

### 效果图

![image-20200208212828302.png](https://raw.githubusercontent.com/iamyujian/PicGo/master/img/image-20200208212828302.png)

### 文档结构图

```
crud-express
│  app.js				───────────── 项目启动文件
│  db.json			───────────── 数据文件
│  operate-data.js	───────── 数据操作文件
│  package-lock.json	───────	项目依赖
│  package.json	─────────────	项目信息
│  
├─node_modules	─────────────	包
│          
├─public				─────────────	公用文件
│  ├─css
│  │      dashboard.css
│  │      
│  └─js
│          router.js ──────── 路由文件
│          
└─views		───────────────────	视图文件夹
        add.html ──────────── 数据添加页面
        edit.html	─────────── 修改页面
        index.html	───────── 入口页面
```

### 项目依赖

```json
"dependencies": {
    "art-template": "^4.13.2",
    "body-parser": "^1.19.0",
    "bootstrap": "^3.3.7",
    "express": "^4.17.1",
    "express-art-template": "^1.0.1"
  }
```

### 路由设计

| 请求方法 | 请求路径 | get 参数 |         post 参数          |     备注     |
| :------: | :------: | :------: | :------------------------: | :----------: |
|   GET    |    /     |          |                            |   渲染首页   |
|   GET    |   /add   |          |                            | 渲染添加页面 |
|   POST   |   /add   |          | name、age、gender、hobbies | 处理添加请求 |
|   GET    |  /edit   |    id    |                            | 渲染编辑页面 |
|   POST   |  /edit   |          |                            | 处理编辑请求 |
|   GET    | /delete  |    id    | name、age、gender、hobbies | 处理删除请求 |

### views

#### head信息

> 所有 html 页面头信息一样

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
  <meta name="description" content="">
  <meta name="author" content="">
  <link rel="icon" href="../../favicon.ico">

  <title>Dashboard Template for Bootstrap</title>
  <!-- Bootstrap core CSS -->
  <link href="/node_modules/bootstrap/dist/css/bootstrap.css" rel="stylesheet">
  <link href="/public/css/dashboard.css" rel="stylesheet">
</head>
</html>
```

#### index.html

```html
<body>
  <div class="container-fluid">
    <h2 class="sub-header">Section title</h2>
    <a href="/add" class="btn btn-success">添加信息</a>
    <div class="table-responsive">
      <table class="table table-striped">
        <thead>
          <tr>
            <th>#</th>
            <th>姓名</th>
            <th>性别</th>
            <th>年龄</th>
            <th>爱好</th>
            <th>操作</th>
          </tr>
        </thead>
        <tbody>
          {{ each students }}
          <tr>
            <td>{{ $value.id }}</td>
            <td>{{ $value.name }}</td>
            <td>{{ $value.gender }}</td>
            <td>{{ $value.age }}</td>
            <td>{{ $value.hobbies }}</td>
            <td>
              <a href="/edit?id={{ $value.id }}">编辑</a>
              <a href="/delete?id={{ $value.id }}">删除</a>
            </td>
          </tr>
          {{/each}}
        </tbody>
      </table>
    </div>
</body>
```

#### add.html

```html
<body>
  <div class="container-fluid">
    <h2 class="sub-header">添加信息</h2>
    <form method="POST" action="/add">
      <div class="form-group">
        <label for="names">姓名</label>
        <input type="text" class="form-control" id="names" minlength="2" maxlength="6" name="name">
      </div>
      <div class="form-group">
        <label for="">性别：</label>

        <label class="radio-inline">
          <input type="radio" name="gender" id="man" value="男"> 男
        </label>
        <label class="radio-inline">
          <input type="radio" name="gender" id="girl" value="女"> 女
        </label>
      </div>
      <div class="form-group">
        <label for="age">年龄</label>
        <input type="number" class="form-control" id="age" maxlength="2" name="age">
      </div>

      <div class="form-group">
        <label for="">爱好：</label>
        <label class="checkbox-inline">
          <input type="checkbox" id="inlineCheckbox1" value="吃饭" name="hobbies"> 吃饭
        </label>
        <label class="checkbox-inline">
          <input type="checkbox" id="inlineCheckbox2" value="睡觉" name="hobbies"> 睡觉
        </label>
        <label class="checkbox-inline">
          <input type="checkbox" id="inlineCheckbox3" value="打豆豆" name="hobbies"> 打豆豆
        </label>
      </div>
      <button type="submit" class="btn btn-success">Submit</button>
    </form>
  </div>
</body>
```

#### edit.html

```html
<body>
  <div class="container-fluid">
    <h2 class="sub-header">添加信息</h2>
    <form method="POST" action="/edit">
      <div class="form-group">
        <!-- 设置隐藏提交给服务器的信息 -->
        <input type="hidden" name="id" value="{{ student.id }}">
        <label for="names">姓名</label>
        <input type="text" class="form-control" id="names" minlength="2" maxlength="6" name="name"
          value="{{ student.name }}">
      </div>
      <div class="form-group">
        <label for="">性别：</label>

        <label class="radio-inline">
          <input type="radio" name="gender" id="man" value="男"> 男
        </label>
        <label class="radio-inline">
          <input type="radio" name="gender" id="girl" value="女"> 女
        </label>
      </div>
      <div class="form-group">
        <label for="age">年龄</label>
        <input type="number" class="form-control" id="age" maxlength="2" name="age" value="{{ student.age }}">
      </div>

      <div class="form-group">
        <label for="">爱好：</label>
        <label class="checkbox-inline">
          <input type="checkbox" id="inlineCheckbox1" value="吃饭" name="hobbies"> 吃饭
        </label>
        <label class="checkbox-inline">
          <input type="checkbox" id="inlineCheckbox2" value="睡觉" name="hobbies"> 睡觉
        </label>
        <label class="checkbox-inline">
          <input type="checkbox" id="inlineCheckbox3" value="打豆豆" name="hobbies"> 打豆豆
        </label>
      </div>
      <button type="submit" class="btn btn-success">Submit</button>
    </form>
  </div>
  </div>
</body>
```

### db.json

```json
{
  "students": [
    {
      "id": 2,
      "name": "张三",
      "gender": 0,
      "age": 18,
      "hobbies": "吃饭、睡觉、打豆豆"
    },
    {
      "id": 3,
      "name": "张三",
      "gender": 0,
      "age": 18,
      "hobbies": "吃饭、睡觉、打豆豆"
    }
  ]
}
```

### app.js

```js
const express = require('express')
const fs = require('fs')
const router = require('./public/js/router')
const bodyParser = require('body-parser')

let app = express()
// 配置模板引擎
app.engine('html', require('express-art-template'));

// 配置body-parser
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())

// 挂载路由
app.use(router)

app.listen(3000, function () {  
  console.log('running...');
}) 
```

### router.js

```js
const express = require('express')
const fs = require('fs')
const operate_data = require('../../operate-data')

// 生成路由容器
let router = express.Router()

//开放资源文件夹
router.use('/node_modules/',express.static('./node_modules/'))
router.use('/public/', express.static('./public/'))

// 渲染首页
router.get('/', function (req, res) {
  // 这里将数据操作封装成函数调用
  operate_data.find(function (err, data) {
    if (err) {
      return res.status(500).send('Server error.')
    }
    res.render('index.html', {
      // data数据是字符串，转成对象
      students: data
    })
  })
})

// 渲染添加页面
router.get('/add', function (req, res) {
  res.render('add.html')
})

// 处理添加请求
router.post('/add', function (req, res) {
  let student = req.body
  operate_data.save(student, function (err) {
    if (err) {
      return res.status(500).send('Server error.')
    }
    res.redirect('/')
  })
})

// 渲染编辑页面
router.get('/edit', function (req, res) {
  operate_data.findById(parseInt(req.query.id), function (err, student) {
    if (err) {
      return res.status(500).send('Server error.')
    }
    res.render('edit.html', {
      student: student
    })

  })
})

// 处理编辑请求
router.post('/edit', function (req, res) {
  operate_data.updataById(req.body, function (err) {
    if (err) {
      return res.status(500).send('Server error.')
    }
    res.redirect('/')
  })
  // console.log(req.body);
})

// 处理删除请求
router.get('/delete', function (req, res) {
  let id = req.query.id
  operate_data.delect(id, function (err) {
    if (err) {
      return res.status(500).send('Server error.')
    }
    res.redirect('/')
  })

})
// 导出路由
module.exports = router
```

### operate-data.js (难点)

> 封装了数据增删改查操作，对异步请求数据的获取方式：回调函数

```js
const fs = require('fs')

let dbpath = './db.json'
/**
 * 获取数据
 * 通过回调函数的方式获取异步读取文件的数据
 **/
exports.find = function (callback) {
  fs.readFile(dbpath, 'utf8', function (err, data) {
    if (err) {
      return callback(err)
    }
    // null 是为了区分 err
    callback(null, JSON.parse(data).students)
  })
}

/**
 *通过 ID 获取数据 
 */
exports.findById = function (id, callback) {
  fs.readFile(dbpath, 'utf8', function (err, data) {
    if (err) {
      return callback(err)
    }
    let students = JSON.parse(data).students
    let ret = students.find(function (item) {
      return item.id === parseInt(id)
    })
    callback(null, ret)
  })
}

/**
 * 保存数据
 **/
exports.save = function (student, callback) {
  fs.readFile(dbpath, 'utf8', function (err, data) {
    if (err) {
      return callback(err)
    }
    let students = JSON.parse(data).students
    student.id = students[students.length - 1].id + 1
    students.push(student)
    // 将字符串转为对象
    let fileData = JSON.stringify({
      students: students
    })
    // 将对象数据写入文件
    fs.writeFile(dbpath, fileData, function (err) {
      if (err) {
        return callback(err)
      }
      callback(null)
    })
  })
}

/**
 * 更新数据
 **/
exports.updataById = function (student, callback) {
  fs.readFile(dbpath, 'utf8', function (err, data) {
    if (err) {
      return callback(err)
    }
    let students = JSON.parse(data).students
    student.id = parseInt(student.id)
    // es6的数组方法，如果item.id === student.id 条件的时候，find 会终止遍历，同时返回 item 
    let stu = students.find(function (item) {
      return item.id === student.id
    })
    for (let key in student) {
      stu[key] = student[key]
    }

    let fileData = JSON.stringify({
      students: students
    })
    fs.writeFile(dbpath, fileData, function (err) {
      if (err) {
        return callback(err)
      }
      callback(null)
    })
  })

}

/**
 * 删除
 **/
exports.delect = function (id, callback) {
  fs.readFile(dbpath, 'utf8', function (err, data) {
    if (err) {
      return callback(err)
    }
    let students = JSON.parse(data).students
		// es6的数组方法，如果item.id === id 条件的时候，会终止遍历，同时返回 item 的下标
    let delected = students.findIndex(function (item) {
      return item.id === parseInt(id)
    })
    students.splice(delected, 1)
    let fileData = JSON.stringify({
      students: students
    })
    fs.writeFile(dbpath, fileData, function (err) {
      if (err) {
        return callback(err)
      }
      callback(null)
    })
  })
}
```


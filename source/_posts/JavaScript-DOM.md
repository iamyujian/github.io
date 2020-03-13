---
title: JavaScript-DOM
date: 2020-02-28 17:17:47
categories:
- 前端
tags:
- JS
- 前端
keywords:
comments:
---

<center>
<img src="https://i.loli.net/2020/02/28/WRMC4fdvBxYN9rw.jpg" style="zoom: 15%;"/>


JavaScript 中的 DOM 操作
</center>
<!-- more -->

学习目标:

  - 掌握API和Web API的概念
  - 掌握常见浏览器提供的API的调用方式
  - 能通过Web API开发常见的页面交互功能
  - 能够利用搜索引擎解决问题

# Web API介绍

## API的概念

API（Application Programming Interface,应用程序编程接口）是一些预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力，而又无需访问源码，或理解内部工作机制的细节。

- 任何开发语言都有自己的API
- API的特征输入和输出(I/O)
  - var max =  Math.max(1, 2, 3);
- API的使用方法(console.log('adf'))

## Web  API的概念

浏览器提供的一套操作浏览器功能和页面元素的API(BOM和DOM)

此处的Web API特指浏览器提供的API(一组方法)，Web API在后面的课程中有其它含义


## 掌握常见浏览器提供的API的调用方式
[MDN-Web API](https://developer.mozilla.org/zh-CN/docs/Web/API)

## JavaScript的组成

## ECMAScript - JavaScript的核心 

定义了JavaScript 的语法规范

JavaScript的核心，描述了语言的基本语法和数据类型，ECMAScript是一套标准，定义了一种语言的标准与具体实现无关

## BOM - 浏览器对象模型

一套操作浏览器功能的API

通过BOM可以操作浏览器窗口，比如：弹出框、控制浏览器跳转、获取分辨率等 

## DOM - 文档对象模型

一套操作页面元素的API

DOM可以把HTML看做是文档树，通过DOM提供的API可以对树上的节点进行操作

# DOM

## DOM的概念 

文档对象模型（Document Object Model，简称DOM），是[W3C](https://baike.baidu.com/item/W3C)组织推荐的处理[可扩展标记语言](https://baike.baidu.com/item/%E5%8F%AF%E6%89%A9%E5%B1%95%E7%BD%AE%E6%A0%87%E8%AF%AD%E8%A8%80)的标准[编程接口](https://baike.baidu.com/item/%E7%BC%96%E7%A8%8B%E6%8E%A5%E5%8F%A3)。它是一种与平台和语言无关的[应用程序接口](https://baike.baidu.com/item/%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E6%8E%A5%E5%8F%A3)(API),它可以动态地访问程序和脚本，更新其内容、结构和[www](https://baike.baidu.com/item/www/109924)文档的风格(目前，HTML和XML文档是通过说明部分定义的)。文档可以进一步被处理，处理的结果可以加入到当前的页面。[DOM](https://baike.baidu.com/item/DOM/50288)是一种基于树的[API](https://baike.baidu.com/item/API/10154)文档，它要求在处理过程中整个文档都表示在[存储器](https://baike.baidu.com/item/%E5%AD%98%E5%82%A8%E5%99%A8)中。

DOM又称为文档树模型

![](https://i.loli.net/2020/02/28/H6MmLqSBtR3wAon.png)


- 文档：一个网页可以称为文档
- 节点：网页中的所有内容都是节点（标签、属性、文本、注释等）
- 元素：网页中的标签
- 属性：标签的属性

## DOM经常进行的操作

- 获取元素
- 对元素进行操作(设置其属性或调用其方法)
- 动态创建元素
- 事件(什么时机做相应的操作)

# 获取页面元素

## 根据id获取元素

```javascript
var div = document.getElementById('main');
console.log(div);

// 获取到的数据类型 HTMLDivElement，对象都是有类型的
```

注意：由于id名具有唯一性，部分浏览器支持直接使用id名访问元素，但不是标准方式，不推荐使用。

## 根据标签名获取元素

```javascript
var divs = document.getElementsByTagName('div');
for (var i = 0; i < divs.length; i++) {
  var div = divs[i];
  console.log(div);
} 
```

## 根据name获取元素*

```javascript
var inputs = document.getElementsByName('hobby');
for (var i = 0; i < inputs.length; i++) {
  var input = inputs[i];
  console.log(input);
}
```

## 根据类名获取元素*

```javascript
var mains = document.getElementsByClassName('main');
for (var i = 0; i < mains.length; i++) {
  var main = mains[i];
  console.log(main);
}
```

## 根据选择器获取元素*

```javascript
var text = document.querySelector('#text');
console.log(text);

var boxes = document.querySelectorAll('.box');
for (var i = 0; i < boxes.length; i++) {
  var box = boxes[i];
  console.log(box);
}
```

- 总结

```
掌握
	getElementById()
	getElementsByTagName()
了解
	getElementsByName()
	getElementsByClassName()
	querySelector()
	querySelectorAll()
```

# 事件

事件：触发-响应机制

## 事件三要素

- 事件源:触发(被)事件的元素
- 事件名称: click 点击事件
- 事件处理程序:事件触发后要执行的代码(函数形式)

## 事件的基本使用

```javascript
var box = document.getElementById('box');
box.onclick = function() {
  console.log('代码会在box被点击后执行');  
};
```

# 属性操作

## 非表单元素的属性

- innerHTML和innerText

```javascript
var box = document.getElementById('box');
box.innerHTML = '我是文本<p>我会生成为标签</p>';
console.log(box.innerHTML);
box.innerText = '我是文本<p>我不会生成为标签</p>';
console.log(box.innerText);
```
- HTML转义符

```
"		&quot;
'		&apos;
&		&amp;
<		&lt;   // less than  小于
>		&gt;   // greater than  大于
空格	   &nbsp;
©		&copy;
```

- innerHTML和innerText的区别

``` 
都可以设置标签的文本内容,如果要设置标签及内容推荐使用innerHTML。
如果要获取标签中的文本,innerText,也可以使用innerHTML。
如果想要获取的是有标签,也有文本---innerHTML。
```



- innerText的兼容性处理


## 表单元素属性

- value 用于大部分表单元素的内容获取(option除外)
- type 可以获取input标签的类型(输入框或复选框等)
- disabled 禁用属性
- checked 复选框选中属性
- selected 下拉菜单选中属性

## 自定义属性操作

标签原本没有这个属性,为了存储数据,程序员自己添加的属性。自定义属性无法直接通过DOM对象的方式获取或者设置。

```
对象.getAttribute("自定义属性名字");获取自定义属性的值。
对象.setAttribute("属性名字","值");设置自定义属性及值。
对象.removeAttribute("属性的名字");移除自定义属性。
```

## 样式操作

- 使用style方式设置的样式显示在标签行内
```javascript
var box = document.getElementById('box');
box.style.width = '100px';
box.style.height = '100px';
box.style.backgroundColor = 'red';
```

- 注意

  通过样式属性设置宽高、位置的属性类型是字符串，需要加上px

## 类名操作

- 修改标签的className属性相当于直接修改标签的类名
```javascript
var box = document.getElementById('box');
box.className = 'show';
```


# 创建元素的三种方式

## document.write()

```javascript
//如果在页面加载完毕后创建元素.页面中的内容会被干掉。
document.write('新设置的内容<p>标签也可以生成</p>');
```

## innerHTML

```javascript
var box = document.getElementById('box');
box.innerHTML = '新内容<p>新标签</p>';
```

## document.createElement()

```javascript
var div = document.createElement('div');
父级元素.appendChild(div);
父级元素.removeChild(要干掉的子级元素对象);
```

## 性能问题

- innerHTML方法由于会对字符串进行解析，需要避免在循环内多次使用。
- 可以借助字符串或数组的方式进行替换，再设置给innerHTML
- 优化后与document.createElement性能相近

# 节点操作

```javascript
var body = document.body;
var div = document.createElement('div');
body.appendChild(div);

var firstEle = body.children[0];
body.insertBefore(div, firstEle);

body.removeChild(firstEle);

var text = document.createElement('p');
body.replaceChild(text, div);
```

## 节点属性

- nodeType  节点的类型
  - 1 元素节点
  - 2 属性节点
  - 3 文本节点 
- nodeName  节点的名字:标签节点---大写的标签名字,属性节点---小写的属性名字,文本节点----#text
- nodeValue  节点的值:标签节点---null,属性节点---属性值,文本节点---文本内容
  - 元素节点的nodeValue始终是null

## 节点层级

```javascript
var box = document.getElementById('box');
  //父级节点
console.log(box.parentNode);
//父级元素
console.log(ulObj.parentElement);
 //子节点
console.log(box.childNodes);
  //子元素
console.log(box.children);
  //某个元素的后一个兄弟节点
console.log(box.nextSibling);
  //某个元素的后一个兄弟元素
  console.log(my$("three").nextElementSibling);
 //某个元素的前一个兄弟节点
console.log(box.previousSibling);
 //某个元素的前一个兄弟元素
  console.log(my$("three").previousElementSibling);
  //第一个子节点,IE8中是第一个子元素
console.log(box.firstChild);
//第一个子元素,IE8中不支持
console.log(ulObj.firstElementChild);
  //最后一个子节点,IE8中是第一个子元素
console.log(box.lastChild);
 //最后一个子元素,IE8中不支持
  console.log(ulObj.lastElementChild);
```

- 注意

  childNodes和children的区别，childNodes获取的是子节点，children获取的是子元素

  nextSibling和previousSibling获取的是节点，获取元素对应的属性是nextElementSibling和previousElementSibling获取的是元素。

  nextElementSibling和previousElementSibling有兼容性问题，IE9以后才支持。

  总结:凡是获取节点的代码在谷歌和火狐得到的都是  相关的节点。
  凡是获取元素的代码在谷歌和火狐得到的都是   相关的元素。
  从子节点和兄弟节点开始,凡是获取节点的代码在IE8中得到的是元素,获取元素的相关代码,在IE8中得到的是undefined----元素的代码,iE中不支持。

- 总结

```
节点操作，方法
	appendChild()
	insertBefore()
	removeChild()
	replaceChild()
节点层次，属性
	parentNode
	childNodes
	children
	nextSibling/previousSibling
	firstChild/lastChild
```

# 事件详解

## 注册/移除事件的三种方式

```javascript
//对象.on事件类型=事件处理函数;
var box = document.getElementById('box');
box.onclick = function () {
  console.log('点击后执行');
};
box.onclick = null;

//对象.addEventListener("没有on的事件类型",事件处理函数,false);IE8不支持
box.addEventListener('click', eventCode, false);
box.removeEventListener('click', eventCode, false);

//对象.attachEvent("有on的事件类型",事件处理函数);谷歌和火狐不支持
box.attachEvent('onclick', eventCode);
box.detachEvent('onclick', eventCode);
```

## 兼容代码

```javascript
function addEventListener(element, type, fn) {
  if (element.addEventListener) {
    element.addEventListener(type, fn, false);
  } else if (element.attachEvent){
    element.attachEvent('on' + type,fn);
  } else {
    element['on' + type] = fn;
  }
}

function removeEventListener(element, type, fn) {
  if (element.removeEventListener) {
    element.removeEventListener(type, fn, false);
  } else if (element.detachEvent) {
    element.detachEvent('on' + type, fn);
  } else {
    element['on'+type] = null;
  }
}
```

## 事件的三个阶段

1. 捕获阶段

2. 当前目标阶段

3. 冒泡阶段

   事件对象.eventPhase属性可以查看事件触发时所处的阶段

## 事件对象的属性和方法

window.event就是事件参数对象----e是一样的

- event.type 获取事件类型
- clientX/clientY     所有浏览器都支持，窗口位置
- pageX/pageY       IE8以前不支持，页面位置
- event.target || event.srcElement 用于获取触发事件的元素
- event.preventDefault() 取消默认行为

## 阻止事件传播的方式

- 标准方式 event.stopPropagation();
- IE低版本 event.cancelBubble = true; 标准中已废弃

## 常用的鼠标和键盘事件

- onmouseup 鼠标按键放开时触发
- onmousedown 鼠标按键按下触发
- onmousemove 鼠标移动触发
- onkeyup 键盘按键按下触发
- onkeydown 键盘按键抬起触发


# BOM

## BOM的概念

BOM(Browser Object Model) 是指浏览器对象模型，浏览器对象模型提供了独立于内容的、可以与浏览器窗口进行互动的对象结构。BOM由多个对象组成，其中代表浏览器窗口的Window对象是BOM的顶层对象，其他对象都是该对象的子对象。

我们在浏览器中的一些操作都可以使用BOM的方式进行编程处理，

比如：刷新浏览器、后退、前进、在浏览器中输入URL等

## BOM的顶级对象window

window是浏览器的顶级对象，当调用window下的属性和方法时，可以省略window
注意：window下一个特殊的属性 window.name

## 对话框

- alert()
- prompt()
- confirm()

## 页面加载事件

- onload

```javascript
window.onload = function () {
  // 当页面加载完成执行
  // 当页面完全加载所有内容（包括图像、脚本文件、CSS 文件等）执行
}
```

- onunload

```javascript
window.onunload = function () {
  // 当用户退出页面时执行
}
```

## 定时器

## setTimeout()和clearTimeout()

在指定的毫秒数到达之后执行指定的函数，只执行一次

```javascript
// 创建一个定时器，1000毫秒后执行，返回定时器的标示
var timerId = setTimeout(function () {
  console.log('Hello World');
}, 1000);

// 取消定时器的执行
clearTimeout(timerId);
```

## setInterval()和clearInterval()

定时调用的函数，可以按照给定的时间(单位毫秒)周期调用函数

```javascript
// 创建一个定时器，每隔1秒调用一次
var timerId = setInterval(function () {
  var date = new Date();
  console.log(date.toLocaleTimeString());
}, 1000);

// 取消定时器的执行
clearInterval(timerId);
```

## location对象

location对象是window对象下的一个属性，使用的时候可以省略window对象

location可以获取或者设置浏览器地址栏的URL

## location有哪些成员？

- 使用chrome的控制台查看

- 查MDN

  [MDN](https://developer.mozilla.org/zh-CN/)

- 成员

  - assign()/reload()/replace()
  - hash/host/hostname/search/href……

## URL

统一资源定位符 (Uniform Resource Locator, URL)

- URL的组成

```
scheme://host:port/path?query#fragment
http://www.itheima.com:80/a/b/index.html?name=zs&age=18#bottom
scheme:通信协议
	常用的http,ftp,maito等
host:主机
	服务器(计算机)域名系统 (DNS) 主机名或 IP 地址。
port:端口号
	整数，可选，省略时使用方案的默认端口，如http的默认端口为80。
path:路径
	由零或多个'/'符号隔开的字符串，一般用来表示主机上的一个目录或文件地址。
query:查询
	可选，用于给动态网页传递参数，可有多个参数，用'&'符号隔开，每个参数的名和值用'='符号隔开。例如：name=zs
fragment:信息片断
	字符串，锚点.
```

## 作业

解析URL中的query，并返回对象的形式

```javascript
function getQuery(queryStr) {
  var query = {};
  if (queryStr.indexOf('?') > -1) {
    var index = queryStr.indexOf('?');
    queryStr = queryStr.substr(index + 1);
    var array = queryStr.split('&');
    for (var i = 0; i < array.length; i++) {
      var tmpArr = array[i].split('=');
      if (tmpArr.length === 2) {
        query[tmpArr[0]] = tmpArr[1];
      }
    }
  }
  return query;
}
console.log(getQuery(location.search));
console.log(getQuery(location.href));
```

## history对象

历史记录的后退和前进

- back() 后退 
- forward() 前进
- go()

## navigator对象

获取系统和浏览器的信息的

- userAgent---获取系统,浏览器的信息的

# 特效

## 偏移量

- offsetParent用于获取定位的父级元素
- offsetParent和parentNode的区别

```javascript
var box = document.getElementById('box');
console.log(box.offsetParent);
console.log(box.offsetLeft);
console.log(box.offsetTop);
console.log(box.offsetWidth);
console.log(box.offsetHeight);
```

![](https://i.loli.net/2020/02/28/bSAvtLsgG8o2nrT.png)

## 客户区大小

```javascript
var box = document.getElementById('box');
console.log(box.clientLeft);
console.log(box.clientTop);
console.log(box.clientWidth);
console.log(box.clientHeight);
client系列:
    *  clientWidth:可视区域的宽度,没有边框
    *  clientHeight:可视区域的高度,没有边框
    *  clientLeft:左边框的宽度
    *  clientTop:上边框的宽度
    *  clientX:可视区域的横坐标
    *  clientY:可视区域的纵坐标
```

## 滚动偏移

```javascript
var box = document.getElementById('box');
console.log(box.scrollLeft)
console.log(box.scrollTop)
console.log(box.scrollWidth)
console.log(box.scrollHeight)
```
![](https://i.loli.net/2020/02/28/KlaWx1neIcPjAqQ.png)


## 动画

```javascript
 //匀速动画
    function animate(element, target) {
      //清理定时器
      clearInterval(element.timeId);
      element.timeId = setInterval(function () {
        //获取元素的当前位置
        var current = element.offsetLeft;
        //移动的步数
        var step = 10;
        step = target > current ? step : -step;
        current += step;
        if (Math.abs(current - target) > Math.abs(step)) {
          element.style.left = current + "px";
        } else {
          clearInterval(element.timeId);
          element.style.left = target + "px";
        }
      }, 20);
    }
```

## 元素隐藏

```javascript
//不占位
my$("dv").style.display="none";
//占位
my$("dv").style.visibility="hidden";
//占位
my$("dv").style.opacity=0;
//占位
my$("dv").style.height="0px";
my$("dv").style.border="0px solid red";
```

```html
//高清放大镜：
<!DOCTYPE html>
<html>
<head lang="en">
  <meta charset="UTF-8">
  <title>哈哈</title>
  <style>
    * {
      margin: 0;
      padding: 0;
    }

    .box {
      width: 350px;
      height: 350px;
      margin: 100px;
      border: 1px solid #ccc;
      position: relative;
    }

    .big {
      width: 400px;
      height: 400px;
      position: absolute;
      top: 0;
      left: 360px;
      border: 1px solid #ccc;
      overflow: hidden;
      display: none;
    }

    .mask {
      width: 175px;
      height: 175px;
      background: rgba(255, 255, 0, 0.4);
      position: absolute;
      top: 0px;
      left: 0px;
      cursor: move;
      display: none;
    }

    .small {
      position: relative;
    }
  </style>
</head>
<body>
<div class="box" id="box">
  <div class="small"><!--小层-->
    <img src="images/small.png" width="350" alt=""/>
    <div class="mask"></div><!--遮挡层-->
  </div><!--小图-->
  <div class="big"><!--大层-->
    <img src="images/big.jpg" width="800" alt=""/><!--大图-->
  </div><!--大图-->
</div>
<!--导入外部的js文件-->
<script src="common.js"></script>
<script>

  //获取需要的元素
  var box = my$("box");
  //获取小图的div
  var small = box.children[0];
  //遮挡层
  var mask = small.children[1];
  //获取大图的div
  var big = box.children[1];
  //获取大图
  var bigImg = big.children[0];

  //鼠标进入显示遮挡层和大图的div
  box.onmouseover = function () {
    mask.style.display = "block";
    big.style.display = "block";
  };
  //鼠标离开隐藏遮挡层和大图的div
  box.onmouseout = function () {
    mask.style.display = "none";
    big.style.display = "none";
  };

  //鼠标的移动事件---鼠标是在小层上移动
  small.onmousemove = function (e) {
    //鼠标此时的可视区域的横坐标和纵坐标
    //主要是设置鼠标在遮挡层的中间显示
    var x = e.clientX - mask.offsetWidth / 2;
    var y = e.clientY - mask.offsetHeight / 2;
    //主要是margin的100px的问题
    x = x - 100;
    y = y - 100;
    //横坐标的最小值
    x = x < 0 ? 0 : x;
    //纵坐标的最小值
    y = y < 0 ? 0 : y;
    //横坐标的最大值
    x = x > small.offsetWidth - mask.offsetWidth ? small.offsetWidth - mask.offsetWidth : x;
    //纵坐标的最大值
    y = y > small.offsetHeight - mask.offsetHeight ? small.offsetHeight - mask.offsetHeight : y;
    //为遮挡层的left和top赋值
    mask.style.left = x + "px";
    mask.style.top = y + "px";

    //遮挡层的移动距离/大图的移动距离=遮挡层的最大移动距离/大图的最大移动距离
    //大图的移动距离=遮挡层的移动距离*大图的最大移动距离/遮挡层的最大移动距离

    //大图的横向的最大移动距离
    var maxX = bigImg.offsetWidth - big.offsetWidth;

    //大图的纵向的最大移动距离
    //var maxY = bigImg.offsetHeight - big.offsetHeight;

    //大图的横向移动的坐标
    var bigImgMoveX = x * maxX / (small.offsetWidth - mask.offsetWidth);
    //大图的纵向移动的坐标
    var bigImgMoveY = y * maxX / (small.offsetWidth - mask.offsetWidth);

    //设置图片移动
    bigImg.style.marginLeft = -bigImgMoveX + "px";
    bigImg.style.marginTop = -bigImgMoveY + "px";
  };
</script>
</body>
</html>

```





# 附录

## 元素的类型

![](https://i.loli.net/2020/02/28/szyGtlAx8hHdJ5N.png)

---
title: bootstrap4 文档
date: 2020-02-28
categories: 
- 前端
tags: 
- 前端
- bootstrap
---
<center><img src="https://i.loli.net/2020/02/28/esD2TLKx4uczZyr.jpg" style="zoom: 70%;"/>

bootstrap4 的学习文档，仅供参考学习使用</center>

<!-- more -->

Bootstrap是当前世界最受欢迎的响应式、移动设备优先的门户和应用前端框架。

(1) Bootstrap: [https://getbootstrap.com/](https://getbootstrap.com/)

(2) jQuery: [http://jquery.com/](http://jquery.com/)

(3) [https://github.com/jquery/jquery/tree/3.3.1)](https://github.com/jquery/jquery/tree/3.3.1))

(3) Popper.js: [https://github.com/FezVrasta/popper.js/releases](https://github.com/FezVrasta/popper.js/releases)

(下拉菜单dropdowns、提示组件popovers、冒泡组件等都提依赖于Popper.js)

IE浏览器支持：

支持**Internet Explorer 10**及更高版本，不支持IE9（即使大多兼容，我们依然不推荐）。

请注意，IE10中不完全支持某些CSS3属性和HTML5元素，或者需要前缀属性才能实现完整的功能。

如果您需要IE8-9支持，请使用Bootstrap 3 ，它是我们代码中最稳定的版本，官方不再发布新版，但仍然支持严重错误修复和文档维护。

(更多兼容性参考：[https://getbootstrap.com/docs/4.3/getting-started/browsers-devices/)](https://getbootstrap.com/docs/4.3/getting-started/browsers-devices/))

重要提示：

1. 响应式meta标签

移动设备优先, Bootstrap 4 不同于历史版本，它首先为移动设备优化代码，然后用CSS媒体查询来扩展组件。为了确保所有的设备的渲染和触摸效果，必须在网页的<head>区添加响应式的视图标签，简要的说就是优先引入下面一行。

``` html
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
```

2. HTML5 doctype头部规范

HTML5标准的 doctype 头部定义是首要的，否则会导致样式失真（对搜索引擎和浏览器友好）。

```html
//英文是en，zh-CN是默认中文网页
<!doctype html>
<html lang="zh-CN">
...
</html>
```

# 布局

## container容器

我们推荐所有样式都定义在.container或.container-fluid容器之中-- **这是启用整个栅格系统必不可少的前置条件**，它们分别对应选择一个响应式的、固定宽度的容器。

- container：容器可以被嵌套，但是大多数布局并不需要这么做（最少层次的嵌套构建出的网页更优雅）

- container-fluid 类，可以使div宽度扩展到整个宽度（如果没有被其它CSS容器包含，则应是浏览器运行时的宽度，否则应是父容器中允许的最大宽度，一般视为100%宽度）

```html
<div class="container">
	<!-- Content here -->
</div>

<div class="container-fluid">
	<!-- Content here -->
</div>
```

## 栅格系统

Bootstrap包含了一个强大的移动优先的网格系统，它是基于一个**12列**的布局、有5种响应尺寸(对应不同的屏幕)。Bootstrap4是完全基于flexbox流式布局构建的，完全支持响应式标准。分界点大小：576px、768px、992px、1200px

|                    | 特小 <576px | Small ≥576px | Medium ≥768px | Large ≥992px | 特大 ≥1200px |
| ------------------ | ----------- | ------------ | ------------- | ------------ | ------------ |
| `.container`       | 100%        | 540像素      | 720px         | 960像素      | 1140px       |
| `.container-sm`    | 100%        | 540像素      | 720px         | 960像素      | 1140px       |
| `.container-md`    | 100%        | 100%         | 720px         | 960像素      | 1140px       |
| `.container-lg`    | 100%        | 100%         | 100%          | 960像素      | 1140px       |
| `.container-xl`    | 100%        | 100%         | 100%          | 100%         | 1140px       |
| `.container-fluid` | 100%        | 100%         | 100%          | 100%         | 100%         |

![](https://i.loli.net/2020/02/28/K8IWiotax5Us6pn.png)

### 自动布局列

```html
<div class="col">占一行显示</div>
<div class="col">占一行显示</div>
```

多个元素一行显示

```html
  <div class="row">
	<div class="col-3">占一行中的3份</div>
	<div class="col">自适应占一行中的9份</div>
  </div>
```

内容自适应

```html
<div class="col-auto">随内容的变化而变化</div>
```

插入.w-100要将列拆分为新行

```html
 <div class="row">
	<div class="col-3"></div>
     <div class="w-100"></div>
	<div class="col"></div>
  </div>
```

混合布局，在不同分辨率下显示不同的布局。

```html
 <div class="row">
   <div class="col-sm-6 col-lg-3"></div>
   <div class="col-sm-6 col-lg-3"></div>
 </div>
```

### 对齐

垂直对齐

```html
//在row上加 .align-items-start/center/end,实现row中所有元素上中下对齐
<div class="row align-items-start/center/end"></div>

//在col中加，实现当前元素的对齐方式
<div class="col align-items-start/center/end"></div>
<div class="col align-items-start/center/end"></div>
```

水平对齐

```html
//justify-content-start/center/end/around(等距对齐)/between(两端对齐)
<div class="row justify-content-center">
```

清除边距：`no-gutters`

### 重排序

- 顺序重定义

> order-*(1-12),默认是0，数值越小，排序越靠前。
>
> order-first的值是-1.

- 偏移

  1. `offset-md-*`：使列向右偏移*列

  2. `ml-auto`：当前列向右偏移。`mr-auto`：向左偏移

### 禁用响应式

样式不会随着分辨率的变化而变化。有四种方式：

1. 给容器设定固定宽度。

   如.container {width: 980px;}

2. 栅格布局使用`col-*`而不是`col-sm-*`的方式。

3. 移除设置浏览器视口（viewport）的标签：`<meta>`。

4. 如果使用了导航条，需要移除所有导航条的折叠和展开行为。

### 响应式的分界点

基于视口宽度的最小值来设置元素在不同的设备上的呈现效果。

```css
/* Extra small devices (portrait phones, less than 576px)
No media query since this is the default in Bootstrap 
Small devices (landscape phones, 576px and up)*/
@media (min-width: 576px(大小可指定)) { ... }
/*Medium devices (tablets, 768px and up)*/
@media (min-width: 768px) { ... }
/*Large devices (desktops, 992px and up)*/
@media (min-width: 992px) { ... }
/*Extra large devices (large desktops, 1200px and up)*/
@media (min-width: 1200px) { ... }

/*或者是这种写法：*/
@media (min-width: 576px) and (max-width: 767px) { ... }
```

```css
<style>
	.topTt {font-size:12px;}
	@media(min-width: 576px){
		.topTt {font-size:20px;}
	}
	@media(min-width: 992px){
		.topTt {font-size:30px;}
	}
</style>
```

# 内容

## 排版

- 标题

  h1-h6

```html
<div class="h1">h1标题样式显示</div>
```

- 标题备注

```html
<div class="h1">
    h1标题样式显示
    <small class="text-muted">
        副标题副标题
    </small>
</div>
```

<img src="https://i.loli.net/2020/02/28/VkjCvFozgcdQNP3.png" style="zoom:67%;" />

- 显示标题

  一种更大型、鲜明的标题样式。

```html
<!-- display-(1-4) -->
<div class="display-1">更大的标题</div>
```

- lead中心内容

  用于提示这是中心内容或重要内容。（字体会变大）

```html
<p>苹果苹果苹果苹果</p>
<p class="lead">香蕉香蕉香蕉香蕉</p>
```

 ![](https://i.loli.net/2020/02/28/CJjEwZIVNkaQ1Ds.png)

- 文本内联元素

```html
<p>看看我是不是<mark>高亮</mark>文本</p>
<p>看看我是不是<span class="mark">高亮</span>文本</p>

<p><small>小号字小号字小号字</small></p>
<p><span class="small">小号字小号字小号字</span></p>

<p><del>删除线删除线删除线</del></p>
<p><s>删除线删除线删除线</s></p>

<p><ins>下划线下划线下划线</ins></p>
<p><u>下划线下划线下划线</u></p>

<p><strong>粗体粗体粗体</strong></p>
<p><b>粗体粗体粗体</b></p>

<p><em>斜体斜体斜体</em></p>
<p><i>斜体斜体斜体</i></p>
```

 <img src="https://i.loli.net/2020/02/28/e7RoLON4ljb2ZfK.png" style="zoom: 80%;" />

- abbr缩略语

```html
<!-- title设置鼠标悬停提示信息，class="initialism"设置小写转大写 -->
<p>
    <abbr title="请填写您的邮箱" class="initialism">
        email
    </abbr>
</p>
```

 ![](https://i.loli.net/2020/02/28/wePFgxhT2Dl57dH.png)

- blockquote 引用与来源备注

  引用文档中另一个来源的内容块

```html
<blockquote class="blockquote text-right">
	<p class="mb-0">爱上一个地方，就应该背上包去旅游，走得更远。</p>
    <!-- 用于标识来源，一般用于页脚 -->
	<footer class="blockquote-footer">
		出自商务印书馆的<cite title="SourchTitle">《新华字典》</cite>
	</footer>
</blockquote>

<!-- <cite> 标签通常表示它所包含的文本对某个参考文献的引用，比如书籍或者杂志的标题。 -->
<!-- text-right左对齐, mb-0去除p标签边距-->
```

 ![](https://i.loli.net/2020/02/28/b5cxDTJXCoI48th.png)

## 列表

- 列表样式初始化

  `list-unstyled`可以删除列表项目上默认的list-style以及左外边距（只针对直接子元素），这只生效于在直接子列表项目上，不影响你嵌套的子列表。

- 分行或单行多列并排

  `.list-inline`可以实现列表逐行显示，并清除样式（默认不引用且无父元素影响也是逐行显示）

  `.list-inline-item`单行并多列并排，并清除样式（遵循从左对右的原则、并清除margin方法）。

```html
<!-- <ul class="list-inline"> -->
<li class="list-inline">列表111</li>
```

- 文本一行内显示（省略点）

  `.text-truncate`用省略号截断文本。

- dl 表格水平显示

  性别和男会显示在一行上。

```html
<dl class="row">
	<dt class="col-md-2">性别</dt>
	<dd class="col-md-10">男</dd>
</dl>
```

## 代码

- 内联代码

  用 `<code>` 包裹内联代码片断，勿忘转义HTML尖括号。

```html
<code>&lt;section&gt;</code>
```

![](https://i.loli.net/2020/02/28/t5NucKj3YU8GVCE.png)

- 代码块

```html
<pre>
  <code>
  &lt;p&gt;Sample text here...&lt;/p&gt;
  &lt;p&gt;And another line of sample text here...&lt;/p&gt;
  </code>
</pre>
```

![](https://i.loli.net/2020/02/28/g8513AKwhMbOlVk.png)

- var 变量

  推荐使用 <var>标签包裹标示变量。

```html
y = mx + b <br />
<var>y</var> = <var>m</var><var>x</var> + <var>b</var>
```

 ![](https://i.loli.net/2020/02/28/lDGWTJ82smQV6LP.png)

- 键盘动作提示

  使用`<kbd>`标签，标明这是一个键盘输入操作。

```html
To switch directories, type <kbd>cd</kbd> followed by the name of the directory.<br>
To edit settings, press <kbd><kbd>ctrl</kbd> + <kbd>,</kbd></kbd>
```

![](https://i.loli.net/2020/02/28/YIprHgci1j25a9d.png)

- 实例标注

  `<samp>` 标签代表这是一个示例。

```html
这是一个代码示例. <br>
<samp>这是一个代码示例.</samp>
```

![](https://i.loli.net/2020/02/28/gQyxCR7jTWI5DSm.png)

# 图片

- 响应式图片&缩略图处理

  给图片添加`.img-fluid`样式，或定义`max-width: 100%`、`height:auto;`样式，即可赋得响应式特性，图片大小会随着父元素大小同步缩放。(`w-100`使图片占满元素)

  `.img-thumbnail`使图片自动被加上一个带圆角且1px边界的外框缩略图样式（你也可以使用系统提供的边隙间距方法，如.p-1再加上边框颜色定义达成）。

```html
<div class="row">
	<div class="col-lg-4">
		<img src="images/lg.jpg" class="img-fluid">
	</div>
	<div class="col-lg-4">
		<img src="images/sm.jpg" class="w-100 img-fluid">
	</div>
	<div class="col-lg-4">
		<img src="images/lg.jpg" class="img-fluid img-thumbnail">
	</div>
</div>
```

<img src="https://i.loli.net/2020/02/28/s9IMRZyb4VLiaed.png" style="zoom: 33%;" />

- 图像对齐处理

  `float-left`、`float-right`设置图片左右浮动。父元素`clearfix`清除浮动带来的影响。`rounded`设置图片的圆角效果。

```html
<div class="clearfix" style="border: 1px solid #F00;">
	<img src="images/sm.jpg" alt="" class="rounded float-left">
	<img src="images/sm2.jpg" alt="" class="rounded float-right">
</div>
```

​	<img src="https://i.loli.net/2020/02/28/MOriwsG6eJT5xNl.png" style="zoom: 33%;" />

`d-block`将图片设置成块级元素，`mx-auto`再设置图片居中显示。

```html
<div style="border: 1px solid #F00;">
	<img src="images/sm.jpg" class="rounded d-block mx-auto">
</div>
<!-- 还可以直接给div设置text-center，也能实现图片居中显示 -->
```

 <img src="https://i.loli.net/2020/02/28/EGbxTQdVk3zoLHN.png" style="zoom: 33%;" />

- picture 元素

  指定图片在不同分辨率下的显示效果

  HTML5标准提供了一个全新的`<picture>` 元素，它可以为 `<img>`指定多个`<source>` 定义，请确保在`<img>` 标签里使用使用`.img-* CSS`样式进行定义绑定，而不是仅仅认为引用了 `<img>` 就达成了。

```html
<!-- 不同分辨率下显示的图片不一样 -->
<picture>
	<source srcset="images/lg.jpg"  media="(min-width: 992px)" >
	<source srcset="images/md.jpg"  media="(min-width: 576px)">
	<img src="images/sm.jpg" alt="">
</picture>
```

- 图文框

  如果你需要显示的内容区包括了一个图片和一个可选的标题，可使用`.figure`样式定义图片。`.figure-caption`定义标题。

  默念认的图片系统不会定义明确的大小，因此请务必将该.img-fluid类添加到您的`<img>`标签中才能实现与响应式的完美结合。

```html
<figure class="figure">
	<img src="../img/l.jpg" class="img-fiuid figure-img rounded">
	<figcaption class="figure-caption text-center">我是刘德华</figcaption>
</figure>
```

 <img src="https://i.loli.net/2020/02/28/cQxUo1SCj8uqJBO.png" style="zoom: 50%;" />

# 表格

向某个`<table>`添加一个基类.table。任何嵌套表格都将以与父类型相同的方式进行样式化。

 ![](https://i.loli.net/2020/02/28/DjJUHLintdGNOB6.png)

- 主题

  `table-dark/danger`为`<table>`添加主题变成黑色或红色。

- 表头

  `thead-light/dark`使表头`<thead>`区显示出浅黑或深灰。

- 条纹状表格

  为`<tbody>`定义`table-striped`，可同`table-dark`结合使用

- 边框

  `table-bordered`定义`<table>`

  `table-borderless`无边框

- 行悬停效果

  `table-hover`定义`<table>`

- 紧缩表格

  `table-sm`定义`<table>`可以将表格的padding值缩减一半，使表格更加紧凑。

- 表格辅助标题

  `<caption>` 标签如同一个表格的标题，它默认是隐藏的，可以协助屏幕阅读器用户找到表格、了解表格内容，且决定是否需要阅读它。

```html
<!-- 添加在table和thead之间 -->
<caption class="text-center">List of users</caption>
```

- 语义状态化

  使用语义状态样式对表格逐行或单个单元格进行着色表达。

  - table-active
  - table-primary
  - table-secondary
  - table-success
  - table-danger
  - table-warning
  - table-info
  - table-light
  - table-dark

   ![](https://i.loli.net/2020/02/28/M25z7RBWZdumGVL.png)

  **深色**表格上没有固定的背景，你可以使用 文字或背景通用样式 获得类似的样式：

  - bg-primary
  - bg-success
  - bg-warning
  - bg-danger
  - bg-info

   ![](https://i.loli.net/2020/02/28/EfpMslwcP3KOQS7.png)

- 响应式表格

  当表格想要始终呈现水平滚动，可在`.table`上加入`.table-responsive`获得响应式表现。也可以在`.table`上，加 `.table-responsive{-sm|-md|-lg|-xl}`属性来定义多屏幕尺寸响应支持。

   ![](https://i.loli.net/2020/02/28/bdLH7NoSeRDtsx6.png)

# 公共样式

## 边框

- 添加边框

  `border、border-top、border-right、border-left、border-bottom`为元素添加边框属性，显示指定边框。

 ![](https://i.loli.net/2020/02/28/onBNqQxLvb6Ig79.png)

- 删除边框

  `border-0、border-top-0、border-right-0、border-bottom-0、border-left-0`删除或显示特定边框定义方法。

 ![](https://i.loli.net/2020/02/28/f3ZEDY15Pxe4r7y.png)

- 边框颜色

```html
<!-- border-secondary/success/danger/warning/info/light/dark/white -->
<span class="border border-secondary"></span>
```

 ![](https://i.loli.net/2020/02/28/BL7o3DfYiyE2XKJ.png)

- 圆角边框

  `.rounded、rounded-top、rounded-right、rounded-bottom、rounded-left`

   ![](https://i.loli.net/2020/02/28/N6Ia13mciXg5y2C.png)

  `rounded-circle、rounded-pill`

```html
<span class="border border-secondary rounded-circle"></span>
<span class="border border-danger rounded-circle" style="width: 120px"></span>
<span class="border border-success rounded-pill"></span>
<span class="border border-danger rounded-pill" style="width: 120px"></span>
```

 ![](https://i.loli.net/2020/02/28/lKtnZFOfoW5Vcs3.png)

## 颜色

- 文本颜色

  text-primary/secondary/success/danger/warning/info/light /dark/muted/white 在p标签中的效果，在a链接中使用会有悬停和焦点状态（除了`.text-white .text-muted`这两个没有链接样式）

  ![](https://i.loli.net/2020/02/28/nACuEi4IPc12HOJ.png)

- 背景颜色

  `bg-primary/secondary/success/danger/warning/info/light /dark/white` 在p标签中的效果

   <img src="https://i.loli.net/2020/02/28/5cX7REANFqGaovf.png" style="zoom: 67%;" />

## display 显示属性

- display类格式：.d{-sm/md/lg/xl}-{value}

  display常用属性(value)：none、inline、inline-block、block、table、table-cell、table-row、flex、inline-flex。

```html
<!-- 转行内属性 -->
<div class="d-inline">aaa</div>
<div class="d-inline">bbb</div>

<!-- 隐藏和显示属性 -->
<div class="d-none">aaa</div>
<div class="d-block">bbb</div>

<!-- 通过 .d-print-{value} 样式来改变相应值处理呈现效果。-->

<p class="d-print-none">bbbbbb</p><!-- 打印的时候隐藏 -->
```

## 文本处理

- 文本对齐

  `text{-sm/md/lg/xl}-left/center/right/justify`样式类轻松地将文本重新对齐到组件。（`justify`调整使全行排满）

- 文本包裹和溢出（换行）处理

  `.text-nowrap`样式类可以防止文本换行。

   ![](https://i.loli.net/2020/02/28/thgPvfOaCb14qZl.png)

  `.text-truncate`以省略号截断文本（需要结合 `display: inline-block` 或 `display: block`来使用）。

   ![](https://i.loli.net/2020/02/28/ABmHStWYfkjTz7I.png)

- 字母大小写转换

  `text-lowercase`：转小写。

  `text-uppercase`：转大写。

  `text-capitalize`：首字母转大写。

   ![](https://i.loli.net/2020/02/28/QD5sPg6laAfCxhU.png)

- 粗体和斜体

  ```html
  <!-- 粗体 -->
  <p class="font-weight-bold">Bold text.</p>
  <!-- 正常 -->
  <p class="font-weight-normal">Normal weight text.</p>
  <!-- 小号 -->
  <p class="font-weight-light">Light weight text.</p>
  <!--斜体-->
  <p class="font-italic">Italic text.</p>
  ```

   ![](https://i.loli.net/2020/02/28/pZh1XgOrFL76tB5.png)

  - 等宽字体

    将选择更改为我们的等宽字体堆栈.text-monospace。

    ```html
    <p>This is in monospace. 这是等宽。</p>
    <p class="text-monospace">This is in monospace. 这是等宽。</p>
    ```

     ![](https://i.loli.net/2020/02/28/CM7ZsoDNVrzqpUb.png)

## 垂直对齐

使用 `vertical-alignment` 通用样式改变元素的对齐，注意：垂直对齐仅影响 内联`inline`、 内联块`inline-block`、 内联表`inline-table`、 表格单元格`table cell` 元素。

可选属性有：`.align-baseline、.align-top、.align-middle、.align-bottom、.align-text-bottom、.align-text-top。`

```html
访问<a href="http://www.web-666.com">网战天下</a>观看更多精品教程。
<button class="align-top">点击观看</button>
```

 ![](https://i.loli.net/2020/02/28/txNvhb5DBFqaOAm.png)

```html
<!--table cells表格单元格-->
<td>top</td>
<td class="align-middle">middle</td>
<td class="align-bottom">bottom</td>
```

 ![](https://i.loli.net/2020/02/28/dYIXnHgjrZ9vRlb.png)

## 规格和尺寸

宽度和高度可以用`.w/h-25/50/75/100`产生，包括 25%、50%、75%、 100%。

`.mw-100、.mh-100`产生`max-width: 100%;` 和 `max-height: 100%;`

 ![](https://i.loli.net/2020/02/28/oshyuq2NMzkYBvF.png)

 ![](https://i.loli.net/2020/02/28/xIFt6HKEPjy3QXT.png)



## 间隔

对于xs屏幕，使用固定格式`{property}{sides}-{size}` 命名CSS方法，对于sm、md、lg、xl使用`{property}{sides}-{breakpoint}-{size}`格式命名CSS方法。

- 属性(property)：

  m - 这个Class属性会设定 margin值。

  p - 这个Class属性会设定 padding值。

- 边缘(sides) 设定：

  t - 这个Class属性会设定 margin-top 或 padding-top

  b - 这个Class属性会设定 margin-bottom 或 padding-bottom

  l - 这个Class属性会设定 margin-left 或 padding-left

  r - 这个Class属性会设定 margin-right 或 padding-right

  x - 这个Class属性会设定 *-left 和 *-right两个值。

  y - 这个Class属性会设定 *-top 和 *-bottom两个值

  空白 - 这个Class属性会设定 margin 或 padding 元素的四个边。

- 尺寸(size) 规格定义：

  0 - 这个Class属性会设定 margin 或 padding 的样式值为 0

  1 - (默认时)这个Class属性会设定 margin 或 padding 以 $spacer * .25规格呈现

  2 - (默认时) 这个Class属性会设定 margin 或 padding 以 $spacer * .5规格呈现

  3 - (默认时)这个Class属性会设定 margin 或 padding 以 $spacer * 1规格呈现

  4 - (默认时) 这个Class属性会设定margin 或 padding 以 $spacer * 1.5规格呈现

  5 - (默认时)这个Class属性会设定 margin 或 padding 以 $spacer * 3规格呈现

  auto - 这个Class属性会设定 margin 值 auto（按浏览器默认值自由展现）。

- 水平居中：Bootstrap也包括一个 `.mx-auto class`样式，用于固定宽度的盒模型水平居中，具有`display: block` 和 width 设置水平边距内容的auto居中。

## 阴影

可以使用`.shadow-none`和`.shadow{-sm/lg}`实用工具类快速添加或删除阴影。

## position定位

- 通用属性

  `.position-static/relative/absolute/fixed/sticky`样式。可以实现快速定位-虽然它们不包含响应式支持。

- 固定在顶（底）部

  `.fixed-top/bottom`将一个元素固定在可见区域的顶(底)部

  >用户在使用固定在顶部时请确认效果带来的影响（如覆盖）-必要时增加额外的自定义CSS。

- 贴齐于top顶部

  该 `.sticky-top` 样式使用 `position: sticky`不能在所有浏览器中获得支持。

  将一个元素轩于可见区域的顶部，从边到边-但只在你的浏览器窗口滚动才能激活它。

## visibility 显示或隐藏处理

`invisible`：隐藏元素但是占位子。

`visible`：显示元素。

## 关闭图标

使用通用的close关闭图标来关闭 modals模态框提示或alert提示组件的内容。

```html
<button type="button" class="close">&times;</button>
<!-- <a href="###" class="close">&times;</a> -->
```

 ![![](https://i.loli.net/2020/02/28/8Zfbl2KeHnphBGL.png)](img/36.png)

## 嵌入(embed)

创建响应式的视频、图像、幻灯片，并能在在任何设备上友好的扩展显示。

将这些规则应用到 <iframe>、<embed>、 <video>、 <object> 上。当需要配合其它属性（如响应式）时，也可以加入 `.embed-responsive-item` 定义。

你不需要将 `frameborder="0"` 加入到你的 <iframe>中，因为我们已经为您覆盖处理了这个属性。

长宽比例处理：`embed-responsive-21by9 / 16by9 / 4by3 / 1by1`

```html
<div class="embed-responsive embed-responsive-16by9">
	<iframe src="https://www.taobao.com" class="embed-responsive-item"></iframe>
</div>
```

 ![](https://i.loli.net/2020/02/28/oZ5Sg1Ye7OXwN8a.png)

## 图像替换

使用 `.text-hide` class样来隐藏一个元素的文字内容并替换成背景图片。

使用.text-hide class样式可以保持标签的亲和性及SEO优化需求，引入后，需要使用 background-image 属性来提供视觉展示，而不是文字内容（文字内容随即隐藏）。

```html
<!-- <h1 class="text-hide">网战天下</h1> -->
<h1 class="text-hide" style="background-image:url('images/sm.jpg'); width:75px;height:75px;">网战天下</h1>
```

## 读屏器

支持视觉隐藏的内容、但保持可访问的辅助技术，如屏幕阅读器，可以使用`.sr-only`类风格。在需要向非视觉用户传达额外的视觉信息或提示（例如通过使用颜色表示的含义）的情况下，这通常很有用。

```html
<p class="text-danger">
  <span class="sr-only">Danger: </span>
  This action is not reversible
</p>
```

通过 .sr-only可定义 屏幕阅读器支持的元素, `.sr-only` 与 `.sr-only-focusable`结合，可以防止被键盘激活后再次显示此地素（如通过键盘）。

```html
<a class="sr-only sr-only-focusable" href="#content">Skip to main content</a>
```

## flex 弹性布局

- 父级：

1. 启用：`.d{-sm/md/lg/xl}-flex/inline-flex`

2. 方向：`.flex{-sm/md/lg/xl}- row /row-reverse / column/column-reverse`

3. 内容对齐与对准：`.justify-content{-sm/md/lg/xl}-start/center/end/between/around`

4. 对齐项目：`.align-items{-sm/md/lg/xl}-stretch/start/center/end/baseline`

5. Wrap包裹：`.flex{-sm/md/lg/xl}-nowrap/wrap/wrap-reverse`

6. 对齐内容：`.align-content{-sm/md/lg/xl}-stretch/start/center/end/around`

- 子元素：

  1. 自对齐：`.align-self{-sm/md/lg/xl}-`stretch/start/center/end/baseline

  2. 自相等：`.flex{-sm/md/lg/xl}-fill`

  3. 等宽变幻：`.flex{-sm/md/lg/xl}-grow-0/1`

  ​       缩小能力：`.flex{-sm/md/lg/xl}-shrink-1/0`

  4. 自浮动：水平：`.mr-auto、.ml-auto`

  ​	   垂直：`.mb-auto、.mt-auto (可结合align-items、flex-direction: column)`

  5. Order排序：`.order{-sm/md/lg/xl}-1至12（默认0，越小越靠前）`

# 组件

## 警告提示框

```html
<div class="alert alert-primary">
  This is a primary alert—check it out!
</div>
```

 ![](https://i.loli.net/2020/02/28/bj8SQwOL4Mo5kRU.png)

- 链接颜色

  使用 .alert-link 类可以为带颜色的警告文本框中的链接加上合适的颜色（BootStrap已经内置了相应的颜色解决方案，会自动对应有一个优化后的链接颜色方案）。

```html
<!--没加 -->
<div class="alert alert-primary">
  This is a primary alert with <a href="#">网战天下</a>. Give it a click if you like.
</div>
<!--加alert-link-->
<div class="alert alert-primary">
  This is a primary alert with <a href="#" class="alert-link">网战天下</a>. Give it a click if you like.
</div>
```

 ![](https://i.loli.net/2020/02/28/56APVdHkGC7mrpa.png)

- 额外附加内容

  警报还可以包含其他HTML元素，如标、段落和分隔符。

  ```html
  <div class="alert alert-success">
  	<h4 class="alert-heading">Well done!</h4>
  	<p>Aww yeah, you successfully read this important alert message. This example text is going to run a bit longer so that you can see how spacing within an alert works with this kind of content.</p>
  	<hr>
  	<p class="mb-0">Whenever you need to, be sure to use margin utilities to keep things nice and tidy.</p>
  </div>
  ```

  ![](https://i.loli.net/2020/02/28/wYtJEu7MCU3Rvz1.png)

## 关闭警告(小贴士效果)

使用.alert结合JavaScript，可以实现警报效果，贴在页面上，并可以自由关闭(关闭警报会将其从DOM中移除)。

可以在右上角定义一个`.close`关闭按钮效果，则需要在容器中引用 `.alert-dismissible` 类。

警告按钮上要增加data-dismiss="alert" 触发 JavaScript 动作(关闭警告)，同时使用<button>元素，以确保在所有设备上都能获得正确的行为响应。

.fade和.show样式：点击关闭时有淡进淡出的效果。

```html
<div class="alert alert-danger alert-dismissible fade show">
	<strong>登录失败!</strong> 您的用户名或密码错误.
	<button type="button" class="close" data-dismiss="alert">&times;</button>
</div>
```

![](https://i.loli.net/2020/02/28/wYtJEu7MCU3Rvz1.png)

js行为：

> .alert(‘close’)方法。
>
> 事件： close.bs.alert、closed.bs.alert

```javascript
//方法
$('#btn').on('click',function(){
	$('#box').alert('close')
})
//事件
$('#box').on('close.bs.alert',function(){
	alert('自闭了')
})
$('#box').on('closed.bs.alert',function(){
	alert('我已经自闭了')
})
```

## 徽章

### 示例

`.badge`可以嵌在标题中，并通过标题样式来适配其元素大小，因为其本身是通过相对字体大小和em单位的，所以有良好的弹性。

```html
<h1>夏季清爽运动鞋 <span class="badge">New</span></h1>
<h2>夏季清爽运动鞋 <span class="badge badge-secondary">New</span></h2>
```

 ![](https://i.loli.net/2020/02/28/OwHNT1VkLSryqoX.png)

徽章可用作链接或按钮的一部分，以提供统计数字样式。

```html
<button type="button" class="btn btn-primary">
	通知 <span class="badge badge-light">6</span>
</button>
<a href="#" class="btn btn-primary">
	通知 <span class="badge badge-light">6</span>
</a> 
```

 ![](https://i.loli.net/2020/02/28/7Q2nRiMGVs9kPmH.png)

徽章在span中的表现

```html
<span class="badge badge-primary">Primary</span>
<span class="badge badge-secondary">Secondary</span>
```

![](https://i.loli.net/2020/02/28/47If5mETBcuLrAp.png)

### 椭圆形胶囊标签

`.badge-pill`样式，可以使标签更加圆润（具体有较大的border-radius边框半径和水平padding）， 如果你错过了V3的标签这是有用的（这是Bootstrap 4中的特色功能）。

```html
<span class="badge badge-pill badge-primary">Primary</span>
<span class="badge badge-pill badge-secondary">Secondary</span>
```

 ![](https://i.loli.net/2020/02/28/gaybCltXfs9FG63.png)

### 链接

`.badge-*` 也可以在 <a> 元素上使用，并实现悬停、焦点、状态等效果。

```html
<a href="#" class="badge badge-primary">Primary</a>
<a href="#" class="badge badge-secondary">Secondary</a>
```

 ![](https://i.loli.net/2020/02/28/NXjPUmCT2x7Soi5.png)

### 面包屑导航

```html
<nav>
	<ol class="breadcrumb">
		<li class="breadcrumb-item"><a href="#">首页</a></li>
		<li class="breadcrumb-item"><a href="#">女装</a></li>
		<li class="breadcrumb-item active">连衣裙</li>
	</ol>
</nav>
```

 ![](https://i.loli.net/2020/02/28/khINfUnx94WtSeq.png)

## 按钮

```html
<button class="btn btn-primary">Primary</button>
<button class="btn btn-secondary">Secondary</button>
```

 ![](https://i.loli.net/2020/02/28/VZtiLkjKMPqnFAp.png)

### 标签按钮

`.btn` 可以在<button>元素上使用，您也可以在 <a>、 或 <input> 元素上使用這些 Class，同样能带来按钮效果（在少数浏览器下会有不同的渲染变异）。

```html
<a class="btn btn-primary" href="#">Link</a>
<button class="btn btn-primary">Button</button>
<input class="btn btn-primary" type="button" value="Input">
<input class="btn btn-primary" type="submit" value="Submit">
<input class="btn btn-primary" type="reset" value="Reset">
```

 ![](https://i.loli.net/2020/02/28/9xaKX2Y18BkHTPe.png)

### 轮廊按钮

`.btn` 在引用中，如果需要一个按钮，但不需要带来的巨大的背景颜色（背景边框缩小），用默认修饰符类替换`.btn-outline-*`任何按钮上的所有背景颜色和图像。

```html
<button class="btn btn-outline-primary">Primary</button>
<button class="btn btn-outline-secondary">Secondary</button>
```

 ![](https://i.loli.net/2020/02/28/KfiSI3lOpdTRX5x.png)

### 尺寸规格与大小定义

配合`.btn-lg` 、 `.btn-sm` 两个邻近元素，可分别实现大规格按钮、小规格按钮的定义。

```html
<button class="btn btn-primary btn-lg">提交</button>
<button class="btn btn-primary">提交</button>
<button class="btn btn-primary btn-sm">提交</button>
<hr>
<button class="btn btn-primary btn-block">提交</button>
```

 ![](https://i.loli.net/2020/02/28/eKlrHbi1s5XgMFx.png)

### 启用与禁用状态

启用：`.btn`样式定义的按钮，默认就是启用状态（背景较深、边框较暗、带内阴影），如果你一定要使按钮固定为启用状态、不需要点击反馈，可以增加.`active`样式。

禁用：直接将disabled布尔属性添加到任何<button>元素（直接嵌套在html标签中，使按钮看起来处于非活动的禁用状态（点击不会有响应和弹性）。

使用` <a>`标签的禁用有所不同：

1. `<a>`标签不支持 disabled 属性，所以你必须增加 .disabled 属性，使之达到视觉禁用的效果。
2. 未来，将包括更多的友好风格，以禁用按钮上的 `pointer-events` 属性，在支持该属性的浏览器中，会你看不到禁用的光标。

```html
<button class="btn btn-primary">提交</button>
<button class="btn btn-primary active">提交</button>
<button class="btn btn-primary" disabled>提交</button>
<a href="#" class="btn btn-primary disabled">提交</a>
```

 ![](https://i.loli.net/2020/02/28/KHsB4SIctA1MJjl.png)

### 按钮插件

#### 切换状态

添加 data-toggle="button" 属性，可以切换按钮的 active 状态。（点击后按钮的状态会在启动与未启动之间切换）

```html
<button class="btn btn-primary" data-toggle="button">Single toggle</button>
<!-- 图为点击后的状态 -->
```

 ![](https://i.loli.net/2020/02/28/cuGJeiEx6p3fSYF.png)

#### 复选框和单选框

`.btn`样式也可以使用于其它元素，比如<label>HTML组件上，从而实现单选、复选效果。添加 `data-toggle="buttons"` 到`.btn-group` 下的元素里，来启用它们的样式切换。

```html
<div class="btn-group" data-toggle="buttons">
	<label class="btn btn-secondary active">
		<input type="checkbox" name="checkbox[]" checked> Java
	</label>
	<label class="btn btn-secondary">
		<input type="checkbox" name="checkbox[]"> PHP
	</label>
	<label class="btn btn-secondary">
		<input type="checkbox" name="checkbox[]"> Python
	</label>
</div>

<div class="btn-group" data-toggle="buttons">
	<label class="btn btn-secondary active">
		<input type="radio" name="radio" checked> Java
	</label>
	<label class="btn btn-secondary">
		<input type="radio" name="radio"> PHP
	</label>
	<label class="btn btn-secondary">
		<input type="radio" name="radio"> Python
	</label>
</div>
```

 ![](https://i.loli.net/2020/02/28/vZJaOX9KDCwzTf6.png)

上面的实例对应传统使用环境。Bootstrap 4提供了`.btn-group-toggle`全新的复选与单选 解决方案：

```html
<!--点击切换点击状态 -->
<div class="btn-group-toggle" data-toggle="buttons">
	<label class="btn btn-secondary active">
		<input type="checkbox"> Checked
	</label>
</div>

<div class="btn-group btn-group-toggle" data-toggle="buttons">
	<label class="btn btn-secondary active">
		<input type="checkbox" name="checkbox[]" checked> Java
	</label>
	<label class="btn btn-secondary">
		<input type="checkbox" name="checkbox[]"> PHP
	</label>
	<label class="btn btn-secondary">
		<input type="checkbox" name="checkbox[]"> Python
	</label>
</div>

<div class="btn-group btn-group-toggle" data-toggle="buttons">
	<label class="btn btn-secondary active">
		<input type="radio" name="radio" checked> Java
	</label>
	<label class="btn btn-secondary">
		<input type="radio" name="radio"> PHP
	</label>
	<label class="btn btn-secondary">
		<input type="radio" name="radio"> Python
	</label>
</div>
```

 ![](https://i.loli.net/2020/02/28/rofdiAO4XT3RyGQ.png)

### js行为

 `.button('toggle')`：切换状态，给予按钮已经启用的外观。

## 下拉菜单

`dropdown`、`btn-group`

需要引入`popper.js`或者使用`bootstrap.bundle.min.js`（内置`popper.js`）

### 示例



- 单一按钮的下拉菜单

  任何一个 .btn块都可以定义变更为下拉菜单，可以使用<button>或<a>元素做下拉菜单的示例。

  `btn-group`是行内块元素，`dropdown`是块级元素。

```html
<div class="dropdown">
<!-- <div class="btn-group"> -->
	<button class="btn btn-primary dropdown-toggle" data-toggle="dropdown">Dropdown</button>
	<!-- <a href="#" class="btn btn-primary dropdown-toggle" data-toggle="dropdown">Dropdown</a> -->

	<div class="dropdown-menu">
		<a href="#" class="dropdown-item">aaa</a>
		<a href="#" class="dropdown-item">bbb</a>
		<a href="#" class="dropdown-item">ccc</a>
	</div>
</div>
```

 ![](https://i.loli.net/2020/02/28/r9jR16lUiuXcePm.png)

- 分裂式按钮下拉菜单

  ```html
  <div class="btn-group">
  	<button class="btn btn-success">Dropdown</button>
  	<button class="btn btn-success dropdown-toggle dropdown-toggle-split" data-toggle="dropdown"></button>
  
  	<div class="dropdown-menu">
  		<a href="#" class="dropdown-item">AAA</a>
  		<a href="#" class="dropdown-item">BBB</a>
  		<a href="#" class="dropdown-item">CCC</a>
  	</div>
  </div>
  ```

   ![](https://i.loli.net/2020/02/28/gvNXnRAW64KxaJI.png)

- 变形

  可以用 `.dropup、.dropright、.dropleft`改变下拉菜单的指向。

### 菜单

`dropdown-menu`

旧版Boostrap(v3)下拉菜单中的子菜单项必须是链接，但v4不再是这种情况，现在你可选择使用<button>下拉列表中的元素，而不是仅仅 <a>标签。

```html
<div class="dropdown">
	<button class="btn btn-primary dropdown-toggle" data-toggle="dropdown">Dropdown</button>
	<div class="dropdown-menu show">
		<a href="#" class="dropdown-item">aaa</a>
		<button class="dropdown-item">bbb</button>
		<span class="dropdown-item-text">ccc</span>
	</div>
</div>
```

 ![](https://i.loli.net/2020/02/28/e1h8Uc6YStBRJZM.png)

### 有效&不可用

加上 .active 让下拉列表中的项 样式为有效菜单。

加上.disabled 让下拉列表中的项 样式为不可用菜单。

### 对齐

默认情况下，一个下拉菜单自动从顶部和左侧的父级100％定位。添加.dropdown-menu-right 到.dropdown-menu右侧轻松对齐下拉菜单。

 ![](https://i.loli.net/2020/02/28/mqD1sVS4r9gCX7K.png)

- 响应式对齐

  如果你想使用响应式对齐，请通过添加data-display="static"属性禁用动态定位，并使用响应式变体类。

  为了下拉菜单左/右对齐和给定断点或更大的断点, 加上`.dropdown-menu-{sm|-md|-lg|-xl}-left/right`。

  你不需要添加 data-display="static"属性设置为导航栏中的下拉按钮，因为导航条中不使用popper.js。

### 内容

### 头部

添加 `h6.dropdown-header`标题来标记任何下拉菜单中的操作部分。

### 分割线

使用`div.dropdown-divider`分隔符分割相关菜单子项，呈现出分组和分割线效果。

 ![](https://i.loli.net/2020/02/28/Y5eaPoTGlJuVX4D.png)

### 文本

```html
<div class="dropdown">
	<button class="btn btn-primary dropdown-toggle" data-toggle="dropdown">Dropdown</button>

<div class="dropdown-menu p-4 text-muted" style="width:200px;">
	<p>一些示例文本在下拉菜单中自由流动。</p>
	<p>这是更多示例文本。</p>
	</div>
</div>    
```

 ![](https://i.loli.net/2020/02/28/2KTC3qwz6ZpRvHX.png)

### 下拉选项

使用data-offset或data-reference更改下拉菜单的位置。

```html
<button class="btn btn-primary dropdown-toggle" data-toggle="dropdown" data-offset="10,20">Dropdown</button>

<button class="btn btn-success">Dropdown</button>
<button class="btn btn-success dropdown-toggle dropdown-toggle-split" data-toggle="dropdown" data-reference="parent"></button>
```

### JavaScript 行为

#### 事件

(1) show.bs.dropdown：当调用show显示方法时，此事件会立即触发。

(2) shown.bs.dropdown：当下拉菜单对用户可见时，会触发此事件(将等待CSS转换完成)。

(3) hide.bs.dropdown：当调用隐藏实例方法时，会立即触发此事件。

(4) hidden.bs.dropdown：当下拉菜单从用户隐藏完毕时，会触发此事件(将等待CSS转换完成)。

```javascript
$('.dropdown').on('show.bs.dropdown',function(){
	alert('show')
}).on('shown.bs.dropdown',function(){
	alert('shown')
}).on('hide.bs.dropdown',function(){
	alert('hide')
}).on('hidden.bs.dropdown',function(){
	alert('hidden')
})
```

## 按钮组(Btn-group)

### 示例

`.btn-group`：将一系列的 `.btn` 包裹在`.btn-group`内，并使用我们提供的插件，可以实现选择按钮、选取块状区的行为功能。

- 大小尺寸：`.btn-group-lg/sm`

```html
<div class="btn-group btn-group-lg">
	<button type="button" class="btn btn-secondary">Left</button>
	<button type="button" class="btn btn-secondary">Middle</button>
	<button type="button" class="btn btn-secondary">Right</button>
</div>
```

 ![](https://i.loli.net/2020/02/28/HxK1PXTi9bUWlym.png)

### 按钮工具栏

`.btn-toolba`定义按钮工具栏，根据需要使用样式定义，对按钮进行群组、间隔等定义，将按钮组的组合成为更复杂组件的按钮工具栏。

```html
<div class="btn-toolbar">
	<div class="btn-group mr-2">
		<button type="button" class="btn btn-secondary">1</button>
		<button type="button" class="btn btn-secondary">2</button>
		<button type="button" class="btn btn-secondary">3</button>
		<button type="button" class="btn btn-secondary">4</button>
	</div>

	<div class="btn-group mr-2">
		<button type="button" class="btn btn-secondary">5</button>
		<button type="button" class="btn btn-secondary">6</button>
		<button type="button" class="btn btn-secondary">7</button>
	</div>

	<div class="btn-group">
		<button type="button" class="btn btn-secondary">8</button>
	</div>
</div>
```

 ![](https://i.loli.net/2020/02/28/EcQKxSbRajlo6rU.png)

### 嵌套

将`.btn-group` 放在另一个 `.btn-group` 里，可以实现按钮组与下拉菜单的组合。（详情看下拉菜单内容）

### 垂直排列

用.btn-group-vertical将一组按钮垂直排列，而不是水平排列，**不支持**分割式下拉菜单的定义。

```html
<div class="btn-group-vertical">
	<button type="button" class="btn btn-primary">Left</button>
	<button type="button" class="btn btn-primary">Middle</button>
	
	<div class="btn-group">
		<button class="btn btn-primary dropdown-toggle" data-toggle="dropdown">Dropdown</button>
		<div class="dropdown-menu">
			<a href="#" class="dropdown-item">aaa</a>
			<a href="#" class="dropdown-item">bbb</a>
			<a href="#" class="dropdown-item">ccc</a>
		</div>
	</div>
</div>
```

 ![](https://i.loli.net/2020/02/28/tgHZSqax7rVIUQW.png)

## input 输入框及输入框群组

`.input-group`中的元素会连接在一行内显示。

### 示例

- 规格尺寸定义：将相对表单大小的class样式加到 `.input-group`中，其内容会自动调整大小，如`.input-group-lg、.input-group-sm`，不需要在每个元素上重重使用样式控制其大小。

  ```html
  <label for="">商品价格</label>
  <div class="input-group">
  	<div class="input-group-prepend">
  		<span class="input-group-text">$</span>
  	</div>
  	
  	<input type="text" class="form-control">
  	<!-- <textarea class="form-control"></textarea> -->
  
  	<div class="input-group-append">
  		<span class="input-group-text">.00</span>
  	</div>
  </div>
  ```

   ![](https://i.loli.net/2020/02/28/76S5qHXRveG4LBj.png)

### 输入组插件

- 勾选或单选框组合

```html
<div class="input-group-prepend">
	<div class="input-group-text">
		<input type="checkbox/radio">
	</div>
</div>
```

- 多个输入

  尽管可视化支持多个 <input>但验证样式仅适用于具有单个<input>的输入组。

- 多类型控件组合

  支持多种控件结合，比如复选框和、文本、input框混合使用。

```html
<div class="input-group-prepend">
	<span class="input-group-text">$</span>
	<span class="input-group-text">&yen;</span>
</div>
```

 ![](https://i.loli.net/2020/02/28/M4ufpXR5ocKLlNr.png)

- 按钮组合

```html
<div class="input-group-prepend">
	<button class="btn btn-outline-secondary">Button</button>
	 <button class="btn btn-outline-secondary">Button</button>
</div>
```

 ![](https://i.loli.net/2020/02/28/s2pLyer6wHQ7xhS.png)

- 下拉菜单

```html
<div class="input-group-prepend">
	<button class="btn btn-outline-secondary dropdown-toggle" data-toggle="dropdown">Dropdown</button>
	<div class="dropdown-menu">
		<a href="" class="dropdown-item">aaa</a>
		<a href="" class="dropdown-item">bbb</a>
		<a href="" class="dropdown-item">ccc</a>
	</div>
</div>
<div class="input-group-prepend">
	<button class="btn btn-outline-secondary">Dropdown</button>
	<button class="btn btn-outline-secondary dropdown-toggle dropdown-toggle-split" data-toggle="dropdown"></button>
	<div class="dropdown-menu">
		<a href="" class="dropdown-item">aaa</a>
		<a href="" class="dropdown-item">bbb</a>
		<a href="" class="dropdown-item">ccc</a>
	</div>
</div>
```

 ![](https://i.loli.net/2020/02/28/zRT1do3WGpNLAKq.png)

### 自定义表单

输入组包括对自定义选择和自定义文件输入的支持。 这些浏览器的默认版本不受支持。

```html
<select class="custom-select">
	<option value="">-请选择-</option>
	<option value="">aaa</option>
	<option value="">bbb</option>
	<option value="">ccc</option>
</select>
```

 ![](https://i.loli.net/2020/02/28/SysrhEYkfozC6qa.png)

```html
<div class="custom-file">
	<input type="file" class="custom-file-input">
	<label for="" class="custom-file-label">选择</label>
</div>
```

  ![](https://i.loli.net/2020/02/28/fFMvJGYB9ECQrgz.png)

## 表单

### 表单控件

表单控件使用form-group包裹。

1. 文本控件（如 <input>、<select>、 <textarea>）统一采用 `.form-control` 样式进行处理优化，包括常规外观、focus选（点）中状态、尺寸大小等。
2. 对于input文件选择控件，Bootstrap v4采用`.form-control-file` 取代了`.form-control`。
3. 大小规格：使用 `.form-control-lg` 和 `.form-control-sm`属性定控件大小高度。
4. 输入范围：使用设置水平滚动范围输入`.form-control-range`。
5. 只读属性：在input控件上增加 `readonly` (布尔值)标签定义，以防止修改input中的值。仅能阅读的input控件显示较谈(就像禁用的输入框)，但保留鼠标效果。
6.  只读纯文本：如果你希望将 <input readonly>属性进一步处理，显示为纯文本（没有控件框），你只要引用 `.form-control-plaintext` class样式，就能移除预设的表单样式，并保留适当的边距和填充间隙。
7. 提示文本：small.form-text.text-muted

```html
<form action="">
	<div class="form-group">
		<label for="">邮箱</label>
		<input type="text" class="form-control">
	</div>
	<div class="form-group">
		<label for="">密码</label>
		<input type="password" class="form-control">
	</div>
	<div class="form-check">
		<input type="checkbox" class="form-check-input">
		<label for="" class="form-check-label">记住我</label>
	</div>
	<button class="btn btn-primary">登录</button>
</form>
```

 ![](https://i.loli.net/2020/02/28/1LvZ72hy6eMPUt4.png)

### 单选框和复选框

- 默认堆叠

```html
<div class="form-group">
	<div class="form-check">
		<input type="checkbox/radio" class="form-check-input">
		<label class="form-check-label">苹果</label>
	</div>
	<div class="form-check">
		<input type="checkbox/radio" class="form-check-input">
		<label class="form-check-label">香蕉</label>
	</div>
	<div class="form-check">
		<input type="checkbox/radio" class="form-check-input" disabled>
		<label class="form-check-label">橘子</label>
	</div>
</div>
```

  ![](https://i.loli.net/2020/02/28/w23i8CONWHIVStg.png)

- 水平排列

  通过添加 `.form-check-inline`到任何一个组，会使 加到任何`.form-check`中的选取框平行排列。

   ![](https://i.loli.net/2020/02/28/8WAgL2btFZOv9Qj.png)

- 没有标签

  添加 `.position-static` 到 `.form-check` 选择器上，可以实现没有文本的输入。(不带label)

```html
<!-- 如果不加position-static则不显示 -->
<div class="form-check">
	<input type="checkbox" class="form-check-input position-static">
</div>
<div class="form-check">
	<input type="radio" class="form-check-input position-static">
</div>
```

 ![](https://i.loli.net/2020/02/28/DOxlih7nLRP2oHy.png)

### 布局

- 表单栅格排列

  可使用我们的栅格系统构建更复杂的表单，包括建立多列、多种宽度和其它对齐选项的布局。

```html
<form>
	<div class="row">
		<div class="col">
			<input type="email" class="form-control" placeholder="邮箱">
		</div>
		<div class="col">
			<input type="password" class="form-control" placeholder="密码">
		</div>
	</div>
</form>
```

 ![](https://i.loli.net/2020/02/28/DH49nlQNfSWywzK.png)

你也可以使用 `.form-row`来取代`.row`（它们二者很多时候可以互换使用），因为`.form-row`提供更小的沟槽缝隙。

  ![](https://i.loli.net/2020/02/28/tjiSJbFDBLVThrH.png)

- 垂直排列表单

  通过添加 `.row` class类，并使用 `.col`-*-* 等栅格组件来指定标签和宽度，可以建立起水平表单。

  确保添加.col-form-label 到您<label>上，以便他们垂直居中与他们相关的表单控件。

  <legend>元素，可以.col-form-legend样式定义，与普通<label>元素相似。

- 使用.col-form-label-sm、.col-form-label-lg 到 <label>上，可以定义控件大小，还有 .form-control-lg、.form-control-sm样式也起相应作用。

- 自动调整大小

  下面的示例使用一个flexbox弹性布局垂直居中的内容，我们将.col改为`.col-auto`，这样的列只占用本身内容所需要的宽度，换句话说列的大小就是内容的大小（宽度）

```html
<form>
	<div class="form-row">
		<div class="col-auto">
			<input type="email" class="form-control" placeholder="邮箱">
		</div>
		<div class="col-auto">
			<input type="password" class="form-control" placeholder="密码">
		</div>
		<div class="col-auto">
			<button class="btn btn-primary">登录</button>
		</div>
	</div>
</form>
```

 ![](https://i.loli.net/2020/02/28/wXuD3q4o8jLV9rK.png)

- 内联式表单

  使用 `.form-inline`样式在单个水平行上显示一系列标签，表单控件和按钮。内联表单中的表单控件与默认状态略有不同：

  - 基于`display: flex`控件组件，并允许您使用 间隙隔离 和 flexbox 弹性布局样式。
  - 控制组件和input接受 `width: auto` 以覆盖预设的 `width: 100%`。
  - 控制组件只会在`viewport 576px`宽度 时才会显示在行内，以便在移动设备上完整呈现。

```html
<form class="form-inline">
	<input type="email" class="form-control mb-2 mr-sm-2" placeholder="邮箱">
	<input type="password" class="form-control mb-2 mr-sm-2" placeholder="密码">
	<div class="form-check mb-2 mr-sm-2">
		<input type="checkbox" class="form-check-input">
		<label for="" class="form-check-label">记住我</label>
	</div>
	<button class="btn btn-primary">登录</button>
</form>
```

 ![](https://i.loli.net/2020/02/28/esuDrWpU8XiPza9.png)

### 禁用表单

被禁用的表单不能点击，呈灰色

```html
<form>
	<fieldset disabled>
	……
	</fieldset>
</form>
```

### 验证

- 自定义样式

  您需要将 novalidate属性添加到您的<form>。这将禁用浏览器默认的反馈工具提示，但仍提供对JavaScript中的表单验证API有效支持。

```html
<!--required为必填属性，不填的话浏览器会提示填写，添加novalidate移除浏览器自带提示 -->
<form action="" novalidate class="needs-validation">
    <div class="form-group">
        <label for="">邮箱</label>
        <input type="text" class="form-control" placeholder="邮箱" required>
        <div class="invalid-feedback">邮箱格式不正确!</div>
    </div>
    <div class="form-group">
        <label for="">密码</label>
        <input type="password" class="form-control" placeholder="密码" required>
        <div class="invalid-feedback">密码格式不正确!</div>
    </div>
    <div class="form-check">
        <input type="checkbox" name="" id="" class="form-check-input">
        <label for="" class="form-check-label">记住我</label>
    </div>
    <button class="btn btn-primary">登录</button>
</form>
```

```javascript
// Example starter JavaScript for disabling form submissions if there are invalid fields
(function() {
	'use strict';
	window.addEventListener('load', function() {
// Fetch all the forms we want to apply custom Bootstrap validation styles to
		var forms = document.getElementsByClassName('needs-validation');
// Loop over them and prevent submission
		var validation = Array.prototype.filter.call(forms, function(form) {
			form.addEventListener('submit', function(event) {
				if (form.checkValidity() === false) {
					event.preventDefault();
  					event.stopPropagation();
				}
				form.classList.add('was-validated');
			}, false);
		});
	}, false);
})();
```

  ![](https://i.loli.net/2020/02/28/yNLO3FbhRmcV8Yf.png)

- 服务器端

  我们建议使用客户端验证，但是如果您需要使用服务器端验证，则可以使用.is-invalid和.is-valid来表示无效和有效的表单字段。注意，.invalid-feedback这些类也支持。

```html
<!--效果同上 -->
<form>
	<div class="form-group">
		<label>邮箱</label>
		<input type="email" class="form-control is-valid" placeholder="邮箱">
		<div class="valid-feedback">邮箱正确!</div>
		<div class="invalid-feedback">邮箱不正确!</div>
	</div>
	<div class="form-group">
		<label>密码</label>
		<input type="password" class="form-control is-invalid" placeholder="密码">
		<div class="valid-feedback">密码格式正确!</div>
		<div class="invalid-feedback">密码格式不正确!</div>
	</div>
	<button class="btn btn-primary">登录</button>
</form>
```

### 自定义表单

为了使自定义表单和跨浏览器保持一致性，请使用自定义的表单元素来替换浏览器的默认值，它们建立在语义和具备友了的标记之上，因此它们是可以替代任何默认表单控制元件的。

- checkbox勾选

```html
<div class="custom-control custom-checkbox">
	<input type="checkbox" class="custom-control-input" id="remember">
	<label class="custom-control-label" for="remember">记住我</label>
</div>
```

 ![](https://i.loli.net/2020/02/28/5w1pl8tbcxkVLjR.png)

- radio 单选框

```html
<div class="custom-control custom-radio">
	<input type="radio" name="sex" id="man" class="custom-control-input">
	<label class="custom-control-label" for="man">男</label>
</div>
<div class="custom-control custom-radio">
	<input type="radio" name="sex" id="woman" class="custom-control-input">
	<label class="custom-control-label" for="woman">女</label>
</div>
```

 ![](https://i.loli.net/2020/02/28/fndWRecGg5CLDsQ.png)

- 一行显示：

  在.`custom-control`添加`.custom-control-inline`。

- IOS风格开关

  开关具有自定义复选框的标记，使用 .custom-switch 类来呈现切换开关。开关还支持 disabled属性(v4.2.1新增组件)。

```html
<div class="custom-control custom-switch">
    <input type="checkbox" class="custom-control-input" id="customSwitch1">
    <label class="custom-control-label" for="customSwitch1">Toggle this switch element</label>
</div>
```

  ![](https://i.loli.net/2020/02/28/i7tLCQ95gpBlHjN.png)

- select 下拉选择菜单

  自定义<select>下拉选择菜单只需要一个`.custom-select` CSS即可触发自定义样式。

  可以在`.custom-select`上添加`.custom-select-lg/sm`改变大小。

```html
<select class="custom-select">
	<option>-请选择-</option>
	<option>aaa</option>
	<option>bbb</option>
	<option>ccc</option>
</select>
```

 ![](https://i.loli.net/2020/02/28/OnXMUez5mpZRLoa.png)

- range 范围

  创建自定义·<input type="range">·与控制`.custom-range`。轨道（背景）和大拇指（值）都被设置为跨浏览器显示相同。由于只有IE和Firefox支持从拇指的左侧或右侧“填充”它们的轨迹，以作为视觉指示进度的手段，所以我们目前不支持它。

```html
<input type="range" class="custom-range">
```

  ![](https://i.loli.net/2020/02/28/xgnsewl3CmqIrcT.png)

- file 浏览器

  文件浏览（选取）是比较原始粗糙的，它需要额外的JavaScript定义支持，如果你将Choose file…文件选取和所选文件的名称关联。

```html
<div class="custom-file">
	<input type="file" class="custom-file-input" id="avatar">
	<label class="custom-file-label" for="avatar">选择文件</label>
</div>
```

  ![](https://i.loli.net/2020/02/28/PS1CENJtyIuOY3X.png)

---
title: Hexo-next主题美化（7.7.1版本）
date: 2020-02-27 23:45:34
categories:
- Hexo
tags:
- hexo
---

<center>
<img src="https://i.loli.net/2020/02/28/6JXmDsw18lRAQM2.jpg
" style="zoom: 50%;"/>

使用的 hexo 版本是 4.2.0，next 主题是 7.7.1 版本
</center>
<!-- more -->

# 出现的问题

## 进度条设置错误（未解决）

主题设置文件里`pace`如果开启会在控制台出3条错：

```js
Refused to apply style from 'http://localhost:4000/lib/pace/pace-theme-minimal.min.css' because its MIME type ('text/html') is not a supported stylesheet MIME type, and strict MIME checking is enabled.

GET http://localhost:4000/lib/pace/pace.min.js net::ERR_ABORTED 404 (Not Found)

Refused to apply style from 'http://localhost:4000/lib/pace/pace-theme-minimal.min.css' because its MIME type ('text/html') is not a supported stylesheet MIME type, and strict MIME checking is enabled.
```

## 界面动画和daovoice聊天冲突（未解决）

添加了`daovoice`聊天功能后，疑是与动画`motion`冲突，两个全部开启的时候界面显示会出错，控制台报如下信息,关闭其中一个功能就会恢复正常。

```js
Uncaught (in promise) Error: Velocity: First argument (transition.slideDownIn) was not a property map, a known action, or a registered redirect. Aborting.
    at j (bundle.b69d69b9cd164a70039e.js:21)
    at menu (motion.js:101)
    at Object.next (motion.js:22)
    at Array.sequence.<computed>.o.complete (motion.js:88)
    at p (velocity.min.js:3)
    at c (velocity.min.js:3)
```

# 添加RSS

- 安装插件：`npm install --save hexo-generator-feed`

- 编辑Blog/_config.yml文件，在文件末尾添加

```yml
# Extensions
# Plugins: http://hexo.io/plugins/
plugins: hexo-generate-feed

```

- 配置主题_config.yml文件，搜索rss，在后面加上/atom.xml

```yml
# Set rss to false to disable feed link.
# Leave rss as empty to use site's feed link.
# Set rss to specific value if you have burned your feed already.
rss: /atom.xml //注意：有一个空格
```

# 背景动画Canvas_nest

1. 进入`theme/next`目录
2. 执行命令：`git clone https://github.com/theme-next/theme-next-canvas-nest source/lib/canvas-nest`
3. 这时将配置文件`_config.yml`中的`canvas_nest: false`改为`canvas_nest: true`

# 设置背景图片

路径：`source/css/_schemes/对应的主题文件`

- 背景

```css
body{   
  background:url('/images/body.png');
  background-size:cover;
  background-repeat:no-repeat;
  background-attachment:fixed;
  background-position:center;
}
```

- 顶栏图片

```css
.header {
  background:url(图片链接) none repeat scroll !important;
}
```

- 底栏背景色

```css
.footer {
  background:rgba(颜色rgb,透明度) none repeat scroll !important;
}
```

- 侧栏图片及内部文字颜色修改

```css
#sidebar {
  background:url(图片链接);
  background-size: cover;
  background-position:center;
  background-repeat:no-repeat;
  p,span,a {color: 颜色代码;}
}
```

# 为博客添加宠物

[官方使用教程](https://github.com/EYHN/hexo-helper-live2d/blob/master/README.zh-CN.md)

1. 在终端切换到你的博客的本地路径里，然后输入如下代码安装live2d插件：

```shell
npm install --save hexo-helper-live2d
```

2. 在hexo的_config.yml中添加参数：

```yml
live2d:
  enable: true
  scriptFrom: local
  pluginRootPath: live2dw/
  pluginJsPath: lib/
  pluginModelPath: assets/
  tagMode: false
  debug: false
  model:
    use: live2d-widget-model-<模型名称>
    # wanko
  display:
    position: right
    width: 150
    height: 300
  mobile:
    show: true
  react:
    opacity: 0.7
```

3. 在站点目录下建文件夹`live2d_models`
4. 挑选喜欢的模型：[模型地址](https://huaji8.top/post/live2d-plugin-2.0/)
5. 再在`live2d_models`下建文件夹`<你喜欢的模型名字>`
6. 再在<你喜欢的模型名字>下建json文件：`<你喜欢的模型名字>.model.json`
7. 安装模型

```shell
npm install --save live2d-widget-model-<你喜欢的模型名字>
```

# 鼠标点击效果

## 桃心

1. 在`\themes\next\source\js`下添加 love.js 文件，写入代码：

```js
!function(e,t,a){function n(){c(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"),o(),r()}function r(){for(var e=0;e<d.length;e++)d[e].alpha<=0?(t.body.removeChild(d[e].el),d.splice(e,1)):(d[e].y--,d[e].scale+=.004,d[e].alpha-=.013,d[e].el.style.cssText="left:"+d[e].x+"px;top:"+d[e].y+"px;opacity:"+d[e].alpha+";transform:scale("+d[e].scale+","+d[e].scale+") rotate(45deg);background:"+d[e].color+";z-index:99999");requestAnimationFrame(r)}function o(){var t="function"==typeof e.onclick&&e.onclick;e.onclick=function(e){t&&t(),i(e)}}function i(e){var a=t.createElement("div");a.className="heart",d.push({el:a,x:e.clientX-5,y:e.clientY-5,scale:1,alpha:1,color:s()}),t.body.appendChild(a)}function c(e){var a=t.createElement("style");a.type="text/css";try{a.appendChild(t.createTextNode(e))}catch(t){a.styleSheet.cssText=e}t.getElementsByTagName("head")[0].appendChild(a)}function s(){return"rgb("+~~(255*Math.random())+","+~~(255*Math.random())+","+~~(255*Math.random())+")"}var d=[];e.requestAnimationFrame=function(){return e.requestAnimationFrame||e.webkitRequestAnimationFrame||e.mozRequestAnimationFrame||e.oRequestAnimationFrame||e.msRequestAnimationFrame||function(e){setTimeout(e,1e3/60)}}(),n()}(window,document);
```

2. 更新`\themes\next\layout_layout.swig`文件，在末尾（在前面引用会出现找不到的 bug）添加以下js引入代码：

```js
<!-- 页面点击小红心 --> 
<script type="text/javascript" src="/js/love.js"></script>
```

## 气泡效果

1. 在`\themes\next\source\js`下添加 fireworks.js 文件，写入代码：

```js
"use strict";
function updateCoords(e){pointerX=(e.clientX||e.touches[0].clientX)-canvasEl.getBoundingClientRect().left,pointerY=e.clientY||e.touches[0].clientY-canvasEl.getBoundingClientRect().top}function setParticuleDirection(e){var t=anime.random(0,360)*Math.PI/180,a=anime.random(50,180),n=[-1,1][anime.random(0,1)]*a;return{x:e.x+n*Math.cos(t),y:e.y+n*Math.sin(t)}}function createParticule(e,t){var a={};return a.x=e,a.y=t,a.color=colors[anime.random(0,colors.length-1)],a.radius=anime.random(16,32),a.endPos=setParticuleDirection(a),a.draw=function(){ctx.beginPath(),ctx.arc(a.x,a.y,a.radius,0,2*Math.PI,!0),ctx.fillStyle=a.color,ctx.fill()},a}function createCircle(e,t){var a={};return a.x=e,a.y=t,a.color="#F00",a.radius=0.1,a.alpha=0.5,a.lineWidth=6,a.draw=function(){ctx.globalAlpha=a.alpha,ctx.beginPath(),ctx.arc(a.x,a.y,a.radius,0,2*Math.PI,!0),ctx.lineWidth=a.lineWidth,ctx.strokeStyle=a.color,ctx.stroke(),ctx.globalAlpha=1},a}function renderParticule(e){for(var t=0;t<e.animatables.length;t++){e.animatables[t].target.draw()}}function animateParticules(e,t){for(var a=createCircle(e,t),n=[],i=0;i<numberOfParticules;i++){n.push(createParticule(e,t))}anime.timeline().add({targets:n,x:function(e){return e.endPos.x},y:function(e){return e.endPos.y},radius:0.1,duration:anime.random(1200,1800),easing:"easeOutExpo",update:renderParticule}).add({targets:a,radius:anime.random(80,160),lineWidth:0,alpha:{value:0,easing:"linear",duration:anime.random(600,800)},duration:anime.random(1200,1800),easing:"easeOutExpo",update:renderParticule,offset:0})}function debounce(e,t){var a;return function(){var n=this,i=arguments;clearTimeout(a),a=setTimeout(function(){e.apply(n,i)},t)}}var canvasEl=document.querySelector(".fireworks");if(canvasEl){var ctx=canvasEl.getContext("2d"),numberOfParticules=30,pointerX=0,pointerY=0,tap="mousedown",colors=["#FF1461","#18FF92","#5A87FF","#FBF38C"],setCanvasSize=debounce(function(){canvasEl.width=2*window.innerWidth,canvasEl.height=2*window.innerHeight,canvasEl.style.width=window.innerWidth+"px",canvasEl.style.height=window.innerHeight+"px",canvasEl.getContext("2d").scale(2,2)},500),render=anime({duration:1/0,update:function(){ctx.clearRect(0,0,canvasEl.width,canvasEl.height)}});document.addEventListener(tap,function(e){"sidebar"!==e.target.id&&"toggle-sidebar"!==e.target.id&&"A"!==e.target.nodeName&&"IMG"!==e.target.nodeName&&(render.play(),updateCoords(e),animateParticules(pointerX,pointerY))},!1),setCanvasSize(),window.addEventListener("resize",setCanvasSize,!1)}"use strict";function updateCoords(e){pointerX=(e.clientX||e.touches[0].clientX)-canvasEl.getBoundingClientRect().left,pointerY=e.clientY||e.touches[0].clientY-canvasEl.getBoundingClientRect().top}function setParticuleDirection(e){var t=anime.random(0,360)*Math.PI/180,a=anime.random(50,180),n=[-1,1][anime.random(0,1)]*a;return{x:e.x+n*Math.cos(t),y:e.y+n*Math.sin(t)}}function createParticule(e,t){var a={};return a.x=e,a.y=t,a.color=colors[anime.random(0,colors.length-1)],a.radius=anime.random(16,32),a.endPos=setParticuleDirection(a),a.draw=function(){ctx.beginPath(),ctx.arc(a.x,a.y,a.radius,0,2*Math.PI,!0),ctx.fillStyle=a.color,ctx.fill()},a}function createCircle(e,t){var a={};return a.x=e,a.y=t,a.color="#F00",a.radius=0.1,a.alpha=0.5,a.lineWidth=6,a.draw=function(){ctx.globalAlpha=a.alpha,ctx.beginPath(),ctx.arc(a.x,a.y,a.radius,0,2*Math.PI,!0),ctx.lineWidth=a.lineWidth,ctx.strokeStyle=a.color,ctx.stroke(),ctx.globalAlpha=1},a}function renderParticule(e){for(var t=0;t<e.animatables.length;t++){e.animatables[t].target.draw()}}function animateParticules(e,t){for(var a=createCircle(e,t),n=[],i=0;i<numberOfParticules;i++){n.push(createParticule(e,t))}anime.timeline().add({targets:n,x:function(e){return e.endPos.x},y:function(e){return e.endPos.y},radius:0.1,duration:anime.random(1200,1800),easing:"easeOutExpo",update:renderParticule}).add({targets:a,radius:anime.random(80,160),lineWidth:0,alpha:{value:0,easing:"linear",duration:anime.random(600,800)},duration:anime.random(1200,1800),easing:"easeOutExpo",update:renderParticule,offset:0})}function debounce(e,t){var a;return function(){var n=this,i=arguments;clearTimeout(a),a=setTimeout(function(){e.apply(n,i)},t)}}var canvasEl=document.querySelector(".fireworks");if(canvasEl){var ctx=canvasEl.getContext("2d"),numberOfParticules=30,pointerX=0,pointerY=0,tap="mousedown",colors=["#FF1461","#18FF92","#5A87FF","#FBF38C"],setCanvasSize=debounce(function(){canvasEl.width=2*window.innerWidth,canvasEl.height=2*window.innerHeight,canvasEl.style.width=window.innerWidth+"px",canvasEl.style.height=window.innerHeight+"px",canvasEl.getContext("2d").scale(2,2)},500),render=anime({duration:1/0,update:function(){ctx.clearRect(0,0,canvasEl.width,canvasEl.height)}});document.addEventListener(tap,function(e){"sidebar"!==e.target.id&&"toggle-sidebar"!==e.target.id&&"A"!==e.target.nodeName&&"IMG"!==e.target.nodeName&&(render.play(),updateCoords(e),animateParticules(pointerX,pointerY))},!1),setCanvasSize(),window.addEventListener("resize",setCanvasSize,!1)};
```

2. 更新`\themes\next\layout_layout.swig`文件，在 head 添加代码：

```
{% if theme.fireworks %}
   <canvas class="fireworks" style="position: fixed;left: 0;top: 0;z-index: 1; pointer-events: none;" ></canvas> 
   <script type="text/javascript" src="//cdn.bootcss.com/animejs/2.2.0/anime.min.js"></script> 
   <script type="text/javascript" src="/js/fireworks.js"></script>
{% endif %}
```

3. 主题设置里添加

```yml
# Fireworks
fireworks: true
```

# 在文章末尾统一添加“本文结束”标记

1. 在路径`\themes\next\layout_macro`中新建`passage-end-tag.swig`文件,并添加以下内容：

```
<div>     
    {% if not is_index %}         
    <div style="text-align:center;color: #ccc;font-size:14px;">
        -------------本文结束<i class="fa fa-paw"></i>感谢您的阅读-------------
    </div>     
    {% endif %} 
</div>
```

2. 接着打开`\themes\next\layout_macro\post.swig`文件，在`post-body`之后，`post-footer`之前添加如下代码：

```
<div>   
    {% if not is_index %}     
        {% include 'passage-end-tag.swig' %}   
    {% endif %} 
</div>
```

3. 然后打开主题配置文件（_config.yml),在末尾添加：

```
# 文章末尾添加“本文结束”标记 
passage_end_tag:  
    enabled: true
```

# 添加RSS

1. 安装插件：

```shell
npm install --save hexo-generator-feed
```

2. 网站设置里添加：

```yml
# Extensions 
# Plugins: http://hexo.io/plugins/ 
plugins: hexo-generate-feed
```

3. 主题文件夹 social： RSS: /atom.xml || rss
4. 配置完之后运行：hexo g
   重新生成一次，在./public文件夹中看到atom.xml文件。然后启动服务器查看是否有效，之后再部署到Github中。

# 添加顶部加载条

修改主题配置文件(_config.yml)将pace: false改为pace: true，可以换不同样式的加载条，如下:

```yml
pace:
  enable: true
  # Themes list:
  # big-counter | bounce | barber-shop | center-atom | center-circle | center-radar | center-simple
  # corner-indicator | fill-left | flat-top | flash | loading-bar | mac-osx | material | minimal
  theme: minimal
```

# 在文章底部增加版权信息

在修改next主题的配置文件_config.yml如下:

```yml
creative_commons:
  license: by-nc-sa
  sidebar: false
  post: true
  language: deed.zh
```

# 博文置顶

1. 修改`hero-generator-index`插件，把文件：`node_modules/hexo-generator-index/lib/generator.js`内的代码替换为：

```js
'use strict';
var pagination = require('hexo-pagination');
module.exports = function(locals){
  var config = this.config;
  var posts = locals.posts;
    posts.data = posts.data.sort(function(a, b) {
        if(a.top && b.top) { // 两篇文章top都有定义
            if(a.top == b.top) return b.date - a.date; // 若top值一样则按照文章日期降序排
            else return b.top - a.top; // 否则按照top值降序排
        }
        else if(a.top && !b.top) { // 以下是只有一篇文章top有定义，那么将有top的排在前面（这里用异或操作居然不行233）
            return -1;
        }
        else if(!a.top && b.top) {
            return 1;
        }
        else return b.date - a.date; // 都没定义按照文章日期降序排
    });
  var paginationDir = config.pagination_dir || 'page';
  return pagination('', posts, {
    perPage: config.index_generator.per_page,
    layout: ['index', 'archive'],
    format: paginationDir + '/%d/',
    data: {
      __index: true
    }
  });
};
```

2. 在文章中添加top值，数值越大文章越靠前，如下:

```md
---
title: ''
date: 2017-05-22 22:45:48
tags: 技巧
categories: 技巧
copyright: true
top: 100
---
```

# 侧边栏推荐阅读

打开主题配置文件修改成这样就行了(links里面写想要的链接):

```
# Blogrolls
links_title: 推荐阅读
#links_layout: block
links_layout: inline
links:
  优设: http://www.uisdc.com/
  张鑫旭: http://www.zhangxinxu.com/
  Web前端导航: http://www.alloyteam.com/nav/
  前端书籍资料: http://www.36zhen.com/t?id=3448
  百度前端技术学院: http://ife.baidu.com/
  google前端开发基础: http://wf.uisdc.com/cn/
```

# 添加sitemap网站地图

1. 安装hexo的sitemap网站地图生成插件

```shell
npm install hexo-generator-sitemap --save #google地图生成插件
npm install hexo-generator-baidu-sitemap --save #百度地图生成插件
```

2. 在hexo站点的_config.yml添加下面的代码，

```yml
# hexo sitemap网站地图
sitemap:
  path: sitemap.xml
baidusitemap:
  path: baidusitemap.xml
```

3. 配置成功后，hexo编译时会在hexo站点根目录的public下生成sitemap.xml和 baidusitemap.xml，其中sitemap.xml适合提交给谷歌搜素引擎，baidusitemap.xml适合提交百度搜索引擎。
   让百度收录你的站点
   刚建站的时候各个搜索引擎是没有收录我们网站的，在搜索引擎中输入site:<域名>,如果显示没找到就是说明网站并没有被百度收录。可以直接点击“网址提交”来提交我们的网站。

4. 登录百度站长平台,只要有百度旗下的账号就可以登录，登录成功之后在站点管理中点击添加网站然后输入你的站点地址，建议输入的网站为www开头的，不要输入github.io的，因为github是不允许百度的spider爬取github上的内容的，所以如果想让你的站点被百度收录，只能使用自己购买的域名

5. 在选择完网站的类型之后需要验证网站的所有权，验证网站所有权的方式有三种：文件验证、html标签验证和cname解析验证，使用哪一种方式都可以，都是比较简单的，但是一定要注意，使用文件验证文件存放的位置需要放在source文件夹下，如果是html文件那么hexo就会将其编译，所以必须要加上的layout:false，这样就不会被hexo编译（还不行就去部署的地方修改文件，如果文件被修改会导致验证失败）。

6. 然后就可以将生成的sitemap文件提交给百度，还是在百度站长平台，找到链接提交，这里我们可以看到有两种提交方式，自动提交和手动提交，自动提交又分为主动推送、自动推送和sitemap
   如何选择链接提交方式
   1、主动推送：最为快速的提交方式，推荐您将站点当天新产出链接立即通过此方式推送给百度，以保证新链接可以及时被百度收录。
   2、自动推送：最为便捷的提交方式，请将自动推送的JS代码部署在站点的每一个页面源代码中，部署代码的页面在每次被浏览时，链接会被自动推送给百度。可以与主动推送配合使用。
   3、sitemap：您可以定期将网站链接放到sitemap中，然后将sitemap提交给百度。百度会周期性的抓取检查您提交的sitemap，对其中的链接进行处理，但收录速度慢于主动推送。
   4、手动提交：一次性提交链接给百度，可以使用此种方式。
   一般来说，主动推送>自动推送>sitemap>手动提交

7. 主动推送

安装插件：`npm install hexo-baidu-url-submit --save`
然后在根目录的配置文件中新增字段

```
baidu_url_submit:
  count: 100 # 提交最新的一个链接
  host: www.cherryblog.site # 在百度站长平台中注册的域名
  token: 8OGYpxowYnhgVsUM # 请注意这是您的秘钥， 所以请不要把博客源代码发布在公众仓库里!
  path: baidu_urls.txt # 文本文档的地址， 新链接会保存在此文本文档里
```

在加入新的deploye

```
deploy:
 - type:baidu_url_submitter
```

这样执行hexo deploy的时候，新的链接就会被推送了

8. 自动推送

题配置文件下设置,将baidu_push设置为true：

```
# Enable baidu push so that the blog will push the url to baidu automatically which is very helpful for SEO
baidu_push: true
```

然后就会将一下代码自动推送到百度，位置是themes\next\layout_scripts\baidu_push.swig,这样每次访问博客中的页面就会自动向百度提交sitemap

```js
{% if theme.baidu_push %}
<script>
(function(){
    var bp = document.createElement('script');
    var curProtocol = window.location.protocol.split(':')[0];
    if (curProtocol === 'https') {
        bp.src = 'https://zz.bdstatic.com/linksubmit/push.js';        
    }
    else {
        bp.src = 'http://push.zhanzhang.baidu.com/push.js';
    }
    var s = document.getElementsByTagName("script")[0];
    s.parentNode.insertBefore(bp, s);
})();
</script>
{% endif %}
```

9. sitemap

  将上一步生成的sitemap文件提交到百度就可以了
  百度收录过程还是蛮久的，一度让我以为我的方法有问题，提交链接在站长工具中有显示大概是有两天的时候，站点被百度收录大概花了半个月，收录后在百度搜索site:cherryblog.site已经可以搜索到结果。
  让google收录你的站点
  相比于百度，google的效率实在不能更快。方法是和百度是一样的，都是先验证你的站点所有权，然后提交sitemap。

10. 进入google站点平台，然后就是在谷歌注册账号、验证站点、提交sitemap。

# 图片可点击放大查看

打开主题配置文件_config.yml，搜索fancybox字段，设置其值为true

```yml
# FancyBox is a tool that offers a nice and elegant way to add zooming functionality for images.
# For more information: https://fancyapps.com/fancybox
fancybox: true
```

# 增加网易云音乐播放器

1. 分享歌单
2. 打开分享界面的歌单链接（个人主页点击动态）
3. 打开歌单即可看到生成外链的点击链接
4. 然后把代码贴到你想要生成外链播放器的地方即可，但是生成的外链还是无法播放没有版权的音乐
5. 将代码放到../themes/next/layout/_macro/sidebar.swig文件中如下div中，这样可以实现当侧边栏显示目录时不会显示音乐播放器：

```html
<div class="site-overview-wrap sidebar-panel">
        {{ partial('_partials/sidebar/site-overview.swig', {}, {cache: theme.cache.enable}) }}

        {{- next_inject('sidebar') }}
		
		<!--网易云音乐-->
	  <div id="music163player">
		<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=260 src="//music.163.com/outchain/player?type=0&id=2504295111&auto=1&height=430">
		</iframe>
	  </div>
	  <!--/网易云音乐-->
      </div>
```

6. 打开主题配置文件，修改侧边宽度：

```yml
sidebar:
  # Sidebar Position.
  position: left
  #position: right

  # Manual define the sidebar width. If commented, will be default for:
  # Muse | Mist: 320
  # Pisces | Gemini: 240
  width: 300
```

7. 需要说明一点，不同浏览器打开博客后后网易云音乐状态不同，比如搜狗浏览器打开博客，音乐就自动播放，但Chrome浏览器不会自动播放。如果不想打开博客就自动播放音乐，可以让产生外链的歌单中第一首歌是因为版权无法播放的。

# 添加来必力评论系统

[来必力官网](https://www.livere.com/)

NexT支持的第三方的评论系统有很多，而且对于国内来说比较友好就有来必力点我进入来必力首页，下面介绍添加来必力评论系统。

1. 首先获取来必力id，登陆来必力注册获取。
   这里要注意，这个韩国的系统注册很慢，所以要记住不要耐不住关闭页面或者狂刷新，耐心等待就好。
2. 注册后点击导航上边的安装，选择免费的city版本
3. 点击现在安装后填入网站的一些信息就可以获取到安装代码，框中的就是你的来必力id
4. 复制上边代码中的`data-uid`的id，在主题配置文件里面搜索livere_uid，在后面添加id即可


# DaoVoice在线联系

1. 首先在daovoice注册账号[点我注册](http://dashboard.daovoice.io/get-started),邀请码是0f81ff2f，注册完成后会得到一个 app_id:

2. 记下这个app_id的值，然后打开`/themes/next/layout/_partials/head/head.swig`,写下如下代码：

```js
{% if theme.daovoice %}
  <script>
  (function(i,s,o,g,r,a,m){i["DaoVoiceObject"]=r;i[r]=i[r]||function(){(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;a.charset="utf-8";m.parentNode.insertBefore(a,m)})(window,document,"script",('https:' == document.location.protocol ? 'https:' : 'http:') + "//widget.daovoice.io/widget/0f81ff2f.js","daovoice")
  daovoice('init', {
      app_id: "{{theme.daovoice_app_id}}"
    });
  daovoice('update');
  </script>
{% endif %}
```

3. 接着打开主题配置文件，在最后写下如下代码：

```yml
# Online contact 
daovoice: true
daovoice_app_id: 这里填你的刚才获得的 app_id
```

4. 重新`hexo g，hexo s`就能看到效果了。
   安装成功后可以在DaoVoice控制台上的聊天设置里设置聊天窗口样式

# 文章阅读量

1. [leadCloud](https://www.leancloud.cn/),登录注册
2. 创建应用-->开发板-->创建
3. 完成后点击设置-->存储-->新建Class-->为了保证对NexT主题的修改兼容，新建Class名字必须为`Counter`
4. Class创建完成后，选择界面最左侧的`设置` → `应用Key`，复制`App ID`和`App Key`
5. 打开`博客根目录/themes/next/`下的`_config.yml`，查找`leancloud`，填写复制来的`App ID`和`App Key`，重新生成、部署博客即可正常统计文章阅读量。
6. 因为AppID以及AppKey是暴露在外的，为了确保只用于我们自己的博客，建议**设置Web安全域名，填入自己的博客域名**。

- 记录文章访问量的唯一标识符是文章的发布日期和文章的标题，因此请确保这两个数值组合的唯一性，如果更改了这两个数值，会造成文章阅读数值的清零重计。

- 初始的文章统计量显示为0。在配置好阅读量统计服务之后，第一次打开博文时，会自动向服务器发送数据，该数据会被记录在对应的应用的Counter表中。

- 修改Counter表中的time字段的数值，可以修改文章的访问量。双击具体的数值，修改之后回车即可保存。
  
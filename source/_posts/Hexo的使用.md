---
title: Hexo的使用
date: 2020-02-27 23:37:53
categories:
- Hexo
tags:
- hexo
---

<center>
<img src="https://i.loli.net/2020/02/28/Dgo5w9N6l8ikUvH.jpg
" style="zoom: 50%;"/>
Hexo 是一个快速、简洁且高效的博客框架
</center>
<!-- more -->

Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。



[官方网址](https://hexo.io/zh-cn/index.html)

- 安装：`npm install hexo-cli -g`
- 本地初始化一个 blog：`hexo init blog`
- 下载依赖：`npm install`
- 开启本地服务：`hexo server`，输入`http://localhost:4000/`即可访问
- 显示 Hexo 版本:`hexo version`
- 创建新文件：`$ hexo new [layout] <title>`,您可以在命令中指定文章的布局（layout），默认为 post，可以通过修改 _config.yml 中的 default_layout 参数来指定默认布局
- 清除缓存文件 (db.json) 和已生成的静态文件 (public):`hexo clean`

- 部署三连：`hexo clean && hexo g && hexo d`
- 创建文章：`hexo n 标题` 也可以在博客目录D:\hexo\source\_posts中新建一个后缀为.md的文件
- 文章抬头信息

```
title:  #文章标题
date:  #时间，一般不用改
categories:  #目录分类
tags:
  - Testing
  - Another Tag
keywords:  #文章关键词，多个关键词用英文逗号隔开
comments: false  禁用评论
```

- 文章图片的存放

想要在文章中插入图片的话，可以按照Markdown语法来插入。图片的存放有两种方式：在本地D:\Hexo\source\目录下新建一个存放图片的文件夹，比如images，然后把想要插入的图片放在里面，插入图片的路径；第二种方法是把图片上传到网络，然后插入图片路径。推荐使用第二种。

- 可以选择喜欢的主题，我使用的是 next 
- 如何设置「阅读全文」？在文章中使用 `<!-- more -->` 手动进行截断，Hexo 提供的方式

- 文章内如果有双大括号，生成的时候会报错，hexo 会错认为是变量进行解析，解决办法可以在`{ {`中间加个空格就可以不解析
---
title: 浏览器请求过程-http
date: 2020-02-28
categories:
- 前端
tags:
- 前端
keywords: HTTP
comments:
---

<center>
<img src="https://i.loli.net/2020/02/28/WsSclZiTg9BIadJ.jpg
" style="zoom: 100%;"/>

浏览器打开网址后发生了什么？
</center>

<!-- more -->

# 浏览器

1. 用户在浏览器中输入URL网址。
2. 浏览器解析用户输入的URL地址 =>域名+端口。
3. 浏览器会先检查本地缓存中有没有这个域名 =>IP。

>有：直接使用IP进行访问。
>
>没有：浏览器发起一个DNS系统调用。（操作系统进行查找）
>
>- 操作系统检查自己的缓存里有没有这个域名。
>
>- 没有的话找系统的hosts文件中有没有这个域名。
>
>- 如果都没有找到，会对DNS服务器发起一个系统调用。
>
>注：谷歌使用`chrome://net-intermals`查看浏览器缓存。

4. 浏览器通过一个本机的随机端口建立一个与服务器指定端口（80）之间的连接通道。
5. 浏览器会将客户端的一些信息打上一个“包”。将这个“包”通过这个连接通道发送到服务端。
6. 打开服务端返回过来的“包”，找到`Content-type`，决定如何处理响应的内容。
7. 如果是HTML则渲染到界面上。
8. “包”的概念是请求报文。

# 服务器

1. 打开客户端提交过来的“包”，拿到“包”里面的 请求路径。
2. 根据请求的路径 对应文件的扩展名 找到文件的类型（MIME Type）。
3. 判断文件类型是否为静态文件

>是：直接读取这个文件的内容。
>
>不是：交给“外包公司”执行代码。

4. 服务端拿到执行的结果，把要发给客户端的数据打上一个“包”。
5. 将这个“包”再通过之前的连接通道发给客户端。

# 请求报文

![](https://i.loli.net/2020/02/28/gKSwrcETh38RmZe.png)

# 响应报文

![](https://i.loli.net/2020/02/28/K6H9hoSeO2Dcxa3.png)

```php
<?php
//php 中 header 函数专门用于设置响应头,不能设置两个相同的，会被覆盖。
//设置响应类型
header('Content-type: text/css');

//设置跳转(重定向)页面
header('location: xxx.php');

//让文件下载
header('Content-type: application/octet-stream');

//设置默认下载文件名
header('Content-Disposition: attachment; filename=demo.txt');

//设置cookie
header('Set-Cookie: key=value');
?>
```


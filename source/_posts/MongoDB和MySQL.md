---
title: MongoDB和MySQL
date: 2020-02-28 21:01:51
categories:
- Node
tags:
- 数据库
- Node
keywords:
comments:
---

<center>
<img src="https://i.loli.net/2020/02/28/5XmqxfNZAlvu4CT.jpg
" style="zoom: 80%;"/>

node 环境下操作数据库
</center>
<!-- more -->

# MongoDB

## 基本概念

- 数据库
- 集合（数组）   --->  相当于表
- 文档   --->   表里的数据
- 文档结构很灵活，没有任何限制

```json
// 存储结构
{
  数据库: {
    集合：[ {文档},{文档},{文档} ],集合1[ {文档} ]
  }
	数据库1：{  }
}
```



## 关系型数据库和非关系型数据库

- 关系型数据库

  >表就是关系，或者说表与表之间存在关系

  1. 所有的关系型数据库都需要通过`sql`语言来操作
  2. 所有的关系型数据库在操作之前都需要设计表结构
  3. 而且数据表还支持约束
     - 唯一的
     - 主键
     - 默认值
     - 非空

- 非关系型数据库

  - 非常的灵活
  - 有的非关系数据库就是 key-value 对儿
  - 但是 MongoDB 是长得最像关系型数据库的非关系型数据库
  - MongoDB 不需要设计表结构，你可以任意的往里面存数据，没有结构性这么一说

## 下载安装

> [官网地址](https://www.mongodb.com/)：没进去？！
>
> 下载地址1：https://www.mongodb.com/download-center/community
>
> 下载地址2：http://dl.mongodb.org/dl/win32/
>
> 文件名格式：win32/mongodb-win32-x86_64-2012plus-v4.2-latest-signed.msi
>
> [安装文档](https://blog.csdn.net/qq_15980721/article/details/102586518)
>
> [安装的时候需要注意的几点坑](https://blog.csdn.net/Fern_1397/article/details/93386989)
>
> 配置环境变量： C:\Program Files\MongoDB\Server\4.2\bin
>
> `mongod --version`: 在 cmd 上查看版本

- 遇到的问题

  `MongoDB Server`服务启动失败，验证您是否有足够的权限启动系统服务
![image-20200209181444970.png](https://raw.githubusercontent.com/iamyujian/PicGo/master/img/image-20200209181444970.png)

  解决方法：打开(services.msc)服务界面,找到 MongoDB Server，右键->属性->登录，登录身份选择**本地系统账户(L)**。
  设置完成后自己手动启动 MongoDB Server 服务，或者在刚刚正在安装的 MongoDB 弹窗提示点击**Retry**重试，安装程序会帮你启动 MongoDB Server 服务。

## 基础使用

>推荐菜鸟教程：https://www.runoob.com/mongodb/mongodb-tutorial.html

### 创建数据目录

> MongoDB 将数据目录存储在 /data/db 目录下。但是这个数据目录不会主动创建，我们在安装完成后需要创建它。请注意，数据目录应该放在根目录下（(如： C:\ 或者 D:\ 等 )。不创建目录启动不了服务

```shell
c:\>cd c:\
c:\>mkdir data
c:\>cd data
c:\data>mkdir db
```

> 如果想要修改默认的数据存储目录

```shell
mongod --dbpath=数据存储目录路径
```

### 启动和关闭数据库
- 启动

```shell
# 如果是在 C 盘启动，就把数据目录创建在 C 盘根目录，其他盘同理
mongod
```

- 停止

> Ctrl + c 或者关闭控制台

### 连接数据库

- 连接


```shell
# 该命令默认连接本机的 MongoDB 服务
mongo
```

- 退出

  ```shell
  exit
  ```

### 基本命令

- 查看显示所有数据库

  ```shell
  > show dbs
  admin   0.000GB	--->这三个是默认的，不要动
  config  0.000GB
  local   0.000GB
  ```

- 查看当前操作的数据库

  ```shell
  > db
  test 	--->默认是在这个数据库中，没有数据的时候通过 show dbs 查询不显示
  ```

- 切换到制定的数据库（如果没有会新建）

  ```shell
  use 数据库名称
  ```

## 在 Node 中操作 MongoDB

### 使用官方的 mongodb 包来操作

> 使用文档：https://github.com/mongodb/node-mongodb-native
>
> 开发的时候不用这个，比较原生

### mongoose 操作

> 第三方包 mongoose 是基于官方包
>
> 官方网址：https://mongoosejs.com/

#### 使用

1. 导入 mongoose 包

2. 连接数据库

   - `mongoose.connect('mongodb://localhost:27017/itcast', { useNewUrlParser: true, useUnifiedTopology: true})`

   - 数据库名称`itcast`如果不存在，当你插入第一条数据之后就会自动被创建

3. 设计集合结构

   - 先要定义架构 `mongoose.Schema`
   - 通过 `new Schema()`实例化一个对象

4. 将文档结构发布为模型

   - `mongoose.model('User', 实例化架构对象)` 用来将一个架构发布为 `model`
   - 第一个参数：传入一个`大写名词单数字符串`，用来表示你的数据库名称 ，`mongoose`会自动将大写名词的字符串生成 `小写复数` 的集合名称，例如这里的 `User` 最终会变成 `users` 集合名称
   - 返回值：模型构造函数

```js
const mongoose = require('mongoose')
// 连接数据库
mongoose.connect('mongodb://localhost:27017/itcast', { useNewUrlParser: true, useUnifiedTopology: true})
// 定义架构
const Schema = mongoose.Schema 
// 设计集合结构
let userSchema = new Schema({
  username: {
    type: String,
    require: true // 这里可以加约束，不能为空
  },
  password: {
    type: String,
    require: true // 不能为空
  }
})
// 将文档结构发布为模型
let User = mongoose.model('User', userSchema)
```

5. **通过模型构造函数操作数据**

   - 增加数据

     ```js
     // User 为模型构造函数
     let admin = new User({
       username: 'zs',
       password: '123456'
     })
     admin.save(function (err, ret) {
       if (err) {
         console.log('保存失败');
       } else {
         console.log('保存成功');
         console.log(ret); 
       /* ret 为添加的数据
       {_id: 5e4008e680121b1a9c335652,
       username: 'zs',
       password: '123456',
       __v: 0 }  */
       }
     })
     ```

   - 查询数据

     ```js
     // 查询所有
     User.find(function (err, ret) {
       if (err) {
         console.log('查询失败');
       } else {
         console.log(ret); // ret 为数组结构，查不到为[]
       }
     })
     
     // 按条件查询
     User.find({username:'zs'},function (err, ret) {
       if (err) {
         console.log('查询失败');
       } else {
         console.log(ret); // ret 为数组结构，查不到为[]
       }
     })
     
     // 按条件查询一条，如果没有条件默认为第一条
     User.findOne({username:'zs'},function (err, ret) {
       if (err) {
         console.log('查询失败');
       } else {
         console.log(ret); // ret 为对象，查不到为 null
       }
     })
     ```

   - 修改数据

     ```js
     // 根据 id 更新一个
     User.findByIdAndUpdate('5e400bbb22acb92a6cea8842', {
       password: '123'
     }, function (err, ret) {
       if (err) {
         console.log('更新失败');
       } else {
         console.log('更新成功');
         console.log(ret);
       }
     })
     
     // 根据条件更新所有
     Model.update(conditions,doc, [options], [callback])
     
     // 根据条件更新一个
     Model.findByIdAndUpdate([conditions],[update], [options], [callback])
     ```

   - 删除数据

     ```js
     // 按条件删除所有
     User.remove({username:'zs'},function (err, ret) {
       if (err) {
         console.log('删除失败');
       } else {
         console.log('删除成功');
         console.log(ret); // ret 为 { n: 1, ok: 1, deletedCount: 1 }
     })
     
     // 根据条件删除一个
     Model.findOneAndRemove(conditions, [options], [callback])
       
     // 根据id删除一个
     Model.findByIdAndRemove(id, [options], [callback])
     ```
     


# MySQL

> 使用 Node 调用 mysql

## 安装

```shell
npm install mysql
```

## 使用

```js
var mysql = require('mysql');

// 1. 创建连接
var connection = mysql.createConnection({
  host: 'localhost',
  user: 'me',
  password: 'secret',
  database: 'my_db'
});

// 2.连接数据库
connection.connect();

// 3.执行数据操作(增删改查直接写 sql 语句)
connection.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results);
});

// 4.关闭连接
connection.end();
```

# MD5加密

安装：`npm i blueimp-md5`

使用

```js
const md5 = require('blueimp-md5')
body.password = md5(md5(body.password))// 重复加密
```


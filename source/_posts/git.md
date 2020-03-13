---
title: git
date: 2020-02-28 12:05:38
categories: 
- 工具
tags: 
- 工具
---

<center>
<img src="https://i.loli.net/2020/02/28/6aw1WLDotVxhvyu.jpg
" style="zoom: 30%;"/>

github 和 git 的使用，偏小白
</center>
<!-- more -->

# github

## 基础概念

### 仓库（Repository）

仓库用来存放项目代码，每个项目对应一个仓库，多个开源项目则有多个仓库

### 收藏（Star）

收藏项目，方便下次查看

### 复制克隆项目（Fork）

![](https://i.loli.net/2020/02/28/KVAjWiSQ5J4zt8q.jpg)

脚下留心：该fork的项目时独立存在的

### 发起请求（Pull Request）

![](https://i.loli.net/2020/02/28/8uN4zkOPvZpsJ3A.jpg)

### 关注（Watch）

关注项目，当项目更新可以接收到通知

### 事务卡片（Issue）

发现代码BUG，但是目前没有成型代码，需要讨论时用；

### 仓库主页说明

![](https://i.loli.net/2020/02/28/os8r7eD5EWtYxRc.jpg)

### Pull Request

情景：张三修改了fork的项目中的文件，希望更新到原来的仓库，这时候他要新建一个pull request

![](https://i.loli.net/2020/02/28/pnfr7B6LYuGtahI.jpg)

# git

## Git工作区域

![](https://i.loli.net/2020/02/28/ZY3LghSBjTV1DiE.jpg)

## 命令

### 初始化

- `设置用户名：git config --global user.name 'name'`

  `设置用户名邮箱：git config --global user.email ' '`

- `初始化工作区`：`git init`

### 过滤文件

> `.gitignore 文件夹`：`git`忽略文件，忽略配置项，哪些文件不需要提交到 git 上就可以在这里进行忽略
>
> `vim .gitignore`: 新增以及编写这个文件 
>
> 此外，git 对于 .ignore 配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效；

```
node_modules/  ---> 过滤整个文件夹
*.zip		---> 过滤zip后缀文件
demo.html   过滤该文件

!src/   不过滤该文件夹
!*.js   不过滤java源文件
!index.html 不过滤该文件
```



### 文件操作

- `创建文件：touch file.txt`

- `添加文件到暂存区： git add file.txt`

  `将所有需要添加的文件添加到暂存区：git add ./`

- `将文件从暂存区提交到仓库：git commit -m '添加描述'`

  `将所有修改的文件直接放到仓库中：git commit --all -m '描述'`

### 查看日志

- `查看当前文件状态：git status`

- `查看日志：git log`

  `查看简洁版的日志：git log --oneline`

![](https://i.loli.net/2020/02/28/c4sEy6BTNhxQvkz.png)

### 回退版本

- `回退到指定的版本：git reset --hard Head~0 代表上次，1代表上上次`

  `通过版本号回退：git reset --hard [版本号]`

- `查看切换版本的记录：git reflog`

### 分支

- `创建分支：git branch name`
- `查看分支：git branch`
- `切换分支：git checkout name`
- `合并分支：git merge name`
- `删除分支：git branch -d name`

### 连接github

- 上传当前分支代码：`git push github仓库 HTTPS 地址 master`

  当我们在 `push/pull` 时，加上`-u`参数，那么在下一次`push/pull`时，我们只需要写`git push/pull`就能上传/下载代码(加上`-u`之后，git会把当前分支与远程的指定分支进行关联)

  `git push -f`:表示将目前自己本机的代码库推送到远端，并覆盖

- 生成变量：`git remote add name github仓库HTTPS地址`

  相当于 `name = github 仓库HTTPS地址`，只在本地当前文件夹生效，其他地方不可用

- 下载到本地：`git pull github仓库HTTPS地址 master` （本地要初始一个仓库，多次执行会合并处理）

- 克隆到本地：`git clone github仓库HTTPS地址 --depth=1` (多次执行会覆盖本地内容)

- 下载中可以加上 `--depth=1` 表示只下载最后一次的 commit，其他历史记录不要，这样可以提高下载速度

- 如果服务器版本和本地版本不同时，先pull，在本地解决冲突后再push到服务器中。

#### ssh连接

创建`ssh`钥匙：`ssh-keygen -t rsa -C "736755736@qq.com"`

路径：C:\Users\Administrator\.ssh

`id_rsa`：私钥，`id_rsa.pub`：公钥

点击 github 头像 --> settings  --> SSH and GPG keys  -->  New SSH key -->将复制的公钥里的内容粘贴到 Key 中-->生成

上传当前分支代码：`git push github 仓库SSH地址 master` (不用输入账号密码)


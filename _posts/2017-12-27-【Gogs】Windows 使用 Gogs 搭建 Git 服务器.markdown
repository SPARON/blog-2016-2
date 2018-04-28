---
layout: post
title: 【Gogs】Windows 使用 Gogs 搭建 Git 服务器
date: 2017-12-27
categories: [环境配置]
description: Windows 使用 Gogs 搭建 Git 服务器
---

**随便说两句**
之前有使用 Gitblit 在Windows搭建Git服务器，用的也挺好的，可能安装起来略麻烦一点。现在全用 Gogs 在windows搭建Git服务器，主要是因界面好看，管理更一些。

# 安装Gogs

**Gogs特点**
- 易安装
- 跨平台
- 轻量级

## step 1

- 官网介绍：https://gogs.io/
- 下载选择自己电脑，Windows amd64(64位)或者386(32位)
- 下载链接：https://dl.gogs.io/

## step 2

- 数据库，我这里使用的 Mysql ,没有的可以自己安装，或都使用其它数据库，可以看官方介绍。
- 步骤省略。

## step 3

- 下载 NSSM，这个用来注册服务的，不用每次都去启动，稍后用到。
- 下载链接：http://nssm.cc/download

## step 4

- 将下载的 Gogs 压缩文件解压到你想安装的目录。

![](https://i.imgur.com/3IhoQ80.png)

- 在gogs文件夹下增加两个文件夹（custom和log）

![(https://i.imgur.com/w5IQ9vl.png)

- custom文件夹中新增conf目录，conf目录中新增app.ini文件，然后编写app.ini

![](https://i.imgur.com/KYWCpoa.png)

![](https://i.imgur.com/978eL7k.jpg)

- log文件夹中添加gogs.log文件

![](https://i.imgur.com/QP8pDx6.png)

- 设置log文件夹的权限

![](https://i.imgur.com/A5BVGJ8.png)

## step 5

- 执行sql语句创建数据库

```sql
DROP DATABASE IF EXISTS gogs;
CREATE DATABASE IF NOT EXISTS gogs CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```

## step 6

- 进入到gogs文件夹目录，按shift,点击cmd处理，不要关掉cmd.
- 输入 （ gogs.exe web ） 启动gogs安装
- 在浏览器地址栏输入 http://localhost:3000/install 即可见首次运行安装程序
- 设置安装程序
- 自己注册一个帐号即可进行管理和创建仓库了,第一个用户默许管理员权限。

> 备注：我这边安装成功，相关的页面出现不了，有一个参考页面。

http://baijiahao.baidu.com/s?id=1582078449743656559&wfr=spider&for=pc

## step 7

- 进入到nssm文件夹目录，按shift,点击cmd处理.

![](https://i.imgur.com/W1TWeE8.png)

- 输入 （ nssm install gogs ） 运行，会弹出一个框，然后按照下面页面一步一步设置。
	https://gogs.io/docs/installation/run_as_windows_service#use-nssm

- 查看服务

![](https://i.imgur.com/FnD9HfE.png)

- 局域网访问验证（配置文件可以要更改成IP访问）

![](https://i.imgur.com/tfurWVr.png)

![](https://i.imgur.com/XwTB3dl.png)

## step 7

- 下载Git客户端使用，链接：https://git-scm.com/downloads
- 不习惯命令，也可以安装TortoiseGit，链接：https://tortoisegit.org/download/
- 还可以下载相对应TortoiseGit语言包。

# 总结

整个流程下来，一个小时就大功告成了，如果是外网服务器，需要配置域名。主要是新公司用的SVN，用的不爽，全部移植到Git上面来，又Get到新技能，这个用的挺舒服的。

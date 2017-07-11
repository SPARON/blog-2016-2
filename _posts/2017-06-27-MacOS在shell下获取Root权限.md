---
layout: post
title: MacOS在shell下获取Root权限
date: 2017-06-27
categories: [环境配置]
description: 在MacOS中获取root权限的方式
keywords: MacOS
---

![](http://static.open-open.com/news/uploadImg/20150624/20150624143847_776.jpg)

# MacOS在shell下获取Root权限

* 方式一
    ```shell
    sudo -i
    # 输入密码即可进入
    ```
* 方式二
	```shell
    sudo su
    # 输入密码进入 sh-3.2#模式
    sh-3.2# 
    su -
    ```
* 方式三
	```shell
    sudo su -
 	# 输入密码即可进入
    ```
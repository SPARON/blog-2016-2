---
layout: post
title: 【MacOS】Golang环境配置
date: 2018-05-09
categories: [环境配置]
description: 在Golang环境配置时，配置额外多余项会导致部分意外问题。
keywords: golang
---

关于Golang的环境配置，请参考之前发布的文章: [【MacOS】配置环境变量]({{ site.baseurl }}/2017/06/22/MacOS-配置环境变量)

## 问题
通过`go get`下载代码后系统总是报无权限问题。

## 解决过程
- 最初以为是`GOPATH`设置未生效，通过`go env`查看环境变量，发现一切正常；
- 于是修改`.bash_profile`配置，将环境变量提升到`/etc/profile`重试后问题依旧；
- 经过对比后发现以前配置golang环境时并未配置 `GOBIN` 一项，将其删除再试，问题解决！

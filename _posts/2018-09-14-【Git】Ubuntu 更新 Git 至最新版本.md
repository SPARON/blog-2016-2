---
layout: post
title: 【Git】Ubuntu 更新 Git 至最新版本
date: 2018-09-14
categories: [环境配置]
description: Ubuntu系统通过添加源后使用APT方式安装最新Git
keywords: [Linux, git]
---

大家平时可能发现，Ubuntu 自带的 Git 版本，比最新的 Git 版本都低一些，就忍不住想升级是不是。但是当你直接sudo apt-get install git时，没啥变化，无奈。

这是因为 Ubuntu 自带的源中，Git 版本就是这么低，能怎么办。

所以需要加入一个源，带有最新 Git 版本的源，步骤如下：


1. 添加源：
  > sudo add-apt-repository ppa:git-core/ppa

2. 更新安装列表：
  > sudo apt-get update

3. 升级 Git：
  > sudo apt-get install git


一气呵成，完成 Git 升级。

最后，可以执行git --version验证是否升级到最新版本。

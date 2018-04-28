---
layout: post
title: 利用 Chocolatey 快速在 Windows 下搭建一个开发环境
date: 2018-01-03
categories: [环境配置]
description: 在 Linux 下，大家喜欢用 apt-get 来安装应用程序，如今在 windows 下，大家可以使用 Chocolatey 来快速下载搭建一个开发环境。
---

![](http://www.ampercent.com/wp/wp-content/uploads/Chocolatey-Logo.jpg)


Chocolatey 的哲学就是完全用命令行来安装应用程序， 它更像一个包管理工具（背后使用 Nuget ）


另外需要说明的是， Chocolatey 只是把官方下载路径封装到了 Chocolatey 中，所以下载源都是其官方路径，所以下载的一定是合法的，但是如果原软件是需要 Licence 注册的话，那么 Chocolatey 下载安装好的软件还是需要你去购买注册。不过 Chocolatey 一般还是会选用免费 Licence 可用的软件。


# 安装 Chocolatey

> 具体安装参见 [Chocolatey主页](http://chocolatey.org/) ，就现在的安装方式如下：

```shell
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```


# 通过 Chocolatey 安装软件

安装软命令 `choco install`, 短写是 `cinst`，可安装的应用程序，可以参见其 Package 列表，window下开发常用的开发环境应用。

## 安装 git

```shell
choco install git.install 
```

## 安装 node

```shell
choco install nodejs.install 
```

## 安装 Microsoft Visual C++ 2010 Redistributable Package

```shell
choco install nodejs.install 
```

## 安装 vagrant

```shell
choco install vagrant
```

## 安装 virtual box

```shell
choco install virtualbox 
```

## 安装编辑器 notepad++/atom/sublime （另外还有各种IDE，不列出了）

```shell
choco install notepadplusplus.install
choco install Atom
choco install SublimeText3 
```

## 安装 Ruby

```shell
choco install ruby
```

## 安装 Python

```shell
choco install python
```

## 安装 Java JDK7 或 JDK8

```shell
choco install jdk7 
```

或

```shell
choco install jdk8 
```

## 安装 Jenkins

```shell
choco install jenkins 
```

这样基本上就可以建立一个强大开发环境了，包含了基本上所有的命令行语言运行环境，构建依赖库，Vagrant， 编辑器， virtual box 以及一个 强大 CI 系统。 其他应用可以根据自己需要从 Package 列表中寻找。

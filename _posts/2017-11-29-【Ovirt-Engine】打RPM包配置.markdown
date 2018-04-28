---
layout: post
title: 【Ovirt-Engine】打RPM包配置
date: 2017-11-29
categories: [环境配置]
description: 打RPM包配置说明
---


# 打RPM包相关说明

官方网站说明：https://www.ovirt.org/develop/developer-guide/engine/engine-development-environment/



## 基本过程

### 1.打rpm包

在ovirt－engine项目中执行下面的命令

```shell
make dist
```

在上一步结束的时候，会看到显示下面的命令 ，执行这个会表示完成所有的打包。耗时较长，且中间可能出现报错的情况

```shell
rpmbuild -tb ovirt-engine-4.1.2.tar.gz
```

所以，一般采用最小化打包的方式

``` sh
rpmbuild -D "ovirt_build_minimal 1" -tb ovirt-engine-4.1.2.tar.gz
```

这个在官网的意思是，只打包针对firefox的浏览器的包

### 1.1针对浏览器的打包

在项目路径根目录下有一个打包控制性文件 ovirt-engine.spec.in 

打开这个文件以后，第21行

```shell
%global _ovirt_build_extra_flags -D gwt.userAgent=gecko1_8 -P gwtdraft
```

注意最后的gecko1_8

翻看官方文档，

https://www.ovirt.org/develop/developer-guide/debugfrontend/

DebugFrontend，当中，有如下一段话



specifies web browser(s) for which to build GWT application(s), supported values:

- `ie8` - Microsoft Internet Explorer 8 - *UserPortal only, WebAdmin requires IE9+*
- `ie9` - Microsoft Internet Explorer 9 and above
- `gecko1_8` - Mozilla Firefox
- `safari` - Safari & Google Chrome
- `opera` - Opera



可以看到，gecko1_8为不同值时，会针对不同的浏览器。

所以，如果需要针对不同的浏览器进行打包，那么就需要修改这个文件的相应参数



### 2. 安装打包文件

⚠️注意，上面步骤打包出来的，仅仅是oVirt中engine的部分，而oVirt非常大，另外的部分，需要通过一个方式来获取

在官方文档中，找到直接安装ovirt的部分

https://www.ovirt.org/documentation/install-guide/chap-Installing_oVirt/

执行下面的命令

安装官方源，然后更新列表

```shell
yum install http://resources.ovirt.org/pub/yum-repo/ovirt-release41.rpm

yum update
```

执行下一段，表示只下载，但是不安装官方的所有rpm包

```shell
yum install ovirt-engine --downloadonly --downloaddir=/tmp/ovirt
```



完成以后，进入到目录中，将第一步打包生成的rpm包覆盖进来，就可以产生整个安装所需要的所有rpm文件了

执行下面的命令，从本地安装

```shell
yum localinstall *
```



## 注意

- 1  打包生成的文件中，有一个带有docker的，如：ovirt-engine-setup-plugin-dockerc-4.1.2-1.el7.centos.noarch.rpm，这个是docker相关的，在安装的时候，需要删除，以免安装docker相关内容
- 2  使用第二步下载的官方安装包，一定是最新稳定版本的安装包，但是我们打包的engine包，不一定是最新的，那么如果不同的版本在覆盖融合的时候，可能出现问题，需要注意
- 3 使用打包命令的时候，可能出现ulimit报错的问题，执行下面的命令修改


```shell
sudo sh -c "ulimit -n 65535 && exec su $LOGNAME"
```


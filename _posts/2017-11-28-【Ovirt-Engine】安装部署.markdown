---
layout: post
title: 【Ovirt-Engine】CentOS 安装部署ovirt-engine
date: 2017-11-28
categories: 环境
description: CentOS 安装部署ovirt-engine手记
---



**简要说明**

overt-engine的编译安装，硬件配置，需要尽量大的内存，16G以上最好，8G也行，整个过程可分为以下几步进行：

1. 安装依赖包
2. 配置数据库
3. 获取代码
4. 编译&安装
5. 修改代码后




## 安装依赖包

### 添加源地址

> ⚠️注意：源地址需要根据版本有所变化，这个需要看[官方文档](https://www.ovirt.org/documentation/install-guide/chap-Installing_oVirt/)

点击路径：`Documentation` -> `Install-guide` -> `Installing oVirt` 这个里面的最开始会说安装源

一般我们在4.1.*版本下是下面的这个源地址

``` shell
yum install -y http://resources.ovirt.org/pub/yum-repo/ovirt-release42.rpm
```

### 安装相关依赖

安装了源以后，需要安装相关软件和依赖

> 注意：依赖包必须全部安装完毕，否则后面正常启动

``` shell
yum install -y git java-devel maven openssl postgresql-server m2crypto python-psycopg2 python-cheetah python-daemon libxml2-python unzip pyflakes python-pep8 python-docker-py mailcap python-jinja2 python-dateutil bind-utils

yum install -y ovirt-engine-wildfly ovirt-engine-wildfly-overlay

yum install -y ovirt-host-deploy ovirt-setup-lib ovirt-js-dependencies
```

> 注意，安装oVirt需要Open JDK，如果系统默认Java不是Open JDK在后面关于JDK报错，那么执行下面的修改

``` shell
alternatives --config java
alternatives --config javac
```



## 配置数据库

初始化postgresql数据库

```shell
postgresql-setup initdb
```

配置数据库登录权限

修改目录 `/var/lib/pgsql/data/`（某些系统会存放在 `/etc/postgresql*`） 下的如下两个文件

- `pg_hba.conf`

	```shell
	# IPv4 local connections:
	host    all             all             0.0.0.0/0               password
	host    all             all             127.0.0.1/32            password
	```

- `postgresql.conf`

	```shell
	listen_addresses = '*'
	max_connections = 150

	work_mem = 8192
	maintenance_work_mem = 65536
	autovacuum_max_workers = 6
	autovacuum_vacuum_scale_factor = 0.01
	autovacuum_analyze_scale_factor = 0.075
	```

修改完成以后，执行下面的命令，重启服务

``` shell
systemctl restart postgresql.service
```

配置服务随系统一起启动

``` shell
systemctl enable postgresql.service
```

配置登录的用户名和密码等信息

``` shell
su - postgres -c "psql -d template1 -c \"create user engine password 'engine';\""
su - postgres -c "psql -d template1 -c \"create database engine owner engine template template0 encoding 'UTF8' lc_collate 'en_US.UTF-8' lc_ctype 'en_US.UTF-8';\""
```



## 获取代码

从git上获取ovirt/engine的官方代码后，首先需要查看remote分支，并切换到已经发布的release版本，然后再开始按照官方说明文档的开始编译安装。

```shell
mkdir -p "$HOME/git"
cd "$HOME/git"
git clone https://gitee.com/hikrosoft/ovirt-engine
git branch -r
git checkout -b <稳定分支名(本地)> origin/ovirt-engine-<稳定分支名（远程）>
```



## 编译&安装

> ⚠️注意，按照官方的，编译的时候会去跑test过程，这个非常耗时，而且，非常有可能会在中间某个过程报错，导致整个过程失败。所以，为了效率起见，可以在编译命令中添加 `BUILD_UT=0` 使得安装过程不 test

### 编译

``` shell
make clean install-dev PREFIX="$HOME/ovirt-engine" BUILD_UT=0 DEV_EXTRA_BUILD_FLAGS_GWT_DEFAULTS="-Dgwt.locale=en_US,zh_CN"
```

### 安装(配置管理员，配置数据库等过程)

``` shell
$HOME/ovirt-engine/bin/engine-setup
```


### 启动服务

``` shell
$HOME/ovirt-engine/share/ovirt-engine/services/ovirt-engine/ovirt-engine.py start
```

- 如果，编译过程哪个地方有bug，请切换分支，tag等，多次尝试。如果，安装配置过程有错误，请确认是否有依赖没有安装完成。

- 如果在编译启动以后，无法进入管理页面或者用户界面，并且终端显示缺少必要的包，则应为缺少必要的组建

执行下面的命令安装组件

```shell
yum install patternfly1
```




## 修改代码后

### 重新编译
```shell
make clean install-dev PREFIX="$HOME/ovirt-engine"
```

### 重新编译指定模块
```shell
make clean install-dev PREFIX=$HOME/ovirt-engine EXTRA_BUILD_FLAGS="-pl org.ovirt.engine.core:bll,org.ovirt.engine:engine-server-ear"
```

### GWT调试模式
```shell
make install-dev PREFIX="$HOME/ovirt-engine"
make gwt-debug DEBUG_MODULE=<module>
```

这里的 `<module>` 是指 `webadmin` 或者 `userportal-gwtp`


# 参考资料

- [官方说明文档：engine-development-environment](https://www.ovirt.org/develop/developer-guide/engine/engine-development-environment/)
- [ovirt-engine安装](https://www.cnblogs.com/starof/p/4772890.html)
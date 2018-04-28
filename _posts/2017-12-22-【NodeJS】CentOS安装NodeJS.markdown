---
layout: post
title: 【NodeJS】CentOS安装NodeJS
date: 2017-12-12
categories: [环境配置]
description: CentOS下安装最新NodeJS操作步骤
---


# NodeJS RPM spec

- node.js rpm spec : https://github.com/kazuhisya/nodejs-rpm
- node.js source : https://nodejs.org/dist/

# Compiled Package

- You can find prebuilt rpm binary from here(el7 and fc23, 24)
	- Stable Release: FedoraCopr khara/nodejs Copr
	- LTS Release: FedoraCopr khara/nodejs-lts Copr


## el7:

```shell
sudo curl -sL -o /etc/yum.repos.d/khara-nodejs.repo https://copr.fedoraproject.org/coprs/khara/nodejs/repo/epel-7/khara-nodejs-epel-7.repo
sudo yum install -y nodejs nodejs-npm

```

## fc23, 24:

```shell
sudo dnf copr enable khara/nodejs
sudo dnf install -y nodejs nodejs-npm
```


# Building the RPM

## Distro support

### Tested

- RHEL/CentOS 7 x86_64
- Fedora23, 24 x86_64


### Probably it works

- RHEL/CentOS/SL/OL 6 x86_64
	- when you try to build on el6, can use devtoolset-3 and SCL repository
		- RHEL6.x: Red Hat Developer Toolset 3 and Red Hat Software Collections
		- CentOS6.x: install centos-release-scl-rh package.
	- devtoolset-3-gcc-c++, devtoolset-3-binutils, python27

- RHEL/CentOS/SL/OL 5 x86_64
	- when you try to build on el5, you can use devtoolset-2 and python27
		- Developer Toolset 2
			- RHEL5.x: Red Hat Developer Toolset 2
			- CentOS5.x: devtools-2
		- Python 2.7
			- IUS Community Project
			- devtoolset-2-gcc-c++, devtoolset-2-binutils, python27


### Prerequisites:

- Python 2.7
- gcc and g++ 4.8 or newer


## Docker (el7, el6, el5)

Docker environment for building nodejs rpm. It will help to build and debug.

- See also: docker/README.md
- You can also try this:  Docker Hub kazuhisya/nodejs-rpm (el7 only)


## Build (el7, el6)

setting up:

```shell
sudo yum install -y yum-utils rpmdevtools make
```
git clone and make:

```shell
git clone https://github.com/kazuhisya/nodejs-rpm.git
# If you want to use other version, You can clone to specify the branch name.
# example: git clone -b v4.x https://github.com/kazuhisya/nodejs-rpm.git
cd nodejs-rpm
sudo yum-builddep ./nodejs.spec
```

el7:

```shell
make rpm
```

el6 : with Software Collections and Devtoolset

```shell
scl enable python27 devtoolset-3 'make rpm'
```

install package:

```shell
cd ./dist/RPMS/x86_64/
sudo yum install ./nodejs-X.X.X-X.el6.x86_64.rpm ./nodejs-npm-X.X.X-X.el6.x86_64.rpm --nogpgcheck
```

## Build (el5)

el5 : with Devtoolset and python27

```shell
sudo yum install -y epel-release ius-release
sudo yum install -y yum-utils rpmdevtools buildsys-macros redhat-rpm-config tar make openssl-devel libstdc++-devel zlib-devel gzip 
sudo yum install -y devtoolset-2-gcc-c++ devtoolset-2-binutils python27
git clone https://github.com/kazuhisya/nodejs-rpm.git
cd nodejs-rpm
rpmdev-setuptree
curl -OLk https://nodejs.org/dist/vX.X.X/node-vX.X.X.tar.gz
cp *.patch ~/rpmbuild/SOURCES/ ; cp *.md ~/rpmbuild/SOURCES/ ; cp *.tar.gz ~/rpmbuild/SOURCES/ 
scl enable devtoolset-2 'rpmbuild -ba ./nodejs.spec'
```

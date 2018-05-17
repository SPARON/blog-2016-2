---
layout: post
title: 【Vagrant】Vagrant使用 - 2.手动创建Vagrant虚拟机
date: 2018-05-10
categories: [环境配置]
description: 网络下载不太靠谱，官方镜像网站下载速度太慢，可以尝试手动自己创建。简单几步即可创建，需要注意的是权限和virtulbox addition的安装，否则会出错哦！
keywords: vagrant
---

# 操作步骤
1. VirtualBox安装虚拟机
2. 配置用户名（建议用户名、密码都用：vagrant）
3. 配置用户免密执行sudo权限命令
4. 安装VBoxGuestAditions.iso
5. 如果用户名、密码为vagrant可添加ssh key到用户目录（~/.ssh/authorized_keys）
6. `vagrant package --base <VB虚拟机名称> --output <输出box名称>`
7. `vagrant box add <输出box名称> --name <vagrant管理名称>`
8. `vagrant init <vagrant管理名称>`
9. `vagrant up`
10. `vagrant ssh`

# 安装过程遇到的问题

## SSH用户名密码未配置

由于虚拟机内未配置ssh key，导致vagrant启动虚拟机后无法连接。

![](/resources/2018-05-10-手动创建Vagrant虚拟机/1-ssh用户名密码未配置_1.PNG)

**解决方案：（以下两种任选其一）**

1. 在vagrantfile中添加ssh用户名、密码配置

   ```shell
   config.vm.boot_timeout = 360
   config.ssh.username = "vagrant"
   config.ssh.password = "vagrant"
   ```

2. 将ssh key文件添加到用户目录的`.ssh`目录下，路径为：`/home/vagrant/.ssh/authorized_keys`



## 用户sudo权限未免密

![](/resources/2018-05-10-手动创建Vagrant虚拟机/2-用户sudo权限未免密_1.PNG)
![](/resources/2018-05-10-手动创建Vagrant虚拟机/2-用户sudo权限未免密_2.PNG)

**解决方案**：

`vi /etc/sudoers`添加`NOPASSWD:`，如下所示：

```shell
root    ALL=(ALL)       ALL
vagrant ALL=(ALL)       NOPASSWD:       ALL
```



## Virtualbox additions未安装

![](/resources/2018-05-10-手动创建Vagrant虚拟机/3-virtualbox additions未安装_1.PNG)

**解决方案**：

没什么其他说的，就是安装了，如果安装过程中缺包，就`yum install -y <packagename>`安装对应包就行了。

```shell
mkdir /media/cdrom
mount /dev/sr0 /media/cdrom
cd /media/cdrom
./VBoxLinuxAdditions.run
```



## 成功启动
最后还是放一张成功的图吧!

![](/resources/2018-05-10-手动创建Vagrant虚拟机/4-成功.PNG)



# 参考资料

1. [使用 VirtualBox 创建 Vagrant Boxes 的完全指南 ](https://linux.cn/article-9144-1.html)
2. [制作自己的Vagrant Box](https://segmentfault.com/a/1190000002507999)
3. [create vagrant base box注意事项](https://blog.csdn.net/ling1874/article/details/46819405)
4. [[已解决]vagrant共享文件夹挂载失败.Vagrant was unable to mount VirtualBox shared folders](https://blog.csdn.net/ifeng6/article/details/76316991)
5. [VirtualBox中的Centos安装增强功能包VBoxLinuxAdditions和共享本机文件夹](https://blog.csdn.net/buyueliuying/article/details/51645649)
6. [CentOS7 在 VirtualBox 上的安装配置（2） -- VirtualBox 增强包安装篇](https://segmentfault.com/a/1190000006233585)
7. [使用Vagrant安装的box镜像都放在了哪里？可以更改嘛？](https://blog.csdn.net/gsls181711/article/details/49450013)
8. [vagrant系列二：vagrant的配置文件vagrantfile详解](https://blog.csdn.net/hel12he/article/details/51089774)
9. [vagrant配置文件vagrantfile详解 ](https://www.36nu.com/post/264)


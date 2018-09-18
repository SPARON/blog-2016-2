---
layout: post
title: 【Linux】LinuxMate下安装ThinkPad E431 Wifi驱动
date: 2018-09-18
categories: [环境配置]
description: LinuxMate下安装ThinkPad E431 Wifi驱动
keywords: [Linux, wifi]
---


Linux中通常有线网卡为eth0，无线网卡则为wlan0，后续增加的以此类推（可能某些无线网卡型号命名为eth1，而非wlan0。用ifconfig命令查看系统的网卡信息，根本没有出现wlan0或者eth1，说明驱动没有安装。


安装网卡驱动的话，需要了解网卡类型，用`lspci`命令查看，发现网卡是

> Broadcom Corporation BCM43142 802.11b/g/n (rev 01)


尝试了很多办法，终于在下面的网上找到了解决方法：

[how-do-i-install-bcm43142-wireless-drivers-for-dell-vostro-3460-3560](http://askubuntu.com/questions/175104/how-do-i-install-bcm43142-wireless-drivers-for-dell-vostro-3460-3560) 



**执行以下命令即可：**

```shell
sudo apt-get install linux-headers$(uname -r | grep -Po "\-[a-z].*")

sudo apt-get install build-essential dkms

sudo apt-get install dpkg

sudo apt-get install bcmwl-kernel-source
```


然后无线网络就可以用了，用ifconfig命令发现出现了无线网卡，享受WIFI吧~




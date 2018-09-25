---
layout: post
title: 【Linux】Linux下SSR客户端的配置与开机自启
date: 2018-09-18
categories: [环境配置]
description: Linux下SSR客户端的配置与开机自启 
keywords: [Linux, wifi]
---

原文出自：[Lucien's Blog](http://www.lucien.ink/archives/208/)

# 环境

需要有`git`、`python3`，如果没有的话：

## Ubuntu

```shell
sudo apt install git python3 -y
```

## CentOS

```shell
sudo yum install git python3 -y
```

# 配置SSR

## 下载安装

```shell
sudo git clone https://github.com/LucienShui/shadowsocksr.git && sudo mv shadowsocksr /opt/ && cd /opt/shadowsocksr/ && sudo cp config.json user_config.json && sudo chmod +x ssr.sh && sudo cp ssr.sh ~/ && cd ~
```

## 编辑SSR的配置文件

  把上面的命令拷到控制台里，运行结束后，执行 `sudo gedit /opt/shadowsocksr/user_config.json` 来编辑你的连接信息，具体的服务器地址，端口，密码，加密方式，协议插件，混淆插件从SSR帐号提供商那里获取。

  主要用到的是以下这几个选项：

```
"server": "0.0.0.0",         # 服务器地址
"server_port": 80890,        # 端口
"password": " ",             # 密码
"method": "chacha20",        # 加密方式
"protocol": "auth_sha1_v4",  # 协议插件
"obfs": "http_simple",       # 混淆插件
```

## 启动SSR客户端

  在~目录下有一个ssr.sh，输入 `~/ssr.sh` 就可以启动客户端。

## 配置开机自启动

  GNOME和Unity桌面环境可以直接打开Startup Applications Preferences，然后在里面添加一个 `/opt/shadowsocksr/ssr.sh` 的启动项即可，KDE同理。

![](https://www.lucien.ink/usr/uploads/2018/06/2137286271.png)

## 配置浏览器

  因为某些原因（我不是很清楚），在大多数Linux下只成功启动ssr客户端的话会发现并没有什么作用，该进不去的仍然进不去，在这里就直接讲在Chrome内自动代理（国内走直连，特定网站走ssr）的解决方案吧。
安装SwitchyOmega

### Chrome

  进入 https://file.lucien.ink/SwitchyOmega ，下载SwitchyOmega.crx

  然后在Chrome里打开 `chrome://extensions`，把 SwitchyOmega.crx 文件拖放到扩展程序页面，点击添加扩展程序进行安装。
  
### Firefox

  进入 https://addons.mozilla.org/zh-CN/firefox/addon/switchyomega/ ，点击添加即可。

## 配置SwitchyOmega

  打开SwitchyOmega的设置页面，跳过设置向导，点击导入/导出、在线恢复，填入 https://file.lucien.ink/SwitchyOmega/OmegaOptions.bak ，恢复完成后点击应用选项。

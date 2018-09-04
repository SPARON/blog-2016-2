---
layout: post
title: 【Linux】Linux忘记root密码
date: 2018-09-04
categories: [环境配置]
description: Linux忘记root密码后，通过通过修改登录模式后修改root密码
keywords: [Linux, root]
---

基于Red Hat Enterprise Linux 7.5

![](https://images2018.cnblogs.com/blog/1439864/201807/1439864-20180722065456669-830913209.png)

- 在启动引导主页上按e进入内核编辑

    ![](https://images2018.cnblogs.com/blog/1439864/201807/1439864-20180722065755367-1748136732.png)

- 找到 Linux16 这一段，在末尾处添加 rd.break

    ![](https://images2018.cnblogs.com/blog/1439864/201807/1439864-20180722065947954-869547817.png)

- 编辑完成后，按下组合键CTRL+X运行内核程序进入紧急救援模式

- 重启后进入如下界面
    ![](https://images2018.cnblogs.com/blog/1439864/201807/1439864-20180722070123585-1737756067.png)

- 在这个模式下依次输入以下命令
    ```shell
    mount -o remount,rw /sysroot
    chroot /sysroot
    passwd  # 注意：到这里的时候会提示输入两次需要重置的密码，输入完成之后回车即可
    touch /.autorelabel
    exit
    reboot
    ```

    ![](https://images2018.cnblogs.com/blog/1439864/201807/1439864-20180722070542896-1093353535.png)

- 重新进入系统输入刚刚重置的密码即可登陆root账户
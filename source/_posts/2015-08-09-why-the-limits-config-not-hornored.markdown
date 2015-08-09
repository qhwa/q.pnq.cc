---
layout: post
title: "为什么 limits 不生效"
date: 2015-08-09 21:14:35 +0800
comments: true
categories: 
---

最近遇到一个奇怪的问题，无法将服务器的最大文件打开数量提高。

服务器是 Ubuntu Server 14.04

    $lsb_release -a
    No LSB modules are available.
    Distributor ID:	Ubuntu
    Description:	Ubuntu 14.04.2 LTS
    Release:	14.04
    Codename:	trusty

正常情况下， `/etc/security/limits.conf` 的改动，应该在下次访问时就生效才对。
但是总是没生效，查了很多资料，尝试了很多修改，终于成功了

## 记录一下填的坑：

1. 确保 pam 生效

    在 `/etc/pam.d/login` 中，存在:

        session required pam_limits.so


2. 确保 ssh 使用 pam

    在 `/etc/pam.d/sshd` 中，存在:

        session required pam_limits.so

    在 `/etc/ssh/ssd_config` 中, 存在:

        UsePAM yes

3. limits.conf 建议不要使用星号

    官方 manual 以及网上的教程有很多都用了 `*` 符号，然而不是所有系统都认的，我最后发现问题就是在这里！

        # 不兼容方式:
        * soft nofile 51200
        * hard nofild 51200
        
        # 兼容方式
        root soft nofile 51200
        root hard nofile 51200

        qhwa soft nofile 51200
        qhwa hard nofile 51200

## 如何确认问题之所在

* 查看当前用户的 limits

    ulimit -a

* 查看另外一个用户的 limits

    # 注意 ulimit 不是命令，而是 shell 方法
    sudo -u <USER> sh -c 'ulimit -a'

* 经过 ssh 查看用户的 limits

    ssh example.com 'ulimit -a'


---
layout: post
title: Ubuntu下使用Array SSL VPN客户端连接VPN网络
tags:
- '- linux -'
- array
- ubuntu
- vpn
status: publish
type: post
published: true
meta:
  _edit_last: '2'
  dsq_thread_id: ''
---
公司用的[Array Networks][AN]提供的SSL VPN系统，vpn网页在Ubuntu下无法正常启动Java Applet。幸好得到了[wenyue](http://wenyue.me/blog/)的指点，找到了方法。如果你也是Ubuntu系统，需要连接到Array SSL VPN，可以参考一下。

安装步骤
--------

1.下载[Array Networks][AN]提供的客户端程序 array_vpnc.bin

    #!bash
    sudo apt-get install libc6-i386 #64位系统也是这个包
    wget https://q.pnq.cc/uploads/array_vpnc.bin
    chmod a+x array_vpnc.bin


2.下载这个小脚本到同个目录

    #!bash
    #下载辅助脚本
    wget https://q.pnq.cc/uploads/vpn-for-common.sh -O vpn.sh
    #里面会包含重要信息，我们不想别人随便访问
    chmod 700 vpn.sh


3.修改vpn.sh中的配置，将vpn_host、user、key修改为你的配置

    #!bash
    vpn_host=your_vpn_server
    user=your_user_name
    key=your_static_passwd #密码中不变的部分


使用方法：
---------

    #!bash
    ./vpn.sh

然后根据提示输入，当看到这个提示时，就说明成功了：
> array_vpnc: VPN TUNNEL SUCCESSFUL!


Have fun!

[AN]: http://www.arraynetworks.com.cn/

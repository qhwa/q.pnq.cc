---
layout: post
title: 自动更新git目录
tags:
- '- linux -'
status: publish
type: post
published: true
meta:
  _edit_last: '2'
  dsq_thread_id: '391398513'
---

假设我们有一批文件用[Git](http://git-scm.com)在管理，然后在服务器上做了一个repo。团队成员先从服务器pull下来最新的版本，然后在本地修改并提交，最后push回服务器，这是很典型的应用场景。

假如现在需要服务器端收到客户端的push后，能自动更新repo目录里面的文件，听起来很简单，用钩子就可以了，不过还是遇到一些问题，好在最后在google帮助下搞定。

总结的步骤如下：

1.先在服务器端运行设置，接受提交

    git config receive.denyCurrentBranch ignore

2.把以下内容保存为服务器端repo中的钩子文件（**.git/hooks/post-receive**）

    #!bash
    \#!/bin/sh
    cd ..
    env -i git reset --hard

3.设置权限为可运行

    chmod a+x post-receive

好了，这样每当服务器收到客户端的push，就会自动更新文件列表了

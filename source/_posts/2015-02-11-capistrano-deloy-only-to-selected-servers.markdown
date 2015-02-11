---
layout: post
title: "capistrano-hostmenu: 只操作指定的服务器"
date: 2015-02-11 22:10:44 +0800
comments: true
categories: 
---

想必大家都用过 [capistrano] 了，部署代码到多个服务器上的神器。
不过使用中有个不太方便的地方是，某些情况下只想部署到其中几台。

例如我们新增了一个功能，但只想找一台服务器先部署上去测试一下，成功后再部署到整个集群。

有好几种方式可以做到：

1. 临时修改发布脚本（`config/deploy.rb` 或 `config/deploy/***.rb`）
2. 使用 `HOST` 命令行环境变量，或者 `--host` 参数, 比如 `HOST=example.com cap production deploy`

第1种不好重用，第2种在 [capistrano] v3.3 以上版本已经失效了。

我把我们项目中用的 task 抽出来做成了一个 gem: [capistrano-hostmenu]
功能实在是太简单，没有什么好描述的。。

一图顶千言：

![](https://ruby-china-files.b0.upaiyun.com/photo/2015/fd0dc13527ea01a9c5461ddc2b37638a.png)


[capistrano]: http://capistranorb.com/
[capistrano-hostmenu]: https://github.com/qhwa/capistrano-hostmenu

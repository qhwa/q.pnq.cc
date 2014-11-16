---
layout: post
title: "如何开发 ruby 命令行工具"
date: 2014-11-16 15:54:01 +0800
comments: true
categories: 
---


最近太太的[花瓣][huaban]账号突然被封，苦心采集的很多图片一下子全部看不到了！
后来虽然联系客服重新开通了账号，但还是心有余悸，觉得还是 [pinterest](http://www.pinterest.com/) 靠谱一些，准备把图片全部迁移到 pinterest 上。由于图片数量比较多，我就用 ruby 写了一个工具，将花瓣上的图片下载下来。（不过 pinterest 不能批量上传，这些图片也只是备份到本地，这是后话了）

这个项目已开源，地址是：
https://github.com/qhwa/huaban_exporter

我喜欢用命令行工作，之前做的几个 gem（[lfd](https://github.com/qhwa/lfd), [fdlint](https://github.com/qhwa/fdlint)）也都提供了命令行。这次就趁这个项目总结了一下怎样用 ruby 开发友好的命令行工具。

1. 初期怎样提高开发效率？

    在写了基础的一些逻辑 model 后，我写个简单的 [rake 文件](https://github.com/qhwa/huaban_exporter/blob/69b16009357a87f2e6e645801694a16b65803a41/Rakefile)，初期用 rake 来作为入口，边开发边测试。

    ~~~sh
    rake boards         # 列出一个用户的所有画板 (user=用户名 rake boards)
    rake export_board   # 导出一个画板的所有图片到本地 (board_id=画板id  rake export_board)
    rake export_boards  # 导出用户所有的画板图片到本地 (user=用户名 rake export_boards)
    rake pins           # 列出一个画板所有的采集 (board_id=画板id rake pins)
    ~~~

2. 项目后期功能稳定后，怎么做命令行入口

    rakefile 很适合自己用，但是要分发别人用，用 rakefile 就不方便了。做成带命令行脚本的 gem 更加方便。

    1. 在 bin 目录下写一个文件，名字就是最终别人要用的命令
    2. 给这个文件加上 [shebang](http://zh.wikipedia.org/zh-cn/Shebang):

        ~~~sh
        #!/usr/bin/env ruby
        ~~~

    3. 给这个文件加上执行权限:

        ~~~sh
        chmod a+x bin/YOUR_SCRIPT
        ~~~

    > 这一步我以前是用下面提到的 gli 来自动进行，但后来改成手动做了，因为很简单，并且 gli 生成了一些额外的文件，和 bundle 有点冲突。

3. 怎样让命令变得友好?

    有个超棒的 gem 叫做 [gli][gli]，帮你很容易实现出类似 git 这样风格的脚本


4. 项目完成后，怎么用做成一个 gem，分享给别人?

    [bundler][bundler] 提供了生成 gem 的功能

    1. `bundle gem <name>` 生成目录结构
    2. 修改 gemspec
    3. `rake install` 先在本地安装这个 gem 进行测试
    4. `rake build`   以最新的文件重新打包成 gem
    5. `gem push pkg/<版本>.gem` 将gem上传到 https://rubygems.org


[huaban]: http://www.huaban.com
[proj]: https://github.com/qhwa/huaban_exporter
[gli]: https://github.com/davetron5000/gli
[bundler]: http://bundler.io/

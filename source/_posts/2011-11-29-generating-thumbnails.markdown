---
layout: post
title: Ubuntu下在命令行批量生成缩略图
tags:
- '- linux -'
- batch
- generating
- image
- imagemagick
- process
- thumbnail
- ubuntu
status: publish
type: post
published: true
meta:
  _edit_last: '2'
  dsq_thread_id: '487398110'
---
{% codeblock lang:sh %}
# 准备工作：安装 imagemagick
sudo apt-get install imagemagick
cd /path/to/big/images #大图所在的目录

#创建小图对应的目录结构
find . -type d -print -exec mkdir '../small/{}' -p \\;

#批量转换! 等比例缩小到320x320之内
find . -type f -name '*.jpg' -print -exec \\
convert '{}' -resize 320x320 '../small/{}' \\;
{% endcodeblock %}

这样小图都会按原先的目录结构，在上级目录的small目录出现了

其实[imagemagick](http://www.imagemagick.org)是一个超级神器，上面只是它很简单的一个应用...

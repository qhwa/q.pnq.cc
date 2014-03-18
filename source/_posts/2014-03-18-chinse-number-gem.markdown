---
layout: post
title: "chinese_number: 一个解析汉字数字的 ~rubygem"
date: 2014-03-18 17:45:38 +0800
comments: true
categories: 
---

[ruby-china](http://ruby-china.org) 上有人问到[怎么优雅地解析汉字数字](http://ruby-china.org/topics/17913)，比如 `二十五` 解析成 `25` 。我第一反应是应该查一下有没有这样的 gem，因为是一个很普遍的需求，说不定已经有人实现了呢！

不过很可惜，不知道是不是我没有查到，还是真的没有，总之没有找到。所以我就写了一个这样的 gem -- **[chinese_number](https://github.com/qhwa/chinese_number)**

用法很简单：

{% codeblock lang:ruby %}
require 'chinese_number'

ChineseNumber.trans '今天二十万'
#=> "今天200000"

ChineseNumber.extract "今天二十晚"
#=> [20]

ChineseNumber::Parser.new.parse '二零一四'
#=> 2014

ChineseNumber::Parser.new.parse '一万三千'
#=> 13000
{% endcodeblock %}

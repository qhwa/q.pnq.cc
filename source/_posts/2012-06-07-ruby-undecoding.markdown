---
layout: post
title: Ruby 如何“反转义”字符串
tags:
- '- Ruby -'
status: publish
type: post
published: true
meta:
  _edit_last: '2'
  dsq_thread_id: '716384023'
---
我们知道Ruby中转义字符串可以用inspect或者dump可以将字符串转义：

{% codeblock lang:ruby %}
"\\t".dump       #=> "\\"\\\\t\\""
"中文".dump     #=> "\\"\\\\u{4e2d}\\\\u{6587}\\""
{% endcodeblock %}

但有时候我们想把已经被转义的字符串反转义回正常的字符串，怎么办?

其实方法很简单：

{% codeblock lang:ruby %}
def unescape( src )
  String.class_eval(%Q("#{src}")) 
end

p unescape("\\\\t\\\\n") == "\\t\\n"  #=> true
{% endcodeblock %}

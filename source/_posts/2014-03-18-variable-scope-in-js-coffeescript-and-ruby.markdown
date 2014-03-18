---
layout: post
title: "《代码的未来》 阅读笔记（1）—— JavaScript/CoffeScript/ruby 局部变量处理的异同"

date: 2014-03-18 16:21
comments: true
categories: 
---

> …… 身为 JavaScript 程序员的好友说，对 javascript 的不满之一，就是它的变量声明和作用域。 —— Mats

## JavaScript

js 可以通过有无`var`来选择是否创建一个新的作用域：

{% codeblock lang:javascript %}
var a = "out";
(function() {
  var a = "in";
})();

alert( a );
// "out"
{% endcodeblock %}

{% codeblock lang:javascript %}
a = "out";
(function() {
  a = "in";
})();

alert( a );
// "in"
{% endcodeblock %}

很灵活。不幸的是，不小心漏写最外层 `var` 之后，变量有可能会变成全局变量，这是容易滋生 bug 的地方。

## CoffeeScript

CoffeeScript 中统一去掉了`var`，全部按局部变量处理，和 js 不同的是，不再创建内层作用域了。

{% codeblock lang:coffeescript %}
a = "out"
(() ->
  a = "in"
)()
alert( a )
// "in"
~~~
{% endcodeblock %}

## Ruby

{% codeblock lang:ruby %}
# version 1
a = "out"
(lambda do
  a = "in"
end).call
puts a
#=> "in"
~~~
{% endcodeblock %}

{% codeblock lang:ruby %}
# version 2
# ruby 1.9+
a = "out"
1..2.each do |i; a|
  a = "in"
end
puts a
#=> "out"
{% endcodeblock %}

Ruby 中默认和 CoffeeScript 一致，使用外层作用域。但多了一种“作用域声明”，允许人工制定创建一个作用域。

结论

 语言 | 同名局部变量处理策略 
------|----------------------
 js  | 内部优先，可以通过去掉 var 向上查找
 coffeescript | 外部
 ruby | 外部优先，可以通过声明强制使用内部

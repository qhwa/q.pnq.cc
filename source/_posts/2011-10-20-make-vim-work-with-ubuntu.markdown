---
layout: post
title: 让VIM与Ubuntu和睦相处
tags:
- '- linux -'
status: publish
type: post
published: true
meta:
  _edit_last: '2'
  dsq_thread_id: '448444940'
---
[Vim][]和[Ubuntu][]都是我的好朋友，不过他们之间好像有点不和睦。在[Ubuntu][]11.04下gvim的菜单不能集成进全局菜单条(global menu)，而在[Ubuntu][]11.10下gvim打开之后会非常卡。需要调解一下 :D

## 解决gvim在[Ubuntu][] 11.04中菜单显示的问题
执行gvim时，gvim的菜单不能立刻显示出来。并且报错：
> ** (gvim:15150): WARNING **: Unable to register window with path '/com/canonical/menu/4200024': Timeout was reached

解决方法是运行：

{% codeblock lang:sh %}
echo 'alias gvim="env UBUNTU_MENUPROXY=0 gvim"' >> ~/.bashrc
source ~/.bashrc
{% endcodeblock %}

----

## 解决gvim在[Ubuntu][] 11.10中导致电脑很卡的问题
运行：

{% codeblock lang:sh %}
echo 'alias gvim="gvim -f"' >> ~/.bashrc
source ~/.bashrc
{% endcodeblock %}

----

## 解决提示“pixmap”的问题
如果终端中提示：
> (gvim:2353): Gtk-WARNING **: 无法在模块路径中找到主题引擎：“pixmap”， 

解决方法是运行：

{% codeblock lang:sh %}
sudo apt-get install gtk2-engines-pixbuf  
{% endcodeblock %}


[Vim]: http://www.vim.org
[Ubuntu]: http://www.ubuntu.com

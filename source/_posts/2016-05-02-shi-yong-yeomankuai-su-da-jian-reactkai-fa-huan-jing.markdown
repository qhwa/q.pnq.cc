---
layout: post
title: "Setting Up Your React Project Is Easier Than You Think"
date: 2016-05-02 22:16:08 +0800
comments: true
categories: 
---

I have heard some ones complaining that setting up a [Webpack][Webpack] + [React][React] project is not an easy job. It's only partly true. [Webpack][Webpack] is not well documented at this moment, and has many powerful features and plugins. This makes configuration on [Webpack][Webpack] seeming difficult to new developers. To make things even worse, there are tons of 'starter kit' projects over there, most of which are lack of maintainance.


![Yeoman](http://yeoman.io/static/yeoman-02.83c46c7213.png)

Indeed, it is super easy to setup a brand new [Webpack][Webpack] + [React][React] project using [Yeoman][Yeoman].

[Yeoman][Yeoman] is a scaffolding tool for web developers. With diffrent `generators` we can generate different kinds of web projects quickly by lines of command.

Here's how it is done:

~~~sh
# install Yeoman command and generator
npm install -g yo
npm install -g generator-react-webpack

# generate project
mkdir test-project
cd test-project
yo react-webpack
~~~

Thanks to [generator-react-webpack](https://github.com/newtriks/generator-react-webpack), answer some questions from `yo` and you will get your project setup.

Easy and quick.

Also this generator can help [generate React components](https://github.com/newtriks/generator-react-webpack#generating-new-components) via command line.

[Yeoman]: http://yeoman.io/
[Webpack]: https://webpack.github.io/
[React]: https://facebook
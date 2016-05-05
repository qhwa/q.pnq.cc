---
layout: post
title: "minifying-with-webpack"
date: 2016-05-05 10:09:12 +0800
comments: true
categories: 
---

![webpack bundling](https://cdn-images-1.medium.com/max/1600/1*rsOjd1jR3eOmJNJh4Zp42g.png)

When coding in a modern modular way with Webpack is done, it enters the deploy phrase. We minify assets to reduce the network transfer cost. While bundling is not necessary nowadays thanks to HTTP/2, minifying is still an important work, because in many cases we can reduce the size to transfer between servers and clients:

* unreachable codes can be removed
* comments code can be removed
* images can be optimised losslessly
* variable names can be shortened in Javascript
* HTML and SVGs can be optimised 

Here in [Helijia][helijia], we use webpack to build mobile apps. Here are some notes from us on minifying with [Webpack][Webpack].

## Minifying Javascript / CSS
[Webpack][Webpack] is shipped with some builtin plugins which can do the job well.
* [Dedupe Plugin](https://webpack.github.io/docs/list-of-plugins.html#dedupeplugin) searches for similar files and deduplicated them in the output.
* [UglyfiJS Plugin](https://webpack.github.io/docs/list-of-plugins.html#uglifyjsplugin) uses the famous [UglifyJS][UglifyJS] to minify JS and CSS assets.

### Tip: Use webpack stats to review your modules
Webpack can generate packing stats in json format while packing. We use [Webpack visualizer](https://chrisbateman.github.io/webpack-visualizer/) to visualize it to find which part of our works can be optimized. It helps a lot by providing an detail view inside the bundled file.

![webpack viz](https://cdn-images-1.medium.com/max/1600/1*fNQylMzJclEm5VDbVuHwVQ.png)

## Minifying HTML
[HTML webpack plugin](https://github.com/ampedandwired/html-webpack-plugin) can help minifying HTML. Here is an example config:

{% codeblock lang:js %}
new HtmlWebpackPlugin({
  template : path.join(__dirname, '../src/template.html.ejs'),
  filename : 'index.html',
  title    : '河狸家',
  inject   : 'body',
  minify   : {
    html5                          : true,
    collapseWhitespace             : true,
    minifyCSS                      : true,
    minifyJS                       : true,
    minifyURLs                     : false,
    removeAttributeQuotes          : true,
    removeComments                 : true,
    removeEmptyAttributes          : true,
    removeOptionalTags             : true,
    removeRedundantAttributes      : true,
    removeScriptTypeAttributes     : true,
    removeStyleLinkTypeAttributese : true,
    useShortDoctype                : true
  }
}),
{% endcodeblock %}

## Minifying SVG
we are currently using [svgo-loader](https://github.com/rpominov/svgo-loader) to keep SVGs clean.

before: 

{% codeblock lang:xml %}
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg width="100%" height="100%" viewBox="0 0 10 18" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xml:space="preserve" style="fill-rule:evenodd;clip-rule:evenodd;stroke-linejoin:round;stroke-miterlimit:1.41421;">
    <path id="Shape-Copy" d="M9.157,0.136L0.157,8.636C-0.052,8.834 -0.052,9.166 0.157,9.364L9.157,17.864C9.357,18.053 9.674,18.044 9.864,17.843C10.053,17.643 10.044,17.326 9.843,17.136L1.222,8.994L9.843,0.864C10.044,0.674 10.053,0.357 9.864,0.157C9.674,-0.044 9.357,-0.053 9.157,0.136Z" style="fill:rgb(189,157,98);"/>
</svg>
{% endcodeblock %}

after: 

{% codeblock lang:xml %}
<svg class="SVGInline-svg icon-svg" style="width: 1em;height: 1em;" viewBox="0 0 10 18" xmlns="http://www.w3.org/2000/svg" fill-rule="evenodd" clip-rule="evenodd" stroke-linejoin="round" stroke-miterlimit="1.414"><path d="M9.157.136l-9 8.5a.5.5 0 0 0 0 .728l9 8.5a.5.5 0 0 0 .686-.728l-8.62-8.142 8.62-8.13a.5.5 0 0 0-.686-.728z" fill="#bd9d62"></path></svg>
{% endcodeblock %}

## Minifying bitmap Images
[Image-webpack-loader](https://github.com/tcoopman/image-webpack-loader) can save a lot bandwidth.


## Conclusion

Webpack provides a powerful way of web developing, we use some plugins to automating the deployment. and there are more out of our view. So let's keep exploring and make web development more enjoyable.

[Webpack]: https://webpack.github.io
[helijia]: http://www.helijia.com
[UglifyJS]: https://github.com/mishoo/UglifyJS

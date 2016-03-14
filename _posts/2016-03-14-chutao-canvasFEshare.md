---
layout: post
title:  "前端小知识"
description: ""
date:   2016-03-13 19:16:00
categories: share
tags: [canvas,前端分享,储涛]
comments: true
---

>canvas 写字

{% highlight js %}


   return function(id, text) {
   
   		var w = 200; 
        var h = 200; 

        var canvas = document.getElementById(id); //获取canvas画布

        var ctx = canvas.getContext("2d");//获取canvas对象

        canvas.height = h;
        canvas.width = w;
        var bg = new Image();实例化一个图片对象
        bg.src = 'images/bg/fill.png';
        bg.onload = function () {
            ctx.drawImage(this, 0, 0, w, h);//画一张图片
            var ft_size = w - 35 * 2;

            setTimeout(function () {
                ctx.font = ft_size + "px fzzy"; //设置字体大小跟字体
                ctx.textAlign = 'center';//文字对齐方式
                ctx.textBaseline = "middle";
                ctx.fillText(text, w / 2, h / 2);
            }, 200)
        };
    };

    canvasText('text1', '你'); //第一个参数是canvas对象 第二个是需要写的字

{% endhighlight %}



>seajs使用



{% highlight js %}

// seajs 的简单配置

seajs.config({
  base: "../bower_components/",
  alias: {
    "zepto": "tp.zepto.requirejs/zepto.min.js"
  }
})

// 加载入口模块
seajs.use("../src/assets/scripts/app")




//app.js

// 所有模块都通过 define 来定义
define(function(require, exports, module) {

  // 通过 require 引入依赖
  var $ = require('zepto');

  // 通过 exports 对外提供接口
  exports.doSomething = ..

  // 或者通过 module.exports 提供整个接口
  module.exports = ..

});

{% endhighlight %}
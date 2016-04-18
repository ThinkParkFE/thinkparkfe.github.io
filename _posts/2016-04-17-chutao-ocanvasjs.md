---
layout: post
title:  "ocanvas.js"
description: ""
date:   2016-04-17 13:10:00
categories: share
tags: [ocanvas.js,前端分享,储涛]
comments: true
---


>oCanvas.js可以帮助你很容易的在 HTML5的Canvas标签上创建对象,并且创建这些对象的动画。支持包括 IE9 以及更新版本和其他包括 FF、Chrome、Safari 和 Opera 浏览器。




//ocanvas.js 包含9大部分具体每个对象的内部方法请参考官网http://ocanvas.org

{% highlight html %}

1.oCanvas Object

2.Core

3.Display Objects

4.Background

5.Timeline 

6.Events

7.Scenes

8.Animation

9.Draw


{% endhighlight %}



1.起步安装插件

{% highlight js %}

bower install ocanvas 

{% endhighlight %}


2.创建一个canvas画布

{% highlight js %}

var canvas = oCanvas.create({
    canvas: "#demo", //获取htmlcanvas对象
    background: "#0cc" //设置画布的背景颜色
});

{% endhighlight %}


3.使用其js方法写一个简单的小示例 点击这个元素有旋转动画 然后改变颜色

{% highlight js %}


var canvas = oCanvas.create({
    canvas: "#demo", //获取htmlcanvas对象
    background: "#0cc" //设置画布的背景颜色
});

var rectangle = canvas.display.rectangle({
    x: 177,
    y: 200,
    origin: { x: "center", y: "center" },
    width: 200,
    height: 100,
    fill: "#000"
});

canvas.addChild(rectangle);

rectangle.bind("click", function () {
    this.fill = "#0f0";
    canvas.redraw();

    this.animate({
        rotation: this.rotation + 360
    }, {
        duration: "long",
        easing: "ease-in-out-cubic",
        callback: function () {
            this.fill = "#f00";
            canvas.redraw();
        }
    });
});

{% endhighlight %}


>现在还在学习了解ocanvas ,在学习使用中发现要比原生的canvas更易懂易学很多，非常适合新手学习canvas的入门级插件。








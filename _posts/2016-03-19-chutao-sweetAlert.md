---
layout: post
title:  "sweetAlert 一款弹窗插件"
description: ""
date:   2016-03-18 16:20:00
categories: share
tags: [sweetAlert,前端分享,储涛]
comments: true
---


>最近浏览国外某网站时无意发现其网站弹窗挺漂亮,于是查看源码看到这款弹窗js 于是下载试了一下PC端和移动设备的兼容性,也尝试了不同场景的弹窗样式 都是很不错的 Sweet Alert 是一个替代传统的 alert警告窗 ,SweetAlert 自动居中对齐在页面中央,兼容PC and 手机或平板电脑看起来效果都很棒 另外还提供了丰富的自定义配置选择,可以灵活控制使用。



//安装插件

{% highlight js %}

bower install sweetalert

{% endhighlight %}




//引入插件以及css样式
{% highlight html %}

<link   href="dist/sweetalert.css">
<script src="dist/sweetalert.min.js"></script> 

{% endhighlight %}




//使用方法

{% highlight html %}


swal("hello world") 默认调用方法添加一条内容即可

swal({  
  title: "Error!",  
  text: "sorry this is error message!", 
  type: "error"
});

插件也提供了很多参数 按照需求不同添加不同的参数


{% endhighlight %}



//更多的详细的内容可以去插件的github查看

{% highlight html %}

http://t4t5.github.io/sweetalert/

{% endhighlight %}



>从使用之后感觉这款插件还是很不错的,不管是界面上还是从功能上都是完全可以代替alert 最重要的是在微信页面弹出来不会显示关闭网页按钮;
有兴趣可以去github看他们的示例








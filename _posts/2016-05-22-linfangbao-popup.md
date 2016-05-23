---
layout: post
title:  "angular的ngSweetAlert 弹出框插件"
description: "ngSweetAlert 弹出框"
date:   2016-05-22 18:00:00
categories: share
tags: [林方保，angular,popup]
comments: true
---


>####angular里面自带的提示框有很多，但我觉得ngSweetAlert 弹出框是比较好用的，之前用的alert标签的，有时候会出现有时候出不来，后来就找到ngSweetAlert 弹出框插件就觉得很好用，包括它的样式。只需要安装它就好了，再引用一下就ok了，也不需要注入，只要在需要用到的地方写几个代码就可以了。也不会出现有时候有时候没有的情况。
>下面是安装的文件和js代码：
{% highlight less %}
bower install sweetalert,
npm install sweetalert
这是对话框的：
swal({   title: "内容",   text: "内容!",   type: "warning",   showCancelButton: true,   confirmButtonColor: "#DD6B55",   confirmButtonText: "Yes, delete it!",   closeOnConfirm: false }, function(){   swal("Deleted!", "Your imaginary file has been deleted.", "success"); });
提示框：
swal("Here's a message!")
还有好几种，可以参考http://oitozero.github.io/ngSweetAlert/地址

 {% endhighlight %}

####很多时候,如果自己发现比较好的东西,可以拿去替换掉不好用的,好的东西是拿来用的,分享的
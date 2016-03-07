---
layout: post
title:  "前端小知识"
description: ""
date:   2016-03-06 18:00:00
categories: share
tags: [前端小知识,前端分享,储涛]
comments: true
---

>JS动画定时器

{% highlight js %}

var timeline = function () {
    this.list = [];
    this.add = function (time, fn) {
        this.list.push({
            time: (time || 0) * 1000,
            fn: typeof(fn) === "function" ? fn : null
        });
        return this;
    };
    this.play = function () {
        var alltime = 0;
        $.each(this.list, function (i, item) {
            alltime += item.time;
            setTimeout(function () {
                if (item.fn) {
                    item.fn();
                }
            }, alltime);
        });
    }
};

使用方法： new timeline();


{% endhighlight %}

>JS判断设备

{% highlight js %}


if (!(navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))) {
    alert('pc')
}else {
    alert('mobile')
}

####判断浏览器内核 写程序兼容时会用到

 if (userAgent.indexOf("Weibo") != -1) {
       
 }


{% endhighlight %}


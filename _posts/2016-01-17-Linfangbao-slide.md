---
layout: post
title:  "滑动小案例"
description: "滑动小案例"
date:   2016-01-17 18:00:00
categories: Sshare
tags: [前端分享,林方保]
comments: true
---
####1、这是我在项目中遇到的，设置项目页面可以上下滑动，之前我直接在Slide事件中，直接使用.page,我在每个页面都有一个共同的类page,在电脑上可以正常的上下滑动，在手机上测试就不可以了，可以上下滑动，但是在往下滑的不灵活，只能一点的往下滑，后来我用一个div把所有的页面都放在里面，再设置这个div的宽和高，就可以正常的上下滑动了

####2、如果需要给一个项目循环上下滑动，在Slide事件里加一个loop参数，设置它为true,光加这一个参数是不行的，还的需要加一个circle参数，同样设置它为true;我之前在motion中看到有一个loop参数，但是设置它还是不可以循环，是在其他资料中看到再加一个circle参数，
例如：
{% highlight js %}
new mo.Slide({
        target: $('.slide  .page '),
        loop:true,
        circle:true
    });
{% endhighlight %}

####3.需要做一个导航，在点击按钮的时就跳到导航中去，这是我第一个碰到，之前都没写过，是同事教我写的，首先经纬度的数据在百度上搜出来，再写触发点击按钮的事件，再调用微信中的接口，再写它的纬度、经度、位置名、地址详情、地图缩放级别一些参数。

####平常，如果碰到自己不会做的项目，可以问同事，向同事请教，即使自己当时不太明白，自己去一个一个去理解，去做，毕竟是自己遇到的问题，印象会加深很多，下次碰到就知道怎么做了，只有遇到问题，用心去解决了，才会加深这个知识点
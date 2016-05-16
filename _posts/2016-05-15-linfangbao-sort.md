---
layout: post
title:  "less的排序"
description: "less文件里的前面的元素覆盖掉后面的元素"
date:   2016-05-15 18:00:00
categories: share
tags: [林方保，前端分享,sort]
comments: true
---
####less里的元素编写的前后顺序：
####实现一个左右滑动页面功能，引用motion里的slide.js。给所有需要滑动页面加div包起来，给它加个类名.slide，再在less文件里设置它的高和宽。当时我把.slide放在它里面的一个类里面，我在预览里面根本看不到滑动的效果，我还以为是别的地方的问题，找了半天也没找出原因，后来就一直在less里面找，当时我还是不知道是排序的问题，就试着把.slide按html结构的顺序把它放在最前面，后来滑动页面就出来了。因为.slide下面的div它们共同的类覆盖掉了.slide的高和宽，所以滑动效果没出来。之前我一直还不明白干嘛要按顺序来放位置，经过这次亲身体验我觉得我以后的less文件一定会按顺序来编写的。
>下面是参考代码：
{% highlight html %}
<div class="slide ">
    <div class="page station1 ">
        <img class="station1_top" src="assets/images/station1/top.png">
        <img class="station1_dove" src="assets/images/station1/dove.png">
 bottom.png">
    </div>
    <div class="page station2 ">
        <img class="station2_top" src="assets/images/station2/top.png">
        <img class="station2_dove" src="assets/images/station2/dove.png">
     </div>
</div>
{% endhighlight %}

{% highlight less %}
 .slide {
  width: 100%;
  height: 100%;
}
.page {
  width: 100%;
  height: 100%;
  text-align: center;
  overflow: hidden;
  background-size: cover;
}
   {% endhighlight %}

####很多事需要自己亲生经历才会明天别人和我们讲的事，告诉我们怎么样避免一些错误发生，自己没有体验是不会明白，只有自己体验了，才会牢牢记住怎样避免错误发生。
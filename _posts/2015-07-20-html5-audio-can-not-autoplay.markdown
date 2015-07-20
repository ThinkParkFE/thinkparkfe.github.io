---
layout: post
title:  "无法自动播放的audio元素"
description: "HTML5 Audio 在 iOS Safari 上的问题,ios移动端不能自动播放音乐"
date:   2015-07-20 14:18:00
categories: mobile
tags: [Audio,iOS,HTML5]
comments: true
---
##一、audio的基本知识
audio:标签定义声音，比如音乐或其他音频流。

##二、audio的属性

<figure>
	<a href="/images/05155426-4996f0d78b9249e58a1c6f7bc720ac48.jpg"><img src="/images/05155426-4996f0d78b9249e58a1c6f7bc720ac48.jpg" alt=""></a>
</figure>

##三、audio的写法

* 写法一：
{% highlight html %}

<audio src="thinkparkBg.mp3"  auto loop>你的浏览器还不支持哦</audio>

{% endhighlight %}

* 写法二：
{% highlight html %}

<audio controls="controls">
<source src="thinkparkBg.ogg" type="audio/ogg">
<source src="thinkparkBg.mp3" type="audio/mpeg">
优先播放音乐thinkparkBg.ogg，不支持在播放thinkparkBg.mp3
</audio>

{% endhighlight %}

##四、audio实战

在项目中使用audio，一开始在chrome浏览器下做测试，使用了autoplay和loop属性，在页面打开时自动播放并循环，在chrome是成功支持，发布到测试环境后，在ios和android手机中音乐不会自动播放- -!，做了一系列测试，使用JS，还是无法自动播放...想用回HTML4的object元素与embed，但手机中有些浏览器禁止了控件....

##五、audio总结
对audio的使用，总结如下：

* 1.audio元素的autoplay属性在ios和andriod上无法使用的，在PC端上正常

* 2.audio元素没有设置controls时，在ios和android上会占据空间大小，而在PC端chrome是不会占据任何空间
音频文件只能从用户触发的触摸（单击）事件加载，如果在 HTML 标记中使用了 autoplay 属性，那么 Safari 将会忽略这个属性，并且不会在加载页面时播放此文件，对于 preload 属性，Safari 同样会忽略。

##六、解决办法
解决办法的就是用户进入页面是，让用户触发 touch 事件：
{% highlight js %}
var audioCtrl = $('#audio')[0];

$(document).on('touchstart', function() {
    audioCtrl.play();
})
{% endhighlight %}

微信端webView可以使用微信jssdk触发，比用户触发事件更高效。

{% highlight js %}
var audioCtrl = $('#audio')[0];

document.addEventListener("WeixinJSBridgeReady", function () {
        WeixinJSBridge.invoke('getNetworkType', {}, function (e) {
            audioCtrl.play();
        });
}, false);
{% endhighlight %}
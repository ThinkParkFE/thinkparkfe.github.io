---
layout: post
title:  "TimelineMax的基本用法"
description: "TimelineMax"
date:   2016-03-20 18:00:00
categories: share
tags: [TimelineMax,GASP，王兆丹]
comments: true
---



>#TimelineMax的基本用法

###1.TimelineMax是GASP的一部分，用于制作动画的工具。使用TimelineMax可以控制“任何JavaScript可以触及到”的动画序列。
###2.TimelineMax是一个JavaScript序列工具，可以充当补间或者其它时间轴的容器，从而更容易把它们作为一个整体来控制，也可以精确地管理它们的时序。TimelineMax提供的方法允许我们访问动画的多个层面，还可以在运行的时候动态调整时间轴的速度。

>###1.初始化准备：

####引用：```<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/1.18.0/TweenMax.min.js"></script>```

>###2.对象字面量的配置

####函数参数的基本的配置

{% highlight js %}

var tmax_options = {
  delay: 0,//延迟时间
  paused: false,//动画暂停
  onComplete: function() {//动画完成之后执行函数
  },
  onCompleteScope: {},
  tweens: [],
  stagger: 0,
  align: 'normal',
  useFrames: false,
  onStart: function() {//动画开始时执行的函数
  },
  onStartScope: {},
  onUpdate: function() {
    console.log('on update called');
  },
  onUpdateScope: {},
  onRepeat: function() {//动画重复时执行的函数
  },
  onRepeatScope: {},
  onReverseComplete: function() {//倒置重复是执行的函数
  },
  onReverseCompleteScope: {},
  autoRemoveChildren: false,
  smoothChildTiming: false,
  repeat: 0,//动画重复次数
  repeatDelay: 0,//动画重复延时
  ease: Elastic.easeInOut,
  yoyo: false,//是否反向重复
  onCompleteParams: [],
  onReverseCompleteParams: [],
  onStartParams: [],
  onUpdateParams: [],
  onRepeatParams: []
};

{% endhighlight %}


     
>###3.创建动画对象
####tl是实例化的TimelineMax函数，将对象字面量作为参数传入，.to()是用于添加动画效果，以下的动画，先执行第一个.to()，再执行第二个.to()，“-=0.5”代表于上个动画的时间间隔，在上一个动画还剩0.5s的时候，再执行第二个动画。

 {% highlight js %}
var tl = new TimelineMax(tmax_options);
tl.to(element, 1, { left: 100 })
  .to(element, 1, { top: 100 }，"-=0.5");
 {% endhighlight %}


>####这是我最近在看TimelineMax的一些理解，是很简短的一个描述，介绍来对象字面量的部分键值，包括常见的：repeat代表重复的次数，yoyo：true代表的是重复的方向为反向等。TimelineMax实例化的过程和添加方法，设置方法的参数。

####这都是基本的定义，没有具体涉及到动画的动态效果。更深层次的理解和运用会在下次再进行分享。
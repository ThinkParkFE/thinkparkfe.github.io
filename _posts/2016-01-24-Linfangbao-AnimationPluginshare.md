---
layout: post
title:  "动画插件和视频"
description: "使用动画插件的小案例"
date:   2016-01-24 03:00:00
categories: share
tags: [前端分享,林方保]
comments: true
---
####插入视频，使用<iframe标签>，在js中，当视频页面出现的时候就使用attr()方法控制写出它的视频地址，隐藏这个页面的时候，也是使用attr()方法控制它。
####比如做一个确认信息页面，也是使用ajax写的，不过它是ajax返回success值里面的，如果填写的值正确的提交到数据库里面的时候，就把填写的值读取到确认信息上，这样在确认信息里面可以看到自己提交的信息了

####使用动画插件，先写它的js，再使用data-fx值，再看自己动画的需要，有fadeInDown：上，fadeInLeft：左，fadeInUp:下，fadeInRight：右四个属性，在后面写上自己所需要动画的哪个属性，不过不要忘记要引入动画插件的css文件，它的js代码如下：
{% highlight js %}
pageCtrl.on("change", function () {
        var _prve = $('.wrap .page').eq(pageCtrl.prevPage);
        _prve.find('[data-fx]').each(function (i) {
            $(this).removeClass($(this).data("fx")).removeAttr("style");
        });
        if (pageCtrl.curPage == 0)pagechang();
    });

    pageCtrl.on("beforechange", pagechang);
    function pagechang() {
        var _this = $('.wrap .page').eq(pageCtrl.curPage);
        var alldelay = 0;
        _this.find('[data-fx]').each(function (i) {

            var ani = $(this).data("fx");
            var ani_delay = $(this).data("animation-delay") || i > 0 ? .5 : 0;
            var ani_duration = $(this).data("animation-duration") || 1;
            alldelay += Number(ani_delay);
            $(this).addClass(ani).addClass("animated").css({
                "-webkit-animation-delay": alldelay + "s",
                "-moz-animation-delay": alldelay + "s",
                "-ms-animation-delay": alldelay + "s",
                "animation-delay": alldelay + "s",
                "-webkit-animation-duration": ani_duration + "s",
                "-moz-animation-duration": ani_duration + "s",
                "-ms-animation-duration": ani_duration + "s",
                "animation-duration": ani_duration + "s"
            });
        });

    }
{% endhighlight %}
####只有多做些实例或者多做些项目，在里面可以学到更多的知识，才会遇到自己想不到的问题，不断的锻炼，才会巩固知识，劳劳的记住，技术是靠经验来丰富，熟练的
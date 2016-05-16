---
layout: post
title:  "指定值中取随机数和类选择器"
description: "指定值中取随机数和类选择器应用案例"
date:   2016-03-06 18:00:00
categories: share
tags: [前端分享,林方保]
comments: true
---



>###指定值中取随机数应用案例

>####在指定题目中，随机出现题目和播放其中正确一题的歌曲，我之前是在网上查的资料，在调试器里是可以的，但是写在程序里播放的歌曲和题目里是不一样的，后来老大说这样写是不对的，但是我知道它的思路，就是不知道怎么去实现它，然后还是老大在一边写一边讲解给我听，先是把那些歌曲放在一个对象里，再定义一个空的数组，再把对象里的数值放到这个空的数组里，再去定义随机数，还要定义随机出来的题目的有一个对应的歌曲。

>####下面是写的代码：
{% highlight html %}
(function () {
    //var cdnbase = '//images.menma.me/nhwsgame.ali.menma.me/';
    //var cdnbase = '//menma.oss-cn-hangzhou.aliyuncs.com/nhwsgame.ali.menma.me/';
    var cdnbase = '';
    var gemings = { 里面是指定的值};
    var _gemings = [];
    $.each(gemings, function (i) {_gemings.push(i);});
    var _allq = [];
    function getq() {
        var choose = [];
        while (choose.length < 多少个题的数量) {
            var _n = Math.floor(Math.random() * _gemings.length + 1) - 1;
            var _choose = _gemings[_n];
            if (_allq.indexOf(_choose) == -1) {
                _allq.push(_choose);
                if (choose.indexOf(_choose) == -1) {
                    choose.push(_choose);
                }
            }
        }
        var _a = choose[Math.floor(Math.random() * choose.length + 1) - 1];
        return {
            q: choose,
            qmusic: cdnbase+"assets/audio/" + gemings[_a] + ".mp3",
            a: _a
        };
    }
    var _qs;
    function reset() {
        _allq = []
        var qs = [];
        var i = 0;
        while (i++ < 5) {
            qs.push(getq());
        }
        return _qs = qs;
    }
    window.qs = {
        get: function () {
            return _qs || reset();
        },
        reset: function () {
            return reset();
        }
    }
})();
{% endhighlight %}

>###类选择器应用案例

####之前我使用jquery的类选择器，但是不知道怎么简洁代码，即使是做同一件事，我还是一个类一个选择器，这样看起来很乱，后来还是老大提醒的我，我才改过来，类选择器里面可以放多个类，做同一件事的时候，不需要一个类就给一个选择器，可以放到同一个选择器里面，下面是参考代码：
$("类1，类2，类3等等").要做的同一件事

####学习一定要找到有效的学习方法，如果不知道怎么去运用这个知识点，可以去参考别人是怎么运用的，自己再加以去学习，理解，使用多了慢慢的就理解了。
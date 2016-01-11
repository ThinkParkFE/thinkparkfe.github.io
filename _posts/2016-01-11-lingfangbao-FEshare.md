---
layout: post
title:  "林方保近期学习总结"
description: "林方保近期学习总结"
date:   2016-01-11 10:18:00
categories: share
tags: [前端分享,林方保]
comments: true
---


>在实践中，通过遇到这些问题，再把问题解决好，从中可以学到很多知识，平常讲的一些问题，也知道怎么解决，使用，但当真正遇到的时候，就不一定会做，只有自己碰到了，解决了，才会牢牢记住这个知识点。


给绝对定位的图片居中，之前只有在photoshop工具里量出与左边或者右边的距离，通过在百度里找到办法，给定位图片left:50%,再用margin-left负的图片大小的一半就可以居中了

{% highlight html %}
<div class="introduces">
        <img class="word" src="assets/images/xx.png">
</div>
{% endhighlight %}
{% highlight css %}
   .word {
    position: absolute;
    width:30%;
    bottom:10%;
    left: 50%;
    margin-left: -15%;
    }
{% endhighlight %}
给箭头加动画 之前按照动画工具里面的代码做出来的向上移动的效果很生硬，加上alternate属性后，动作要好看许多

{% highlight css %}
  animation: arrow 1s 0s infinite ease alternate;
{% endhighlight %}

背景音乐图标，之前没有加上z-index属性，点击时切换不了另一个图，事件也触发不了，给图标设置同级关系一样就可以了，我都是忘了加
{% highlight css %}
 z-index: 2;
{% endhighlight %}

提交表单，需要定义它的变量，需要判断它的格式，是否有填写，电话号码需要用正则表达式来判断是否填写有误，ajax是用来提交表单用的，要通过http请求加载数据。
{% highlight js %}
$("form").on("submit", function () {
        var name = $("input[name='name']").val();
        var phone = $("input[name='tel']").val();
        if (name.length == 0) {
            alert("名字不能为空!");
            return false;
        }
        if (!(/^1[3|4|5|7|8][0-9]\d{8}$/.test(phone))) {
            alert("电话号码填写错误!");
            return false;
        }
        $.ajax({
            url: "/api/v2/userBm/",
            dataType: "json",
            type: "post",
            data: $(this).serialize(),
            success: function (res) {
                console.log(res);
                if (res.ret == 200) {
                    alert("报名预约成功!");
                  //...
                } else {
                    alert(res.msg);
            }
            }
        });
        return false;
    });
{% endhighlight %}



项目中如果遇到要做一个按钮，按钮的背景是一张图，我觉得比较简单的方法就是把图当做背景图片来放，然后定义相应的属性就可以了，我之前是把图和文字分开来写，代码量会很多，而且要做许多兼容，后来把图片用作背景图来做，减少很多代码量
{% highlight html %}
<div class="btn">
        <button> 去送祝福吧</button>
</div>
{% endhighlight %}
{% highlight css %}
    button {
      position: absolute;
      background-image: url("../images/voice/box.png");
      background-size: 100% 100%;
      margin-left: percentage(240/750);
      bottom: percentage(110/1206);
      line-height: 3em;
      width: 36%;
      font-size: 12px;
      color: #fff;
    }
{% endhighlight %}
如果遇到做一个输入框，需要把一张图和input在同一行中，在图的那头的背景颜色和input这边的颜色不一样，先把它们用div把它们全部包在里面,给它们相对定位，定义属性display: inline-block;，设为内联元素，设垂直居中，再加上相应的属性，之前我是分别给它们绝对定位，在把它们慢慢调整在一起，但是，要做很多兼容
{% highlight html %}
<div class="input-group">
            <span class="icon"><img src="assets/images/p9/tel.png"></span>

            <input type="text" placeholder="电话" name="tel" autocomplete="off">
</div>
{% endhighlight %}


{% highlight css %}
.input-group {
      position: relative;
      display: table;
      border-collapse: separate;

      width: 100%;
      margin: 10px auto 0;
      box-sizing: content-box;
      .icon {
        display: inline-block;
        width: 4px;
        padding: 0px 26px;

        border-right: 0;
        border-top-left-radius: 4px;
        border-bottom-left-radius: 4px;
        vertical-align: middle;
        background-color: #e9e9e9;
        text-align: center;
      }
      img {
        width: 600%;
        margin: 0px -9px;
        padding-top: 2px;
      }
    }
    input {
      position: relative;
      z-index: 2;

      width: 160px;
      padding: 6px 6px;
      border-left: 0;
      border-top-right-radius: 4px;
      border-bottom-right-radius: 4px;
      background-color: #216b53;
      opacity: 0.7;

      color: #fff;

      text-indent: 10px;
      font-size: 10px;
    }
{% endhighlight %}

微信端，当用户横屏时要给出一个提示，横屏时看不了内容，需要再写一个提示页面，再写js，给出判断，当屏幕旋转到90渡或者-90渡的时候，就给出提示，旋转到180渡的时候就正常呈现内容
{% highlight js %}
function orient() {
        if (window.orientation == 0 || window.orientation == 180) {
            orientation = 'portrait';
            //竖屏
            $('.rotate').addClass('hide');
            return false;
        }
        else if (window.orientation == 90 || window.orientation == -90) {
            orientation = 'landscape';
            //横屏
            $('.rotate').removeClass('hide');
            return false;
        }
    }
    orient();
    $(window).on('orientationchange', function (e) {
        orient();
    });
{% endhighlight %}

在实践中，通过遇到这些问题，再把问题解决好，从中可以学到很多知识，平常讲的一些问题，也知道怎么解决，使用，但当真正遇到的时候，就不一定会做，只有自己碰到了，解决了，才会牢牢记住这个知识点。


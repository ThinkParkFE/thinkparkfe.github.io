---
layout: post
title:  "Dialog组件获取"
description: "这是一个很典型的例子，来理解闭包、形参、实参"
date:   2016-01-17 18:00:00
categories: share
tags: [前端分享,王兆丹]
comments: true
---




>gulp 现有已编辑好的一套微信组件，先摘取其中的Dialog组件，将alert(), confirm(),toast(),loadingtoast()和actionsheet()事件封装在一个js文件中，包括css样式和HTML格式。

###参考代码：motion.js

>一.构建css引入函数
 构造函数importStyle,将css样式引入js中；

>二.创建全局变量
 var tp = window.tp = window.tp || {};
 将闭包中的变量暴露在全局中

>三.函数构造
  1.定义变量tpls，存储html代码；
  2.设置函数的默认值，定义变量defaults；
  3.通过全局变量来构造函数，top.Dialog={};
  4.通过键值对，alert：function（options，callback）｛｝构造,可传入参数和回调函数;对传入参数进行判断，是否符合条件，对象参数是否为对象，回调函数参数是否为函数；var opts = $.extend({}, defaults.alert, options) 将传入的参数和默认值合并到空对象，形成一个新的对象；再通过对DOM的查找、修改，将传入的对象值落实；根据安卓机和ios机的软键盘差异，对样式进行更改；


>四.涉及到的关键代码
  >1.对传入的参数进行验证处理

{% highlight js %}
 if (!$.isPlainObject(options)) {
        options = {content: options};
        if (callback && $.isFunction(callback)) {
             options.success = callback;
           }
      }
      //success不是一个函数的时候，将success赋值为一个空函数s
     if (!$.isFunction(opts.success)) {
                opts.success = $.noop;
     }
{% endhighlight %}


  >2.判断安卓机和iOS系统
   {% highlight js %}
  var u = navigator.userAgent;
      var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Adr') > -1; //android终端
      var isiOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/); //ios终端
      if (isiOS) {.... }

    {% endhighlight %}

  >3.将参数动态添加到html上

   {% endhighlight %}
  var _DOM = $(".TP_dialog_confirm");
  _DOM.find(".TP_dialog_title").text(opts.title);
  _DOM.find(".TP_dialog_bd").html(opts.content);
  _DOM.find(".TP_btn_dialog.default").text(opts.cancel_text).off("tap").on("tap", function () {
          _DOM.addClass("hide");
          opts.cancel();
  });

  _DOM.find(".TP_btn_dialog.primary").text(opts.ok_text).off("tap").on("tap", function () {
        _DOM.addClass("hide");
        opts.success();
   });
   {% endhighlight %}

   >4.根据参数设置添加的信息

    {% endhighlight %}
    $.each(opts.cells, function (i, cell) {
       _DOM.find(".TP_actionsheet_menu").append($(tpls.actionsheet_cell).html(cell.text).off("tap").on("tap", function () {
       _DOM.addClass("hide");
       if ($.isFunction(cell.success))
           cell.success();
       }));
    });
    {% endhighlight %}

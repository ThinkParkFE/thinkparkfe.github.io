---
layout: post
title:  "Andorid 常见问题及解决方案"
description: "Mars，移动Web前端知识库，收集与归纳移动Web开发中常见的问题。主要介绍移动端Web解决方案，包括代码结构规范、字体设置最佳实践、模拟原生效果实践、工具类方法汇总、iOS与Android平台上问题列表、高性能Mobile Web开发、类库依赖推荐等。"
date:   2015-08-07 14:10:00
categories: mobile
tags: [mobile,css,js,html5,javascrpt,Andorid]
comments: true
---


解决Andorid上的各种坑。

##Andorid 常见问题及解决方案

  <p>1.三星I9100 （Android 4.0.4）不支持display:-webkit-flex这种写法的弹性布局，</p> 
         <p>但支持display:-webkit-box这种写法的布局, </p>
         <p>相关的属性也要相应修改，如-webkit-box-pack: center;</p>
         <p>移动端采用弹性布局时，建议直接写display:-webkit-box系列的布局</p>
    <p>    </p>
  <p>2.touchmove事件在Android部分机型(如LG Nexus 5 android4.4，小米2 android 4.1.1)上只会触发一次</p> 
         <p>解决方案是在触发函数里面加上e.preventDefault(); 记得将e也传进去。</p>
        

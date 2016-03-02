---
layout: post
title:  "采用cdn路径获取资源"
description: "使用又拍云资源管理器,采用cdn路径获取资源"
date:   2016-02-28 18:00:00
categories: share
tags: [前端分享,王兆丹]
comments: true
---

##分享采用cdn的方式获取资源

>1.项目正式完成之后；
>2.生成dist文件，将dist文件中的压缩过的除了html/php文件之外的资源上传到cdn中；
 2.1 使用又拍云资源管理器，进入相应的空间，建立目录；
 2.2 按照项目的目录格式建立云存储,将js/css等资源以压缩的形式存储；

>3.修改gulp文件，将cdn的默认路径修改为在cdn建立的路径，执行cdn的任务，统一将路径修改；

#3.1 默认配置中添加cdn（路径修改为资源存储的路径）
  {% highlight js %}
var config = {
    ......
    cdn: '//images.menma.me/website.hydq.menma.me/assets/'
};
 {% endhighlight %}

#3.2 替换静态cdn，替换路径，只更改了php文件，其他的保持不变

  {% highlight js %}
gulp.task('cdn', function () {
    return gulp.src(config.distPath + [
                '*.php'
            ])
        .pipe(cdn({
            domain: "assets/",
            cdn: config.cdn
        }))
        .pipe(gulp.dest(config.distPath + "/"))
});
 {% endhighlight %}

---
layout: post
title:  "gulp配置配置使用"
description: ""
date:   2016-01-11 10:18:00
categories: share
tags: [前端分享,储涛]
comments: true


常用的gulp插件

{% highlight html %}
less的编译（gulp-less）
自动添加css前缀（gulp-autoprefixer）
压缩css（gulp-minify-css）
合并js文件（gulp-concat）
压缩js代码（gulp-uglify）
压缩图片（gulp-imagemin）
自动刷新页面（gulp-livereload）
更改提醒（gulp-notify）
清除文件（del）

{% endhighlight %}


首先引入gulp依赖文件

{% highlight js %}

//引入插件
var gulp = require('gulp'),
    less = require('gulp-less'),
    htmlmin = require('gulp-htmlmin'),
    uglify = require('gulp-uglify'),
    concat = require('gulp-concat'),
    minifyCss = require('gulp-minify-css'),
    autoprefixer = require('gulp-autoprefixer'),
    livereload = require('gulp-livereload'),

{% endhighlight %}


建立任务

{% highlight js %}
  定义一个watch任务（自定义任务名称）
  gulp.task('watch', function () {
      livereload.listen();
      gulp.watch(config.appPath + '/**/*.*', function (event) {
          livereload.changed(event.path);
      });
      gulp.watch(config.appPath + 'assets/less/*.less', ['less']);
  });

{% endhighlight %}


建立默认任务
{% highlight js %}

gulp.task('default', ['less', 'watch']);

{% endhighlight %}



执行任务
{% highlight js %}
    gulp default
{% endhighlight %}

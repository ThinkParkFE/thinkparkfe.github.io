---
layout: post
title:  "gulp使用"
description: "gulp配置及使用"
date:   2016-01-17
categories: share
tags: [前端分享,储涛]
comments: true
---

>gulp 是前端构建工具、相比grunt来说 本人更亲赖于gulp 从less编译速度到生成线上目录、压缩图片效率远远大于grunt ;
>gulp 里面一个强大的插件livereload 写好代码保存浏览器自动刷新,懒人必备 更能大大提升写代码的效率。
>gulp

###首先安装依赖插件环境

{% highlight js %}

sudo cnpm install 插件名

{% endhighlight %}



>常用的gulp插件

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


*首先引入gulp及插件依赖文件


{% highlight js %}

var gulp = require('gulp'),
    less = require('gulp-less'),
    htmlmin = require('gulp-htmlmin'),
    uglify = require('gulp-uglify'),
    concat = require('gulp-concat'),
    minifyCss = require('gulp-minify-css'),
    autoprefixer = require('gulp-autoprefixer'),
    livereload = require('gulp-livereload'),

{% endhighlight %}


*设置默认配置

var config = {
    distPath: 'dist/',
    appPath: 'app/'
};

*建立自定义任务

>建立livereload示例代码

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



*建立默认任务

>添加上面定义的watch任务

{% highlight js %}

gulp.task('default', ['watch']);

{% endhighlight %}



*执行默认任务

>这里就可以直接执行前面定义好的默认任务;也可以代码行运行
{% highlight js %}
    gulp default
{% endhighlight %}




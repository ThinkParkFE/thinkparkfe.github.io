---
layout: post
title:  "angularjs ng-table插件"
description: ""
date:   2016-04-04 19:50:00
categories: share
tags: [ngTable,前端分享,储涛]
comments: true
---


>ngTable是一个基于AngularJS的directive设计一个表格项目，支持基本的表格操作，分页，排序，异步加载等功能 API，demo什么的请参考官网，http://ng-table.com。




//引入插件js以及css样式
{% highlight html %}

引入ngTable js/css

<link rel="stylesheet" href="https://cdn.rawgit.com/esvit/ng-table/v1.0.0/dist/ng-table.min.css">
<script src="https://cdn.rawgit.com/esvit/ng-table/v1.0.0/dist/ng-table.js"></script> 

{% endhighlight %}




//使用方法

控制器首先注入 ngtable 

{% highlight js %}

angular.module("myApp", ["ngTable"]); 


 var self = this;
 var data = [{name: "Moroni", age: 50}];


 self.tableParams =  new NgTableParams({
                count: 10, //每页显示数量
                sorting: {age: "desc"} //默认排序的方式
            }, {
                paginationMaxBlocks: 5,
                paginationMinBlocks: 2,
                data: data,
                counts: false
            });

{% endhighlight %}



{% highlight html %}

//首先ng-table的值是控制器部分实力化的名字 
<table ng-table="tableParams" class="table"> 

用ng-repeat指令实现数据循环输出 $data也可換成控制器後面自定義的變量
    <tr ng-repeat="user in $data">

filter 是過濾数据内容
        <td title="'Name'" filter="{ name: 'text'}" sortable="'name'">
            {{user.name}}
</td>
        <td title="'Age'" filter="{ age: 'number'}" sortable="'age'"> 
排序使用内置的softtable 裡面的值就是后面控制器部分定义的 name
            {{user.age}}
</td>
    </tr>
</table

{% endhighlight %}


>虽然现在只是用到了一小部分的插件方法,从使用之后感觉确实ng-table这款插件功能相当强大，像搜索、排序、分页、每页表格显示数目等都有。








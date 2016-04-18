---
layout: post
title:  "angular绑定下拉框绑定"
description: "angular下拉框绑定多个值"
date:   2016-04-17 18:00:00
categories: share
tags: [林方保，angularjs]
comments: true
---
####angular下拉框从后台数据里面绑定多个值
####在标签里面添加下面的几个属性：
>isteven-multi-select：主要的

                input-model = "后台获取数据的列表" ,
                output-model = "绑定到后台去的数据",
                button-label = "呈现需要显示出来的数据，如:名字" ,
                item-label = "和上面的一致" ,
                tick-property = "定义的名字" ,
                ng-model  
####在从后台去获取数据先绑定到下拉框下面，然后再从下拉框选择值绑定添加到后台去。
>下面是参考代码：

{% highlight html %}

                <span>项目负责人</span>
                <div class="form-group" isteven-multi-select input-model="userList" output-model="anyOutput"
                     button-label="name" item-label="name" tick-property="ticked" ng-model="achievements.staff1">
                </div>
{% endhighlight %}


{% highlight js %}
  先是获取到下拉框下面：

apiService("DingTalk.UserList", {token: token, deptId: 1})
        .success(function (res) {
                 $scope.userList = res.data;
        })
再从下拉框绑定到后台去

    $scope.achievements = {staff1:[]};
        apiService("KPI.Add", $scope.achievements)
                .success(function (res) {
                if(res.ret==200)
                    $scope.alert = {"title": "绩效添加成功", "type": "success"};
            })
  {% endhighlight %}

####选择多个值也可以用复选框,它和isteven-multi-select是差不多的，有一个不同的是复选框页面上的值和数据列表里值是相同的，isteven-multi-select页面上显示的值和数据显示是不一样的，数据显示的是整个列表出来
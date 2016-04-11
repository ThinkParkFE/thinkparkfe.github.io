---
layout: post
title:  "angular数据绑定"
description: "angular从后台获取数据再绑定到后台去"
date:   2016-04-10 18:00:00
categories: share
tags: [林方保，angualrjs,dataBinding]
comments: true
---
####angular从后台获取数据再绑定到后台去
####angular从后台获取数据用数组排序出来，再把数组里的数据绑定到数据库里面去。之前我在这个问题上做了好几天才做出来的，把数组里面的数据绑定到数据库里面去，和之前的方法是一样的，只需要给它一个下标就可以了。它就根据下标去添加所选的数据。
>####页面的列表HTMl的展示
{% highlight html %}
   <div class="form-group">

            <label class="control-label">权限</label>

            <div class="checkbox" ng-repeat="(rulesKey,rulesData) in rulesDatas">

                <label>

                    <input type="checkbox" ng-model="applicationRules[$index]" >{{rulesData}}

                </label>

            </div>

            <pre>{{applicationRules}}</pre>

        </div>
{% endhighlight %}

{% highlight js %}
$scope.rulesDatas = [];

    $scope.applicationRules = [];

    $scope.alerts = [];

    apiService("Application.Rules")
        .success(function (res) {

            if (res.ret != 200) {
                alert(res.msg);
                return;
            }

            $scope.rulesDatas = res.data.rules;

        });

    var token = $cookies.get("token");

 apiService("Application.Add", {token: token, rules: $scope.applicationRules})
            .success(function (res) {

                if (res.ret == 200) {
                    $scope.alert = {"title": "应用管理添加成功", "type": "success"};

                    $timeout(function () {

                        //$rootScope.alerts="";

                        $location.path('/application/list');

                    }, 1500);

                }

            })
            .error(function (data, status, headers, config) {

            });
{% endhighlight %}

####如果遇到难题时，只要自己坚持，不放弃地去解决它，总是会解决的。自己可以通过很多途径去解决，有时候在自己不经意的时候也会想到解决的方法。只要自己坚持不懈。
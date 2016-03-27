---
layout: post
title:  "angular框架的三大集成"
description: "Augularjs是非常强大且非常灵活的前端MVC框架"
date:   2016-03-27 18:00:00
categories: share
tags: [王兆丹，angualrjs，service]
comments: true
---



#Augularjs的三大集成
###Angularjs是通过为开发者呈现一个更高层次的抽象来简化应用的开发应用。在实际的工作中非常受用，作为一个框架，它很强大。

###1.Augularjs是非常强大且非常灵活的前端MVC框架。
###2.Augularjs提供了双向数据绑定（操作数据模块会自动刷新DOM元素）、路由控制、拦截器。
###3.Augularjs的强大之处在于关注点分离，不仅如此，它还将关注点分离做成了集成。
####3.1Angular中将负责数据提供的组件抽象为Service；
####3.2Angular中将页面展现包装在指令中Directive；
####3.3Angular中试图之间的逻辑抽象为Controller；
###所有的DOM操作，事件处理都会放在指令，与展现无关的逻辑放在Service中，而Controller则负责展现相关的数据组织。

###4.数据的双向绑定
{% highlight html %}

	<div ng-controller="SimpleController">
    <input type="text" name="name" ng-model="name">
    <span>{{name}}}</span>
    </div>

{% endhighlight %}

{% highlight js %}

 var app=angular.module('SimpleApp',[]);
 app.controller('SimpleComtroller',['$scope',function($scope){
    $scope.name="Juntao QIU"
 }]);

{% endhighlight %}
第一句定义了Angularjs的模块，模块名是SimpleApp
第二行定义了一个名字为SimpleComtroller的Controller；

{% highlight js %}

['$scope',function($scope){
    $scope.name="Juntao QIU"
 }]);

{% endhighlight %}
这是一段注入依赖关系的简写。
首先它是一个数组，数组的最后一个元素是函数，这种写法表示，将数组的前几项作为依赖，当这些依赖都完成时，执行最后一项的函数，并将之前的依赖项作为参数传递给该函数；

###5.内置的指令
####所有的内置指令都是以前缀ng开头的；
####一些常见的指令：
###5.1 ng-model 表单控件与当前的作用域的属性进行绑定；
###5.2 ng-app 作为作用域的起点 <html ng-app="myApp">
###5.3 ng-controller 控制器
###5.4 ng-form 表单指令
###5.5 ng-if  ng-if中的表达式为false，则对应的元素整个会从DOM中移除而非隐藏，但审查元素时你可以看到表达式变成注释了。
###5.6 ng-repeat 遍历
###5.7 ng-class 用于作用域对象动态变类样式  <p ng-class="{red: x%2==0,blue: x%2!=0}" > ，用于判断，满足条件就显示当前的类；
###内置的指令是用于业务逻辑的处理，将html页面通过逻辑的方式表现。

###6.Angualar中的服务
###在前端应用中，要想完成与后台的交互，需要定义一个服务Service。

{% highlight js %}

app.factory('apiService', ['$http',"$cookieStore",function($http,$cookie) {
  return function (){
       console.log("Service");
    });
  }
}]);

{% endhighlight %}
###factory是Angularjs支持Service的一种。与Jq方法中的Ajax方法比较相似。


###这段时间在研究Angularjs的相关内容，也了解了框架的基本定义，以上是这几天学习的部分总结，分享了关于Angularjs的几个大块内容，MVC是模型(model)－视图(view)－控制器(controller)的缩写。这一块的知识也是以后需要好好学习的部分。
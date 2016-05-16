---
layout: post
title:  "angular.js"
description: "发现Angular的好处"
date:   2016-03-20 18:00:00
categories: share
tags: [林方保,angularjs]
comments: true
---

###Angular.js. 是一个比较完善的前端MV*框架，包含模板，数据双向绑定，路由，模块化，服务，过滤器，依赖注入等所有功能,比jQuery插件还灵活
####之前老大和我们说过Angular，只是后来我们没有用，然后我也没有去看，直到这个星期我们要拿别人做的模版改成我们公司的后台。他们那个就是用Angular写的，后来我上网先查了下它的用法，其实也是蛮好用的。就比如我们用的表单验证，在js里面需要一个一个去判断，但是在Angular里面，只需要在html里面写上限制它的长度就可以了。也可以在里面写上不符合要求的提示语句，然后在按钮里面写上一个判断是否可以提交的代码即可，比js要简洁多了，这个减少了好多代码，目前只是发现它的好处，还没有发现它不足的地方，只有待以后发现
####代码如下
{% highlight html %}
ng-model="user.username" required ng-minlength="4" ng-maxlength="12"
 ng-disabled="!(loginForm.$valid)"                    
{% endhighlight %}
####写前端有许多的框架和库给我们用，不要只待在一个知识点里面，我们可以去发现更多好用的东西，然后去学习，去使用。这样就可以学到很多的知识，在写代码的时候就可以提高质量
---
layout: post
title:  "页面滚动动态加载数据的情况分析"
description: "瀑布流的思想，实现数据的动态加载，当滚动条到一定的位置的时候，加载所需的数据，降低了页面的复杂性，对触屏的设备更加友好！"
date:   2016-04-18 18:00:00
categories: share
tags: [王兆丹，angualrjs，Jquery，scroll]
comments: true
---



###瀑布流加载数据
###瀑布流数据加载的方式起源于pinterest，是目前比较流行的一种网站页面布局，当页面向下滚动并达到一定的位置的时候，进行数据的加载并显示在当前页面的尾部；


>###1.jquery的瀑布流方式
####1.1 html样式

{% highlight html %}

	<div class="scrollA" id="scrollA" >
       <p>123</p>
       <p>1</p>
       <p>1</p>
       ......
   </div>
   
{% endhighlight %}


####1.2 js样式

{% highlight js %}

<!--调用接口.scroll（），当触发滚动时间的时候，执行函数-->
 $(".scrollA").scroll(function () {
         <!--获取滚动条的位置-->
        var scrollTop = document.getElementById("scrollA").scrollTop;
        <!--获取滚动区域的位置-->
        var scrollHeight = document.getElementById("scrollA").scrollHeight;
        <!--获取内容的可见区域的高度-->
        var height = document.getElementById("scrollA").offsetHeight;

        console.log("滚动条的位置scrollTop：" + scrollTop);
        console.log("元素内容的高度scrollHeight：" + scrollHeight);
        console.log("div的可见高度offsetHeight：" + offsetHeight);
        
        if (scrollHeight - （offsetHeight - scrollTop） <= 50) {
            console.log("到底部");
        <!--ajax数据加载~~~-->
        }
        else console.log("未到底部~ ");

    }); 
{% endhighlight %}





>###2.angualr的瀑布流方式

####2.1 html样式

{% highlight html %}
<!--“when-scrolled”，使用自定义的指令，绑定函数-->
 <section class="grid-field grid-conference" when-scrolled="loadMore()">
   <div class="grid-item" ng-repeat="item in siteData">
      <a ng-href="{{item.url}}" target="_blank"> 
      <img class="icon-proj" ng-src="{{item.iconurl}}"> </a>
     <div class="grid-item-desc">{{item.name}}</div>
   </div>
</section>

    
{% endhighlight %}

####2.2 angualr指令和模块化使用


{% highlight js %}
<!--自定义指令-->
app.directive('whenScrolled', function() {
    return function(scope, elm, attr) {
        var raw = elm[0];
        elm.bind('scroll', function() {
            if (raw.scrollHeight-(raw.scrollTop+raw.offsetHeight)<=50) {
                <!--//滚动条的位置：-->console.log(raw.scrollTop);
                <!--//元素内容的高度：-->console.log(raw.offsetHeight);
                <!--//滚动区域的高度：-->console.log(raw.scrollHeight);
                scope.$apply(attr.whenScrolled);
            }
        });
    };
});
 
{% endhighlight %}

{% highlight js %}
app.controller("siteController", ['$scope', 'apiService', function ($scope, apiService) {
$scope.loadMore = function () {
             <!--判断当前的页面是否小于页面的总数-->
            if ($scope.page.page <= $scope.pages) {
                <!--加载下一页面-->
                $scope.page.page++;
                <!--调用接口，实现数据的加载-->
                apiService($scope.page)
                    .success(function (res) {
                        if (res.ret != 200) {
                            alert("res.msg");
                        }
                        $scope.siteData = $scope.siteData.concat(res.data.list);
                        <!--获取页面的总数-->
                        $scope.pages = Math.ceil(res.data.total / $scope.page.pageMax);
                     });
            }
            };
}
 
{% endhighlight %}



>###3.滚动条相关参数的说明：
####3.1 scrollTop  被选元素的垂直滚动条位置。
####3.2 scrollHeight   被选中元素的滚动条的滚动区域高度，自身元素加上隐藏元素。
####3.3 offsetHeight   被选中元素的高度，自身元素





>####本次分享的内容是有关于滚动条的相关操作，首先在css样式中，选中要滚动的标签，设置overflow: scroll；然后在js中处理位置的变化；在jq中，我们可以运用Api（.scroll()）对滚动事件进行监听和处理，通过判断scrollHeight和offsetHeight+scrollTop的大小，页面相应的做出改变;在angular中，自定义指令来判断scrollHeight和offsetHeight+scrollTop的大小，接着在html页面中引用该指令，进行函数处理；

#### 这是相对比较简单的案例，在angualr操作的时候，百度搜到的都是无限滚动指令ng-infinite-scroll，我也参照demo，将这个用于自己的操作中，但不能达到效果，根据我的操作来说手机端不能适配，电脑端也有问题，没有到达最后的时候，就加载了数据，并且根本停不下来~~，也是这个事件中得到了一个结论，很多封装好的指令并不能直接使用，要进行修改，如果修改还不可以使用，那就要自己根据理解，写一段自己的代码；

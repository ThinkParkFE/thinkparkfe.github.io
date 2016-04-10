---
layout: post
title:  "说明书类展示H5"
description: "展示类的前端，主要用于介绍一款产品或一些功能"
date:   2016-04-10 18:00:00
categories: share
tags: [王兆丹，angualrjs，instructions]
comments: true
---



##说明书类展示H5
###Angularjs可以利用数据绑定的方式实现说明书类H5的展示。

>####说明书类H5的实现的功能示例：（http://help.apple.com/iphone/9/）

###主要实现两大功能
####1.实现数据绑定，当点击前面的标签时，通过路由展示相对应得页面；
####2.当页面跳转到某一页的时候，相对应的标签处于高亮选中状态；


>####1.页面的列表HTMl的展示

{% highlight html %}

	<div class="row list" ng-class="{change:!ischange}">
            <div id="tree" class="treeview">
                <ul class="list-group">
                    <li class="list-group-item icon expand-icon node-tree" ng-repeat="tree in treedatas"
                        ng-click="toggleTree($index)" ng-class="{selected:checkSelectedClass($index)}"
                        ng-show="checkSelected($index,tree.level)">
                        
                        <span class="textA" ng-if="tree.level==1"></span>

                        <span class="indent" ng-if="tree.level==2"></span>
                        <span class="textB" ng-if="tree.level==2"></span>

                        <span class="indent" ng-if="tree.level==3"></span>
                        <span class="textC" ng-if="tree.level==3"></span>
                        <span class="indentx" ng-if="tree.level==3"></span>

                        <img class="icon-image" ng-if="tree.level==1" src="{{tree.icon_url}}">
                        <img class="icon-image" ng-if="tree.is_directory==1"
                             ng-class="{'expand-icon':tree.level==2,'iconN':tree.level==2,}">
                    

                        <a ng-href="#/show/{{tree.id}}">{{tree.title}}</a>
                        <img class="iconright" ng-if="tree.level==1" ng-class="{'iconchange':checkSelected($index)}"src="//s.rokidcdn.com/guide/assets/img/icon1.png">

                    </li>
                </ul>
            </div>
        </div>

{% endhighlight %}

>####2.实现第一功能（数据绑定）

####2.1 showpage的展示html

{% highlight html %}

 <p class="title"> {{info.title}}</p>
 <div class="RokidGuideContent" ng-bind-html="info.content" ></div>
    
{% endhighlight %}

####2.2 nav标签的实现（）

{% highlight html %}

 <nav>
        <ul class="pager">
            <li class="pre" ng-hide="check('pre')" ng-click="turn('pre')">
                <a  >< &nbsp;上一页</a>
            </li>
            <li class="nex"  ng-hide="check('next')" ng-click="turn('next')">
                <a>下一页 &nbsp;></a>
            </li>
        </ul>
    </nav>
    
{% endhighlight %}


{% highlight js %}

 $scope.turn = function (flag) {
            if (flag == "pre") {
                while (currLoaction-- > 0) {
                    if (_directory.indexOf(_dataList[(currLoaction)]) == -1) 
                        break;
                    }
                }
                $rootScope.currTreeid=currLoaction;
                //_dataList[(currLoaction)]代表当前的页面的id
                $location.path("/show/" + _dataList[(currLoaction)]);
                return;
            }
            while (currLoaction++ < _dataList.length) {
                if (_directory.indexOf(_dataList[(currLoaction)]) == -1) {
                    break;
                }
            }
            $rootScope.currTreeid=currLoaction;
            $location.path("/show/" + _dataList[(currLoaction)]);
        };

{% endhighlight %}


>####3.实现第二功能（treeID代表当前标签的位置，level代表层级）

####3.1当level==1的时候，判断标签页面的展示机会

{% highlight js %}
$rootScope.checkSelected = function (treeID, level) {
if (level == 1) {
            return true;
 }

{% endhighlight %}

####3.2当level==2的时候，判断标签页面的展示机会

{% highlight js %}

$rootScope.checkSelected = function (treeID, level) {
 if (level == 2) {
            if($rootScope.currTreeid==-1){
                 return false;
            }
            //_data
            //判断主目录节点
            var i = treeID;
            while (--i > 0) {
                if (_data[i].level == 1) {
                    //console.log(_data[i], i);
                    break;
                }
            }
            //判断当前节点的上一个主目录节点
            var ii = $rootScope.currTreeid;
            if (_data[ii].level == 1 ) ii =$rootScope.currTreeid;
            else {
                while (--ii > 0) {
                    if (_data[ii].level == 1) {
                        //console.log(_data[i], i);
                        break;
                    }
                }
            }
            if (($rootScope.currTreeid == i ) || ( ii == i && $rootScope.currTreeid != i )) {
                return treeID > i;
                //return true;
            }
            else {
                return false;
            }
            return treeID > i;
        }
   }
        
{% endhighlight %}


####3.2当level==3的时候，判断标签页面的展示机会

{% highlight js %}

$rootScope.checkSelected = function (treeID, level) {
            if (level == 3) {
            var i = treeID;
            //判断层级为二的目录节点
            while (--i > 0) {
                if (_data[i].level == 2) {
                    //console.log(_data[i], i);
                    break;
                }
            }
            var ii = $rootScope.currTreeid;
            //判断当前节点的上一个层级为二的主目录节点
            while (--ii > 0) {
                if (_data[ii].level == 2) {
                    //console.log(_data[i], i);
                    break;
                }
            }
            if ($rootScope.currTreeid == i || ii==i) {
                return treeID > i;
            }
             else {
                return false;
            }
            return treeID > i;
        }
        return $rootScope.currTreeid == treeID;
    };
    
{% endhighlight %}


>####这款说明书类的展示是大致模仿apple的的说明书，在功能上实现了路由的跳转、标签和页面实时更新、通过后台api实时获取后台数据，适配了手机端和pc端；我采用的方式是比较直接的一种方式，将所有的情况都综合考虑之后的方案；
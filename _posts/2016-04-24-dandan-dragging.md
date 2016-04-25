---
layout: post
title:  "元素的点击拖动事件"
description: "创建canvas对象，实现鼠标点击元素并且移动鼠标，拖动元素，使用了mousedown、mousemove、mouseup事件"
date:   2016-04-24 18:00:00
categories: share
tags: [王兆丹，angualrjs，Jquery，scroll]
comments: true
---



###创建canvas对象，实现拖动功能
####本次的分享主要涉及到canvas的创建和鼠标事件的处理，要实现的效果是创建canvas标签，并通过鼠标事件拖动元素


>###1.首先在页面上创建一个框div，命名为Canvas，代表里面的元素都是canvas标签的元素

####1.1 html页面

{% highlight html %}

	 <div id="Canvas"></div>
   
{% endhighlight %}


####1.2 css样式

{% highlight css %}

    html,
    body {
        width: 100%;
        height: 100%;
        margin: 0;
        padding: 0;
        background-color: #999;
    }
    #Canvas {
        width: 100%;
        height: 100%;
    }
  
   <!-- 定义canvas为浮动元素，用于鼠标点击移动 -->
   
    canvas{
        position: absolute;
    }
    
{% endhighlight %}





>###2.其次，在Canvas中创建canvas标签，获取当前Canvas的元素，通过参数传递，将canvas标签作为Canvas的子标签，并定义其位置；

####2.1  初始化定义

{% highlight js %}

    //'box1'代表的是创建元素的id，50代表半径和xy坐标

    init('box1', 50);

    
{% endhighlight %}

####2.2 函数定义


{% highlight js %}

    function init(Box,radius) {
  
        creatBox(Box, radius);
        place('#'+Box);
        move('#' + Box);
    }
    
{% endhighlight %}

{% highlight js %}

    function creatBox(Box,radius) {

        var Canvas = document.getElementById('Canvas');
       <!-- //创建元素-->
        var box = document.createElement('canvas');
        <!--//属性设置-->
        box.setAttribute('id', Box);
        box.setAttribute('width', radius*2);
        box.setAttribute('height', radius*2);
        <!--//作为子元素-->
        Canvas.appendChild(box);
       
       <!-- //绘制元素arc-->
        var boxContext = document.getElementById(Box).getContext('2d');

        boxContext.beginPath();
        boxContext.fillStyle = '#333';
        boxContext.arc(radius, radius, radius, 0, Math.PI * 2, false);
        boxContext.fill();
        boxContext.closePath();


    }
    
{% endhighlight %}

{% highlight js %}

     function place(box){
     
     //设置定位的top值和left，在页面位置随机出现
       
        var positionTop=Math.random()*1000;
        
        var positionLeft=Math.random()*1000;
        
        $(box).css({
            top:positionTop,
            left:positionLeft
        })
    }
    
{% endhighlight %}



>###3.最后设置移动的功能，监听mousedown、mousemove、mouseup这三个鼠标事件，根据不同的位置让元素的位置进行移动；


####移动move的函数定义
{% highlight js %}

     function move(box) {
       <!-- //设置变量-->
        
        var mouseX, mouseY;
        var objX, objY;
        var isDowm = false; 
        
       <!-- //是否按下鼠标-->

    <!--   //当鼠标按下的时候，-->
       
        $(box).mousedown(function (e) {
    
            mouseX = e.clientX;
            mouseY = e.clientY;
            //元素原本的值
            objX = e.target.offsetLeft;
            objY = e.target.offsetTop;
            isDowm = true;
            console.log('mousedown:mouseX:' + mouseX, 'mouseY:' + mouseY);
            console.log('mousedown:objX:' + objX, 'objY:' + objY);

        });
        
        <!--//当鼠标移动的时候-->
        
        $(box).mousemove(function (e) {
            
            var x = e.pageX;
            var y = e.pageY;
            console.log('mousemove:x:' + x, 'y:' + y);
            if (isDowm) {

       <!-- //在鼠标移动的过程中，位置不断的发生改变-->

                $(this).css({
                    "top": parseInt(objY) + parseInt(y) - parseInt(mouseY) + "px",
                    "left": parseInt(objX) + parseInt(x) - parseInt(mouseX) + "px"
                });

            }
        });
        
       <!-- //当鼠标抬起的的时候-->
        
        $(box).mouseup(function (e) {
            if (isDowm) {

            <!--    //  .pageX,clientX,.offsetX这些属性提供了鼠标指针位置相对于页面的左上角的X和Y坐标，在鼠标抬起的时候，位置不再改变-->
                
                var x = e.pageX;
                var y = e.pageY;

                $(this).css({
                    "top": (parseInt(y) - parseInt(mouseY) + parseInt(objY)) + "px",
                    "left": (parseInt(x) - parseInt(mouseX) + parseInt(objX)) + "px"
                });

                isDowm = false;
            }
        });

    }
    
{% endhighlight %}


>####在设置鼠标移动的方法的时候，我使用了JQuery进行编写，通过参数的传递进行事件的触发。在操作的过程中，通过输出当前的x/y来判断是否事件有执行，不断调试之后出来的方法；

####最主要的判断准则：parseInt(objY) + parseInt(y) - parseInt(mouseY)，objY是代表最开始的y轴位置，y代表的是当前鼠标所在的y轴位置，mouseY是指当鼠标点击的时候在的位置，所以该表达式，是最开始的objY轴位置+（鼠标所在的位置y-鼠标点击时的位置mouseY），如果（鼠标所在的位置y-鼠标点击时的位置mouseY）<0,top值就变小，元素往上移动；如果（鼠标所在的位置y-鼠标点击时的位置mouseY）>0,top值就变大，元素往下移动；

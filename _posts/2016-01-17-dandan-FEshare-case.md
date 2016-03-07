---
layout: post
title:  "小案例分享"
description: "这是一个很典型的例子，来理解闭包、形参、实参"
date:   2016-01-17 18:00:00
categories: share
tags: [前端分享,王兆丹]
comments: true
---



### 小案例一：获取数组的下标值

尝试：
{% highlight js %}

<ul>
    <li>This is the Num 1</li>
    <li>This is the Num 2</li>
    <li>This is the Num 3</li>
    <li>This is the Num 4</li>

</ul>


<script type="text/javascript">

    var li = document.getElementsByTagName("li");
    for (var i = 0; i < li.length; i++) {
       li[i].onclick = function () {
            this.innerText = i;

        }
    }
</script>

{% endhighlight %}

>此方法输出的内容：

4
4
4
4

###最初思考步骤：
1.要想遍历li的标签，并将li的文本改为该li的数组下标值，原生的方法中可以用for循环；
2.循环li，定义一个数组li［］，将所有的li标签都置于该数组中；
3.用.onclick（）点击事件实现点击改变text的值，可以定义函数；

>初步考虑得到以上的代码，but：
>结果，每一个li标签的文本都变成了4，也就是循环结束的最后一个；
>每一个.onclick的匿名函数都绑定了同一个i变量的，当这个匿名函数被执行的时候，i的值就是固定的li.length。
>在函数内定义了一个函数，形成了闭包，内部函数可以访问外部函数的值，外部函数不能访问内部函数

>改进之后：

{% highlight js %}
<script type="text/javascript">

        var li = document.getElementsByTagName("li");
        for (var i = 0; i < li.length; i++) {
            li[i].onclick =(function(arg){
              return  function(){
                  this.innerText=arg;
              }

            })(i)
        }

</script>
{% endhighlight %}

>修改过后输出的值：
0
1
2
3

>理解闭包，获取列表li的下标值
>1.获取标签li；
>2.用for循环遍历该li标签，创建onclick事件，将onclick事件用闭包的形式展现；
>3.arg作为本地的私有变量，以形参的形式传入闭包，i作为实参，传入闭包；
>4.在闭包中return一个函数，获取li标签的下标，将传入的i值作为本地私有变量arg的形式进行传递；


###总结：
###这是一个很典型的例子，来理解闭包、形参、实参；
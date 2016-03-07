---
layout: post
title:  "伪元素的应用案例"
description: "熟悉伪元素，分析伪元素的应用案例"
date:   2016-03-06 18:00:00
categories: share
tags: [前端分享,王兆丹]
comments: true
---

#伪元素的使用:
>伪元素能够在文档中插入假想的元素，从而得到某种效果，这样的元素在css中定义了4个
::first-letter  定义首个字母的样式
::first-line   定义第一行内容的样式
::before     设置之前元素的样式
::after      设置之后元素的样式
>这里主要讲述在使用::after和::before的几个例子：要与content一起使用

####1.引用语录：
  {% highlight html %}
 <p class="ex-three"> 引用语录 </p>
 {% endhighlight %}

 {% highlight css %}
  .ex-three{
            position: relative;
            display: inline-block;
            outline: none;
            text-decoration: none;
            color: #000;
            font-size: 18px;
            padding: 5px 10px;
            margin-left: 10%;
  }
  .ex-three:hover{
          color:red;
   }
  .ex-three:before{
         content: open-quote;

   }
   .ex-three:after{
        content: close-quote;
   }
  {% endhighlight %}

####2.添加前缀

#####2.1添加外框

{% highlight html %}
<p class="ex-one" >HYHYUHY</p>
 {% endhighlight %}

 {% highlight css %}
 .ex-one {
            position: relative;
            display: inline-block;
            outline: none;
            text-decoration: none;
            color: #000;
            font-size: 18px;
            padding: 5px 10px;
            margin-left: 10%;
        }
        .ex-one:hover::before, a:hover::after { position: absolute; }
        .ex-one:hover::before { content: "\5B"; left: -5px; }
        .ex-one:hover::after { content: "\5D"; right:  -5px; }

{% endhighlight %}

#####2.2添加外框和前缀

{% highlight html %}
<p class="box">Other content.</p> 
{% endhighlight %}

 {% highlight css %}
p.box {  
  width: 300px;  
  border: solid 1px white;  
  padding: 20px;  
}  
p.box:before {  
  content: "#";  
  border: solid 1px white;  
  padding: 2px;  
  margin: 0 10px 0 0;  
}
{% endhighlight %}


####3.添加图片
{% highlight css %}
::after{
   content:url(img.jpg);
}
{% endhighlight %}
 

####4.显示相应的地址

{% highlight html %}
<a class="ex-two" href="http://www.baidu.com">百度链接:</a>
{% endhighlight %}

{% highlight css %}
.ex-two{
            position: relative;
            display: inline-block;
            outline: none;
            text-decoration: none;
            color: #000;
            font-size: 18px;
            padding: 5px 10px;
            margin-left: 10%;
 }
 .ex-two:after{
            content: attr(href);
            color: blue;

 }

 {% endhighlight %}

####5.时尚焦点相框   http://www.jiawin.com/css-before-after


####6.计数器

#####6.1冰激凌计数
{% highlight html %}
<strong>下面中国十大冰淇淋你吃过几个？</strong>
<ol>
    <li><input type="checkbox" id="icecream1"><label for="icecream1">哈根达斯</label></li>
    <li><input type="checkbox" id="icecream2"><label for="icecream2">和路雪wall's</label></li>
    <li><input type="checkbox" id="icecream3"><label for="icecream3">八喜冰淇淋</label></li>
    <li><input type="checkbox" id="icecream4"><label for="icecream4">DQ冰淇淋</label></li>
    <li><input type="checkbox" id="icecream5"><label for="icecream5">蒙牛冰淇淋</label></li>
    <li><input type="checkbox" id="icecream6"><label for="icecream6">雀巢冰淇淋</label></li>
    <li><input type="checkbox" id="icecream7"><label for="icecream7">伊利冰淇淋</label></li>    
    <li><input type="checkbox" id="icecream8"><label for="icecream8">乐可可冰淇淋</label></li>
    <li><input type="checkbox" id="icecream9"><label for="icecream9">新城市冰淇淋</label></li>
    <li><input type="checkbox" id="icecream10"><label for="icecream10">明治MEIJI</label></li>
</ol>
你总共选择了 <strong class="total"></strong> 款冰淇淋！

{% endhighlight %}


{% highlight css %}
body {
  counter-reset: icecream;
}
input:checked {
  counter-increment: icecream;
}
.total::after {
  content: counter(icecream);
}
{% endhighlight %}



#####6.2显示目录 

{% highlight html %}

<h1>HTML tutorials</h1>

<h2>HTML Tutorial</h2>

<h2>XHTML Tutorial</h2>

<h2>CSS Tutorial</h2>

<h1>Scripting tutorials</h1>

<h2>JavaScript</h2>

<h2>VBScript</h2>

<h1>XML tutorials</h1>

<h2>XML</h2>

<h2>XSL</h2>
 {% endhighlight %}
 
 
{% highlight css %}
body{
    counter-reset: section;
}
h1{
    counter-reset: subsection;
}
h1:before{
    counter-increment:section;
    content:counter(section) "、";
}

h2:before{
    counter-increment:subsection;
    content: counter(section) "." counter(subsection) "、";
}
{% endhighlight %}




####7. 特殊字符html css 和js
http://www.cnblogs.com/starof/p/4718550.html




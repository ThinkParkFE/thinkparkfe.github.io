---
layout: post
title:  "组件化工具vue.js的简单使用"
description: "视图与数据的分离，数据绑定的形式和组件的自定义"
date:   2016-03-13 18:00:00
categories: share
tags: [vuejs,王兆丹]
comments: true
---



#组件化工具vue.js

>Vue.js原本是着眼于轻量的嵌入式使用场景。在今天，Vue.js也依然适用于这样的场景。由于其轻量、高性能的特点，对于移动场景也有很好的契合度。更重要的是，设计完备的组件系统和配套的构建工具、插件，使得Vue.js在保留了其简洁API的同时，也已经完全有能力担当起复杂的大型应用的开发。

####初始化准备：
>安装：bower install vue --save-dev

>引用
```<script src="../bower_components/vue/dist/vue.min.js"></script>```
## 数据绑定（msg是数据）

 {% highlight html %}
<!-- 指令 -->
<span v-text="msg"></span>
<!-- 插值 -->
<span>{{msg}}</span>
<!-- 双向绑定 -->
<input v-model="msg">  
 {% endhighlight %}
 
##图片资源的引用：
图片数据的引用HTML

{% highlight html %}
<div id="footer”>
<img :src="img1">
<img :src="img2">
<img :src="img3">
<img :src="img4">
<div>
{% endhighlight %}

数据的形式JSON：

{% highlight js %}
var date=｛
"footer":{
    "img1":"p1.png",
    "img2":"p2.png",
    "img3":"p3.png",
    "img4":"p4.png"
  }
 ｝
{% endhighlight %}

js的处理（数据可以直接写进js，也可以用ajax将数据读取出来）：

{% highlight js %}
new Vue({
         el: '#footer',
         data: data
       });
{% endhighlight %}  
     
##组件的使用示例：
html：
{% highlight html %}
<my-component msg="hello"></my-component>
{% endhighlight %}

js：
{% highlight js %}
Vue.component('my-component', {
    // 模板
    template: '<div>{{msg}} {{privateMsg}}</div>',
    // 接受参数
    props: {
        msg: String<br>    

    },
    //私有数据，需要在函数中返回以避免多个实例共享一个对象
    data: function () {
        return {
            privateMsg: 'component!'
        }
    }
})      
{% endhighlight %}

渲染效果：
{% highlight html %}
<div>hello component!</div>
{% endhighlight %}

以上主要是介绍了vue.js的数据绑定的方法和组件使用的相关例子。我们可以比较一下这种方式与之前的方式，看看哪种方式更适合当前的项目或者更适合你的逻辑，工具只是帮助我们更快更方便的实现目的，并不是最重要的。


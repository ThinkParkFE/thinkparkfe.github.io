---
layout: post
title:  "three.js 打造3D全景漫游"
description: ""
date:   2016-05-15 19:46:00
categories: share
tags: [three.js,前端分享,储涛]
comments: true
---


>three.js是JavaScript编写的WebGL第三方库。提供了非常多的3D显示功能。



//使用到的JS库：
three.min.js
CSS3DRenderer.js


//设置相机
{% highlight html %}

camera = new THREE.PerspectiveCamera(50, window.innerWidth / window.innerHeight, 1, 1000);

{% endhighlight %}


//设置场景
{% highlight html %}

scene = new THREE.Scene();

{% endhighlight %}


//设置3D空间的6个面，通过pano2vr直接将鱼眼全景图生成立体空间的六个面；也可通过Photoshop或其他的专业3D建模工具，将鱼眼图贴到3D球面上，再将球面转为立方面，获得立体空间的六个面。

{% highlight js %}
var sides = [{
    url: 'assets/images/posx.jpg',
    position: [-512, 0, 0],
    rotation: [0, Math.PI / 2, 0]
}, {
    url: 'assets/images/negx.jpg',
    position: [512, 0, 0],
    rotation: [0, -Math.PI / 2, 0]
}, {
    url: 'assets/images/posy.jpg',
    position: [0, 512, 0],
    rotation: [Math.PI / 2, 0, Math.PI]
}, {
    url: 'assets/images/negy.jpg',
    position: [0, -512, 0],
    rotation: [-Math.PI / 2, 0, Math.PI]
}, {
    url: 'assets/images/posz.jpg',
    position: [0, 0, 512],
    rotation: [0, Math.PI, 0]
}, {
    url: 'assets/images/negz.jpg',
    position: [0, 0, -512],
    rotation: [0, 0, 0]
}];

{% endhighlight %}


//将定义好的6各面添加到空间中,并为每个空间指定ID
{% highlight js %}

for (var i = 0; i < sides.length; i++) {
    var side = sides[i];
    var element = document.createElement('section');
    element.id = 'section_'+i;
    var imgElement = document.createElement('img');
    imgElement.width = 1026; // 2 pixels extra to close the gap.
    imgElement.src = side.url;
    element.appendChild(imgElement);
    var object = new THREE.CSS3DObject(element);
    object.position.fromArray(side.position);
    object.rotation.fromArray(side.rotation);
    scene.add(object);
}
{% endhighlight %}


//设置渲染器
{% highlight js %}
renderer = new THREE.CSS3DRenderer();//定义渲染器
renderer.setSize(window.innerWidth, window.innerHeight);//设置尺寸
document.body.appendChild(renderer.domElement);//将场景加入页面
{% endhighlight %}


//实时渲染
{% highlight js %}
function animate() {
    requestAnimationFrame(animate);
    //lon = Math.max(-180, Math.min(180, lon));//限制固定角度内旋转
    //lon += 0.1;//自动旋转
    lon += 0;
    lat = Math.max(-85, Math.min(85, lat));
    phi = THREE.Math.degToRad(90 - lat);
    theta = THREE.Math.degToRad(lon);
    target.x = Math.sin(phi) * Math.cos(theta);
    target.y = Math.cos(phi);
    target.z = Math.sin(phi) * Math.sin(theta);
    camera.lookAt(target);
    renderer.render(scene, camera);
}
{% endhighlight %}


//为每个面构建空间的图标物件
{% highlight js %}

function addIcon(){
    var imgIcon = document.createElement('img');
    imgIcon.src = '../static/img/arrow_right.png';
    imgIcon.classList.add('icon');
    document.getElementById('section_4').appendChild(imgIcon);
}
addIcon();

{% endhighlight %}



//监听触摸事件
{% highlight js %}

function onDocumentTouchStart(event) {
    event.preventDefault();
    var touch = event.touches[0];
    touchX = touch.screenX;
    touchY = touch.screenY;
}

function onDocumentTouchMove(event) {
    event.preventDefault();
    var touch = event.touches[0];
    lon -= (touch.screenX - touchX) * 0.1;
    lat += (touch.screenY - touchY) * 0.1;
    touchX = touch.screenX;
    touchY = touch.screenY;
}
{% endhighlight %}


>现在还在该尝试基本上使用，但在性能优化，细节完善上和功能上面还继续打磨。

---
layout: post
title:  "HTML5 重力感应"
description: ""
date:   2016-01-24 17:00:00
categories: share
tags: [重力感应,前端分享,储涛]
comments: true
---

>HTML5 重力感应功能介绍

#html5 中针对高端手机提供了重力感应和重力加速的接口，开发可以利用这个接口获取到移动设备重力加速感应数据。



>提供的感应事件

{% highlight js %}


* window.addEventListener('deviceorientation', this.orientationListener, false); //方向感应器

* window.addEventListener('MozOrientation', this.orientationListener, false); //方向感应器 for firefox

* window.addEventListener('devicemotion', this.orientationListener, false); //重力加速感应器 for iphone, android

{% endhighlight %}



>重力感应示例代码

{% highlight js %}

function Orientation(selector) {

	            }

	            Orientation.prototype.init = function(){
		            window.addEventListener('deviceorientation', this.orientationListener, false);
		            window.addEventListener('MozOrientation', this.orientationListener, false);
		            window.addEventListener('devicemotion', this.orientationListener, false);
	            }

	            Orientation.prototype.orientationListener = function(evt) {
	              // For FF3.6+

	              if (!evt.gamma && !evt.beta) {
	              	// angle=radian*180.0/PI 在firefox中x和y是弧度值,
	                evt.gamma = (evt.x * (180 / Math.PI)); //转换成角度值,
	                evt.beta = (evt.y * (180 / Math.PI)); //转换成角度值
	                evt.alpha = (evt.z * (180 / Math.PI)); //转换成角度值
	              }

	                /* beta:  -180..180 (rotation around x axis) */
	             	/* gamma:  -90..90  (rotation around y axis) */
	             	/* alpha:    0..360 (rotation around z axis) (-180..180) */

	              var gamma = evt.gamma
	              var beta = evt.beta
	              var alpha = evt.alpha

	              if(evt.accelerationIncludingGravity){

	               // window.removeEventListener('deviceorientation', this.orientationListener, false);

					gamma = event.accelerationIncludingGravity.x*10
					beta = -event.accelerationIncludingGravity.y*10
					alpha = event.accelerationIncludingGravity.z*10

	              }


	              if (this._lastGamma != gamma || this._lastBeta != beta) {
	              	 document.querySelector("#test").innerHTML = "x: "+ beta.toFixed(2) + " y: " + gamma.toFixed(2) + " z: " + (alpha != null?alpha.toFixed(2):0)

	                  var style = document.querySelector("#pointer").style;
	                  style.left = gamma/90 * 200 + 200 +"px";
	                  style.top = beta/90 * 100 + 100 +"px";


	                this._lastGamma = gamma;
	                this._lastBeta = beta;
	              }
	            };

	            (new Orientation()).init();

{% endhighlight %}

{% highlight html %}

方向中分alpha，beta，gamma三个，其实对应我们常说的 y, z, x 三个方向, 方向可以通过 event 来直接获取得到。

{% endhighlight %}

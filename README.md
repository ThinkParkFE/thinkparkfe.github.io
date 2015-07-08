# thinkparkfe.github.io
ThinkPark FE开源项目官网 - 我们的愿景: 成为业界卓越的Web团队！  http://ThinkParkFE.github.io/
=================
One Team, One Dream! 多年以后，让我们创造一个奇迹！

By [ThinkPark FE](http://ThinkParkFE.github.io/)

## 我们的愿景

成为业界卓越的Web团队！


## 团队部分代码规范
虽然这些细节是小事，但是却体现了一个coder的专业程度。
更多详细情况请看：
http://ThinkParkFE.github.io/CodeGuide/


### 标准文件结构

	[mainfolder]
	 |--[js]		//js文件夹
	 |   |-- main.js
	 |--[style]		//所有样式相关的css和image
	 |   |-- [image]	//主要image文件夹
	 |   |    |-- img1.png
	 |   |    ...
	 |   |-- [style_name_a]	//皮肤A的文件夹
	 |   |    |-- [image]	//皮肤A的image
	 |   |    |-- style_name_a.css	//皮肤A的css文件
	 |   |    ...
	 |   |-- [style_name_b]	//皮肤B的文件夹
	 |   |-- [style_name_c]	//皮肤C的文件夹
	 |   |-- main.css	//主要css文件
	 |--[audio]		//所有样式相关的audio音频文件
	 |   |-- sound.mp3	//audio文件
 	 |-- index.html		//index文件
 	 |-- page1.html		//其他页面
 	 ...
	  
	  
文件名全部英文小写，用下划线分隔。

	  
	  
### 标准html5代码

	<!DOCTYPE html>
	<html>
	<head>
		<meta charset="utf-8" />
		<meta name="author" content="ThinkPark.FE.Andy" />
		<meta name="copyright" content="ThinkParkFE" />
		<meta name="keywords" content="ThinkPark FE 团队" />
		<meta name="description" content="ThinkParkFE" />
		
		<title>ThinkParkFE 标准文档</title>
		<link href="./style/main.css" rel="stylesheet" type="text/css" />
	</head>
	<body>
		<!-- 注释 -->
		<h1 id="title" class="title">ThinkParkFE 标准文档</h1>
		<div>
			<h3>Title</h3>
			<p>
				标准文档
			</p>
		</div>

		<script type="text/javascript" src="./js/jx.min.js"></script>
		<script type="text/javascript">

			var J = new Jx();

		</script>
	</body>
	</html>



### 标准javascript代码

	/**
	 * === Javascript eXtension 模块 =========================================================================
	 * Copyright (c) 2015 ThinkParkFE, All rights reserved.
	 * http://ThinkParkFE.github.io/
	 * Code licensed under the BSD License:
 	 * http://ThinkParkFE.github.io/license.txt
	 * 
	 * @version 2.0
	 * @author	andy <hejun@socialpark.com.cn>
	 * @description 描述文字
	 * ---2015.7.8 ----------------------------
	 */

	/**
	 * 注释
	 */
	Jx().$package('ThinkParkFE', function(J) {
		var self = this,
			$D = J.dom,
			$E = J.event,
			$H = J.http;

		// 输出字符串'Hello world!'
		J.out('Hello world!');

		// 输出this === ThinkParkFE的判断结果
		J.out(this === ThinkParkFE);
	});


### 标准css代码
	
	.copyright {
	    margin: 50px 0 0 0;
	    height: 50px;
	
	    font-family: Tahoma;
	    font-size: 12px;
	    text-align: center;
	
	    color: #999;
	}
	
	.copyright a {
	    text-decoration: none;
	
	    color: #999;
	}
	
	/* 注释 */
	.copyright a:hover,
	.copyright a:focus {
	    text-decoration: underline;
	
	    outline: none;
	}

### 标准版权声明代码

  	<div class="copyright">Copyright &copy; <script>document.write(new Date().getFullYear());</script> <a href="http://ThinkParkFE.github.io/" target="_blank">ThinkParkFE</a>. All Rights Reserved.</div>


### 标准捐赠代码

	 <a href="#" target="helpus" title="支持开源项目，请我们喝杯咖啡吧^_Q"> <img src="http://ThinkParkFE.github.io/style/image/alipay_btn.jpg" alt="支持开源项目，请我们喝杯咖啡吧^_Q" /> </a>
	 
	 <a href="#" target="helpus" title="感谢支持开源项目，我们会努力做的更好！"> <img src="http://ThinkParkFE.github.io/style/image/alipay_btn.jpg" alt="捐赠开源项目" /> </a>

### 标准访问统计代码

	<!--baidu Analytics-->
	<script>
var _hmt = _hmt || [];
(function() {
  var hm = document.createElement("script");
  hm.src = "//hm.baidu.com/hm.js?699f59be37467ca880923a030224adc4";
  var s = document.getElementsByTagName("script")[0]; 
  s.parentNode.insertBefore(hm, s);
})();
</script>





### 关于团队

	var ThinkParkFE = {
	    name: 'ThinkParkFE',
	    qq: 4240249,
	    site: 'http://ThinkParkFE.github.io/',
	    github: 'http://ThinkParkFE.github.io/'
	}

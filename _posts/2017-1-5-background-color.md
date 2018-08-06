---
layout: post
title: CSS3背景颜色渐变属性
---

CSS3渐变（gradients）可以让你在两个或多个指定的颜色之间显示平稳的过度。  
CSS3定义了两种类型的渐变(gradients):  
线性渐变（linear gradients）：向下/向上/向右/对角方向  
径向渐变(radial gradients)：由它们的中心定义  
语法：background: linear-gradient(direction, color-stop1, color-stop2,...)  
但针对不同的浏览器要加不同的名称。 

Webkit 

尽管Mozilla和Webkit通常对CSS3属性采取同样的语法，但是对于渐变，它们并不能达成一致。Webkit是第一个支持渐变的浏览器内核，它使用下面的结构:

```javascript
    -webkit-gradient(<type>,<point>[,<radius>]?,<point>[,<radius>]?[,<stop>]*)
    <!-- 实际用法 -->
    background:-webkit-gradient(linear,0 0, 0 100%, from(pink),to(red));
```
效果如下图：    
![_config.yml]({{ site.baseurl }}/images/170105-1.png)   
渐变类型：linear  
渐变开始的x y轴坐标(0 0-或者left-top)  
渐变结束的x y轴坐标(0 100% 或者left-bottom)  
开始的颜色(from(red))  
结束的颜色(to(blue))  

Mozilla  
Firefox,从3.6版本才开始支持渐变，语法和Webkit略微不同。   

~~~javascript
    -moz-linear-gradient([<point>||<angle,]?<stop>,<stop>[,<stop>]*)
    <!-- 实际用法 -->
    background:-moz-linear-gradient(top,red,green);
~~~   

效果如图：   
![_config.yml]({{ site.baseurl }}/images/170105-2.png)  
渐变从哪里开始？(top-我们也可以使用度数，比如-45deg)   
开始的颜色（red）
结束的颜色（blue)   

Color-Stops  
如果不需要从一个颜色到另一个颜色的100%渐变，可以使用color-stops   

~~~javascript
    background:white;
    <!-- 为较旧的或者不支持的浏览器设置备用属性 -->
    background:-moz-linear-gradient(bottom,#dedede,white 40%);
    background:-webkit-gradient(linear,0 100%,0 40%, from(#dedede), to(white));
    border:1px solid #000;
~~~   

这个例子中，我们让渐变结束于40%，而不是默认的100%，效果如下图：
![_config.yml]({{ site.baseurl }}/images/170105-3.png)  

如果想要添加多几种颜色，可以这样做：

```javascript
    background:white;
    <!-- 备用属性 -->
    background:-moz-linear-gradient(top,#dedede,white 8%, red 20%);
    <!-- 这里定义，从元素的20%高度的地方开始是红色 -->
    background:-webkit-gradient(linear,0 0, 0 100%, from(#dedede),color-stop(8%,white),color-stop(20%,red));
```

效果如下图：（只有Firefox中能显示，chrome和360都不能显示，可能是color-stop的原因）   
![_config.yml]({{ site.baseurl }}/images/170105-4.png)

IE   
linear-gradient在IE9以下是不支持的，所以对于ie6-ie8可以使用滤镜来解决，代码如下：  

```javascript
    .gradient{
    filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#000000', endColorstr='#ffffff',GradientType=0 );
}
```

由于 filter 是 ie 的私有属性，所以我们需要针对 ie9单独处理滤镜效果，代码如下：  

~~~javascript
    :root {filter:none;}
~~~

<b>总结</b>：线性渐变的兼容写法如下：

```javascript
    .gradient{
    background: #000000;
    background: -moz-linear-gradient(top,  #000000 0%, #ffffff 100%);
    background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#000000), color-stop(100%,#ffffff));
    background: -webkit-linear-gradient(top,  #000000 0%,#ffffff 100%);
    background: -o-linear-gradient(top,  #000000 0%,#ffffff 100%);
    background: -ms-linear-gradient(top,  #000000 0%,#ffffff 100%);
    background: linear-gradient(to bottom,  #000000 0%,#ffffff 100%);
    filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#000000', endColorstr='#ffffff',GradientType=0 );
}
:root .gradient{filter:none;}
```

效果如下图   
![_config.yml]({{ site.baseurl }}/images/170105-5.png)

<b>比较通用的简单写法：</b>   


~~~javascript
    background: -webkit-gradient(linear, 0 0, 0 bottom, from(transparent), to(red));
	background: -webkit-linear-gradient(transparent, red);
	background: -moz-linear-gradient(transparent, red);
	background: -ms-linear-gradient(transparent, red);
	background: -o-linear-gradient(transparent, red);
	background: linear-gradient(transparent, red);
	-pie-background: linear-gradient(transparent, red);"
~~~   


![_config.yml]({{ site.baseurl }}/images/170105-6.png)

本文参考自[前端开发博客](http://caibaojian.com/css3-background-gradient.html)   
遗留问题：颜色+百分比

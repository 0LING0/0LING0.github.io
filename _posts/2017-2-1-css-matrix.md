---
layout: post
title: CSS 矩阵
---

矩阵看起来是个比较复杂的工具，其实吧，它真的就比较复杂。我开始看也是稀里糊涂，翻了几本书，看了几个大牛的博客，反复看相关视频，
才感觉理解了一部分。如果想更好更透彻地理解，可以参见[张鑫旭老师的博客](http://www.zhangxinxu.com/wordpress/2012/06/css3-transform-matrix-%E7%9F%A9%E9%98%B5/)，讲得非常滴好。   

方便自己学习，就先记录下几个常用结论，后续理解更深了，再来更新。   

<b>矩阵是怎么来的?</b>

CSS的transform 有4种转换方法：旋转rotate,移动translate, 缩放scale, 扭曲skewm,每一种都可以将图形进行相应的转换。但是这些方法都是一对一的，而矩阵，正是他们强大的综合体！  

matrix()是元素2D平面的移动变换(transform), 2D变换矩阵为3X3；matrix3d()是元素3D的移动变化，3D变化则是4X4矩阵。   

transform:matrix(a,b,c,d,e,f); 书写方向是数值方向。  
![_config.yml]({{ site.baseurl }}/images/170201-1.png)

转换公式：X,Y 表示转换元素的所有坐标，就是transform-origin的值，如果没写，默认是 0 0 1；
目标矩阵：ax+cy+e为变换后的水平坐标，bx+by+f表示变换后的垂直位置。  

1. 平移：transform:matrix(1,0,0,1,x,y)=transform:translate(x,y);前面四个参数1,0,0,1或者0,1，1,0表示不对图形进行缩放、变形操作。注意矩阵的参数不需要带单位，而translate却需要。  

2. 缩放：matrix(sx,0,0,sy,0,0)=scale(sx,sy)
前面四个参数sx,0,0,sy或0，sy,sx,0表示将图像横向扩大sx倍，纵向扩大sy倍。后来两个参数为0，表示不移动坐标原点。

3. 旋转：matrix(cosθ,sinθ,-sinθ,cosθ,0,0)=rotate(θdeg)
前面四个参数cosθ,sinθ,-sinθ,cosθ 或-sinθ, cosθ, cosθ, sinθ共同完成图形按angle角度的旋转处理。后面两个参数0,0表示不移动坐标原点。

4. 拉伸：matrix(1,tanθy,tanθx,1,0,0)=skew(θxdeg,θydeg);

5. 矩阵matrix镜像对称效果
沿着y=kx做对称k为斜率，matrix((1-k*k)/(1+k*k),2k/(1+k*k),2k/(1+k*k),(k*k-1)/(1+k*k),0,0)
说明：  
1.对称轴一定通过元素变换的中心点，k是对称轴的斜率   
2.注意CSS的x轴是向右的，y轴是向下的。

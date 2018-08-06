---
layout: post
title: background-position和雪碧图
---

<b>background-position定义</b>  
background-position属性设置背景图像的起始位置，这个属性设置背景愿图像（由background-image定义）的位置，背景图像如果要重复，将从这一点开始。  

提示：background-position属性设置背景原图像（由background-image定义）的位置，意味着使用这个属性的前提是必须设置背景原图像background-image.

<b>background-position的属性值</b>  
background-position有两个属性值，background-position:x|y,用法上可以对其一个属性单独使用background-position-x和background-position-y.  

background-position属性值有三种表示方法  
1. 方向值：x轴方向：left，right，center  y轴方向：top，bottom，center  
2. 百分比：x轴方向：x%    y轴方向：y%
3. 数值：x轴方向：x px(单位值)  y轴方向：x px(单位值)  

background-position 两个属性值可以混用，例如：方向值和数值、数值和百分值，并非x轴和y轴需要设置为同一类型的属性值，这点也正是说明了background-position属性可以衍生单独设置background-position-x和background-position-y.  

background-position属性值之神奇的百分比  

我们都知道background-position属性的作用：设置背景图像的起始位置，这里的起始位置是相对于自身容器而言，如果属性值为数值，比如：background-position：100px 50px 这个属性值意味着图片在距离自身容器x轴为100px,y轴为50px的位置作为图片显示的起点位置。  

然而使用百分比来设置属性值，是以自身容器的长宽  减去  图片的长宽  乘以百分比所得的数值来确定图片的起始位置。  

公式：（容器自身的宽度/高度-图片自身的宽度/高度）*百分比  

例如：background-position：50% 50%  最终的结果是显示在自身容器的正中央，而不是以（容器宽度的50%，容器高度的50%）来作为图片的起点。  

提示：  
1.background-position属性值如果是数值，那么指相对于容器自身数值的距离作为起始位置；如果是百分比或者是方向，那么指的是相对于容器自身（容器自身宽度/高度-图片自身的宽度/高度）*百分比所得的数值作为起始位置。  
2.如果不设置background-position属性值，那么默认起始位置为background-position：0% 0%  
3.方向值和百分比的计算方式是一样的，它们可以相互转换：left:0%, right:100%, center:50%  
4.如果background-position属性值只设置一个，那么另一个默认为center。  

<b>雪碧图</b>  
了解了background-position的定义之后，我们便很好理解雪碧图的设置原理了。  
![_config.yml]({{ site.baseurl }}/images/170107-sprite.png)  

显示第一个图片的时候，利用默认0% 0%的位置就可以了  
![_config.yml]({{ site.baseurl }}/images/170107-1.png)  

显示第一列第二张图片的时候，我们把位置设置为background-positiion: 0 -50px，相当于背景图片的起始位置是0 -50px。其他位置也同理，我们只是通过改变背景图片的起始位置从而得以改变背景图像在div中的显示。  
![_config.yml]({{ site.baseurl }}/images/170107-2.png)  

本文参考自[bingkingboy的博客](http://blog.csdn.net/bingkingboy/article/details/51059209)


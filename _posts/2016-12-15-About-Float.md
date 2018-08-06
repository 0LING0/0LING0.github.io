---
layout: post
title: 关于清除浮动的几种方法
---

BFC: Block Formating Content 用来清除浮动，处理浮动元素脱离文档流的问题 

清除浮动共有六种方法，目前最推荐的是第六种。 

方法一：父级也浮动
缺点：左右margin：0 auto 会失效，而且当嵌套多个父元素时不好用

方法二：给父级加display:inline-block(不会脱离文档流)
缺点：margin:0 auto 失效，想居中的话还要加text-align:center

方法三：给父级加高（扩展性不好）

方法四：&lt;br&gt;标签
&lt;br clear="all"/&gt; 但是不符合W3C标准、

方法五：clear:both

方法四与五均不符合W3C规范，违反结构、样式、行为三者分离原则

方法六：伪类清浮动（**）  
：after{content:'';
        display:block;
        clear:both;}

这个是目前的主流方法，建议使用（可以放在css中，在父级中调用下面的clear就可以，但是要应用在包含浮动子元素的父元素上）

.clear:after{
	content:'';
	display:block;
	clear:both;
}

.clear{zoom:1;}  (因为IE6,7不认伪类，保证兼容)  

添加zoom:1属性可触发IE下的haslayout,就解决了塌陷的问题
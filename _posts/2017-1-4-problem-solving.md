---
layout: post
title: 浏览器中文乱码处理
---

问题：中文乱码，除了chrome能正常显示，其他浏览器（ie,firefox,360）均出现乱码。   
解决方案：在头部添加如下代码

~~~javascript
    <meta http-equiv="Content-Type" content="text/html;charset=utf-8"/>
~~~

---
layout: post
title: 关于mouseover和mouseout事件的处理
---
当鼠标进入和离开一个节点的时候，mouseover和mouseout事件都会被分别激活。然而我们并不能按照字面意思简单地调用这两个事件。因为，当鼠标从一个节点进入它的子节点的时候，mouseout事件也会被激活，同时，当鼠标从子节点移出的时候，由于事件冒泡机制，mouseout事件会再次被激活，显然这样的情况并不是我们想要的。

解决这个问题，我们可以使用事件对象的一个<b>relatedTarget</b> 属性，它的定义是这样的："in the case of "mouseover", what element the pointer was over before and, in the case of "mouseout", what element it is going to." 在mouseover事件中，它指的是鼠标进入节点之前的那个元素；在mouseout事件中，它指的鼠标即将进入的那个元素。总之，relatedTarget所指的这个节点是在我们的目标节点之外的。
所以我们可以这样处理一个鼠标划过字体变色的问题。

~~~javascript
<p>Hover over this <strong>paragraph</strong>.</p>
<script>
  var para = document.querySelector("p");
  function isInside(node, target) {
    for (; node != null; node = node.parentNode)
      if (node == target) return true;
  }
  para.addEventListener("mouseover", function(event) {
    if (!isInside(event.relatedTarget, para))
      para.style.color = "red";
  });
  para.addEventListener("mouseout", function(event) {
    if (!isInside(event.relatedTarget, para))
      para.style.color = "";
  });
</script>
~~~

当然对于这个问题，我们可以使用css 的伪类hover进行简单处理，这里只是举一个例子，如果遇到更复杂的情况，我们可以这种方法来规避一些问题。
---
layout:     post
title:      神奇的负边距
category:   blog
tags :      [css、margin]
description: 负边距有什么作用？负边距能产生什么效果？利用这些效果我们能做什么？就让我们一起进行探索吧。
---


##什么是margin

margin（外边距）：是标签和标签之间的空白，通俗的讲就是框与其他元素的距离。

	margin:10px -20px 30px 40px;

当目标元素有周围有兄弟元素时，就是与兄弟元素之间的距离

在正常文档流（没有float）中，负边距的标下如下图所示：

![在正常文档流中的负边距](https://raw.githubusercontent.com/xuhp/xuhp.github.io/master/images/theMagicalNegativeMargin/margin-motion.gif)

> 以上图片主要针对于element的 display 属性为 block 或 inline-block,


<a class="jsbin-embed" href="http://jsbin.com/wahelirari/1/embed?html,css,output">JS Bin on jsbin.com</a>
<script src="http://static.jsbin.com/js/embed.min.js?3.34.1"></script>


##




##参考文档

[The Definitive Guide to Using Negative Margins](http://www.smashingmagazine.com/2009/07/the-definitive-guide-to-using-negative-margins/)

[负值之美：负值在页面布局中的应用](http://www.topcss.org/?p=94)

[CSS布局奇淫巧计之-强大的负边距](http://www.cnblogs.com/2050/archive/2012/08/13/2636467.html)
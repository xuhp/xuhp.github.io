---
layout:     post
title:      神奇的负边距
category:   blog
tags :      [css、margin]
description: 负边距有什么作用？负边距能产生什么效果？利用这些效果我们能做什么？就让我们一起进行探索吧。
---


##1. 负边距能产生什么效果

margin（外边距）：是标签和标签之间的空白，通俗的讲就是边框与其他元素的距离。

	margin:10px -20px 30px 40px;

当目标元素有周围有兄弟元素时，就是与兄弟元素之间的距离，没有兄弟元素就是与父元素的之间的距离。如下代码所示：

<a class="jsbin-embed" href="http://jsbin.com/xecugaxumo/1/embed?html,css,output">JS Bin on jsbin.com</a>

如果将 margin 改为负值会怎么样呢？可以通过修改 jsbin 的代码查看结果：

	.target {
	  background: #0f0;
	  margin: -10px;
	}

**具体的效果可以总结如下**

1. 对于 left/top 负边距，会将目标元素向对应的方向偏移，并会覆盖在偏移方向的元素。
2. 对于 right/bottom 负边距，会将它随后的元素移动到目标元素上，如果是兄弟元素则会覆盖目标元素，如果是父元素则父元素会被目标元素覆盖。

下面再看一段比较特殊的代码：

<a class="jsbin-embed" href="http://jsbin.com/ruxoku/embed?html,css,output">JS Bin on jsbin.com</a>

上面的效果可以总结以下第三条结论：

3. 当子元素为块级元素，并且不设置宽度。若给子元素设置负边距，子元素为了保持与父元素之间的距离，只能将自己的宽度增大。

通过以上三条结论，就可以开始神奇的负边距之旅了。

##2. 去除列表右边距

<a class="jsbin-embed" href="http://jsbin.com/jelona/embed?html,css,output">JS Bin on jsbin.com</a>

**剖析：**

wrap 元素的宽度为 460px，4个 li 元素需要 100*4 + 20*4 = 480px,才能在一行排列。 我们使用了第三条结论，给 ul 增加了负 20px 的右边距，ul的宽度就增加了 20px, 4个li元素就刚好能在一行显示。

##3. 去除最后表格最后一行的 border-bottom

<a class="jsbin-embed" href="http://jsbin.com/vomuhe/embed?html,css,output">JS Bin on jsbin.com</a>

**剖析：**

这里应用了结论二，并且使用 overflow:hidden 把超出父元素的部分隐藏了。 

##4. 负边距自适应布局

<a class="jsbin-embed" href="http://jsbin.com/gufisa/embed?html,css,output">JS Bin on jsbin.com</a>

**剖析**

这里是用了结论二，给 content 设置了负的右边距，其随后的 side 元素就覆盖到了content 元素上，为了让 content 里面的内容保持可见，对 main 设置了padding-left。


> 如果想了解更多可以查看参考文档中的内容。

##5. 参考文档

[The Definitive Guide to Using Negative Margins](http://www.smashingmagazine.com/2009/07/the-definitive-guide-to-using-negative-margins/)

[负值之美：负值在页面布局中的应用](http://www.topcss.org/?p=94)

[CSS布局奇淫巧计之-强大的负边距](http://www.cnblogs.com/2050/archive/2012/08/13/2636467.html)


<script src="http://static.jsbin.com/js/embed.min.js?3.34.1"></script>





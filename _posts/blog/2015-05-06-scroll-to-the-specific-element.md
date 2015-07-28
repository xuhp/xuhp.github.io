---
layout: post
title: 如何滚动实现文档中的某个元素可见
category: blog
tags : [js]
description: 在项目中我们经常会碰到这样的问题：form表单验证，如果表单数据很多（超过一屏），校验时就需要定位到报错元素的位置。这时我们就需要滚动实现文档中的错误元素可见。
---

##1. 问题来源

在项目中我们经常会碰到这样的问题：form表单验证，如果表单数据很多（超过一屏），校验时就需要定位到报错元素的位置。这时我们就需要滚动实现文档中的错误元素可见。

##2. 背景知识介绍

当讨论元素的位置时，必须弄清楚所使用的坐标是文档坐标还是视口坐标。（视口坐标有时候也叫做窗口坐标）

如果文档比视口要小，或者说它还未出现滚动，则文档的左上角就是视口的左上角，文档和视口坐标系统是同一个。

文档坐标比视口坐标更加基础，并且在用户滚动时它们不会发生变化。

**getBoundingClientRect()：不需要参数，返回一个有left、right、top、bottom属性的对象。left和top属性表示元素左上角的X和Y坐标，right和bottom属性表示元素的右下角的X和Y坐标。

getBoundingClientRect()方法名中的“Client”是一种间接指代，它就是Web浏览器客户端 —— 专指它定义的窗口或视口。

##3. 解决思路

###3.1 迂回策略

利用getBoundingClientRect()得到元素的视口坐标，并转换为文档坐标，然后用scrollTo方法达到目的。

**如何将视口坐标转换为文档坐标？**

为了在坐标系统之间互相转换，我们需要判定浏览器窗口的滚动条的位置。

pageXOffset和pageYOffset支持IE9+，scrollLeft和scrollTop在所有浏览器中都支持。
	
	// 以一个对象的x和y属性的方式返回滚动条的偏移量
	function getScrollOffsets(w){
		// 使用指定的窗口，如果不带参数则使用当前窗口
		w = w || window;
		
		// 除了IE 8及更早版本以外，其他的浏览器都支持
		if(w.pageXOffset != null){
			return {
				x: w.pageXOffset,
				y: w.pageYOffset
			};
		}
		
		// 对标准模式下的IE（或任意浏览器）
		var d = w.document;
		if(document.compatMode == 'CSS1Compat'){
			return {
				x: d.documentElement.scrollLeft,
				y: d.documentElement.scrollTop
			}
		}
		
		//在怪异模式下
		return {
			x: d.body.scrollLeft,
			y: d.body.scrollTop
		};
	}



###3.2 使用scrollIntoView()方法直接定位

兼容IE5.5及以上浏览器

	element.scrollIntoView()

##4. 参考文章

《JavaScript权威指南》 第15章 脚本化文档




















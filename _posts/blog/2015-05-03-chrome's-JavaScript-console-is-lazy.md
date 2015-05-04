---
layout:     post
title:      JavaScript console "惰性"求值
category:   blog
tags :      [ js, 调试]
description: 今天使用console调试代码时，碰到了一个很有趣的问题，我们就暂且称它为 console“惰性”求值 问题。下面就让我们一起看看它到底什么。
---

今天使用console调试代码时，碰到了一个很有趣的问题，我们就暂且称它为 console“惰性”求值 问题。下面就让我们一起看看它到底什么。

> 以下案例均在**chrome 41.0.2272.118 m**中演示。

##1. 问题呈现

	var o = {
		age:25,
		name:'xuhp',
		score:{
			chinese:100,
			english:90
		}
	}
	o.name = 'xuhp2';
	console.log(o);
	o.score.math = 100;
	console.log(o);

此时在控制台中呈现：

	> Object {age: 25, name: "xuhp", score: Object}
	> Object {age: 25, name: "xuhp2", score: Object}

这并没有什么问题，当点击展开第一条数据之后数据是这样的：

	{
		age:25,
		name:"xuhp",
		score:{
			chinese:100,
			english:90
			math:100
		}
	}

我们发现在score中居然会有**math:100**这条数据，这到底是怎么回事？

##2. 原因分析

在查阅了相关资料之后得到了一个比较合理的解释：

1. console.log()传入的参数如果指向一个对象，它记录下的是这个对象的引用。
2. 当你查看输出结果时，才会读取这个对象，把相关属性和值显示出来

o.name能正常显示是因为一输出时就被读取到了，此时name的值还未改变。而当展开第一条数据时，score中已经添加了math,所以我们能读取到它。

我可以做如下测试来验证以上解释是否正确：

	var o = {
		age:25,
		name:'xuhp',
		score:{
			chinese:100,
			english:90
		}
	}
	console.log(o);
	setTimeout(function(){
		o.name = 'xuhp2';
		o.score.math = 100;
		console.log(o);
	},5000)

在第二条数据输出之前展开第一条数据，score中并没有math:100这条数据，可见console的结果确实是异步输出的。

这个“功能特性”的好处在于对正在运行的程序性能影响小；坏处是对调试造成一些不必要的麻烦。

##3. 解决方案

解决思路是输出一个复制的对象，当对象被修改之后被复制的对象是不会改变的。具体解决问题的方法有如下两种：

> 更多的解决方案其实就是研究对象的复制问题

###3.1 JSON.stringify和JSON.parse

	console.log(JSON.parse(JOSN.stringify(o)));

JSON.stringify：将 JavaScript 值转换为 JavaScript 对象表示法 (Json) 字符串。

JSON.parse: 将 JavaScript 对象表示法 (JSON) 字符串转换为对象。

> JSON.stringify和JSON.parse支持ie8+，对于不支持这两个方法的浏览器可以引入json2.js。

###3.2 使用 object_copy 函数深层复制对象

	function object_copy(o){
		var cache = {};
		for(var key in o){
			if(typeof(o[key]) == 'object'){
				cache[key] = object_copy(o[key]);
			}else{
				cache[key] = o[key];
			}
		}
		return cache;
	}

如下输出：

	console.log(object_copy(o));

这里有递归操作，如果页面里有大量这样的调试的话，可能会内存溢出或者堆栈溢出。

##4. 参考文章

[Is Chrome's JavaScript console lazy about evaluating arrays?](http://stackoverflow.com/questions/4057440/is-chromes-javascript-console-lazy-about-evaluating-arrays)

[alert 和 console.log 的结果不同？](http://www.zhihu.com/question/20507212)

[用深拷贝解决console.log的中对象的调试问题](http://iwebcode.iteye.com/blog/1791131)



















---
layout: post
title: bootstrap插件之前加 "+" 是什么意思？
category: blog
tags : [js]
description: 在阅读 bootstrap 插件时发现每个插件的的前面都会有一个 "+" 号 —— +function ($) {}(jQuery)， 那么这个加号有什么作用呢？如果没有加号会怎么样？是否有其他的写法？
---

## 1. 如果没有加号会怎样

在阅读 bootstrap 插件时发现每个插件的的前面都会有一个 "+" 号 —— +function ($) {}(jQuery)，为什么要加这个加号，如果将加号去掉会怎么样？比如下面的代码：

	function demo(){ alert(1) }()  // Unexpected token

这是一个函数声明，直接调用就会报错。

这里涉及了函数声明和函数表达式的概念。

## 2. 函数声明、函数表达式
 
定义函数有以下三种方式：

1. 函数声明     (Function Declaration)
2. 函数表达式   (Function Expression)
3. 通过调用new  Function 返回

###2.1. 函数声明
	
	add(3,4);

	function add(a, b){
		return a + b;
	}

1. 如果函数中没有返回值则默认返回 undefined
2. 函数声明会在预执行阶段解析，所以一个函数可以再代码的任何地方声明

###2.2. 函数表达式

	var fun = function(name){
		alert(name);
	}
	fun('xuhp')

####2.3. 'function' 关键字什么时候用作 表达式，什么时候又用作 声明？

当js解析器看到function出现在 main code flow ，function被认为是声明。

当 function 作为语句(statement)的一部分出现的，都会是表达式。

> 在function前面添加 + 是将函数声明转化为函数表达式的一种方式。

##3. 如何将函数声明转换为函数表达式

如何将函数声明转换为函数表达式，就是如何让 js 解析器将 funcition 当做语句的一部分。

在function前面加一元运算符

	!function(){alert('1')}()        // true
	+function(){alert('1')}()        // NaN
	-function(){alert('1')}()        // NaN
	~function(){alert('1')}()        // -1

在function前面加关键字

	void function(){alert('1')}()        // undefined  
	new function(){alert('1')}()        // Object  
	delete function(){alert('1')}()        // true  

使用括号

	(function(){alert('1')})()        // undefined
	(function(){alert('1')}())        // undefined

##4. 参考文章

[为什么function a(b){alert(b)}(1) 不会报错](http://segmentfault.com/q/1010000003028413)

[函数：声明和表达式](http://www.cnblogs.com/yuzhongwusan/archive/2012/01/30/2331693.html)

[javascript里function之前加上感叹号 ' ! ' 会怎么样？](http://segmentfault.com/q/1010000000117476)

[从function前面的!想到的](http://www.cnblogs.com/yichengbo/p/3794515.html)

[function与感叹号](http://swordair.com/function-and-exclamation-mark/)
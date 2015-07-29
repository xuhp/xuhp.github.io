---
layout:     post
title:      jQuery事件命名空间
category:   blog
tags :      [js、jQuery、event]
description: 最近在看 bootstrap 插件源码 ，看到了很多像下面这样的代码 $(document).on('click.bs.alert.data-api', dismiss, Alert.prototype.close) ，突然发现原来 jQuery 竟然是有事件命名空间的。那么事件为什么需要命名空间呢？ jQuery事件的命名空间是怎么实现的呢？
---

## 为什么事件需要命名空间

在jQuery中可以对同一个元素绑定多个事件侦听器，如下所示：

	$(element).on('click', fun1)
	$(element).on('click', fun2)

当单击element元素时会同时触发fun1， fun2 两个事件侦听器，这是jQuery的一个便利的地方，不像原生 js 中的 onclick 新的侦听器会覆盖旧的。

如果想解绑 fun1 侦听器，保留 fun2 侦听器该怎么办？

	$(element).off('click');

> 上面的代码会把所有的 click 事件侦听器都解绑。

那么如何用命名空间解决如上的问题呢？首页改写绑定的代码：

	$(element).on('click.namespace1', fun1);
	$(element).on('click.namespace2', fun2);

这是就可以用下面的代码进行解绑了：

	$(element).off('click.namespace1');

## jQuery 事件命名空间是如何实现的

源码还未看明白，等看明白了在添加。

## 参考文档

[jQuery 事件的命名空间](http://segmentfault.com/a/1190000000339421)





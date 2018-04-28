---
layout: post
title: 【JavaScript】JS中异步开发遇到的问题
date: 2017-07-04
categories: [程序开发]
description: JS中异步开发起因与我在程序开发过程中遇到的问题梳理、总结。
keywords: JavaScript, 同步异步
---

JS实际上是单线程的，其异步无非是通过CPU信号间隔间切换任务实现的。

如今在JS中做异步开发已经是习以为常的事了，在ES6标准确立之前，就已经有国内外众多JS异步框架，当然基本上都是基于 `Promise A` 规范开发的。

在网上JS异步相关的文章太多了，我就不在这里讲述了，此文就当作本人在使用JS异步开发过程中的记录。

# JS异步的几种方式

这里只做总结列举，具体请移步[Javascript异步编程的4种方法][js-asnyc-4-types]

* 回调函数
* 事件监听
* 发布/订阅
* Promises对象
* Generator(*)／next/yield(ES6 语法)
* Async/await(ES7 语法)


# 参考

* [JavaScript 异步进化史](http://div.io/topic/1802)
* [Javascript异步编程的4种方法][js-asnyc-4-types]
* [JavaScript：彻底理解同步、异步和事件循环(Event Loop)](https://segmentfault.com/a/1190000004322358)
* [JavaScript 异步编程学习笔记](https://github.com/riskers/blog/issues/22)
* [探索Javascript异步编程](http://web.jobbole.com/82291/)
* [Promise 语法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)
* [JavaScript Promise启示录](http://www.csdn.net/article/2014-05-28/2819979-JavaScript-Promise)
* [https://promisesaplus.com/](https://promisesaplus.com/)
* [Promises/A+规范](http://www.ituring.com.cn/article/66566)



[js-asnyc-4-types]:http://www.ruanyifeng.com/blog/2012/12/asynchronous＿javascript.html

---
layout: post
title: TypeScript + ThinkJS开发
date: 2017-06-26
categories: [程序开发]
description: 主要讲一下使用TS开发ThinkJS过程中遇到的一些问题
keywords: ThinkJS, TypeScript
---


本文作为开发日志，记录在使用TS+ThinkJS开发过程中遇到问题。

# 为什么要采用TypeScript + ThinkJS

* TypeScript
    做前端开发的都知道[TypeScript](http://www.typescriptlang.org)，它是微软C#之父开发的一款前端语言，它是JavaScript的一个超类，相对JavaScript，TypeScript在语法方面更为严谨，对于入门或非精通JavaScript的开发者来说是更好的选择，它可以在语法层面避免很多不必要的错误。
* ThinkJS
    [ThinkJS](http://thinkjs.org)是360奇舞团开发的一款前端框架，它主要是基于[ThinkPHP](http://www.thinkphp.cn)思想改造而来，目前版本为2.2.19，据官方报道会在6月底发布测试版，7月发布正式版，目前在Github中已经可以看到[3.0](https://github.com/thinkjs/thinkjs/tree/3.0)版本分支了。
    为什么要选择ThinkJS，ThinkJS跟流行的Express、KOA、Egg.JS一样都是标准的mvc框架，与之不同的是，ThinkJS在框架层面为你做了更多，所以你可以将更多的精力分配在业务、逻辑处理，而不必过多的关心数据库连接、模型Curd、路由、页面渲染等方面的工作。

# 遇到的问题

使用ThinkJS开发不是第一次了，但采用TypeScript+ThinkJS开发，这是首次，当然也是不例外的出现了很多问题，本着程序员的精神，我们最后还是逐个的将问题消化了。

* 扩展JavaScript原生对象方法
    因为对TypeScript不熟悉，所以在开发中会遇到很多低级错误，扩展JavaScript对象方法就是其中一个。正因为JavaScript弱类型语言的灵活性，我们通常在JavaScript中写程序都很随意，而TypeScript则需要对每一个对象、方法、类型都需要事先定义，犹豫我们没有对原生对象需要扩展的方法进行定义，导致程序报错，以至于整个项目无法运行。
    > 需要注意的是：TypeScript中扩展对象（包括JavaScript原生），都需要在 `*.d.ts` 文件中进行事先定义，然后再做实现。
* REST接口的定义
    ThinkJS本身是支持Rest开发的，但需要继承 `think.controller.rest` 类，根据我们使用后的感受而言，目前版本的ThinkJS对Rest的支持力度不是很强，路径参数也只有一个固定的 `id` ，无法做到自定义，更别提多个、多级自定义参数了。
    虽然对自定义参数的支持不够，但是对多级路由的解析支持还是挺到位的。
* 数据库操作
    对于数据库的操作，ThinkJS的支持还是挺到位的，这点还是很欣慰。在定义好元数据模型后，Controller层可以很轻松的对数据库模型进行操作，在操作过程中ThinkJS会自动识别并链接数据库。CURD操作也提供了相应的方法，操作起来也很方便，一个简单的方法调用即可实现。
* 关联关系绑定？
    该问题目前还在解决过程中，通过测试发现，在多级关联关系中，ThinkJS无法自动加载到子对象中。

# 参考资料



---
layout: post
title: NodeJS输出乱码问题
date: 2017-07-13
categories: [程序开发]
description: NodeJS从读取文件到输出页面中编码处理问题
keywords: JavaScript, 编码处理
---

![](http://articles.phodal.com/javascript/nodejs.png)

从nodejs后台将中文传给页面显示，不小心就会出现乱码

1. 没有用框架

    直接用 `res.write()` 时，在 `res.writeHead()` 时就 `charset='utf-8'` , 还有一个最容易忽略掉的是：你保存该后台文件，或html文件时，注意选择编码也要为 `‘utf-8’`

2. 使用express框架时

    ```javascript
    在function(req,res){
        res.charset = 'utf-8';
        //默认是‘utf-8’,如果所有文件使用的编码是其他的，在这里就要进行相应设置了
        //比如，所有其他文件用的编码是ascii, 那这里 res.charset = 'ascii';
    }
    ```

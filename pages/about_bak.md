---
layout: page
title: About
description: 程序猿的博客
keywords: ZKer, SPARON, ZhaoKeYong
comments: true
menu: 关于
permalink: /about/
---

仰慕「优雅编码的艺术」。

坚信熟能生巧，努力改变人生。

## 博客

* 主：[blog.zhaokeyong.cn](http://blog.zhaokeyong.cn) 、 [sparon.github.io](http://sparon.github.io)
* 备：[sparon.oschina.io](http://sparon.oschina.io) 、 [sparon.coding.me/blog](http://sparon.coding.me/blog)

## 社交

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}

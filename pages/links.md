---
layout: page
title: Links
description: 没有链接的博客是孤独的
keywords: 友情链接
comments: true
menu: 链接
permalink: /links/
---

> God made relatives. Thank God we can choose our friends.

{% for item in site.data.links %}
{% if item.type %}
## {{ item.type }}
{% for link in item.items %}
1. [{{ link.name }}]({{ link.url }}){:target="_blank"}
{% endfor %}
{% endif %}
{% endfor %}

## 未分类
{% for item in site.data.links %}
{% if item.type %}
{% else %}
1. [{{ item.name }}]({{ item.url }}){:target="_blank"}
{% endif %}
{% endfor %}

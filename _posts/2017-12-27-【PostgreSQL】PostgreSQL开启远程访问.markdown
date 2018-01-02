---
layout: post
title: 【PostgreSQL】PostgreSQL开启远程访问
date: 2017-12-27
categories: 环境
description: PostgreSQL开启远程访问
---


- 修改 `postgresql.conf` 文件配置

	```shell
	listen_addresses = '*'
	```

- 修改 `pg_ha.conf` 文件配置

	```shell
	host    all             all             0.0.0.0/0               password
	```

- 重启服务

	```shell
	systemctl restart postgresql.service
	```

- 添加防火墙过滤

	```shell
	# 添加	--permanent永久生效，没有此参数重启后失效
	firewall-cmd --zone=public --add-port=5432/tcp --permanent
	# 重新载入
	firewall-cmd --reload
	# 查看
	firewall-cmd --zone= public --query-port=5432/tcp
	```

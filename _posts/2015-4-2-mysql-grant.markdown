---
layout: post
title:  "MySQL Create and Grant"
date:   2015-4-2 14:07:32
categories: 技术
tags: MySQL
---
> MySQL 创建DB并授权

## 创建：

	CREATE DATABASE XXX CHARACTER SET utf8

## 授权：

	GRANT ALL PRIVILEGES ON XXX.* TO 'USER'@'localhost' IDENTIFIED BY 'my_password';

	GRANT ALL PRIVILEGES ON *.* TO 'USER'@'localhost' IDENTIFIED BY 'my_password';

## 取消授权：
	REVOKE ALL PRIVILEGES ON XXX.* From 'USER'@'localhost' IDENTIFIED BY 'my_password';

### 授权或者取消授权之后
	flush privileges

## 查看用户的权限：

	show grants for username

## 修改bind-address

	在my.conf 文件中将bind-address = 127.0.0.1改为bind-address = 0.0.0.0即可

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

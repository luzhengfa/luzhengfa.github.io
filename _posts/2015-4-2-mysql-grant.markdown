---
layout: post
title:  "MySQL Grant"
date:   2015-4-2 14:07:32
categories: 技术
tags: MySQL
---
> MySQL 授权

## 授权：
	
	GRANT ALL PRIVILEGES ON redmine.* TO 'redmine'@'localhost' IDENTIFIED BY 'my_password';

	GRANT ALL PRIVILEGES ON *.* TO 'redmine'@'localhost' IDENTIFIED BY 'my_password';

## 取消授权：
	REVOKE ALL PRIVILEGES ON redmine.* From 'redmine'@'localhost' IDENTIFIED BY 'my_password';

## 查看用户的权限：
	
	show grants for username
## 修改bind-address

在my.conf 文件中将bind-address = 127.0.0.1改为bind-address = 0.0.0.0即可

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

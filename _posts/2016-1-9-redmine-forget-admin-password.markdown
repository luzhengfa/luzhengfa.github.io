---
layout: post
title:  "Redmine reset admin password with DB admin"
date:   2016-1-9 16:26:49
categories: redmine
---
> Redmine 忘记admin密码，通过数据库来重置

## 登陆mysql

	mysql -u root -p

## 重置

	UPDATE users SET hashed_password='353e8061f2befecb6818ba0c034c632fb0bcae1b' WHERE login='admin';
	UPDATE users SET salt='' WHERE login='admin';
	exit

## 原理
	在/app/models/user.rb中，密码的加密方式为：SHA1\(salt + SHA1)
	而：
	sah1(password)=0bd181063899c9239016320b50d3e896693a96df
	sha1(0bd181063899c9239016320b50d3e896693a96df)=353e8061f2befecb6818ba0c034c632fb0bcae1b
	所以能通过以上方式重置

## Reference
	http://www.redmine.org/projects/redmine/wiki/FAQ#Reset-password-lost-without-admin-redmine-account-but-with-admin-redmine-database-account

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

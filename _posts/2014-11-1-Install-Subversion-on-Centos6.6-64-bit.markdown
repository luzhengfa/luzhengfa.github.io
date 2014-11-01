---
layout: post
title:  "Install subversion on Centos 6.6-64 bit"
date:   2014-11-1 17:02:18
categories: redmine subversion
---

> 本次安装不介绍防火墙，SELinux等的配置！ 安装Subversion 和Apache

## 安装Subversion
	# yum install mod_dav_svn subversion

这一过程会自动安装Apache

### 设置Apache开机自动启动
	# chkconfig httpd on

## 创建用户
	htpasswd -cm /etc/svn-auth-conf yourusername

根据提示输入密码！这次创建第一个用户时的命令，其中密码将会以MD5的方式加密，存储在文件中

### 再次添加用户
	htpasswd -m /etc/svn-auth-conf anotherusername

## 设置版本库
	cd /var/www/   (或者其他目录)
	mkdir svn
	cd svn
	svnadmin create repositories
	chown -R apache.apache repositories
	service httpd restart

## 设置访问控制清单
创建 /etc/svn-acl-config 文件，如：

	[:/]
	admin = rw

表示前面创建的admin用户对根目录下的版本库都可以读写。
其他设置如

	[版本库名称:版本库路径]
	用户 = 访问权

当中访问权可以是 r（只读）、rw（读写）、或空白（禁止访问）。缺省的 ACL 是禁止用户访问版本载。假设你有一个名叫 framework 的版本库，而你想给 john 只读的权限，及 joe 读写的权限。你可以加入下面这个分段

	[framework:/]
	john =  r
	joe = rw

也可以在名叫 groups 的分段内置立群组，然后在访问控制清单内将 @ 符号放在群组前面。例如：

	[groups]
	staff = joe, george
	[framework:/]
	john =  r
	@staff = rw

如果你想令所有用户能阅读每个版本库，你可以为每个版本库的根目录加入以下一个分段：

	[/]
	* = r

## 分配版本库
	|-- project1
	|   |-- branches
	|   |-- tags
	|   |-- trunk
	
建立如上的目录结构并导入

	cd /tmp
	mkdir project1
	cd project1
	mkdir branches
	mkdir tags
	mkdir trunk
	svn import /tmp/project1/ file:///var/www/svn/repositories/project1 -m "Initial repository layout for mytestproj"

如果需要有初始的文件，可以再project1及其子目录下创建

## 在Apache中配置svn
	# vi /etc/httpd/conf.d/subversion.conf

添加

	<Location /svn>
			DAV svn
			SVNPath /var/www/svn/repositories
			AuthzSVNAccessFile /etc/svn-acl-conf
			AuthType Basic
			AuthName "Subversion repos"
			AuthUserFile /etc/svn-auth-conf
			Require valid-user
	</Location>

### 重启Apache
	servic httpd restart

## 浏览器中访问
	http://127.0.0.1/svn

> 参考[http://wiki.centos.org/zh/HowTos/Subversion](http://wiki.centos.org/zh/HowTos/Subversion)

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

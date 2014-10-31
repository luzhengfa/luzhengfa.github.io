---
layout: post
title:  "Install Redmine on Centos 6.6-64 bit"
date:   2014-10-31 22:41:39
categories: redmine
---

> 本文安装redmine是完全按照这篇文章[Install Redmine on Centos 6.5 - 64 bit](http://www.redmine.org/projects/redmine/wiki/Install_Redmine_25x_on_Centos_65_complete)安装的，基本就是翻译一下!只是我安装的系统是Centos 6.6 64 bit

## Centos 系统下载
[Download](http://wiki.centos.org/Download)

## 安装依赖的包
	yum -y install nano zip unzip libyaml-devel zlib-devel curl-devel openssl-devel httpd-devel apr-devel apr-util-devel mysql-devel gcc ruby-devel gcc-c++ make postgresql-devel ImageMagick-devel sqlite-devel perl-LDAP mod_perl perl-Digest-SHA

## 安装Mysql和Apache
	yum -y install httpd mysql mysql-server

### 设置Mysql和Apache 开机自动启动
	chkconfig httpd on
	chkconfig mysqld on
	service httpd start
	service mysqld start

### 设置Mysql的root密码
	/usr/bin/mysql_secure_installation

其中

	Set root password? [Y/n] y
	Remove anonymous users? [Y/n] y
	Disallow root login remotely? [Y/n] n
	Remove test database and access to it? [Y/n] y
	Reload privilege tables now? [Y/n] y

## 关闭SELinux
	nano /etc/sysconfig/selinux

![关闭SELinux](/images/2014/11/TurnOffSELinux.png)

## 修改主机名
	nano /etc/hosts

![修改主机名](/images/2014/11/ConfigDomain.png)

## 配置防火墙

### 配置IPV4防火墙
	nano /etc/sysconfig/iptables

![配置防火墙](/images/2014/11/ConfigFirewall.png)

	-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT
	-A INPUT -m state --state NEW -m tcp -p tcp --dport 443 -j ACCEPT

### 配置IPV6防火墙
	nano /etc/sysconfig/ip6tables

在类似配置IPV4防火墙的位置加上

	-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT
	-A INPUT -m state --state NEW -m tcp -p tcp --dport 443 -j ACCEPT

### 重启防火墙并设置开机自动启动
	/etc/init.d/iptables restart
	/etc/init.d/ip6tables restart
	chkconfig iptables on
	chkconfig ip6tables on

### 重启系统
	reboot

## 安装PHP
	yum -y install php php-mysql php-gd php-imap php-ldap php-mbstring php-odbc php-pear php-xml php-xmlrpc php-pecl-apc php-soap

### 重启Apache服务
	service httpd restart

## 安装phpMyAdmin
	rpm --import http://dag.wieers.com/rpm/packages/RPM-GPG-KEY.dag.txt
	yum install http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el6.rf.x86_64.rpm
	yum -y install phpmyadmin

### 设置phpMyAdmin的远程登录
	nano /etc/httpd/conf.d/phpmyadmin.conf

修改

	<Directory "/usr/share/pypmyadmin">
	  Order Deny,Allow
	  Deny from all
	  Allow from 127.0.0.1
	</Directory>

为

	<Directory "/usr/share/pypmyadmin">
	  Order Deny,Allow
	  Deny from all
	  Allow from all
	</Directory>

### 配置phpMyAdmin
	nano /usr/share/phpmyadmin/config.inc.php

修改

	$cfg['Servers'][$i]['auth_type'] = 'cookie';

为

	$cfg['Servers'][$i]['auth_type'] = 'http';

### 重启Apache
	service httpd restart

访问http://your-domain/phpmyadmin,使用root,root_password就可以登陆

## 为phpMyAdmin配置防火墙：

因为80端口将留给redmine使用，所以将8080端口给phpMyAdmin使用
IPV4

	nano /etc/sysconfig/iptables

添加

	-A INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT

IPV6

	nano /etc/sysconfig/ip6tables

添加

	-A INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT

### 重启Iptables
	/etc/init.d/iptables restart
	/etc/init.d/ip6tables restart

### 为phpMyAdmin指定端口
	nano /etc/httpd/conf/httpd.conf

添加

	<VirtualHost *:8080>
    DocumentRoot /usr/share/phpmyadmin/
    ServerName your_domain.com
	</VirtualHost>

同时设置Apache监听8080端口，在Listen 80 的下一行添加

	Listen 8080

### 重启Apache
	service httpd restart

即可通过http://your-domain:8080访问

## 安装Ruby
	\curl -L https://get.rvm.io | bash
	source /etc/profile.d/rvm.sh
	rvm list known
	rvm install 1.9.3

查看安装的版本：

	ruby -v

## 安装Rubygems
	yum -y install rubygems

## 安装Passenger
	gem install passenger
	passenger-install-apache2-module

### 为Passenger添加配置文件
	nano /etc/httpd/conf.d/passenger.conf

添加以下部分

	LoadModule passenger_module /usr/local/rvm/gems/ruby-1.9.3-p545/gems/passenger-4.0.37/buildout/apache2/mod_passenger.so
	<IfModule mod_passenger.c>
	   PassengerRoot /usr/local/rvm/gems/ruby-1.9.3-p545/gems/passenger-4.0.37
	   PassengerDefaultRuby /usr/local/rvm/gems/ruby-1.9.3-p545/wrappers/ruby
	</IfModule>

### 重启Apache服务
	service httpd restart

## 创建Redmine数据库
	mysql --user=root --password=root_password_mysql
	create database redmine_db character set utf8;
	create user 'redmine_admin'@'localhost' identified by 'your_new_password';
	grant all privileges on redmine_db.* to 'redmine_admin'@'localhost';
	quit;

## 安装Redmine
	cd /var/www
	wget http://www.redmine.org/releases/redmine-2.5.0.tar.gz
	tar xvfz redmine-2.5.0.tar.gz
	mv redmine-2.5.0 redmine
	rm -rf redmine-2.5.0.tar.gz

### 配置redmine数据库
	cd /var/www/redmine/config
	cp database.yml.example database.yml
	nano database.yml

![配置redmine数据库](/images/2014/11/ConfigRedmineDatabase.png)

## 安装 Rails
	cd /var/www/redmine
	gem install bundler
	bundle install

安装完成之后，启动redmine

	rake generate_secret_token
	RAILS_ENV=production rake db:migrate
	RAILS_ENV=production rake redmine:load_default_data

### 激活FCGI
	cd /var/www/redmine/public
	mkdir plugin_assets
	cp dispatch.fcgi.example dispatch.fcgi
	cp htaccess.fcgi.example .htaccess

### 配置Apache和HastCGI
	cd /var/www/
	rpm --import https://fedoraproject.org/static/0608B895.txt
	wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
	rpm -ivh epel-release-6-8.noarch.rpm
	yum -y install mod_fcgid
	rm -rf epel-release-6-8.noarch.rpm

### 创建redmine文件目录
	mkdir -p /opt/redmine/files
	chown -R apache:apache /opt/redmine
	cd /var/www/redmine/config
	cp configuration.yml.example configuration.yml
	nano configuration.yml

设置

	attachments_storage_path: /opt/redmine/files

### 配置redmine的Email
	nano /var/www/redmine/config/configuration.yml

使用Centos的默认SendMail

	email_delivery:
		delivery_method: :sendmail

使用 Gmail

	email_delivery:
	   delivery_method: :smtp
	   smtp_settings:
    	    enable_starttls_auto: true
        	address: "smtp.gmail.com" 
       		port: 587
        	domain: "smtp.gmail.com" 
        	authentication: :plain
        	user_name: "your_email@gmail.com" 
        	password: "your_password" 

### 配置redmine的端口
	<VirtualHost *:80>
    	    ServerName your_domain
    	    ServerAdmin your_domain@domain.com
        	DocumentRoot /var/www/redmine/public/
        	ErrorLog logs/redmine_error_log
        	<Directory "/var/www/redmine/public/">
            	    Options Indexes ExecCGI FollowSymLinks
            	    Order allow,deny
            	    Allow from all
            	    AllowOverride all
        	</Directory>
	</VirtualHost>

### 启动redmine
	cd /var/www
	chown -R apache:apache redmine
	chmod -R 755 redmine
	service httpd restart

在浏览器输入http://your-domain即可访问

## 安装Subversion
	mkdir -p /opt/repositories/svn
	chown -R apache:apache /opt/repositories/
	chmod 0755 /opt/repositories
	yum install mod_dav_svn subversion subversion-ruby
	mkdir /usr/lib64/perl5/vendor_perl/Apache
	ln -s /var/www/redmine/extra/svn/Redmine.pm /usr/lib64/perl5/vendor_perl/Apache/Redmine.pm

重启redmine，在管理员>配置>版本库下即可看到安装成功

### 配置subversion的访问
	nano /etc/httpd/conf.d/subversion.conf

添加

	PerlLoadModule Apache::Redmine
	<Location /svn>
    	    DAV svn
        	SVNParentPath "/opt/repositories/svn" 
        	SVNListParentPath on
        	Order deny,allow
        	Deny from all
        	Satisfy any
        	LimitXMLRequestBody 0
        	SVNPathAuthz off
        	PerlAccessHandler Apache::Authn::Redmine::access_handler
        	PerlAuthenHandler Apache::Authn::Redmine::authen_handler
        	AuthType Basic
        	AuthName "Subversion Repository" 
        	Require valid-user
        	RedmineDSN "DBI:mysql:database=redmine_db;host=localhost:3306" 
        	RedmineDbUser "redmine_admin" 
        	RedmineDbPass "your_password_database_redmine" 
	</Location> 

到此，配置完毕！ SVN版本库的创建等在新的文章介绍！

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

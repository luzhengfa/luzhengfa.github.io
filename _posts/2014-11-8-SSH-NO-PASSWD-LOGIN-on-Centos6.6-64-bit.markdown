---
layout: post
title:  "centos6.6 SSH 免密码登录"
date:   2014-11-8 21:37:55
categories: 技术
tags: Linux SSH
description: centos6.6 下 SSH 免密码登录配置
---

> 本文主要是介绍centos下ssh免密码登录的配置，是ssh，不是ssh2


## 修改ssh的配置
这个是配置的前提，不然是不可能成功的

	nano /etc/ssh/sshd_config

修改

	# RSAAuthentication yes
	# PubkeyAuthentication yes
	# AuthorizedKeysFile      .ssh/authorized_keys

为

	RSAAuthentication yes
	PubkeyAuthentication yes
	AuthorizedKeysFile      .ssh/authorized_keys

## 配置免密码登录
这里有两个机器（A和B），每个机器有一个hadoop用户.

### 在A机器下生成公钥\私钥对
	[hadoop@A ~]$ ssh -keygen -t rsa -P ''

-P表示密码，-P '' 就表示空密码，也可以不用-P参数，这样就要三车回车，用-P就一次回车
然后再/home/hadoop/.ssh目录下生成id_rsa和id_rsa.pub

### 将公钥（id_rsa.pub）拷贝到B机器

[hadoop@A ~]$ scp /home/hadoop/.ssh/id_rsa.pub hadoop@B:/home/hadoop/id_rsa.pub

这次要输入hadoop的密码

### 在B机器上配置
在B机把从A机复制的id_rsa.pub添加到.ssh/authorzied_keys文件里,如果没有.ssh目录，可以类似在A机器上，执行ssh-keygen命令；如果没有.ssh/authorzied_keys，就新建一个。

	cat id_rsa.pub >> .ssh/authorized_keys 

### 修改authorized_keys的权限
在authorized_keys所在的目录下

	chmod 600 authorized_keys

此时，在A机器上，只需输入ssh xxx.xxx.xxx.xxx(B机器的Ip) 即可免密码登录

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

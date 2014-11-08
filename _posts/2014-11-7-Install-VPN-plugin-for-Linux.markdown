---
layout: post
title:  "Linux下VPN添加不了的解决办法"
date:   2014-11-7 11:06:32
categories: 技术
tags: Linux VPN
description: Linux下VPN添加不了，需要安装插件的解决办法
---

在ubuntu 或者centos下要建立VPN，出现插件没有安装的问题

![No plugin installed](/images/2014/11/centosVPNplugininstall.png)

## 解决办法

### 启用epel resource
	wget http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
	rpm -ivh epel-release-6-8.noarch.rpm

如果用wget 下载不下来或者其他原因，可以在其他机器下载再通过winscp传到centos上

###  Debian / Ubuntu Linux
	$ sudo apt-get install network-manager-openvpn network-manager-pptp network-manager-vpnc

### RHEL / Fedora / CentOS / Scientific Linux / Red Hat Enterprise 
	# yum install NetworkManager-vpnc NetworkManager-pptp NetworkManager-openvpn

安装完成之后，需要重启network-manager

	# /etc/init.d/network-manager restart

## 连接VPN出现VPN service failed to start 解决办法

### 方法一 
就将vpn设置里面—ipv4设置中选择“只自动获取（vpn）地址"
再在dns服务器中填入opendns的地址即：208.67.222.222 或 8.8.8.8 或 8.8.8.4
dns就是域名转换服务器，免费dns有很多替代品，比如google也有免费dns服务器地址等。

### 方法二
将vpn设置里面勾选“MPPE”，同时去掉“MSCHAP”，然后去掉"所有用户可用"

## 参考资料
[Gnome Network Manager VPN Tab Disabled ( Greyed out )](http://www.cyberciti.biz/faq/deiban-ubuntu-linux-networkmanager-pptp-cisco-vpn-tab-disabled/)
[ubuntu VPN service failed to start 解决方案](http://blog.csdn.net/h3139597/article/details/7362578)
[How to add NetworkManager plugin for VPN on CentOs 6](http://www.lampnode.com/linux/how-to-add-networkmanager-plugin-for-vpn-on-centos-6/)

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

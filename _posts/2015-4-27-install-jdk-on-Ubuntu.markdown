---
layout: post
title:  "Install jdk on ubuntu"
date:   2015-4-27 15:32:00
categories: 技术
tags: jdk
---
> Install jdk on ubuntu  


## 下载jdk

	wget -c http://download.oracle.com/otn-pub/java/jdk/7/jdk-7-linux-i586.tar.gz  

其他版本的下载地址[http://www.oracle.com/technetwork/java/archive-139210.html](http://www.oracle.com/technetwork/java/archive-139210.html)

## 解压安装

	sudo mkdir /usr/lib/jvm
	sudo tar zxvf jdk-7u5-linux-x64.tar.gz -C /usr/lib/jvm 

## 修改环境变量

	sudo gedit /etc/profile 
	添加：
	#set java environment
	export JAVA_HOME=/usr/lib/jvm/java-7-sun  
	export JRE_HOME=${JAVA_HOME}/jre  
	export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib  
	export PATH=${JAVA_HOME}/bin:$PATH  

## 配置默认JDK版本

	sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/java-7-sun/bin/java 300  
	sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/java-7-sun/bin/javac 300  
	sudo update-alternatives --config java  
	系统会列出各种JDK版本，如下所示：
	sudo update-alternatives --config java  
	
	有 3 个候选项可用于替换 java (提供 /usr/bin/java)。  
  
  
	选择       路径                                    优先级  状态  
	------------------------------------------------------------  
	* 0            /usr/lib/jvm/java-6-openjdk/jre/bin/java   1061      自动模式  
	1            /usr/lib/jvm/java-6-openjdk/jre/bin/java   1061      手动模式  
	2            /usr/lib/jvm/java-6-sun/jre/bin/java       63        手动模式  
	3            /usr/lib/jvm/java-7-sun/bin/java           300       手动模式  

要维持当前值[*]请按回车键，或者键入选择的编号：3  
update-alternatives: 使用 /usr/lib/jvm/java-7-sun/bin/java 来提供 /usr/bin/java (java)，于 手动模式 中。  
#
# 测试
	
	java -version
	输出如下则成功：
	java version "1.7.0"
	Java(TM) SE Runtime Environment (build 1.7.0-b147)
	Java HotSpot(TM) Client VM (build 21.0-b17, mixed mode)

### 参考资料[http://blog.csdn.net/microfhu/article/details/7667393](http://blog.csdn.net/microfhu/article/details/7667393)

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

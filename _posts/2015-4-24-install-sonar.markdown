---
layout: post
title:  "Install sonar"
date:   2015-4-24 15:11:33
categories: 技术
tags: sonar
---
> Install sonar on ubuntu  

## 安装包下载 
[download](http://www.sonarqube.org/downloads/)

## 安装MySQL
安装完mysql之后新建数据库：sonar

## 修改sonar安装包下的conf文件夹下的sonar.properties文件，如：
	sonar.jdbc.username=sonarqube
	sonar.jdbc.password=mypassword
	sonar.jdbc.url=jdbc:mysql://localhost:3306/sonar?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true

完成以上即可启动简单的sonar,在bin/\linux-x86-64目录下执行
	
	sudo ./sonar.sh start

#### 以下不做修改也可以使用

     默认是端口是9000，可以改为如下
	sonar.web.host=0.0.0.0
	sonar.web.port=80
	sonar.web.context=/sonar

修改Web Server

	sonar.web.javaOpts=-server

### 修改使用的jvm

修改conf文件夹下的wrapper.conf 文件

	wrapper.java.command=/path/to/my/jdk/bin/java

### 配置开机自动启动

创建文件 /etc/init.d/sonar，输入以下内容
	
	#!/bin/sh
	#
	# rc file for SonarQube
	#	
	# chkconfig: 345 96 10
	# description: SonarQube system (www.sonarsource.org)
	#
	### BEGIN INIT INFO
	# Provides: sonar
	# Required-Start: $network
	# Required-Stop: $network
	# Default-Start: 2 3 4 5
	# Default-Stop: 0 1 6
	# Short-Description: SonarQube system (www.sonarsource.org)
	# Description: SonarQube system (www.sonarsource.org)
	### END INIT INFO
	
	/usr/bin/sonar $*
 
#### 添加开机自动启动（X64）

	sudo ln -s $SONAR_HOME/bin/linux-x86-64/sonar.sh /usr/bin/sonar
	sudo chmod 755 /etc/init.d/sonar
	sudo update-rc.d sonar defaults

# 安装sonar-runner
[download](http://repo1.maven.org/maven2/org/codehaus/sonar/runner/sonar-runner-dist/2.4/sonar-runner-dist-2.4.zip)
解压之后修改数据库连接

	sonar.jdbc.url=jdbc:mysql://localhost:3306/sonar?useUnicode=true&amp;characterEncoding=utf8
	sonar.jdbc.username=sonar
	sonar.jdbc.password=sonar

添加环境变量

	$ vim /etc/profile
	PATH="$PATH:/home/ubuntu/sonar/sonar-runner-2.4/bin/"
	export PATH

使环境变量生效

	$ source /etcprofile

测试安装是否成功

	sonar-runner -h 

输出如下则成功

	usage: sonar-runner [options]
	Options:
 	-D,--define <arg>     Define property
             -e,--errors           Produce execution error messages
             -h,--help             Display help information
             -v,--version          Display version information
             -X,--debug            Produce execution debug output

## 使用example项目分析 

[download](https://github.com/SonarSource/sonar-examples/zipball/master)
解压之后直接在目录projects/languages/java/code-coverage/combined ut-it/combined-ut-it-sonar-runner-jacoco 下运行sonar-runner分析，项目下已有配置文件sonar-project.properties
或以下目录
 /projects/languages/java/code-coverage/it/it-jacoco-sonar-runner；
 /projects/languages/java/sonar-runner/java-sonar-runner-simple

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

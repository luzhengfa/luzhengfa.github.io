---
layout: post
title:  "windows 安装jekyll"
date:   2015-11-1 00:25:43
categories: 技术
tags: jekyll
---

### on ubuntu
- 安装ruby
 apt-get install ruby1.9.1-dev
- 安装rubygem
 从http://rubygems.org/pages/download下载，手动安装
- 安装jekyll
 gem install jekyll
- 安装nodejs
 apt-get install nodejs

### on windows:
- ruby,devkit : http://rubyinstaller.org/downloads/ 
- 在devkit目录下，分别执行 ruby dk.rb init;ruby dk.rb install
- gem install jekyll -version=2.5.1
- gem install wdm

### Reference:
- http://jekyll-windows.juthilo.com/
- http://www.madhur.co.in/blog/2011/09/01/runningjekyllwindows.html
 

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

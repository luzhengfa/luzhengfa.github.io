---
layout: post
title:  "gem修改使用淘宝源"
date:   2015-7-1 23:11:33
categories: 技术
tags: ruby
---
> gem 修改默认源，改为使用淘宝源

## 操作
	gem sources -l  # 查看现使用的源
	gem sources --remove http://rubygems.org/ #删除现在使用的源
	gem sources -a http://ruby.taobao.org/ #使用淘宝源

## 如果是使用Bundle，修改Gemfile,将source改为如下：
	source 'http://ruby.taobao.org/'

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

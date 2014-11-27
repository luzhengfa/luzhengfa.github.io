---
layout: post
title:  "redmine install with apache ProxyPass "
date:   2014-11-26 23:00:44
categories: 技术
tags: redmine
---
> 安装redmine+apache+thin

在使用Apache的 ProxyPass时，在httpd.conf中会写上

	ProxyPass        /redmine http://127.0.0.1:3000/redmine
	ProxyPassReverse /redmine http://127.0.0.1:3000/redmine

## 启动redmine
	bundle exec thin -e production -a localhost -p 3000 --prefix /redmine start

注意到--prefix 后面写上了/redmine
在environment.rb文件中的“RedmineApp::Application.initialize!”后面要写上
Redmine::Utils::relative_url_root = "/redmine" ，即：

	# Initialize the rails application
	RedmineApp::Application.initialize!
	Redmine::Utils::relative_url_root = "/redmine" 

不然会出现js等找不到！

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

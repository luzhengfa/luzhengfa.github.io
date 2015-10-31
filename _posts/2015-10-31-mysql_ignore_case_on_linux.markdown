---
layout: post
title:  "Linux 下 MySql 忽略大小写"
date:   2015-10-31 23:31:22
categories: MYSQL
---

### on windows
> mysql 数据库默认忽略大小写

### on linux
> mysql  默认是识别大小写

当把window下的mysql 迁移到linux下时，需要修改linux下mysql的配置文件

在 /etc/my.conf 文件中的[mysqld] 这一节下面加上
			 lower_case_table_names=1
然后重启mysql 即可

其中：
lower_case_table_names = 0 表示区分大小写
lower_case_table_names = 1 忽略大小写

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
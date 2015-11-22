---
layout: post
title:  "windows 10 修改远程桌面端口 "
date:   2015-11-22 20:42:09
categories: 技术
tags: 技术
---

1. regedit
2. 进入HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\ Wds\rdpwd\Tds\tcp修改PortNumber
3. 进入HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp修改PortNumber
4. 修改防火墙
 

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

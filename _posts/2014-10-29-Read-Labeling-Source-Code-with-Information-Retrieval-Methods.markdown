---
layout: post
title:  "阅读论文-Labeling Source Code with Information Retrieval Methods"
date:   2014-10-29 12:45:20
categories: 学术
tags: Source Code Label
description: 阅读Labeling Source Code with Information Retrieval Methods.pdf的总结
---
论文链接[Labeling Source Code with Information Retrieval Methods](http://link.springer.com/article/10.1007/s10664-013-9285-5)

本文是一个实证研究验证从源代码中萃取的标签对软件开发人员理解源代码是否有意义

### 这篇文章主要研究三个问题：

1.LDA,LSI,VSM等自动标记源代码技术标记的结果与开发人员手动标记源代码的结果相似的范围；

2.软件开发人员标记源代码主要使用的是哪些术语；

3.哪些因素影响自动标记源代码技术的准确率

### 研究方法：

研究人员从JHotDraw和wXVantage这两个软件系统中选取20个类来做两个实验，同时参与实验的开发人员有38人，包括本科生和研究生。然后将自动标记技术标记的结果与开发人员标记的结果进行比较。

### 研究结果：

1.从类的标识和类的注释中萃取的标签与开发人员标记的相似度更高；

2.开发人员主要是用类的和方法的名称以及标识源代码；

3.简单的启发式学习方法的标记效果与类的大小和注释长度无关；
  对于大的类和有大量注释的类LSI和LDA的标记效果更好；

### 学习到的：

对LDA等算法没有基本了解，对实验结果分析的理解有一定的困难！

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

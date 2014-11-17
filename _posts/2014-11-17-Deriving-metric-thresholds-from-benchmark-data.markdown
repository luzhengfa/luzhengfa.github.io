---
layout: post
title:  "阅读论文-Deriving metric thresholds from benchmark data"
date:   2014-11-17 17:43:42
categories: 学术
tags: SoftwareQuality
description: 阅读Deriving metric thresholds from benchmark data.pdf的总结
---
论文链接[Deriving metric thresholds from benchmark data](http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=5609747&tag=1)

> 本文作者提出了一个新的方法从Benchmark Data中得到度量元的阈值。
该方法考虑了源代码度量的分布和规模，并且能有效应对度量元值或者系统大小中的离群值

## 方法的步骤

1.metrics extraction：从benchmark中提取度量元

2.weight radio calculation：计算系统中每个实体（如method）的权重比

3.entity aggregation：聚集所有实体中每个度量元值的权重，也就是计算一个权重直方图

4.system aggregation:根据系统的数量归一化权重，然后聚集所有系统的权重

5.weight radio aggregation：即计算一个密度函数，x轴代表权重比（0-100%），y轴代表度量元值

6.thresholds derivation:通过选择需要表示的所有代码中的百分比来得到阈值

## 文章的创新的

1. 考虑了度量元的统计特性，如规模和分布

2. 用于分析的数据是从benchmark中，而不是从简单的实验

3. 能够有效处理离群值的影响

## 贡献

该方法得到度量元的阈值，表示系统中处于不同度量元值的范围的源码的百分比！指出了源代码中可能存在问题的源码。

度量元的阈值可以用于评价系统在度量元对应的属性上的质量

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

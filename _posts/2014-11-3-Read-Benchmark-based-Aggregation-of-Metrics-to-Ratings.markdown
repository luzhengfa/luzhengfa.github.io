---
layout: post
title:  "阅读论文-Benchmark-based Aggregation of Metrics to Ratings"
date:   2014-11-3 21:28:29
categories: 学术
tags: software quality
description: 阅读 Benchmark-based Aggregation of Metrics to Ratings.pdf的总结
---
论文链接[Benchmark-based Aggregation of Metrics to Ratings](http://wiki.di.uminho.pt/twiki/pub/Personal/Tiago/Publications/alves2011-draft.pdf)

> 本文中，作者主要完成了从源代码度量元到系统评级中第二步评级阈值的计算。

## 本文工作
在本文之前，有作者（I. Heitlager, T. Kuipers, and J. Visser）提出了分两步完成从源代码度量元到系统评级的方法，第一步：从度量元得到源代码的风险概况（risk profiles），
第二步，根据第一步得到的风险概况中每个风险类别所占的比率，以及评级阈值（rating thresholds）对系统进行评级。这一方法使用了两种阈值：度量元阈值（1st-level），评级阈值（2nd-level）。

本文中，作者使用的度量元阈值是论文（Deriving metric thresholds from benchmark data）中的结果。对于评级阈值，作者提出了一种方法，从100个系统中训练出阈值的值。
作者的创新之处在于他从100个系统中训练出第二步所需的评级阈值，相对于其他作者从经验来设定评级阈值，更具有说服力。
作者使用提出的方法对SIG Quality Model 中的所有度量元（unit complexity,unit size,unit interfacing,module inward coupling）进行验证，
得到的结果显示其提出的方法得到好的评级阈值。

## 学习到的
1.要对系统进行评级来评判系统的质量，同时能回溯找到引起系统质量问题的度量元，需要分多步进行，需要建立度量元到系统质量的映射关系，以便能在知道系统质量时找出可能引起系统质量问题的度量元。
2.对软件进行评价时，如果没有可以直接使用的客观数据作为评价标准。可以对多个系统进行训练来提取。

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

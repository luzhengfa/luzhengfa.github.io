---
layout: post
title:  "阅读论文-Quantifying the Analyzability of Software Architectures"
date:   2014-11-9 22:40:05
categories: 学术
tags: SoftwareQuality
description: 阅读Quantifying the Analyzability of Software Architectures.pdf的总结
---
论文链接[Quantifying the Analyzability of Software Architectures](http://www.sig.eu/blobs/Research/Scientific%20publication/2011/QuantifyingTheAnalyzabilityOfSoftwareArchitectures_camera_ready.pdf)

> 本文作者提出了一种新的度量元--"Component Balance"来评价软件体系结构的可分析性

## Component Balance
度量元Component Balance 的定义是将System Breakdown和Component Size Uniformity 两个度量元联合在一起。

### 作者定义了该度量元的需求
1.度量元的值能够对系统的可分析性进行暗示
2.在软件声明周期的各个阶段都能获取该度量元值来评价系统的可分析性
3.该度量元是技术独立的

### 然后作者定义了四个目标来评价该度量元
1.CB能够用于评价系统的可分析性
2.度量元的定义是否合适
3.理解CB的值对评价系统的结构的帮助
4.理解随着时间的推移，CB的值的变化

### 公式： CB(S)=SB(|C|)×CSU(C)

## 实验方法
通过建立一个组件标准库，该库通过抽样方法，选取不同语言编写的系统，也包含了开源和商业的系统来组成，然后让专家将每个系统分解成多个组件，最后观察出一般系统大概会分成几个组件（u），以及一般最多分解为多少个组件（w）,u,w 用于计算SB；
CSU通过使用基尼系数（Gini coefficient）来计算。
文中作者通过多种方式计算CB的值，最后选择CB(S)=SB(|C|)×CSU(C)
作者还通过一个实例来分析该方法在评级系统的可分析性。

## Learn
在对系统质量的某一方面进行评价时，如果还没有合适的度量元来评价，可以考虑提出新的度量元。新的度量元是否与已存在的其他度量元存在关系。如果度量元基于已存在的度量元，那得证明在选择已存在的度量元时，选择的是合适的度量元，同时也要说明度量元的价值。

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

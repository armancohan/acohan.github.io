---
layout: post
title:  "Deep Residual Learning for Image Recognition"
date:   2015-05-12 07:27:43 -0500
categories: paper-notes
---
## [Paper - arXiv](https://arxiv.org/pdf/1512.03385v1.pdf)

Kaiming He, Xiangyu Zhang, Shaoqing Ren, Jian Sun (Microsoft Research)

___

### _Hypothesis / Main methods_:

When deeper networks are able to start converging, the degradation problem occurs: the accuracy gets saturated and degrades rapidly. It is easier to optimize / fine tune the residual effect of each layer on the previous layer. Thus in their architecture, each layer learns the residual to the input.

 <img src="{{ site.url }}/img/he-2015-resnet.png" width="300" align="middle">

 The output is element-wise addition of input `x` to `F(x)`. `F(x)` is the residual.

---
layout: post
title:  "Document Classification by Combining Convolution and Recurrent Layers"
date:   2016-05-12 07:27:43 -0500
categories: paper-notes
---
## [Paper - arXiv](http://arxiv.org/pdf/1602.00367.pdf)

### _Hypothesis_

- CNNs need to be very deep to be able to capture long term dependencies. Using RNN along-side CNN, one can capture long dependencies with significantly less number of parameters.

### _Interesting methods_

- They Add a recurrent layer on top of the conv later. Their model is character level.

Architecture:

![architecture]({{ site.url }}/img/xiao2016efficient.png "Model architecture")

- Details
  + Motivation: CNN can learn to extract higher-level features that are invariant to local translation. By stacking multiple convolutional layers, the network can extract higher-level, abstract, (locally) translation invariant features from the input sequence.
  + The recurrent layer is able to capture long-term dependencies even when there is only a single layer.

### _Results_

  * Compare their model with [Zhang et al. (2015)](https://papers.nips.cc/paper/5782-character-level-convolutional-networks-for-text-classification.pdf) and achive slightly better results.

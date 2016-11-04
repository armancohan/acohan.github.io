---
layout: post
title:  "Learning Semantically Coherent and Reusable Kernels in Convolution Neural Nets for Sentence Classification"
date:   2016-08-12 12:30:34 -0500
categories: paper-notes
---
### [Paper - arXiv](https://arxiv.org/pdf/1608.00466v1.pdf)

#### Lakshmana, et al (MSR India)

#### _Hypothesis_

- CNNs (model by Kim (2014)) do not learn kernels that are semantically coherent (having similar meanings). Propose a method for learning semantically coherent kernels and visualizing them.

#### _Interesting methods_
- A two step approach:
 + Group k-grams into desired number of clusters.
 + Associate a filter with each cluster as a weighted combination for Word2Vec representations of the k-grams that are members of that cluster (learn the weights).
- Details
  + Clustering: Using concatenations of Word2Vec and SentiwordNet  (2 dimentional vectors for positive and negative words) and compute eculidean distances between them for clustering.
  + Study the reusability of learned Kernels

#### _Results_
  * Achieve results close to Kim (2014)

---
layout: post
title:  "Convolutional Neural Network Architectures for Matching Natural Language Sentences"
date:   2015-02-01 17:48:53 -0400
categories: paper-notes
---
### Published at NIPS 2015 - [arXiv](https://arxiv.org/pdf/1503.03244v1.pdf)

#### Baotian Hu, et al

#### _Hypothesis_

Convolutional architechtures can help in matching natural language sentences (e.g. question and answer pairs).

#### _Interesting methods_

- They present two architectures. In first one they basically train two convnets on the source and target sentence and they compare the final sentence embeddings with consine.

- The disadvantage of the first model is that it does not take into account the interactions of the source and target sentences. Their second architecture addresses that by training the convnet on all possible segment concatentations of the source and destination sentences.
Convolution is done on the following:

$$ z_{i,j} = [x_{i:i+k-1}, y_{j:j+k-1}] $$

 Where x and y are the source and destination sentences and k is the length of the convolution. Then 2D max pooling for window of 2x2 is performed:

$$ z_{i,j}^{(2)} = \max(z_{2i-1, 2j-1}^{(1)}, z_{2i, 2j-1}^{(1)}, z_{2i-1, 2j}^{(1)}, z_{2i, 2j}^{(1)}) $$

![max-pooling]({{ site.url }}/img/hu2016-maxpool.png)

 Then 2D-convolution on the output of previous layer is performed. The 2D comes from aligning segment i and j of the source and target sentences. Then max pooling and this continues.

- objective function is similar to max margin:

$$ e(x, y^+, y^-; \Theta) = \max(0, 1+s(x,y^-)-s(x,y^+)) $$

 where they assume that the training dataset contains triples of (x,y+,y-), and s(x,y) is predicted matching score for (x,y), and \Phi includes all parameters for the convolution and fully connected layers.



#### _Other notes_
- Using padding in convolutions. Modify the convolution layer by adding a component that returns zero when the input is all zero:

$$ z_i^{(\ell, f)} \stackrel{def}{=} z_i^{(\ell,f)}(x) = g(\hat{z}_i^{(\ell-1)}).\sigma(w^{(\ell,f)}\hat{z}_i^{(\ell-1)} + b^{(\ell, f)}) $$

 where g(v) = 0 i fall the elements in vector v equals 0, otherwise g(v) = 1. This creates a natural hierarchy of all-zero padding

#### _Experiments_

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; All done on huge datasets.

 1. Matching second part of a clause with its first part (3M pairs).
 2. Matching responses to tweets (300K)
 3. MSRP Paraphrase dataset (4076 samples) -- did not get state-of-the-art results in this task. Reason is the size of the dataset

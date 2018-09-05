---
layout: post
title:  "Learned in Translation: Contextualized Word Vectors"
date:   2018-07-30 14:29:34 -0500
categories: paper-notes
---
#### [Paper-pdf](https://arxiv.org/pdf/1708.00107.pdf)
Authors: Bryan McCann, James Bradbury, Caiming Xiong, Richard Socher (Salesforce)

#### _Hypothesis_

Adding context vectors learned from an MT task can improve performance over using only unsupervised word and charachter vectors on a variety of NLP tasks.

#### _Model_

- Use an MT LSTM English-German model to encode the words and get a contextual representation.
- The hidden states of the encoder in the MT model are basically called the CoVe (context ) vectors.

_Classification_:  

Use a biAttentive classification network along with CoVe vectors.

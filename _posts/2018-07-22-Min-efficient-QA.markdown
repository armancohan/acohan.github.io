---
layout: post
title:  "Efficient and robust question answering from minimal context over documents"
date:   2018-07-23 11:29:34 -0500
categories: paper-notes
---
#### [Paper-pdf](https://arxiv.org/pdf/1805.08092.pdf)
Authors: Sewon Min Victor Zhong, Richard Socher, Caiming Xiong (Salesforce) -- ACL 2018

#### _Hypothesis_

- Successful neural QA models build codependent representation of the document and question.
- Learning the full context over the document is challenging and inefficient
- They are prone to errors given adverserial inputs
- The authors present a QA systems that is scalable to large documents. They do so using a sentence selector module that selects a few sentences that are relevant to the query. They also show on the SQuAD-Adverserial dataset that their method is more rebust compared to the previous methods.

#### _Model_

- The authors conduct human analysis and observe that 88% of the examples in TriviaQA are answerable given the full document and out of those, 95% are answerable using 1 or two sentences.
- The proposed model consists of a sentence selector and a QA model
- The sentence selector scores each sentence with respect to the query.

_Encoder_:  
First the encoder computes:  
$D$: sentence embeddings  
$Q$: question embedding  
$D^q$: question-aware sentence embeddings  
$D_i^q = \sum(\alpha_{i,j}Q_j) $  # $D_i$ is the hidden state of the $i_{th}$ word in the sentence embedding
$\alpha_i = \mathrm{softmax}(D_iW_1Q) $

$D^{enc} = RNN([D_i;D_i^q])$

_Decoder_:  
Computes the score for the sentence by calculating bilinear similarities between sentence encodings and question encodings.

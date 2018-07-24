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
$Q^{enc} = RNN([Q_u])$

_Decoder_:  
Computes the score for the sentence by calculating bilinear similarities between sentence encodings and question encodings.

To get a single hidden representation of the question they use a weighted sum according to the following:  

$\beta = \mathrm{softmax}(w^T Q_{enc})$    &nbsp;&nbsp;&nbsp;&nbsp;                 # weights for each query word hidden state  
$q^{enc} = \sum(\beta_j Q_j)$              &nbsp;&nbsp;&nbsp;&nbsp;                 # A hidden layer size vector representing the query  
$h_i = D^{enc}_i W_2 q^{enc}$              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;           # how similar each sentence is to the query  
$\tilde{h} = \max{h_1, ..., h_L}$          &nbsp;&nbsp;&nbsp;&nbsp;                 # the most similar sentence  
$\mathrm{score} = W_3^T h$ where $W_3 \in R^{h \times 2}$ &nbsp;&nbsp;&nbsp;&nbsp;  # each dimension in `score` means that the question is answerable or non-answerable given the sentence  

#### _Weaknesses_

- The modeling contribution does not seem to be strong enough for a full paper. Basically, the main contribution seems to be just adding a sentence selector module and using a previous q/a model.
- A simple TF-IDF model works very close to the proposed sentence selection component. It is not clear why the speedups of TF-IDF sentence selection is very similar to the proposed sentence selector. TF-IDF is completely unsupervised and must be much faster than the proposed model.

---
layout: post
title:  "A Deep Reinforced Model for Abstractive Summarization"
date:   2017-07-28 11:29:34 -0500
categories: paper-notes
---
### [Paper-pdf](https://arxiv.org/pdf/1705.04304.pdf)

Romain Paulus, Caiming Xiong and Richard Socher (Salesforce), arxiv

published date: 2017-05-11

### _Summary_

Using intra-decoder attention, pointer-generator hybrid, and reinforcement learning for document summarization.

### _Interesting methods_

#### Notations

- input: $x=\\{x_1,...,x_n\\}$, sequence of article tokens
- output: $y=\\{y_1,...,y_n'\\}$, sequence of summary tokens
- hidden states of encoder: $h_i^e=\\{RNN^{e-fw}_i \|\| RNN^{e-bw}_i\\}$
- decoder: $RNN^d$ computes hidden states $h_t^d$ from embedding vectors of $y_t$

#### Attention over input

- Following the standard attention mechanism in seq2seq models
- (bilinear) dot product attention between the query and the inputs, calculates the attention score of the hidden input state $h_i^e$ at decoding step $t$

\begin{align}
e_{ti}=f(h_t^d,h_i^e)={h_t^d}^T W_{attn}^e h_i^e
\end{align}

- normalized attention scores are computed with softmax:

\begin{align}
\alpha_{ti}^e = \frac{\exp\\{e_{ti}\\}}{ \sum_j \exp\\{e{tj}\\}}, \; c_t^e=\sum_{i=1}^n \alpha_{ti}^e h_i^e
\end{align}

#### Decoder attention

- Incorporate information about previously decoded sequences into the decoder to avoid repeating the same information.

- For decoding step $t$, the model computes a new decoder context vector $c_t^d$.

\begin{align}
e_{tt'}^d = {h_t^d}^T W_{attn}^d h_{t'}^d
\end{align}

\begin{align}
\alpha_{tt'}^d = \frac{\exp(e_{tt'}^d)}{\sum_{j=1}^{t-1} \exp(e_{tj}^d)}, \; c_t^d=\sum_{j=1}^{t-1} \alpha_{tj}^d h_j^d
\end{align}

#### Token generation and pointer

- Following work in MT, they add a switch to the decoder to decide to either generate a token or point to a word in the source at each time step.
- Token generation: $p(y_t \| u_t = 0) = \mathrm{softmax}\big{(} W_{out} \big[h_t^d \|\| c_t^e \|\| c_t^d \big] + b_{out} \big{)}$
- Pointer: $p(y_t=x_i \| u_t=1) = \alpha_{ti}^e$, i.e. temporal attention weights
- Probability of using copy mechanism: $\sigma\big(W_u \big[h_t^d \|\| c_t^e \|\| c_t^d \big] \big)$
- final probability distribution for output token $y_t$: $p(y_t) = p(u_t=1)p(y_t \| u_t=1) + p(u_t=0)p(y_t \| u_t=0)$

#### Sharing decoder weights

- To make the model converge faster, they share the output weights with embedding learned weights:
$W_{out} = tanh(W_{emb}W_{proj})$

#### Avoiding repetition at test time

- Use a heuristic: no 3-gram should be repeated (based on an observation in the training data)

#### Training

- Use reinforcement learning for training the model (details will be added here later)

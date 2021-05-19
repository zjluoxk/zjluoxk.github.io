---
layout: post
title:      "NLP For Numbers"
date:       2021-05-19 07:01:36 +0000
permalink:  nlp_for_numbers
---


Source:
https://www.aclweb.org/anthology/D19-1534.pdf
Do NLP Models Know Numbers? Probing Numeracy in Embeddings
by Eric Wallace, Yizhong Wang, Sunjian Li, Sameer Singh, Matt Gardener from Allen Insitute for Artificial Intelligence, Peking University, and University of California, Irvine

So we in the DS course are familiar with NLP used to predict sentiments, such as Tweets after humans has label emotions associate with it. But can we NLP for numbers? If so, how good is it?

Turns out, sometimes pretty okay, but mostly not very good. For the above paper, the arthors explored Word2Vec, GloVe, ELMo, BERT, Char-CNN and Char-LSTM to identify numbers.

In the below graph, the arthors train different algorithms to identify numbers between -500 and +500. For the range trained, depends on which algorithms, they variable between bad, okay, and good.
![](https://d3i71xaburhd42.cloudfront.net/0427110f0e79f41e69a8eb00a3ec8868bac26a4f/1-Figure1-1.png)

However, as soon as it gets out of the untrained range, all the algorithms failed. So therefore, it may not be a good idea to mix numbers in a text for numerical reasoning.


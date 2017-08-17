---

layout: post
title:  Medical Text Classification using CNN

---

__Tl;dr : This paper presents usage of CNNs to classify clinical text at a sentence level. This approach outperforms traditional NLP methods (Sentence Embeddings, Mean Word Embeddings and Word Embedding with BOW) by at least15 %.__

### Summary:

The authors claim the purpose of writing this paper is to "apply machine learning approaches to build models that allow an automatically generated context-based and rich representation of health related information”. Their justification of using CNNs is their ability to learn complex feature representations. 

NOTE:  A good visualisation of this ability is Mattew Zeiler’s paper on [Visualisation and Understanding Convolutional Networks](https://arxiv.org/pdf/1311.2901.pdf)

### Methods: 

Two different models are used and compared - the first one was training a Word2Vec model on a large corpus of medical text and the second one was the sentence classifier — which was trained on pre-classified medical documents.

From the paper,

>Merck Manual dataset contains articles from various topics like Brain, Cancer, etc. Each of these articles is classified under a parent header representing a specific category of medical issues and conditions. In total our dataset consisted of 26 medical categories and 4000 sentences were chosen at random for each category extracted from the Merck articles to use as our training data and to ensure balance across all categories. Our validation dataset consisted of 1000 sentences from each of the categories

Each sentence is converted to a word level matrix which is extracted from the Word2Vec model. Since, CNNs require static sized inputs, the sentence length is limited to 50 words. In case of more or less words, appropriate adjustments are made.

The architecture of the CNN is as follows: (the hyper parameters were chosen after a grid search)




### Evaluation

The results of the CNN based approach was compared with the following models -

* Sentence Embeddings (_Log R + _Doc2Vec_)
* Mean Word Embeddings (_ZeroMean/ElimMean + Word2Vec_)
* Word Embeddings with BOW features (_BOW + LogR_)

The results are as follows:



### Summary:

The authors show that it is possible to use CNNs to represent the semantics of clinical text enabling semantic classification at a sentence level. The model outperforms classical NLP approaches due to its ability to learn optimal features during the training phase to represent the semantics of the sentence being analysed.








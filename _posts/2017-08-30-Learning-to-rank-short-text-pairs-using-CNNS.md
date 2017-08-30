---

title: Learning to rank short text pairs using deep CNNs
layout: post

---

### Tl;dr: This paper presents a CNN architecture for reranking pairs of short texts - in particular, the task of reranking short text pairs where elements of the pair are sentences.


## Link to paper: 

[Learning to Rank Short Text Pairs with Convolutional Deep Neural Networks](https://pdfs.semanticscholar.org/73d8/26d4c2363701b88e3e234fe3b8756c0f9671.pdf)

## Introduction:

Traditional reranking approaches require complex lexical, syntactic and semantic features.
Also, the choice of representations and features is a completelyempirical process, driven by the intuition, experience and
domain expertise. It is also shown to be computationally expensive and requires a number of tools. So, the authors have tried
to use deep learning methods to perform the task. 

From the paper,

> Recently, it has been shown that the problem of semantic text
matching can be efficiently tackled using distributional word matching,
where a large number of lexical semantic resources are used for
matching questions with a candidate answer.

> ... In particular, it has been recently shown that convolutional neural networks are able
to efficiently learn to embed input sentences into low-dimensional
vector space preserving important syntactic and semantic aspects of
the input sentence, which leads to state-of-the-art results in many
NLP tasks.

___

### Architecture of the model:

From the paper,

> Its main building blocks are two distributional sentence
models based on convolutional neural networks (ConvNets). These
underlying sentence models work in parallel mapping queries and
documents to their distributional vectors, which are then used to
learn the semantic similarity between them.

#### Sentence model:

Similar to the model published [by Y.Kim](http://www.aclweb.org/anthology/D14-1181), 
the input to the sentence model is a sentence treated as a sequence of words.

For each sentence, a sentence matrix is built where each column \\( i \\) represents a word embedding \\( w\_{i} \\) at the corresponding position \\( i \\) in a sentence.

From the paper,

>To learn to capture and compose features of individual words in a
given sentence from low-level word embeddings into higher level
semantic concepts, the neural network applies a series of transformations
to the input sentence matrix S using convolution, nonlinearity
and pooling operations.

![The sentence matrix](http://i.imgur.com/IFgZOyR.png)

#### CNN architecture:

![The CNN model](http://i.imgur.com/b6XY9Fw.png)

*Convolution feature maps:*

>The convolution filter is also a matrix of weights. 
The convolution filter is of the same dimensionality as the input sentence
matrix. As shown in Fig. 1, it slides along the column dimension
of S producing a vector c in output. Each component
\\( c\_{i} \\) is the result of computing an element-wise product between a
column slice of S and the filter matrix F, which is then flattened
and summed producing a single value.

*Activation units:*

To allow the model to learn non-linear boundaries, each
convolutional layer is typically followed by a non-linear activation
function \\( \alpha() \\) applied element-wise to the output of the preceding
layer. Common choices include hyperbolic tangent, ReLU or sigmoid.

*Pooling layer:*

The goal of the pooling layer is to aggreggate the information and
reduce the representation. There are a variety of choices in pooling functions -
the most commonly used ones are max pool and average pool.

Max pool is preferred over average pool in most cases, but it also has its drawbacks
as it can overfit on small models leading to poor generalisation. 

Convolutional layer passed through the activation function together with 
pooling layer acts as a non-linear feature extractor.
Given that multiple feature maps are used in parallel to process
the input, deep learning networks are able to build rich feature representations
of the input.

### Architecture for matching text pairs:

The output of the ConvNet models map input sentences to vectors - which can 
be used to map the similarity. These are then used to compute a query-document
similarity score, which together with the query and document vectors 
are joined in a single representation.

*Matching query and documents*:

The similarity between two vectors \\( x\_{q} \\) and \\( x\_{d} \\) is given by: 

  $$ sim(x_{q}, x_{d}) = x_{q}^TMx_{d} $$ 

where M is a similarity matrix. 
  
*Hidden Layer*:

The hidden layer computes the transfomation:
  
  $$ \alpha(w_{h}.x + b) $$
  
  where \\(w\_{h} \\) is the weight vector and \\( \alpha \\) is the non-linearity.
  
*Softmax*
  
The output of the penultimate convolutional and pooling layers
is flattened to a dense vector \\( x \\), which is passed to a fully connected
softmax layer.

*Information flow*:

From the paper,

>The output of our sentence models are distributional
representations of a query \\( x\_{q} \\) and a document \\( x\_{d} \\). These are then
matched using a similarity matrix M. This produces
a single score \\( x\_{sim} \\) capturing various aspects of similarity
(syntactic and semantic) between the input queries and documents.
Note that it is also straight-forward to add additional features \\( x\_{feat} \\)
to the model.

>The join layer concatenates all intermediate vectors, the similarity
score and any additional features into a single vector.

>This vector is then passed through a fully connected hidden layer,
which allows for modelling interactions between the components
of the joined representation vector. Finally, the output of the hidden
layer is further fed to the softmax classification layer, which
generates a distribution over the class labels.

The model is trained to minimise the cross-entropy loss function and
 \\( l\_{2} \\) norm regularization is done to mitigate overfitting. Dropout 
 is also used to prevent overfitting.
 
 





---

layout: post
title: Convolutional Neural Networks

---

### Tl;dr: This



### Link to paper:
___

[An introduction to CNNs](https://arxiv.org/abs/1511.08458v2)

___


### What are Convolutional Neural Networks? 
___

Convolutional Neural Networks (henceforth abbreviated as CNNs) are a type of artificial neural network (ANN). CNNs are primarily
used to solve difficult image-driven pattern recognition tasks with their precise yet simple architecture.

While CNNs are mostly similar to ANNs, the only major difference is that CNNs are primarily used in the field of 
pattern recognition in images. This allows us to encode image specific characteristics in the architecture of the
neural network and thus making the netwok more suitable for image specific tasks.

We may ask why aren't ANNs used for image classification? Why do we need another special class of ANNs?

This is answered in the paper as:

>One of the largest limitations of traditional forms of ANN is that they tend to
struggle with the computational complexity required to compute image data.
Common machine learning benchmarking datasets such as the MNIST database
of handwritten digits are suitable for most forms of ANN, due to its relatively
small image dimensionality of just 28 × 28. With this dataset a single neuron in
the first hidden layer will contain 784 weights (28×28×1 where 1 bare in mind
that MNIST is normalised to just black and white values), which is manageable
for most forms of ANN. If you consider a more substantial coloured image input of 64 × 64, the number
of weights on just a single neuron of the first layer increases substantially to
12, 288. Also take into account that to deal with this scale of input, the network
will also need to be a lot larger than one used to classify colour-normalised
MNIST digits, then you will understand the drawbacks of using such models.

One may say that we could increase the complexity of the network to make recognition better?

There are two reasons why this isn't the best solution:

* We do not have unlimited computational power and large models take more time to train.
* We introduce the possibility of overfitting. 
  * Overfitting is when our models lose the ability to generalise. When we are doing machine learning, we are trying to learn from data that follows
  a specific probability distribution. Due to randomness, the training data _will_ contain some amount of noise
  which is specific to it. When we overfit, we learn from the noise as well - except that this isn't favourable.
  Now when we try to make predictions from the test data, the accuracy goes down as some noise made its way into
  our model which was specific only to the training data. Hence, our model doesn't generalise - it is too specific.
  
 Hence, this is the reason behind reducing the complexity of our ANNs - it reduces chances of overfitting and increases
 the accuracy of our model.
 ___
 
 ### CNN architecture:
 ___
 
 The CNN architecture is set up in a way that it expects the input to be in the form of images. 
 This focuses the architecture to be set up in way to best suit the need for dealing with the specific type of data.
 
 Another key difference between ANNs and CNNs is explained as follows:

>One of the key differences is that the neurons that the layers within the CNN
are comprised of neurons organised into three dimensions, the spatial dimensionality
of the input (height and the width) and the depth. The depth does not
refer to the total number of layers within the ANN, but the third dimension of a
activation volume. Unlike standard ANNS, the neurons within any given layer
will only connect to a small region of the layer preceding it.

>In practice this would mean that for the example given earlier, the input ’volume’
will have a dimensionality of 64 × 64 × 3 (height, width and depth), leading
to a final output layer comprised of a dimensionality of 1 × 1 × n (where
n represents the possible number of classes) as we would have condensed the
full input dimensionality into a smaller volume of class scores filed across the
depth dimension.

#### Overall architecture:

CNNs comprise of mainly three layers:

* Convolutional layers
* Pooling layers
* Fully connected layers

When these layers are stacked, a CNN architecture has been formed.

A simple architecture from the paper for MNIST classification is shown as follows:

![Mnist](http://i.imgur.com/WtHw9io.png)

Let us look at each of these layers in detail:
___

#### Convolutional Layer:
___

The primary purpose of convolution in the context of ConvNets is to extract features from an image.
Convolution preserves the spatial relationship between pixels by learning image features using small squares of input data.

....





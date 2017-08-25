---

layout: post
title: Convolutional Neural Networks

---

### What are Convolutional Neural Networks? 
___

Convolutional Neural Networks (henceforth abbreviated as CNNs) are a type of artificial neural network (ANN). CNNs are primarily
used to solve difficult image-driven pattern recognition tasks with their precise yet simple architecture.

While CNNs are mostly similar to ANNs, the only major difference is that CNNs are primarily used in the field of 
pattern recognition in images. This allows us to encode image specific characteristics in the architecture of the
neural network and thus making the netwok more suitable for image specific tasks.

We may ask why aren't ANNs used for image classification? Why do we need another special class of ANNs?

Quoting from [1],

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
* We introduce the possibility of __overfitting.__ 
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
 
 Another key difference between ANNs and CNNs is explained as follows in [1]:

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

* __Convolutional layers__
* __Pooling layers__
* __Fully connected layers__

When these layers are stacked, a CNN architecture has been formed.

A simple architecture from the paper for MNIST classification is shown as follows:

![Mnist](http://i.imgur.com/WtHw9io.png)

Let us look at each of these layers in detail:
___

#### Convolutional Layer:
___

The primary purpose of convolution in the context of ConvNets is to extract features from an image.
Convolution preserves the spatial relationship between pixels by learning image features using small squares of input data.
We will not go into mathematical details of the convolution operator and look at it's implications in the context of CNNs.

As discussed, images are usuall represented in the form of matrix of pixel values. 

Consider a 5 x 5 matrix as shown below:

![alt](https://ujwlkarn.files.wordpress.com/2016/07/screen-shot-2016-07-24-at-11-25-13-pm.png?w=127&h=115)

Also, consider another matrix which is of size 3 x 3:

![alt](https://ujwlkarn.files.wordpress.com/2016/07/screen-shot-2016-07-24-at-11-25-24-pm.png?w=74&h=64)

Convolution can be depicted as the following operation:

![alt](https://i.stack.imgur.com/9Iu89.gif)

#### What just happened here?

The 3 x 3 matrix slides over the image matrix by 1 pixel (caled as "stride") and in every iteration, element wise multiplication is performed. Afer that, sum of the elements after the product is added to give a single integer output which forms the first element of the output matrix. 

In CNN terminology, the 3×3 matrix is called a ‘filter‘ or ‘kernel’ or ‘feature detector’ and the matrix formed by sliding the filter over the image and computing the dot product is called the ‘Convolved Feature’ or ‘Activation Map’ or the ‘Feature Map‘. The filters acts as feature detectors from the original input image.

A more concrete definition of kernels can be given as:

>An image kernel is a small matrix used to apply effects like the ones you might find in Photoshop or Gimp, such as blurring, sharpening, outlining or embossing. They're also used in machine learning for 'feature extraction', a technique for determining the most important portions of an image. In this context the process is referred to more generally as "convolution"

Depending on the values of the filter, multiple effects such as sharpening, bluring, embossing can be achieved.

Now, the size of the feature map is determined by three hyperparameters which we need to decide before
performing the convolution:

* __Depth:__ Depth corresponds to the number of filters we use for the convolution operation. More is the depth, more 
is the number of feature maps created which can be stacked over each other - leading to better results. However, reducing this hyperparameter can significantly minimise the total number of neurons of the network, but it can also significantly reduce the pattern recognition capabilities of the model.

* __Stride:__ Stride can be defined as the number of pixels by which the filter moves while performing convolution. When the stride is 1 then we move the filters one pixel at a time and similarly for more number of pixels. However, smaller stride
sizes lead to heavy overlapping producing extremely large activations. Alternatively, setting the stride to a
greater number will reduce the amount of overlapping and produce an output of lower spatial dimensions.

* __Zero Padding:__ It is the simple process of padding the border of the input, and is an effective method to give further control as to the dimensionality of the output volumes. A nice feature of zero padding is that it allows us to control the size of the feature maps. Adding zero-padding is also called _wide convolution_, and not using zero-padding would be a _narrow convolution._

Another operation called ReLU is used a lot after convolutional layers.

ReLU stands for Rectified Linear Unit and is defined as f(x) = max(0,x). It is used to turn all the negative inputs into zero. It is applied pixel wiseon the feature map. 

The purpose of ReLU is to introduce non-linearity in our ConvNet, since most of the real-world data we would want our ConvNet to learn would be non-linear (Convolution is a linear operation – element wise matrix multiplication and addition, so we account for non-linearity by introducing a non-linear function like ReLU)

[Further discussion on why ReLU is used.](https://stats.stackexchange.com/questions/126238/what-are-the-advantages-of-relu-over-sigmoid-function-in-deep-neural-networks)

___

#### Pooling layer:
___

After obtaining features using convolution, we would next like to use them for classification. In theory, one could use all the extracted features with a classifier such as a softmax classifier, but this can be computationally challenging.

To solve this problem, we use pooling.

Quoting,

>Pooling layers aim to gradually reduce the dimensionality of the representation,
and thus further reduce the number of parameters and the computational
complexity of the model.

#### How is pooling performed?

Pooling can be of different types depending on the function used - max, mean, sum etc. 

The following image shows how pooling is done over 4 non-overlapping regions of the image:

![alt](http://deeplearning.stanford.edu/wiki/images/0/08/Pooling_schematic.gif)

We can see that the pooled feature has lesser dimensions than the convolved feature. 

The pooled feature can be obtained using max, mean, sum or any other function. CNNs are shown to work well
when max-pool is used (i.e the maximum from the window size is used to create the pooled feature.) However,
CNN architectures may contain general-pooling. General pooling layers are comprised of pooling
neurons that are able to perform a multitude of common operations including
L1/L2-normalisation, and average pooling.

___

#### Fully connected layer:
___

The fully-connected layer contains neurons of which are directly connected to
the neurons in the two adjacent layers, without being connected to any layers
within them. This is analogous to way that neurons are arranged in traditional
forms of ANN.


The Fully Connected layer uses a softmax activation function in the output layer (other classifiers like SVM can also be used). The term “Fully Connected” implies that every neuron in the previous layer is connected to every neuron on the next layer.

The output from the convolutional and pooling layers represent high-level features of the input image. The purpose of the Fully Connected layer is to use these features for classifying the input image into various classes based on the training dataset.
___

### Putting it all together, the Convolution + Pooling layers act as Feature Extractors from the input image while Fully Connected layer acts as a classifier. Different classifiers can be used, but generally softmax is used. 
___


### How to build our ConvNet?
___

Although there is no standard method to build ConvNets, some ideas based on practical evidence can be 
used.

Quoting from [1],

>Despite the relatively small number of layers required to form a CNN, there
is no set way of formulating a CNN architecture. That being said, it would be
idiotic to simply throw a few of layers together and expect it to work. Through
reading of related literature it is obvious that much like other forms of ANNs,
CNNs tend to follow a common architecture. This common architecture is illustrated
in the MNIST ConvNet above, where convolutional layers are stacked, followed by pooling
layers in a repeated manner before feeding forward to fully-connected layers.

>Another common CNN architecture is to stack two convolutional layers before
each pooling layer, as illustrated in Figure 5. This is strongly recommended as
stacking multiple convolutional layers allows for more complex features of the
input vector to be selected.

![img](http://i.imgur.com/7RzHHEZ.png)

Further ideas can be found in the paper mentioned in the source.

___

### Conclusion: 

Convolutional Neural Networks are very similar to ordinary Neural Networks: they are made up of neurons that have learnable weights and biases. Each neuron receives some inputs, performs a dot product and optionally follows it with a non-linearity.

So what does change? ConvNet architectures make the explicit assumption that the inputs are images, which allows us to encode certain properties into the architecture. These then make the forward function more efficient to implement and vastly reduce the amount of parameters in the network.

### Further readinng and sources:

* [1] [The paper by which this post was inspired](https://arxiv.org/pdf/1511.08458v2.pdf)
* [2] [An intuitive explanation for ConvNets - excellent read](https://ujjwalkarn.me/2016/08/11/intuitive-explanation-convnets/)
* [3] [Stanford's Deep Learning Tutorial](http://deeplearning.stanford.edu/wiki/index.php/UFLDL_Tutorial)
* [4] [cs231n: Convoluntional Neural Networks](http://cs231n.github.io/)
* [5] [Image Kernels Visualisation](http://setosa.io/ev/image-kernels/)










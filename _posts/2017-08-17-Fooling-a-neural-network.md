---
layout: post
title: Fooling a neural network
use_math: true
---

With the advent of deep learning in various fields, it becomes equally important to discuss the security and privacy concerns that come with it. It has been shown that neural networks can be easily fooled to misclassify with the help of _adversarial examples_.

### What are adversarial examples?

Let us imagine we need to build a model which takes images as inputs and classifies them into classes. This is a standard image classification problem.

In recent years, convolutional neural networks (CNNs) have done really well in recoginising images - sometimes even beating human accuracy. So, we build a deep learning model which is been pre-trained on the ImageNet model and classifies the images into one of the thousand classes which ImageNet provides. Now, if all goes well, we should be able to provide an input and the model should be able to predict the output with a desired accuracy level. 

However, researchers have found out that the model can be easily made to misclassify by manipulating input examples. These examples which are specifially designed to fool the model into misclassifying are known as _adversarial examples_.

### How do they work?

Not to go into the detail of CNNs work, it can be said that they work by finding features in the images using a series of processes such as convolutions, pooling etc.

However, these features are ultimately learnt from the pixels of the image and we might think that changing a few pixels wouldn't lead to misclassification. 

However, researchers have found out that these input pixels can be manipulated into fooling our model into misclassifying the image.  In a paper published in 2013 called [Intriguing properties of neural networks](https://arxiv.org/abs/1312.6199), researches found out that "we can cause the network to misclassify an image by applying a certain imperceptible perturbation" i.e if we know what pixels to change and how much to change them, we can force the neural network to misclassify our image. 

From Ian Goodfellow's [cleverhans](www.cleverhans.io) blog,

![alt](http://cleverhans.io/assets/adversarial-example.png)

Note that despite being indistinguishable to the human eye, the perturbation is sufficient to change the model’s prediction and misclassify the image. 

Another interesting point is that these hacked images can fool the network, even if they are printed on [paper](https://www.youtube.com/watch?v=zQ_uMenoBCk&feature=youtu.be).

This happens because a machine learning classifier works by finding a dividing line between the things it’s trying to tell apart. This is the fundamental concept behind any classification problem. So, if we can push the boundary to include some examples which do not belong on that side, we have misclassified the object succesfully. 

Quoting from Adam Geitgey's [blog](https://medium.com/@ageitgey),

>In image classification with deep neural networks, each “point” we are classifying is an entire image made up of thousands of pixels. That gives us thousands of possible values that we can tweak to push the point over the decision line. And if we make sure that we tweak the pixels in the image in a way that isn’t too obvious to a human, we can fool the classifier without making the image look manipulated.

So the procedure to trick a neural network can be as follows: 
* Feed in the input.
* Check the neural network’s prediction and see how far off the is __from the answer we want__ to get for this photo.
* Tweak the photo using _backpropagation_ and make the final prediction closer to what we want.
* Repeat the same process thousands of time for __the same photo__ until the network gives us the answer we want.

At end of this, we’ll have an image that fools the neural network without changing anything inside the neural network
itself.

### But doesn't this require the attacker to have knowledge of our model?

As pointed in this paper titled [Practical Black-Box Attacks against Deep Learning Systems using Adversarial Examples.](https://arxiv.org/abs/1602.02697), researchers showed a more practical way by which the attack is possible. 

From the abstract of the paper,

> Potential attacks include having malicious content like malware identified as legitimate or controlling vehicle behavior. Yet, all existing adversarial example attacks require knowledge of either the model internals or its training data. We introduce the first practical demonstration of an attacker controlling a remotely hosted DNN with no such knowledge. Indeed, the only capability of our black-box adversary is to observe labels given by the DNN to chosen inputs.

This can have a lot of malicious applications - ranging from labelling legit mails as spam to crashing self-driving cars. 

### How do we protect our model against such attacks?

The short answer is, there aren't a lot of ways right now.

Quoting Ian Goodfellow again,

>It is now December 2016. At present, we know many different ways of attacking machine learning models, and very few ways of defending.

However, we are not completely helpless and one of the most common methodology to prevent this is _adversarial training._

In adversarial training, a set of machines learn together by pursuing competing goals. For instance, in Generative Adversarial Networks or GANs, a _generator function_ learns to synthesize samples that best resemble some dataset, while a _discriminator function_ learns to distinguish between samples drawn from the dataset and samples synthesized by the generator. From a conceptual perspective, adversarial training is fascinating because it bypasses the need of loss functions in learning, and opens the door to new ways of regularizing (as well as fooling or attacking) learning machines.


### Where to go from here?

This is a relatively new field and you can bring yourself up to date by reading some of the papers published:

* [Practical Black-Box Attacks against Machine Learning](https://arxiv.org/abs/1602.02697)
* [Intriguing properties of neural networks](https://arxiv.org/abs/1312.6199)
* [Adversarial examples in the physical world](https://arxiv.org/abs/1607.02533)

Also, follow the blog [cleverhans](http://www.cleverhans.io/) to stay up to date with the latest developments in the field.






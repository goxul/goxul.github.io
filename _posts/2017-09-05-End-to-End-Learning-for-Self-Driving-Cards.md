---

title: Using CNNs to train self-driving cars
layout: post
---

### Tl;dr: A convolutional neural network (CNN) was trained to map raw pixels from a single front-facing camera directly to steering commands. With minimum training data from humans, the system learns to drive in traffic on local roads with or without lane markings and on highway.
___

### Link to paper:
___
[End To End Learning For Self Driving Cars](https://arxiv.org/abs/1604.07316)
___

### Thoughts:

After reading various comments on this paper, some of the more important ones are:

1. Lane following is only a tiny sub task on the way to automated driving. The driving task tackled here (lane following) has been solved previously, so it isn't completely novel either.


2. More importantly, the approach of mapping input images to steering angles throws away a lot of information embedded in the images which can be used for higher level reasoning and prediction.


3. NNs are difficult to reason about and even more difficult to verify. This is bad when the testability of a system is a hard requirement. 
Real world car manufacturers have found that it's practically impossible to test/verify an end-to-end system. 

4. CNNs are great at vision tasks. However to further automate driving we have to deal with lots of tasks that aren't vision tasks 
and we have to interface with real electronic/mechatronic systems. This is the point where end-to-end NNs run into trouble, while hard coding behavior is relatively simple.

5. On the positives, the idea of how to break down driving activities and train a separate learner for each is really clever, and might let this be integrated into higher-level systems.

6. Despite these problems, Despite this problem, 'lane following', being well solved this pixels-to-motor-torques end-to-end method is a promisingly practical methodology with wide application in robotics.

___


Traditionally, CNNs perform well at tasks related to vision because they can learn features from the data automatically -
contrary to prior methods where the features had to be hand crafted before they were fed into a classifier.

In this paper, the authors describe a CNN that goes beyond pattern recognition. It learns the entire processing
pipeline needed to steer an automobile with data collected from cameras.

However, this isn't exactly new. The authors write:

>The groundwork for this project was done over 10
years ago in a Defense Advanced Research Projects Agency (DARPA) seedling project known as
DARPA Autonomous Vehicle (DAVE) [5] in which a sub-scale radio control (RC) car drove through
a junk-filled alley way. DAVE was trained on hours of human driving in similar, but not identical environments.
The training data included video from two cameras coupled with left and right steering
commands from a human operator.

But, the model had some limitations:

>While DAVE demonstrated the potential of end-to-end learning, and indeed was used to justify
starting the DARPA Learning Applied to Ground Robots (LAGR) program [7], DAVE’s performance
was not sufficiently reliable to provide a full alternative to more modular approaches to off-road
driving. DAVE’s mean distance between crashes was about 20 meters in complex environments

So what has changed in DAVE-2?

> Our work differs in that 25 years of
advances let us apply far more data and computational power to the task. In addition, our experience
with CNNs lets us make use of this powerful technology

___

### Overview of the DAVE-2 System:

![alt](http://i.imgur.com/uIXziqh.png)

>Three cameras are mounted behind the windshield of the data-acquisition car. Time-stamped video
from the cameras is captured simultaneously with the steering angle applied by the human driver.
This steering command is obtained by tapping into the vehicle’s Controller Area Network (CAN)
bus. In order to make our system independent of the car geometry, we represent the steering command
as \( 1/r \) where \( r \) is the turning radius in meters.

The authors mention that training with data from only the human driver is not sufficient. The network must
learn how to recover from mistakes. Otherwise the car will slowly drift off the road. The training
data is therefore augmented with additional images that show the car in different shifts from the
center of the lane and rotations from the direction of the road.

How is the CNN incorporated in this model?

![alt](http://i.imgur.com/wjOKBe9.png)

Images are fed into a CNN which then computes a proposed steering command. The proposed command is compared to the desired
command for that image and the weights of the CNN are adjusted to bring the CNN output closer to
the desired output.

Once trained, the network can generate steering from the video images of a single center camera.

![alt](http://i.imgur.com/2ePRpFA.png)

___

### Data Collection:

>Training data was collected by driving on a wide variety of roads and in a diverse set of lighting
and weather conditions. Most road data was collected in central New Jersey, although highway data
was also collected from Illinois, Michigan, Pennsylvania, and New York. Other road types include
two-lane roads (with and without lane markings), residential roads with parked cars, tunnels, and
unpaved roads. Data was collected in clear, cloudy, foggy, snowy, and rainy weather, both day and
night. In some instances, the sun was low in the sky, resulting in glare reflecting from the road
surface and scattering from the windshield

____

### Network Architecture:

![alt](http://i.imgur.com/8MCsqdD.png)

The network is designed to o minimize the mean squared error between the steering command
output by the network and the command of either the human driver, or the adjusted steering
command for off-center and rotated images.

Details about the network:

>The network consists of 9 layers, including a normalization layer, 5 convolutional layers
and 3 fully connected layers. The input image is split into YUV planes and passed to the network.

>The first layer of the network performs image normalization. The normalizer is hard-coded and is not
adjusted in the learning process

>The convolutional layers were designed to perform feature extraction and were chosen empirically
through a series of experiments that varied layer configurations. We use strided convolutions in the
first three convolutional layers with a 2×2 stride and a 5×5 kernel and a non-strided convolution
with a 3×3 kernel size in the last two convolutional layers.

>We follow the five convolutional layers with three fully connected layers leading to an output control
value which is the inverse turning radius.

___

### Training Details:

#### Data Selection:

>The first step to training a neural network is selecting the frames to use. Our collected data is
labeled with road type, weather condition, and the driver’s activity (staying in a lane, switching
lanes, turning, and so forth). To train a CNN to do lane following we only select data where the
driver was staying in a lane and discard the rest. We then sample that video at 10 FPS

#### Augmentation:

>After selecting the final set of frames we augment the data by adding artificial shifts and rotations
to teach the network how to recover from a poor position or orientation. The magnitude of these
perturbations is chosen randomly from a normal distribution.

___

### Conclusions:

The authors conclude that CNNs are able to learn the entire task of lane and road
following without manual decomposition into road or lane marking detection, semantic abstraction,
path planning, and control.  The CNN is able to learn meaningful road features
from a very sparse training signal (steering alone). A small amount of training data from less than a hundred hours of driving
was sufficient to train the car to operate in diverse conditions, on highways, local and residential
roads in sunny, cloudy, and rainy conditions.







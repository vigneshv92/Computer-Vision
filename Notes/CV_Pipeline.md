## Cognitive and Emotional Intelligence
Cognitive intelligence is the ability to reason and understand the world based on observations and facts. It's often what is measured on academic tests and what's measured to calculate a person's IQ.

Emotional intelligence is the ability to understand and influence human emotion. For example, observing that someone looks sad based on their facial expression, body language, and what you know about them - then acting to comfort them or asking them if they want to talk, etc. For humans, this kind of intelligence allows us to form meaningful connections and build a trustworthy network of friends and family. It's also often thought of as only a human quality and is not yet a part of traditional AI systems.

If you'd like to learn more about Affectiva and emotion AI, check out their [website](http://www.affectiva.com/).

## Computer Vision Pipeline

A computer vision pipeline is a series of steps that most computer vision applications will go through. Many vision applications start off by acquiring images and data, then processing that data, performing some analysis and recognition steps, then finally performing an action. The general pipeline is pictured below!

<img src="/Visual Representations/CV_Pipeline_001.png" align="center"/></p>

<div align="center"><b>General computer vision processing pipeline</b></div>

</br> Now, let's take a look at a specific example of a pipeline applied to facial expression recognition.

<img src="/Visual Representations/CV_Pipeline_002.png" align="center"/></p>

<div align="center"><b>Facial recognition pipeline</b></div>

## Standardizing Data

Pre-processing images is all about standardizing input images so that you can move further along the pipeline and analyze images in the same way. In machine learning tasks, the pre-processing step is often one of the most important.

For example, imagine that you've created a simple algorithm to distinguish between stop signs and other traffic lights.

<img src="/Visual Representations/CV_Pipeline_003.png" align="center"/></p>

<div align="center"><b> Images of traffic signs; a stop sign is on top and a hiking sign is on the bottom </b></div>

</br> If the images are different sizes, or even cropped differently, then this counting tactic will likely fail! So, it's important to pre-process these images so that they are standardized before they move along the pipeline. In the example below, you can see that the images are pre-processed into a standard square size.

The algorithm counts up the number of red pixels in a given image and if there are enough of them, it classifies an image as a stop sign. In this example, we are just extracting a color feature and skipping over selecting an area of interest (we are looking at the whole image). In practice, you'll often see a classification pipeline that looks like this.

<img src="/Visual Representations/CV_Pipeline_004.png" align="center"/></p>

## Training a Neural Network

To train a computer vision neural network, we typically provide sets of labelled images, which we can compare to the predicted output label or recognition measurements. The neural network then monitors any errors it makes (by comparing the correct label to the output label) and corrects for them by modifying how it finds and prioritizes patterns and differences among the image data. Eventually, given enough labelled data, the model should be able to characterize any new, unlabeled, image data it sees!

A training flow is pictured below. This is a convolutional neural network that learns to recognize and distinguish between images of a smile and a smirk.

This is a very high-level view of training a neural network, and we'll be diving more into how this works later on in this course. For now, we are explaining this so that you'll be able to jump into coding a computer vision application soon.

<img src="/Visual Representations/CV_Pipeline_005.png" align="center"/></p>

<div align="center"><b>Example of a convolutional neural network being trained to distinguish between images of a smile and a smirk</b></div>

</br> Gradient descent is a a mathematical way to minimize error in a neural network. More information on this minimization method can be found [here](https://en.wikipedia.org/wiki/Gradient_descent).

Convolutional neural networks are a specific type of neural network that are commonly used in computer vision applications. They learn to recognize patterns among a given set of images. If you want to [learn more](https://ujjwalkarn.me/2016/08/11/intuitive-explanation-convnets/), refer to this resource, and we'll be learning more about these types of networks, and how they work step-by-step, at a different point in this course!

## Machine Learning and Neural Networks

When we talk about machine learning and neural networks used in image classification and pattern recognition, we are really talking about a set of algorithms that can learn to recognize patterns in data and sort that data into groups.

The example we gave earlier was sorting images of facial expressions into two categories: smile or smirk. A neural network might be able to learn to separate these expressions based on their different traits; a neural network can effectively learn how to draw a line that separates two kinds of data based on their unique shapes (the different shapes of the eyes and mouth, in the case of a smile and smirk). Deep neural networks are similar, only they can draw multiple and more complex separation lines in the sand. Deep neural networks layer separation layers on top of one another to separate complex data into groups.

### Separating Data
Say you want to separate two types of image data: images of bikes and of cars. You look at the color of each image and the apparent size of the vehicle in it and plot the data on a graph. Given the following points (pink dots are bikes and blue are cars), how would you choose to separate this data?

<img src="/Visual Representations/CV_Pipeline_006.png" align="center"/></p>

<div align="center"><b>Pink and blue dots representing the size and color of bikes (pink) and cars (blue). The size is on the x-axis and the color on the left axis. Cars tend to be larger than bikes, but both come in a variety of colors.</b></div>

### Layers of Separation

What if the data looked like this?

<img src="/Visual Representations/CV_Pipeline_007.png" align="center"/></p>

<div align="center"><b>Pink (bike) and blue (car) dots on a similar size-color graph. This time, the blue dots are collected in the top right quadrant of the graph, indicating that cars come in a more limited color palette.</b></div>

<img src="/Visual Representations/CV_Pipeline_008.png" align="center"/></p>

<div align="center"><b>Two, slightly-angled lines, each of which divides the data into two groups.</b></div>

</br>

<img src="/Visual Representations/CV_Pipeline_009.png" align="center"/></p>

<div align="center"><b>Both lines, combined, clearly separate the car and bike data!</b></div>

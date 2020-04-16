## Computer Vision Pipeline

A computer vision pipeline is a series of steps that most computer vision applications will go through. Many vision applications start off by acquiring images and data, then processing that data, performing some analysis and recognition steps, then finally performing an action. The general pipeline is pictured below!

<img src="/Visual Representations/CV_Pipeline_001.png" align="center"/></p>

Now, let's take a look at a specific example of a pipeline applied to facial expression recognition.

<img src="/Visual Representations/CV_Pipeline_002.png" align="center"/></p>

## Standardizing Data

Pre-processing images is all about standardizing input images so that you can move further along the pipeline and analyze images in the same way. In machine learning tasks, the pre-processing step is often one of the most important.

For example, imagine that you've created a simple algorithm to distinguish between stop signs and other traffic lights.

<img src="/Visual Representations/CV_Pipeline_003.png" align="center"/></p>

If the images are different sizes, or even cropped differently, then this counting tactic will likely fail! So, it's important to pre-process these images so that they are standardized before they move along the pipeline. In the example below, you can see that the images are pre-processed into a standard square size.

The algorithm counts up the number of red pixels in a given image and if there are enough of them, it classifies an image as a stop sign. In this example, we are just extracting a color feature and skipping over selecting an area of interest (we are looking at the whole image). In practice, you'll often see a classification pipeline that looks like this.

<img src="/Visual Representations/CV_Pipeline_004.png" align="center"/></p>

## Training a Neural Network

To train a computer vision neural network, we typically provide sets of labelled images, which we can compare to the predicted output label or recognition measurements. The neural network then monitors any errors it makes (by comparing the correct label to the output label) and corrects for them by modifying how it finds and prioritizes patterns and differences among the image data. Eventually, given enough labelled data, the model should be able to characterize any new, unlabeled, image data it sees!

A training flow is pictured below. This is a convolutional neural network that learns to recognize and distinguish between images of a smile and a smirk.

This is a very high-level view of training a neural network, and we'll be diving more into how this works later on in this course. For now, we are explaining this so that you'll be able to jump into coding a computer vision application soon.

Gradient descent is a a mathematical way to minimize error in a neural network. More information on this minimization method can be found [here](https://en.wikipedia.org/wiki/Gradient_descent).

Convolutional neural networks are a specific type of neural network that are commonly used in computer vision applications. They learn to recognize patterns among a given set of images. If you want to [learn more](https://ujjwalkarn.me/2016/08/11/intuitive-explanation-convnets/), refer to this resource, and we'll be learning more about these types of networks, and how they work step-by-step, at a different point in this course!

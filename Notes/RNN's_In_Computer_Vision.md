## Recurrent Neural Networks
So far, we've been looking at convolutional neural networks and models that allows us to analyze the spatial information in a given input image. CNN's excel in tasks that rely on finding spatial and visible patterns in training data.

In this and the next couple lessons, we'll be reviewing RNN's or recurrent neural networks. These networks give us a way to incorporate memory into our neural networks, and will be critical in analyzing sequential data. RNN's are most often associated with text processing and text generation because of the way sentences are structured as a sequence of words, but they are also useful in a number of computer vision applications, as well!

## RNN's in Computer Vision
At the end of this lesson, you will be tasked with creating an automatic image captioning model that takes in an image as input and outputs a sequence of words, describing that image. Image captions are used to create accessible content and in a number of other cases where one may want to read about the contents of an image. This model will include a CNN component for finding spatial patterns in the input image and and RNN component that will be responsible for generative descriptive text!

RNN's are also sometimes used to analyze sequences of images; this can be useful in captioning video, as well as video classification, gesture recognition, and object tracking; all of these tasks see as input a sequence of image frames.
Sketch RNN
One of my favorite use cases for RNN's in computer vision tasks is in generating drawings. Sketch RNN (demo here) is a program that learns to complete a drawing, once you give it something (a line or circle, etc.) to start!

Sketch RNN example output. Left, Mona Lisa. Right, pineapple.
It's interesting to think of drawing as a sequential act, but it is! This network takes a starting line or squiggle and then, having trained on a number of types of sketches, does it's best to complete the drawing based on your input squiggle.
Next, you'll learn all about how RNN's are structured and how they can be trained! This section is taught by Ortal, who has a PhD in Computer Engineering and has been a professor and researcher in the fields of applied cryptography and embedded systems.

#### Supporting Materials
[Video classification methods]()

## Recurrent Neural Networks
So far, we've been looking at convolutional neural networks and models that allows us to analyze the spatial information in a given input image. CNN's excel in tasks that rely on finding spatial and visible patterns in training data.

In this and the next couple lessons, we'll be reviewing RNN's or recurrent neural networks. These networks give us a way to incorporate memory into our neural networks, and will be critical in analyzing sequential data. RNN's are most often associated with text processing and text generation because of the way sentences are structured as a sequence of words, but they are also useful in a number of computer vision applications, as well!

### 1. RNN's in Computer Vision
At the end of this lesson, you will be tasked with creating an automatic image captioning model that takes in an image as input and outputs a sequence of words, describing that image. Image captions are used to create accessible content and in a number of other cases where one may want to read about the contents of an image. This model will include a CNN component for finding spatial patterns in the input image and and RNN component that will be responsible for generative descriptive text!

RNN's are also sometimes used to analyze sequences of images; this can be useful in captioning video, as well as video classification, gesture recognition, and object tracking; all of these tasks see as input a sequence of image frames.

#### Sketch RNN
One of my favorite use cases for RNN's in computer vision tasks is in generating drawings.</br>
[Sketch RNN (demo here)](https://magenta.tensorflow.org/assets/sketch_rnn_demo/index.html) is a program that learns to complete a drawing, once you give it something (a line or circle, etc.) to start!

Sketch RNN example output. Left, Mona Lisa. Right, pineapple.

It's interesting to think of drawing as a sequential act, but it is! This network takes a starting line or squiggle and then, having trained on a number of types of sketches, does it's best to complete the drawing based on your input squiggle.
Next, you'll learn all about how RNN's are structured and how they can be trained! This section is taught by Ortal, who has a PhD in Computer Engineering and has been a professor and researcher in the fields of applied cryptography and embedded systems.

##### Supporting Materials
[Video classification methods](https://video.udacity-data.com/topher/2018/May/5af0e03b_video-classification/video-classification.pdf)

### 2. [RNN's Introduction](https://youtu.be/AIQEqg6F38A)

The neural network architectures you've seen so far were trained using the current inputs only. We did not consider previous inputs when generating the current output. In other words, our systems did not have any memory elements. RNNs address this very basic and important issue by using memory (i.e. past inputs to the network) when producing the current output.

In this lesson, we will focus on recurrent neural networks, or what we call in short RNNs. Many applications involve temporal dependencies or dependencies over time. What does that mean? Well, it means our current output depends not only on the current input, but also on past inputs. 

So, if I want to make dinner tonight, let's see, I had pizza yesterday, so maybe I should consider a salad. Essentially, what we will have is a network that is similar to feedforward networks that we've seen before, but with the addition of memory. You may have noticed, that in the applications you've seen before, only the current input mattered. 

For example, classifying a picture, is this a cat? But perhaps this is not a static cat. Maybe when the picture was shot, the cat was moving. From a single image, it may be difficult to determine if it is indeed walking or maybe it's running. Maybe it's just a very talented cat standing in a funny pose with two feet up in the air.

When we observe the cat, frame by frame, we remember what we saw before, so we know if the cat is still or if it's walking. We can also distinguish walking from running, but can the machine do the same? This is where recurrent neural networks or RNNs come in. 

RNNs are artificial neural networks, that can capture temporal dependencies, which are dependencies over time. If you look up the definition of the word recurrent, you will find that it simply means occurring often or repeatedly. 

So, why are these networks called recurrent neural networks? 
> It's simply because with RNNs we perform the same task for each element in the input sequence. In this lesson, we will start with a bit of history. 

It's really interesting to see how this field has evolved. We will remind ourselves what feedforward networks are. You will see that RNNs are based on very similar ideas to those behind feedforward networks. So, once we have a clear understanding of the fundamentals, we can easily understand the next steps.

While focusing on feedforward networks, you will learn about, non-linear function approximation, training using backpropagation, or what we call stochastic gradient descent, and evaluation. All these should be familiar to you. Our main focus of course will be RNNs. I have given you a good example of why we need RNNs. Remember the cat, but there are many other applications, we will focus on those as well. We will look at the simple RNN also known as the Elman network, and learn how to train the network. We will also understand the limitations of simple RNNs, and how they can be overcome by using what we call LSTMs. Don't be alarmed, you don't need to remember all these names right now. We will slowly progress into each concept and talk about all of them in much detail later.

### 3. [RNN's History](https://www.youtube.com/embed/HbxAnYUfRnc)

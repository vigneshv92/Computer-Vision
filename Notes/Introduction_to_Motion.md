## Motion in Computer Vision

### 1. Object Tracking

So far, you've learned a lot about how to extract important information from images and how to use deep learning techniques to recognize patterns in images and identify objects. In this part of the course, we'll focus less on images and more on pattern recognition over time and space. 

We'll talk about different computer vision methods for tracking objects and predicting their movement. In fact, in this lesson, you'll be programming a filter that tracks a robot as it moves and senses its environment over time. This requires having a model of motion and the mathematical way to represent uncertainty in that motion. Finding out where a moving object is located with some certainty at any given time is called localization. 

Localization techniques are used extensively in computer graphics applications that track certain objects and people over time, and localization is used in autonomous vehicles, like in self-driving cars that need to know where they are in the world so that they can safely navigate. Next, let's talk about the specific skills that we'll cover in the next few lessons.

### 2. Localization

We'll start off by talking about representing motion and tracking objects in a video. Then, we'll move onto uncertainty and robotic motion and learn a simple localization technique, the histogram filter, which can account for this uncertainty. Then, you'll learn about motion models and tracking the position of a self-driving car over time.

By the end of this lesson, you'll have all the skills you need to code an implementation of SLAM, which stands for Simultaneous Localization and Mapping. Slam is a technique that allows autonomous vehicles to build up a model of the world while locating itself within that world. So, let's get started.

### 3. [Motion](https://youtu.be/A-QJf04LBb0)

So far we've been looking at a lot of static images and processing them to identify objects and interesting features, and the exact same processing techniques can be used on a video stream. This is because a video stream is just made up of a sequence of image frames. 

One thing we haven't talked about that's unique to these sequences of image frames is the idea of motion. For example, when you're watching a video you can see or envision an object move and to create an intelligent computer vision system, we also want to give computers a way to understand motion.

This is useful in a number of applications. Knowledge about motion is used to isolate moving pedestrians from a still background. It's used in intelligent navigation systems, in movement prediction models, and in distinguishing behaviors like running versus walking in a given video. One way to track objects over time and detect motion is by extracting certain features and observing how they change from one frame to the next. Next we'll learn about one such method called optical flow.

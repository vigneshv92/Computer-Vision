## Compuer Vision Algorithms

### 1. YOLO

Now you've learned about a number of region-based methods for recognizing and locating multiple objects in a scene.
Architectures like faster R-CNN are accurate, but the model itself is quite complex, with multiple outputs that are each a potential source of error.
Once trained they're still not fast enough to run in real time. In this lesson we'll be learning about YOLO which stands for You Only Look Once,
and it's a real-time object detection algorithm, that avoid spending too much time on generating region proposals.
Instead of locating objects perfectly, it prioritizes speed and recognition. 

Let's see an example of YOLO in action.
<img src="/Visual Representations/YOLO_Introduction.png" align="center"/></p>
Consider a self-driving car that sees this image of a street.

It's essential for a self-driving car to be able to detect the location of objects all around it, such as pedestrians cars, and traffic lights. On top of that, this detection has to happen in near real time,
so that the car can safely navigate the street. The card doesn't always need to know what all these objects are? 
It mostly needs to know not to crash into them but it does need to recognize traffic lights bikes and pedestrian to be able to correctly follow the rules of the road.

In this image we've used the YOLO algorithm to locate and classify different objects, there's a bounding box that locates each object and a corresponding class label.
In the next lesson we'll learn the details of how the YOLO algorithm works.

### 2. YOLO Output

When we talked about localization in images, we talked about creating a CNN that could output a predicted class front object in an image and a predicted bounding box for that object. In the CNN examples that we've seen, these outputs are analyzed separately in the network trains by using a weighted combination of classification and regression losses. Another way to process these outputs is by merging them into a single output vector, which is what the yellow algorithm does.

Let's see this in an example.
Let's assume I want to train a CNN to be able to detect three classes, a person, a cat, and a dog.
In this case, because we only have three classes, the output vector y will only have three elements, C one, two, and three.
Each of which is a class score or a probability that the image is of a person, cat, or dog.
If you have more classes, this vector will get longer.

<img src="/Visual Representations/YOLO_Output.png" align="center"/></p>

For this image, we want to train the CNN so that it can identify the person in this image and look at that person within a bounding box. We can do this by adding some box parameters to our output vector. We can add four more numbers, x, y, w and h, that determine the position and size of the bounding box. X and y determine the coordinates of the center of the box,
and w and h determine its width and height.

<img src="/Visual Representations/YOLO_Ouput_Vector.png" align="center"/></p>

Once you've trained your CNN to output class probabilities and bounding box coordinates, you're one step closer to being able to detect objects in any given image.
Next we'll briefly go over the sliding-windows approach that you've seen before with our example output vector in mind.
Then you'll see how yellow improves upon sliding windows and breaks an image into a grid for efficient object detection.

### 3. Sliding Windows

### 4. CNN & Sliding Window

#### A Convolutional Approach to Sliding Windows

Let’s assume we have a 16 x 16 x 3 image, like the one shown below. This means the image has a size of 16 by 16 pixels and has 3 channels, corresponding to RGB.

<img src="/Visual Representations/CNN_Sliding_Window_0.png" align="center"/></p>

Let’s now select a window size of 10 x 10 pixels as shown below:

<img src="/Visual Representations/CNN_Sliding_Window_1.png" align="center"/></p>

If we use a stride of 2 pixels, it will take 16 windows to cover the entire image, as we can see below.

<img src="/Visual Representations/CNN_Sliding_Window_2.png" align="center"/></p>

In the original Sliding Windows approach, each of these 16 windows will have to be passed individually through a CNN. Let’s assume that CNN has the following architecture:

<img src="Visual Representations/CNN_Sliding_Window_4.png" align="center"/></p>

The CNN takes as input a 10 x 10 x 3 image, then it applies 5, 7 x 7 x 3 filters, then it uses a 2 x 2 Max pooling layer, then is has 128, 2 x 2 x 5 filters, then is has 128, 1 x 1 x 128 filters, and finally it has 8, 1 x 1 x 128 filters that represents a softmax output.

What will happen if we change the input of the above CNN from 10 x 10 x 3, to 16 x 16 x 3? The result is shown below:

<img src="Visual Representations/CNN_Sliding_Window_5.png" align="center"/></p>

As we can see, this CNN architecture is the same as the one shown before except that it takes as input a 16 x 16 x 3 image. The sizes of each layer change because the input image is larger, but the same filters as before have been applied.

If we follow the region of the image that corresponds to the first window through this new CNN, we see that the result is the upper-left corner of the last layer (see image above). Similarly, if we follow the section of the image that corresponds to the second window through this new CNN, we see the corresponding result in the last layer:

<img src="Visual Representations/CNN_Sliding_Window_6.png" align="center"/></p>

Likewise, if we follow the section of the image that corresponds to the third window through this new CNN, we see the corresponding result in the last layer, as shown in the image below:

<img src="Visual Representations/CNN_Sliding_Window_7.png" align="center"/></p>

Finally, if we follow the section of the image that corresponds to the fourth window through this new CNN, we see the corresponding result in the last layer, as shown in the image below:

<img src="Visual Representations/CNN_Sliding_Window_8.png" align="center"/></p>

In fact, if we follow all the windows through the CNN we see that all the 16 windows are contained within the last layer of this new CNN. Therefore, passing the 16 windows individually through the old CNN is exactly the same as passing the whole image only once through this new CNN.

<img src="Visual Representations/CNN_Sliding_Window_9.png" align="center"/></p>

This is how you can apply sliding windows with a CNN. This technique makes the whole process much more efficient. However, this technique has a downside: the position of the bounding boxes is not going to be very accurate. The reason is that it is quite unlikely that a given size window and stride will be able to match the objects in the images perfectly. In order to increase the accuracy of the bounding boxes, YOLO uses a grid instead of sliding windows, in addition to two other techniques, known as Intersection Over Union and Non-Maximal Suppression.

The combination of the above techniques is part of the reason the YOLO algorithm works so well. Before diving into how YOLO puts all these techniques together, we will look first at each technique individually.

## Compuer Vision Algorithms

### YOLO

Now you've learned about a number of region-based methods for recognizing and locating multiple objects in a scene.
Architectures like faster R-CNN are accurate, but the model itself is quite complex, with multiple outputs that are each a potential source of error.
Once trained they're still not fast enough to run in real time. In this lesson we'll be learning about YOLO which stands for You Only Look Once,
and it's a real-time object detection algorithm, that avoid spending too much time on generating region proposals.
Instead of locating objects perfectly, it prioritizes speed and recognition. 

Let's see an example of YOLO in action.
Consider a self-driving car that sees this image of a street.

It's essential for a self-driving car to be able to detect the location of objects all around it, such as pedestrians cars, and traffic lights. On top of that, this detection has to happen in near real time,
so that the car can safely navigate the street. The card doesn't always need to know what all these objects are? 
It mostly needs to know not to crash into them but it does need to recognize traffic lights bikes and pedestrian to be able to correctly follow the rules of the road.
In this image we've used the YOLO algorithm to locate and classify different objects, there's a bounding box that locates each object and a corresponding class label.
In the next lesson we'll learn the details of how the YOLO algorithm works.

### YOLO Output

When we talked about localization in images, we talked about creating a CNN that could output a predicted class front object in an image and a predicted bounding box for that object. In the CNN examples that we've seen, these outputs are analyzed separately in the network trains by using a weighted combination of classification and regression losses. Another way to process these outputs is by merging them into a single output vector, which is what the yellow algorithm does.

Let's see this in an example.
Let's assume I want to train a CNN to be able to detect three classes, a person, a cat, and a dog.
In this case, because we only have three classes, the output vector y will only have three elements, C one, two, and three.
Each of which is a class score or a probability that the image is of a person, cat, or dog.
If you have more classes, this vector will get longer.

For this image, we want to train the CNN so that it can identify the person in this image and look at that person within a bounding box. We can do this by adding some box parameters to our output vector. We can add four more numbers, x, y, w and h, that determine the position and size of the bounding box. X and y determine the coordinates of the center of the box,
and w and h determine its width and height. Once you've trained your CNN to output class probabilities and bounding box coordinates, you're one step closer to being able to detect objects in any given image.
Next we'll briefly go over the sliding-windows approach that you've seen before with our example output vector in mind.
Then you'll see how yellow improves upon sliding windows and breaks an image into a grid for efficient object detection.

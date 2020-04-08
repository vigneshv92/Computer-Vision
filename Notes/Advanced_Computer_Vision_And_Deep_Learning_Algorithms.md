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

# Table of Contents

### 1. CNN's and Scene Understanding

### 2. More than Classification

### 3. Classification and Localization

### 4. Beyond Bounding Boxes & Regression </br>
To predict bounding boxes, we train a model to take an image as input and output coordinate values: (x, y, w, h). This kind of model can be extended to any problem that has coordinate values as outputs! One such example is human pose estimation.

<img src="/Visual Representations/human_pose_estimation.png" align="center"/></p>

In the above example, we see that the pose of a human body can be estimated by tracking 14 points along the joints of a body.

#### Weighted Loss Functions</br>
You may be wondering: how can we train a network with two different outputs (a class and a bounding box) and different losses for those outputs?

We know that, in this case, we use categorical cross entropy to calculate the loss for our predicted and true classes, and we use a regression loss (something like smooth L1 loss) to compare predicted and true bounding boxes. But, we have to train our whole network using one loss, so how can we combine these?

There are a couple of ways to train on multiple loss functions, and in practice, we often use a weighted sum of classification and regression losses ```(0.5*cross_entropy_loss + 0.5*L1_loss);``` the result is a single error value with which we can do backpropagation. This does introduce a hyperparameter: the loss weights. We want to weight each loss so that these losses are balanced and combined effectively, and in research we see that another regularization term is often introduced to help decide on the weight values that best combine these losses.

### 5. Loss Values

### 6. Region Proposals </br>

Now you've seen how to locate one object in an image by generating a bounding box around that object.</br>
But what if there are multiple objects in an image? How can you train a network to detect all of them?

</br> Well, let's think about the case where we just have two objects in an image.

<img src="/Visual Representations/region_proposals.png" align="center"/></p>

</br>How can we localize and label both of these? </br>
> One approach could be to try to simplify this input image and split it into two different regions, 
each of which only contains one object. Then we can proceed in the same way as before,
putting each region through a CNN that generates one class label and one bounding box.

</br> Then you might think, what about if there are three objects in an image or four or more?
> The real challenge here is that there's a variable output. You don't know ahead of time how many objects are going to be in a given image and CNNs and most neural networks have a defined unchanging output size. So, to detect a variable amount of 
objects in any image, you first must break that image up into smaller regions and produce bounding boxes and class labels for 
one region and one object at a time.

</br> So how can we go about breaking up an image into regions? </br>
> We know that we want these regions to correspond to different objects in the image and we don't want to miss any objects.
We could just make a bunch of cropped regions to make sure we don't miss anything.
This would mean defining a small sliding window and passing it over the entire image using some value for stride
to create mini different crops of the original input image. Then for each cropped region, we can put it through a CNN and 
perform classification. However, this approach produces a huge amount of cropped images and is extremely time-intensive.

Also, in this case, most of the cropped images don't even contain objects. 

</br> So how can you better choose these cropped regions, especially when objects vary in size and location? </br>
> Next, I want you to think about how you might improve this region selection process.
You want to make sure not to miss any objects but you also don't
want to put a huge number of cropped regions through a CNN.

We'll learn about techniques for finding these regions shortly.
Then, you should be able to locate and classify any objects that appear in an original image,
whether that's one object or three or 20. 

###### Reflect
Considering the above image, how do you think you would select the best proposed regions, what criteria do good regions have? </br>
> Your reflection </br>
By Increasing the sliding window size to reduce the number of cropped regions.

</br> Solution </br>
> Things to think about, The regions we want to analyze are those with complete objects in them. We want to get rid of regions that contain image background or only a portion of an object. So, two common approaches are suggested: 
</br> 1. identify similar regions using feature extraction or a clustering algorithm like k-means, as you've already seen; these methods should identify any areas of interest.
</br> 2. Add another layer to our model that performs a binary classification on these regions and labels them: object or not-object; this gives us the ability to discard any non-object regions!

## 7. R-CNN

To localize and classify multiple objects in an image, we want to be able to identify a limited set of cropped regions for a CNN to look at. In the ideal case, we would generate three perfectly cropped regions for three different objects in an image.
To approach this goal and generate a good limited set of cropped regions, the idea of region proposals was introduced.
Region proposals give us a way to quickly look at an image and generate regions only for areas in which we think there may be an object. We can use traditional computer vision techniques that detect things like edges and textured bobs to produce a set of regions in which objects are most likely to be found; areas of similar texture or the same unifying boundary, 
for example. 

These proposals often produce noisy non-object regions, but they are also very likely to include the regions in which objects are located. So the noise is considered a worthwhile cost for not missing any objects. So let's see how this looks when incorporated into a CNN architecture. We can use a region proposal algorithm to produce a limited set of cropped regions. Often called regions of interests or ROIs. And then we put these regions through a classification CNN, one at a time and see what kind of class label the network predicts for each crop.

This model is called an R-CNN, Which stands for region convolutional neural network. The R-CNN produces a class for each region of interest, and so it can identify the region that is a dog and the region that is a cat in an image.In this case we also include a class called background, that's meant to capture any noisy regions. Since these regions are often different sizes they first need to be transformed and warped into a standard size that a CNN can accept as input. Now, the main shortcoming of this method is that it still time intensive because it requires that each cropped region go through an entire CNN before a class label can be produced. Next, we'll see some examples of region-based CNNs that aim to speed up this process and efficiently classify multiple objects in an image.

##### R-CNN Outputs </br>
The R-CNN is the least sophisticated region-based architecture, but it is the basis for understanding how multiple object recognition algorithms work! It outputs a class score and bounding box coordinates for every input RoI.

An R-CNN feeds an image into a CNN with regions of interest (RoI’s) already identified. Since these RoI’s are of varying sizes, they often need to be warped to be a standard size, since CNN’s typically expect a consistent, square image size as input. After RoI's are warped, the R-CNN architecture, processes these regions one by one and, for each image, produces 1. a class label and 2. a bounding box (that may act as a slight correction to the input region).

R-CNN produces bounding box coordinates to reduce localization errors; so a region comes in, but it may not perfectly surround a given object and the output coordinates (x,y,w,h) aim to perfectly localize an object in a given region.
R-CNN, unlike other models, does not explicitly produce a confidence score that indicates whether an object is in a region, instead it cleverly produces a set of class scores for which one class is "background". This ends up serving a similar purpose, for example, if the class score for a region is Pbackground = 0.10, it likely contains an object, but if it's Pbackground = 0.90, then the region probably doesn't contain an object.

### 8. Fast R-CNN

<img src="/Visual Representations/Fast_RCNN.png" align="center"/></p>

The next advancement in region-based CNNs came with the Fast R-CNN architecture. Instead of processing each region of interest individually through a classification CNN, this architecture runs the entire image through a classification CNN only once.
The image goes through a series of convolutional and pooling layers and at the end of these layers, we get a stack of feature maps. We still need to identify regions of interest but instead of cropping the original image, we project these proposals into the smaller feature map layer. Each region in the feature map corresponds to a larger region in the original image. So we can grab selected regions in this feature map and feed them one by one into a fully connected layer that generates a class for each of these different regions.

In this model we complete the most time-consuming steps, processing an image through a series of convolutional layers only once and then selectively use that map to get our desired outputs. Again, we have to handle the variable sizes and these protections,
since layers further in the network are expecting input of a fixed size. So, we do something called ROI pooling to warp these regions into a consistent size before giving them to a fully connected layer. Now this network is faster than R-CNN but it's still slow when faced with a test image for which it has to generate region proposals and it's still looking at regions that do not contain objects at all. The next architecture we'll look at aims to improve this region generation step.

#### RoI Pooling </br>

To warp regions of interest into a consistent size for further analysis, some networks use RoI pooling. RoI pooling is an additional layer in our network that takes in a rectangular region of any size, performs a maxpooling operation on that region in pieces such that the output is a fixed shape. Below is an example of a region with some pixel values being broken up into pieces which pooling will be applied to; a section with the values:

```python
[[0.85, 0.34, 0.76],
 [0.32, 0.74, 0.21]]
 ```
 
Will become a single max value after pooling: 0.85. After applying this to an image in these pieces, you can see how any rectangular region can be forced into a smaller, square representation.

An example of pooling sections, below.

<img src="/Visual Representations/Fast_RCNN_RoI.png" align="center" width="700" height="700"/></p>

You can see the complete process from input image to region to reduced, maxpooled region, below.

<img src="/Visual Representations/roi-pooling.gif" align="center"/></p>

### 9. Faster R-CNN

To speed up the time it takes to run a test image through a network and detect all the objects in it, we want to decrease the time it takes to form region proposals.

For this we have the faster R-CNN architecture.</br>
* Faster R-CNN learns to come up with its own region proposals.
* It takes in an input image, runs it through a CNN up until a certain convolutional layer just like Fast R-CNN, but this time it uses the produced feature map as input into a separate region proposal network. So it predicts its own regions from the features produced inside the network.
* If an area in the feature map is rich in detected edges or other features, it's identified as a region of interest. 
* Then this part of a network does a quick binary classification. 
* For each ROI it checks whether or not that region contains an object. If it does then the region will continue on and go through the classification steps and if it doesn't, then the proposal is discarded.
* Once we have the final region proposals, the rest of the network looks the same as Fast R-CNN. It takes cropped regions from the feature map and learns to classify those regions.

By eliminating the analysis of non-object regions, this model is the fastest of all the region-based CNNs that we've seen.

###### Region Proposal Network
You may be wondering, how exactly are the RoI's generated in the region proposal portion of the Faster R-CNN architecture? </br>
> The region proposal network (RPN) works in Faster R-CNN in a way that is similar to YOLO object detection, which you'll learn
> about in the next lesson. The RPN looks at the output of the last convolutional layer, a produced feature map, and takes a 
> sliding window approach to possible-object detection. It slides a small (typically 3x3) window over the feature map,
> then for each window the RPN Uses a set of defined anchor boxes, which are boxes of a defined aspect ratio (wide and short or tall and thin, for example) to generate multiple possible RoI's, each of these is considered a region proposal.
> For each proposal, this network produces a probability, Pc, that classifies the region as an object (or not) and a set of bounding box coordinates for that object.
> Regions with too low a probability of being an object, say Pc < 0.5, are discarded.

###### Training the Region Proposal Network
Since, in this case, there are no ground truth regions, how do you train the region proposal network?</br>
> The idea is, for any region, you can check to see if it overlaps with any of the ground truth objects. That is, for a region, if we classify that region as an object or not-object, which class will it fall into? For a region proposal that does cover some portion of an object, we should say that there is a high probability that this region has an object init and that region should be kept; if the likelihood of an object being in a region is too low, that region should be discarded.

I'd recommend this [blog post](https://towardsdatascience.com/deep-learning-for-object-detection-a-comprehensive-review-73930816d8d9) if you'd like to learn more about region selection.

###### Speed Bottleneck</br>

Now, for all of these networks including Faster R-CNN, we've aimed to improve the speed of our object detection models by reducing the time it takes to generate and decide on region proposals. You might be wondering: is there a way to get rid of this proposal step entirely? And in the next section we'll see a method that does not rely on region proposals to work!

If you'd like to look at an implementation of this network in code, you can find a peer-reviewed version, at this 
[Github repo](https://github.com/jwyang/faster-rcnn.pytorch).

### 10. Conclusion

You've really learned a lot about the evolution of CNN architectures in this lesson, especially about how to detect multiple objects in an image using region proposals.

As we mentioned at the start, simple image classification problems are really the most basic application for CNNs. And if we're aiming to reach levels of human understanding, we have to add complexity to these networks so that they're able to recognize multiple objects and their relations to one another. You may also be wondering if there's a way to perform object recognition without region proposals like this, and there is. There's a whole other family of object detection networks that don't use region proposals. 

> One of these is YOLO, which stands for you only look once, and another is SSD, or single shot detection.
These both came out around the same time, and in the next lesson you'll learn all about YOLO and get a chance to work with a code implementation of a YOLO Detection Network.

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

#### 5. Loss Values

### 6. Region Proposals </br>

Now you've seen how to locate one object in an image by generating a bounding box around that object.
> But what if there are multiple objects in an image?
> How can you train a network to detect all of them?

</br> Well, let's think about the case where we just have two objects in an image.

> How can we localize and label both of these? </br>
One approach could be to try to simplify this input image and split it into two different regions, 
each of which only contains one object. Then we can proceed in the same way as before,
putting each region through a CNN that generates one class label and one bounding box.

Then you might think, what about if there are three objects in an image or four or more?
The real challenge here is that there's a variable output. You don't know ahead of time how many objects are going to be in a given image and CNNs and most neural networks have a defined unchanging output size. So, to detect a variable amount of 
objects in any image, you first must break that image up into smaller regions and produce bounding boxes and class labels for 
one region and one object at a time.
We'll learn about techniques for finding these regions shortly.
Then, you should be able to locate and classify any objects that appear in an original image,
whether that's one object or three or 20. 

> So how can we go about breaking up an image into regions? </br>
We know that we want these regions to correspond to different objects in the image and we don't want to miss any objects.
We could just make a bunch of cropped regions to make sure we don't miss anything.
This would mean defining a small sliding window and passing it over the entire image using some value for stride
to create mini different crops of the original input image. Then for each cropped region, we can put it through a CNN and 
perform classification. However, this approach produces a huge amount of cropped images and is extremely time-intensive.

Also, in this case, most of the cropped images don't even contain objects. 

> So how can you better choose these cropped regions, especially when objects vary in size and location? </br>

Next, I want you to think about how you might improve this region selection process.
You want to make sure not to miss any objects but you also don't
want to put a huge number of cropped regions through a CNN.

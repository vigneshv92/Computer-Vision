Table of Contents

1. CNN's and Scene Understanding

2. Beyond Bounding Boxes</br>
To predict bounding boxes, we train a model to take an image as input and output coordinate values: (x, y, w, h). This kind of model can be extended to any problem that has coordinate values as outputs! One such example is human pose estimation.

In the above example, we see that the pose of a human body can be estimated by tracking 14 points along the joints of a body.
Weighted Loss Functions
You may be wondering: how can we train a network with two different outputs (a class and a bounding box) and different losses for those outputs?

We know that, in this case, we use categorical cross entropy to calculate the loss for our predicted and true classes, and we use a regression loss (something like smooth L1 loss) to compare predicted and true bounding boxes. But, we have to train our whole network using one loss, so how can we combine these?

There are a couple of ways to train on multiple loss functions, and in practice, we often use a weighted sum of classification and regression losses (0.5*cross_entropy_loss + 0.5*L1_loss); the result is a single error value with which we can do backpropagation. This does introduce a hyperparameter: the loss weights. We want to weight each loss so that these losses are balanced and combined effectively, and in research we see that another regularization term is often introduced to help decide on the weight values that best combine these losses.

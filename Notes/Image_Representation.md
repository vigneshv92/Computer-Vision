
### Images as Numerical Data

Every pixel in an image is just a numerical value and, we can also change these pixel values. We can multiply every single one by a scalar to change how bright the image is, we can shift each pixel value to the right, and many more operations!

Treating images as grids of numbers is the basis for many image processing techniques.

Most color and shape transformations are done just by mathematically operating on an image and changing it pixel-by-pixel.

### Importance of Color

In general, when you think of a classification challenge, like identifying lane lines or cars or people, you can decide whether color information and color images are useful by thinking about your own vision.

If the identification problem is easier in color for us humans, it’s likely easier for an algorithm to see color images too!

### Color Spaces and Transforms

So we've seen how to detect a blue screen background.
But this detection assumed that the scene was very well
lit and that the screen was a very consistent blue.
What would happen if the lighting changed and part of
the wall was in shadow or washed out and bright?
The simple blue color threshold wouldn't work very well in this scenario.
So how can we consistently detect objects under varying light conditions?
Well, there are many other ways to represent
the colors in an image besides just composed of red,
green, and blue values.
These different color representations are often called "color spaces".
RGB is red, green, blue color space.
You can think of this as a 3D space where
any color can be represented by a 3D coordinate of R,
G, and B values.
For example, white is on the corner here with a value of
255 255 255 for red green and blue values.
There's also HSV color space for hue, saturation, and value.
And HLS for hue, lightness, and saturation.
And these are some of the most commonly used color spaces in image processing.
We'll be going through an image processing example in HSV color space.
This isolates the value or V component of each pixel in an image.
And this is the component that varies the most under different lighting conditions.
The H channel stays fairly consistent under shadow or excessive brightness.
And if we rely mainly on this channel and discard the information in the V channel,
we should be able to detect colored objects more reliably than in RGB color space.
In this notebook, I read in an image of water balloons and displayed it.
I'll be trying to use RGB color space and
HSV to see if I can select all the pink balloons.
Right now each pixel and this image has x and
y values for its position in RGB values for its color.
And to see the relative values of each of
these colors or isolate each of these color values,
which I'll call color channels, and display them.
To isolate the red channel,
I can just take the RGB image array,
image copy take all the x and the y values in the first two array columns.
Then the zero index of the third column which is the red value for each pixel.
Similarly, for green and blue I'll take all the x and y coordinates of the image pixels,
and take the first and second index of
the third column to get the green and blue values for each pixel.
Then I can plot each of these channels in grayscale to see their relative intensities.
And here are the three channels represented in grayscale intensity.
The brighter pixels indicate higher values of red,
green, or blue, respectively.
We can see that the pink balloons have high values for red and medium high for blue.
But there's a lot of variations especially when the balloon is in shadow.
Now, let's repeat the same process for HSV color space.
First, only to convert this image to HSV color space using CVT color as before.
This time with the conversion code RGB to HSV.
This will return a new converted image which I'll call HSV.
Then I'll isolate each of these channels using
the same process as before and I'll plot them on the same axis.
Here are the three channels hue, saturation, and value.
And let's compare it to our original image.
Note the pink balloons and their location.
Here we can see that the hue channel is pretty high for pink balloons,
and even in shadow the hue level is pretty consistent.
The saturation and value channels vary a lot
more especially under shadow and at the edges of balloons.
The next step is to create color thresholds in both these colors spaces to compare.
Here I've determined the pink color range by using a color selector,
and defined the lower and upper boundaries in our RGB values to reflect this.
These thresholds allow some high values of red and medium values of blue.
Next I'll do the same thing in HSV color space.
Remember that hue only goes from 0 - 180 as a measurement of degrees.
Here I'm allowing a narrow high range for the hue channel from 160 - 180.
And I'm allowing any value for the saturation and value channels, 0 - 255.
Next I'll create masked images to see how
well each of these thresholds selects the pink balloons.
First I'll create the RGB mask.
As before I'm using open CVs in range function,
our RGB image and the lower and upper pink thresholds.
Next I'll create a copy of the image and apply the mask,
setting the pixels equal to zero where the mask is equal to zero or black.
And finally, I'll display the result.
And we can see that this selects most of the pink area but also has
some other sections and it misses the parts of the balloons that are in shadow.
Then I'll do the same with our HSV image creating a mask using
inRange passing in our HSV color converted image and our lower and upper hue boundaries.
I'll then create another masked image blocking out
the part of the image with a mask is equal to zero.
If we look at this selection we can see that the pink balloons are almost all selected,
and we can see that HSV space is actually more
valuable in selecting an area under varying light conditions.

# **Finding Lane Lines on the Road** 



**Finding Lane Lines on the Road**

The goals of this project is to make a pipeline that finds lanes on the road.

[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Explaination the pipeline

The pipeline takes an image and performs the following steps:

* Convert the image grayscale image
* Apply Gaussian Blurring with kernel size 5
* Apply Canny Edge detector to detect edges in the images
* Apply image masking to just include the region of interest by using opencv fillpoly to calculate mask and apply bitwise_and to get the masked image. 
* Next, Hough Transform is applied to detect the lines (using opencv HoughLinesP method). This will generate multiple lines on each side. 

In order to draw a single line on the left and right lanes, the algorithm is modified to calculate average slope and interception of right-side lines and left-side lines. Slope and intercept are calculated as the equation below:

```
slope = (y2-y1)/(x2-x1)
intercept = y1 - slope*x1
``` 
The implementation keeps track of `y_min` and `y_max` from all the lines which is used to determine where the single lines shall start and end in y direction. 

Also, to calculate the average slope only the slopes that are between 30 and 60 degrees to account for lines that get detected when the road conditions are not ideal.

<!--![alt text][image1]-->


### 2. Potential shortcomings with your current pipeline

The detection does not really care for the curvature that happens when the street/highway is not straight and since the average of all slopes are used it make the lines to be off when there are pretty sharp turns.

Also if there are slanted edges detected between the lanes then with slope from 30-60 degrees it might mess up the average slope calculation 



### 3. Possible improvements to this pipeline

To have better edge detection where it only the edges that are in x-direction and not care much about the y-direciton if cross-sections on the street are not concenr and can be ignored.

To imporve the algorithm to account for road turns and make sure.



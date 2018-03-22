**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

[image1]: ./sample_images/gray.jpg "Grayscale"
[image2]: ./sample_images/gauss.jpg "Gaussian filter"
[image3]: ./sample_images/canny.jpg "Canny Edge detection"
[image4]: ./sample_images/roi.jpg "Region of Interest"
[image5]: ./sample_images/final.jpg "Output Image"

My pipeline consisted of 6 steps:

1. Convert the images to grayscale.
<img src="./sample_images/gray.jpg" height="24" width="48">
2. Apply gaussian filter with kernel size 3, in order to reduce noise.
![Gaussian filter][image2]
3. Apply canny edge detection with low_threshold=50 and high_threshold=150.
![Canny Edge detection][image3]
4. Define the polygon vertices for region of interest and apply masking.
![Region of Interest][image4]
5. Define the parameters and apply probabilistic hough transform.
6. Overlay lane lines on the actaul image.
![Output Image][image5]

Modification of draw_lines() function:

1. Initialize lists to store the x and y coordinate values from the Hough trasform lines.
2. For each of the Hough transform lines, compute the slope and use it to group porints as the left lane points and right lane points.
3. It is important to choose the lines which do not deviate too much from the expected slope. 
4. For both left and right lane, fit a line using `np.polyfit()` function.
5. Draw the line on the initial input image with large thinkness (5).


### 2. Identify potential shortcomings with your current pipeline

Potential shortcoming:

1. One shortcoming of this model is that it does not consider the history of detected lane lines, and hence might return incorrect values (lane line) when curved lanes are encountered. This means the output is not smooth.
2. Another shortcoming is that it does not function as expected when the image is too bright or has low contrast.

### 3. Suggest possible improvements to your pipeline

1. Storing the history of predicted lane lines and using the mean of these values as reference to the future predictions would be helpful to avoid anomalies.
2. Convert the input image to more suitable color space.


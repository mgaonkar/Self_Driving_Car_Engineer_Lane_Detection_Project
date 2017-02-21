#**Finding Lane Lines on the Road** 


**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Description of pipeline.Explanation of how the draw_lines() function was modified.

My pipeline consisted of 8 steps.
1. Converted the input image from RGB to GrayScale
2. Since the lane markings are in yellow and White converted RGB image into HSV to draw out the color information and then 
teased out these colors to create a unified yellow and white mask.
3. Applied the mask from above to Grayscale image where the instensity of Gray was reduced.
4. Applied Gaussian Blur.
5. Detected edges experimenting with different values of high and low threshold using canny edge detection.
6. Found a region of interest with the provided helper function. Parameters were chosen based on the image dimensions.
7. Got Hough lines by providing the masked image as input and by tweaking the Hough transform parameters.
8. Applied the Hough lines to the original image using the weighted_img helper function.


In order to draw a single line on the left and right lanes:

1. Computed Slopes, Intercepts of all lines
2. Found the Highest and the lowest slope lines
3. Used output of step 2 to determine the segments which are part of the left line vs the right line using a percentage deviation
4. Calculated an average left line and right line (averaged the slope and intercept) and extrapolated the line based on the image dimensions.




###2. Identification of potential shortcomings with current pipeline


One potential shortcoming:
1. When we input images/vidoes of a lane which continues on straight and exits from the same lane (no separate exit lane), edge 
detection will momentarily detect the split of the lane causing weird extrapolation, merging at the horizon of the guidance lines.

Another shortcoming could be:
1. Driving on mountain switchbacks when the lane markings curves are extreme and and the guidance lines might merge away from the road.


###3. Suggest possible improvements to your pipeline

A possible improvement would be:
1. Detect the HOV lanes by the white Diamond HOV symbol

Another potential improvement could be:
1.For an undivided highway, filter out the opposite lane headlights for better detection of lanes.
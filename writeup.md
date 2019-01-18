# **Finding Lane Lines on the Road** 


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./fig/color_filiter.jpg "Color filiter"
[image2]: ./fig/roi.jpg "Roi"
[image3]: ./fig/canny.jpg "After Canny and limit field of vision"
[image4]: ./fig/line.jpg "Lane line"
[image5]: ./fig/result.jpg "Result"


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 main steps. First, I constructed the color filiter to select intresting color, e.g. yellow and white, then I setting ROI to restrict the field of vision to make work more easy. Second, I  converted the images to grayscale, then using Hough method to find all lines in the ROI. Third, the most important part, I computed the slope for all lines which found by Hough method, then classify the slopes by + slope and - slope, in this part, I also find the closets bottom point in each slope. Forth, I sorted the slope to computed the line which is best fit the lane line. At Last, I fused the result of color filiter, ROI and best fit line to generate the result of finding lane line.


The detail development process about finding best fit line have some main imporvent. In this part, I computed all lines slope and divided it into + and - slope and find the closets bottom point and top point in each slope. Initially, I only use bottom point, image's highet and the first slope in the slope stack to find the complete line, and it worked well in image part. However, when I ran the program in the video prat, it got many worst result. To solve the problem, I try to find the median in the slope stack but it still have some problem when stack size is even the median was the mean of two slope, it will make line not really precise. Then I sorted the + and - slope stack and select the true median in the stack to compute bottom points. So far it work well, but in the second video, this method it seems not good so I try to make it well, so I also compute the top points via bottom points and the boundary of ROI. Finally, it work well.

![alt text][image1]
<center>After color filiter</center>

![alt text][image2]
<center>Selected Roi</center>

![alt text][image3]
<center>After Canny and limit field of vision</center>

![alt text][image4]
<center>Lane line</center>

![alt text][image5]
<center>Results</center>


### 2. Identify potential shortcomings with your current pipeline

I have two shortcomings in the project. 

One potential shortcoming would be what would happen when the car drive in the tree shadow, it make my program can not find lines well although I filiter the slope.

Another shortcoming could be when cars turn. In my program, it can not compute the angle and draw the turn lines.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to find the ROI, automatically.

Another potential improvement could be to make code more simple and clear.



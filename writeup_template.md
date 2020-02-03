# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of 5 steps. First, I convert the images to grayscale, then I apply Gaussian blurring which is followed by Canny Edge Detection. I define a polyhedron in order to mask out images which are not in front of the car. Then I applied HoughLinesP() to identify lines on the road. The predefined draw_lines() method then draws each line segment on the picture.

I wrote a test function which apply the pipeline to the examplatory images. Based on these I fine-tune the parameters as explained in the lecture.

In order to draw a single line on the left and right lanes, I used a new draw_lines2() method. First I split the points describing the lines into left and right lane by investigating the direction of the line segments. Each line segment is described by 2 points. Thus I can check which point is further away from the car and which point has a smaller x-value, i.e. is more left. This allows me to filter thelane of the line segment.
Afterwards I use linear regression to compute a linear function describing the lane.



### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen if horizontal lines are on the road. Currently these are not detected.
Another shortcoming could be that the detection of left or right lane might fail if the line segment is far away.

Linear regression takes outliers into account equally important. Thus one wrong line segment has a hugh effect on the overall lane prediction.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to add additional masking. For instance another polyhedron masking out parts of the image in between the lanes might help to overcome the issue.
It might make sense to line segments being close to the car. In that way it's easier to distinguish between left and right lane.

An additional analysis step which gets rid of outliers using statistical tools might very well improve the lane prediction.
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

### 1. Describe your pipeline:

My pipeline consisted of 5 steps. 
Started with the original image:
<img src="pipeLine-screenshots/1.original_image.jpg" width="480" />

* First, I converted the original images to grayscale, so that I can apply Canny algorithm.
<img src="pipeLine-screenshots/2.gray_image.jpg" width="480" />
* Second, applied Gaussian filter to grayscaled image to filter-out noise and spurious gradients.
<img src="pipeLine-screenshots/3.blur_gray.jpg" width="480" />
* Third, applied the apply canny algorithm on the above image.
<img src="pipeLine-screenshots/4.canny_edges.jpg" width="480" />
* Fouth, 
Created mask
<img src="pipeLine-screenshots/5.mask.jpg" width="480" />
created a masked image
<img src="pipeLine-screenshots/6.masked_image.jpg" width="480" />
created a canny masked image
<img src="pipeLine-screenshots/7.masked_canny_edges.jpg" width="480" />

* Fifth, calulated Hough lines from canny edges.
<img src="pipeLine-screenshots/8.HoughLines_Drawn.jpg" width="480" />
<div class="alert alert-block alert-info">The hough_lines() function internally calls draw_lines() function to draw the lines to the full extent. The lines returned from hough_lines() function are drawn on the bases of edges/dots returned from canny algorithm. So, basicaly lines will only be drawn on the pixels which has qualified certain threshold of pixel intensity. Therefore, if the current pipeline watches a unbroken any-color lane-lines then it will annotate it, but if it the lane-lines are broken, which they are on roads, then they will only recognise the any-color broken patches.</div>
Here, **The goal now is to draw a consistent annotation on the lane lines irrespective of whether it is broken or not.**

>  In order to draw a single annotation on the left and right lanes, I modified the draw_lines() function as follows
>  1. We got an image with hough lines drawn from hough_lines() function. 
>  2. Seperate the left-lane lines & right-lane lines from the lines returned from hough_lines() function. We can perform 
   it by finding slope of each line and checking under the condition whether it's <0 or >0, respectively put the lines
   in left-lane lines, right-lane lines list.
>>   *  **I observed that there were no verticle lines(slope Infinity) detected in any image. But, can't' find a solid reason           for it.
      May be Hough transformation has excluded them because, these lines are parallel to y-axis and will never meet.
      But, I can defend against this point that, these lines could intersect with many other +ve or -ve slope lines,
      then they are significant.**
>>   * **I found few Horizontal lines. I have seperated them into left-lane lines & right-lane lines on the basis of a 
      condition <500 & >500 respectively**
>  3. After finding the left-lane lines & right-lane lines. I followed the follow points. Consider now only left-lane lines
>>  * First find out minimum of all y's.
>>  * Now, Calculate minimum of x for the minimum y, `Oops...!` You do not know Intercept & slope. Follow the below steps:
>>  * Calculate average slope among all left-lane lines,
>>>   *  find the average of all `(x1,y1,x2,y2)` coordinates to get (x1_avg,y1_avg,x2_avg,y2_avg)
>>>   *  Now, calculate `slope_avg = (y2_avg - y1_avg) / (x2_avg - x1_avg)`
>>  * Calculate average Intercept,
>>>    *  `intercept_avg = y1_avg - (slope_avg * x1_avg)`
>>  * Now you have all the tools `x1_avg, y1_avg, slope_avg, intercept_avg` to calculate `minimum of x for minimum y` point by       using:
         `min_x = (y_min - intercept_avg) / slope_avg`
> 4. Now, we have `(min_x, min_y)` among all left-lane lines and we can calculate `(max_x, max_y)` similarly by following the
   above algorithm.
   Next step is to find `(min_x, min_y) & (max_x, max_y)` for right-lane lines from the above steps.
* Sixth, To achive the goal to get a consistent line on both lanes connect & color above lines with cv2.line() function.
<img src="pipeLine-screenshots/9.LaneLinesAnnotated.jpg" width="480" />
Later, made the annotation semi-transpared by using cv2.addWeighted() function.
<img src="pipeLine-screenshots/10.LaneLinesDetected_output.jpg" width="480" />
After implementing the above Twice, I got the below given results:
---
* When I kept the slope condition as 
<img src="findings/slope_criteria-1.png" width="300" />
* The following were the points selected for annotation.
<img src="findings/slope-criteria-1,both lines-coordinates.png" width="300" />
* The below are the reflections on the image:
<p float="left">
  <img src="findings/slope-criterion-1/solidWhiteCurve_output.jpg" width="100" />
  <img src="findings/slope-criterion-1/solidWhiteRight_output.jpg" width="100" />
  <img src="findings/slope-criterion-1/solidYellowCurve2_output.jpg" width="100" />
  <img src="findings/slope-criterion-1/solidYellowCurve_output.jpg" width="100" />
  <img src="findings/slope-criterion-1/solidYellowLeft_output.jpg" width="100" />
  <img src="findings/slope-criterion-1/whiteCarLaneSwitch_output.jpg" width="100" />
</p>
---
* When I kept the slope condition as 
<img src="findings/slope-criteria-2.png" width="300" />
* The following were the points selected for annotation.
<img src="findings/slope-criteria-2-coordinates.png" width="300" />
* The below are the reflections on the image:  
<p float="left">
  <img src="findings/slope-Criterion-2/solidWhiteCurve_output.jpg" width="100" />
  <img src="findings/slope-Criterion-2/solidWhiteRight_output.jpg" width="100" />
  <img src="findings/slope-Criterion-2/solidYellowCurve2_output.jpg" width="100" />
  <img src="findings/slope-Criterion-2/solidYellowCurve_output.jpg" width="100" />
  <img src="findings/slope-Criterion-2/solidYellowLeft_output.jpg" width="100" />
  <img src="findings/slope-Criterion-2/whiteCarLaneSwitch_output.jpg" width="100" />
</p>
---
Now, I have fixed the x's and y's for annotation to get the following:
* When I kept the above slope condition as 
<img src="findings/slope-criteria-2.png" width="300" />
* The following were the fixed points selected for annotation.
<img src="findings/fixedValuesOfx&ys.png" width='300'/>
* The below are the reflections on the image:  
<p float="left">
  <img src="findings/Fixed-the-x&y's/solidWhiteCurve_output.jpg" width="100" />
  <img src="findings/Fixed-the-x&y's/solidWhiteRight_output.jpg" width="100" />
  <img src="findings/Fixed-the-x&y's/solidYellowCurve2_output.jpg" width="100" />
  <img src="findings/Fixed-the-x&y's/solidYellowCurve_output.jpg" width="100" />
  <img src="findings/Fixed-the-x&y's/solidYellowLeft_output.jpg" width="100" />
  <img src="findings/Fixed-the-x&y's/whiteCarLaneSwitch_output.jpg" width="100" />
</p>
### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...


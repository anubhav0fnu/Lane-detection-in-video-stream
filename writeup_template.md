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

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...
1. We got an image with hough lines drawn from hough_lines() function. These lines are drawn on the bases of edges/dots
   returned from canny algorithm.So, basicaly lines will only be drawn on the pixels which has qualified certain threshold
   of pixel intensity. Therefore, if the current pipeline watches a unbroken any color lane lines then it will annotate
   it, but if it the lane lines are broken, which they are on roads, them they will only recognise the any color broken
   patches. The goal now is to draw a consistent annotation on the lane lines irrespective of whether it is broken or not.
   . Inorder to do that, I have to follow below algorithm
2. Seperate the left-lane lines & right-lane lines from the lines returned from hough_lines() function. We can perform 
   it by finding slope of each line and checking under the condition whether it's <0 or >0, respectively put the lines
   in left-lane lines, right-lane lines list.
   > 
   * ** I observed that there were no verticle lines(slope Infinity) detected in any image. But, can't' find a solid reason           for it.**
      May be Hough transformation has excluded them because, these lines are parallel to y-axis and will never meet.
      But, I can defend against this point that, these lines could intersect with many other +ve or -ve slope lines,
      then they are significant.
   * ** I found few Horizontal lines. I have seperated them into left-lane lines & right-lane lines on the basis of a 
      condition <500 & >500 respectively**
3. After finding the left-lane lines & right-lane lines. I followed the follow points. Consider now only left-lane lines
    * First find out minimum of all y's.
    * Now, Calculate minimum of x for the minimum y, `oops...!` You do not know Intercept & slope. Follow the below steps:
    * Calculate average slope among all left-lane lines,
        *  find the average of all `(x1,y1,x2,y2)` coordinates to get (x1_avg,y1_avg,x2_avg,y2_avg)
        *  Now, calculate `slope_avg = (y2_avg - y1_avg) / (x2_avg - x1_avg)`
    * Calculate average Intercept,
        *  `intercept_avg = y1_avg - (slope_avg * x1_avg)`
    * Now you have all the tools x1_avg, y1_avg, slope_avg, intercept_avg to calculate minimum of x for minimum y point by           using:
         ` min_x = (y_min - intercept_avg) / slope_avg$`

4. Now, we have `(min_x, min_y)` among all left-lane lines and we can calculate `(max_x, max_y)` similarly by following the
   above algorithm.
   Next step is to find `(min_x, min_y) & (max_x, max_y)` for right-lane lines.
5. The goal to get a consistent line on both lanes, you did step 3 & 4.
   Now, it's the time to connect & color them with cv2.line() function.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...

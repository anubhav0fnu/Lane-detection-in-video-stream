# **Finding Lane Lines on the Road** 
<img src="findings/Fixed-the-x&y's/whiteCarLaneSwitch_output.jpg" width="480" />
Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project I used Python and OpenCV( Open-Source Computer Vision-a package that has many useful tools for analyzing images) to detect lane lines in images.

To complete the project, two files will be submitted: a file containing project code and a file containing a brief write up explaining your solution. We have included template files to be used both for the [code](https://github.com/udacity/CarND-LaneLines-P1/blob/master/P1.ipynb) and the [writeup](https://github.com/udacity/CarND-LaneLines-P1/blob/master/writeup_template.md).The code file is called P1.ipynb and the writeup template is writeup_template.md 



Writeup : [writeup.md](https://github.com/anubhav0fnu/Lane-detection-in-video-stream/blob/master/writeup.md)
---
Details about 

1. Describe the pipeline

2. Identify any shortcomings

3. Suggest possible improvements

The Project
---
**Step 1:** 
INSTALL:
1. [Anaconda](https://conda.io/docs/user-guide/install/index.html)(Just a package manager) according to O.S you want to work on. I worked on Mac OS Sierra v10.12.06. 
   Then you can Install python3.6 from conda
2. [Jupyter notebook](http://jupyter.readthedocs.io/en/latest/install.html) to write [code](https://github.com/anubhav0fnu/Lane-detection-in-video-stream/blob/master/P1.ipynb).
3. Python packages.
    conda config --add channels conda-forge
    conda install -c conda-forge matplotlib 
    conda install -c menpo opencv3
    conda install -c anaconda numpy
    conda install -c conda-forge moviepy


**Step 2:** Open the code in a Jupyter Notebook

**Step 3:** Complete the project and submit both the Ipython notebook and the project writeup

Cover these topics anubhav:

a list of files contained in the repository with a brief description of each file
any instructions someone might need for running your code
an overview of the project

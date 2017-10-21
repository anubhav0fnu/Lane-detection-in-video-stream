# **Finding Lane Lines on the Road** 
<img src="findings/Fixed-the-x&y's/whiteCarLaneSwitch_output.jpg" width="480" /> <br />
### Overview <br />
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm. <br />
In this project I used Python and OpenCV( Open-Source Computer Vision-a package that has many useful tools for analyzing images) to detect lane lines in images. <br />

---

### Writeup : [writeup.md](https://github.com/anubhav0fnu/Lane-detection-in-video-stream/blob/master/writeup.md)
Details about 

1. Describe the pipeline

2. Identify any shortcomings

3. Suggest possible improvements

4. Questions to Evaluator?

### How to run the project:
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

**Step 2:** Open the [code](https://github.com/anubhav0fnu/Lane-detection-in-video-stream/blob/master/P1.ipynb) in a Jupyter Notebook.

**Step 3:** Run it.

---

#### a list of files contained in the repository with a brief description of each file
* examples &#160; &#160; &#160; &#160;: Few initial images to play with.
* findings &#160; &#160; &#160; &#160;: contains the annotated images after manuallu fixing the x's and y's
* pipeLine-screenshots  &#160; &#160; &#160;: has images from 1-->10 explaining How the created pipeline.
* test_images           : Input images to test the pipeline.
* test_images_output    : output images after implementing pipeline
* test_videos           : Input videos to text the pipeline.
* test_videos_output    : output videos after applying the pipeline
* P1.ipynb              : My code.(mostly modular)
* README.md             : Brief overview on the project and how to run it.
* writeup.md            : Complete line by line understanding of how the pipeline has been implemented.

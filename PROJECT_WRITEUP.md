## Advanced Lane Finder

### Alex Paden

---

**SDC Nano Project 2**

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.
* Run the pipeline on given videos


### Writeup / README

#### 1. Requirements & Packages
 - Numpy
 - CV2
 - matplotlib
 - glob
 - imageio

### Camera Calibration

#### 1. Checkerboard Calibration

The code first begins by calibrating the camera using a set of checkerboard images. Using one of these images we can calculate the distortion coefficients which can be used to correct all of the possible checkerboard images as well as the car camera images.

![before-after][https://i.gyazo.com/073371b2506efdd12a58731310a47ce3.png]

### Pipeline

#### 1. Distortion-correction

To demonstrate this step, I will describe how I apply the distortion correction to one of the test images like this one:
![distortion on car][https://i.gyazo.com/8251c4dffb6f8ed30d98e9b3de4a226e.png]

#### 2. Color transforms, gradients or other methods to create a thresholded binary image.  

The code in block 5 of the jupyter notebook contains the functions used to calculate the thresholding and gradients for the images. The code is implemented individually in block 6 and in block 7 the individual thresholds are all combined using the comb_thresh() function.
![combo-thresh][https://i.gyazo.com/308b9dbb05fc9780a61f8c9e0ffba83c.png]

#### 3. Perspective Transform

The code for the perspective transform is found in block 8 and the implementation of the code is found in block 9.
The perspective transform function makes use of the cv2 warpPerspective() function and is relatively straight forward.

![perspective warp][https://i.gyazo.com/d472112427c562c30698d81227c68c8d.png]

#### 4. Lane-line pixels and fitting their positions

The lane pixel identification function can be found in block 11 and the mapping of this function can be found in block 12. The function is primarily based on the code given by udacity as it was robust enough for the task at hand. The calculations for curvature can also be found in block 11 as this was the simplest implementation while coding but retrospectively can now be seperated for simplicity and ease-of-use.

![lane_pixels][https://i.gyazo.com/782ad79ca5369b3501363d600b458026.png]


#### 5. Map to image

The final result for a single image can be found in the output of block 12

![mapped-lane][https://i.gyazo.com/0be8061814105d02e039ece37273080c.png]

---

### Pipeline (video)

#### 1. Pipeline Function

The pipeline function contains all the core functions from beginning to end given the input of a single unmodified image from the test_images folder or the given video files.


Here's a [link to my video result](./output_project_video.mp4)

---

### Discussion

In the grand scheme of things lots of small changes could be made to give some serious optimization to this project and I may return in the future to do so. A few of the major ones I outlined as TODO in my code include: 

#average previous lines for smoothing + a fail safe of any radically miscategorized lines (also cross lines on road)
#Check for similarity in left & right lines + balance the more radical using most like previous / less radical line
#simple catch for bad road mappings based on avg road width line-to-line (e.g. challenge video outputs nearly 2x wide)
#Settings could probably be optimized a bit better given some trial-and-error



Useful help from:
https://github.com/jeremy-shannon/CarND-Advanced-Lane-Lines/
https://github.com/miguelangel/sdc--advanced-lane-finding/
https://github.com/udacity/

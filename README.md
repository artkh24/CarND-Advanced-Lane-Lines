## Advanced Lane Finding

### Udacity Self Driving Car Engineer Nanodegree Project 1

---

**Advanced Lane Finding Project**

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (Image References)

[image1]: ./output_images/Undistorted_straight_lines1.jpg "Undistorted and transformed image"
[image2]: ./output_images/Thresholded_straight_lines1.jpg "Thresholded"
[image3]: ./output_images/calibration10.jpg "Image with corners"


### Camera Calibration

The code for this step is contained in the first code cell of the IPython notebook located in "Advanced Lane Lines.ipynb" 
I start by preparing "object points", which will be the (x, y, z) coordinates of the chessboard corners in the world. Here I am assuming the chessboard is fixed on the (x, y) plane at z=0, such that the object points are the same for each calibration image.  Thus, `objp` is just a replicated array of coordinates, and `objpoints` will be appended with a copy of it every time I successfully detect all chessboard corners in a test image.  `imgpoints` will be appended with the (x, y) pixel position of each of the corners in the image plane with each successful chessboard detection.  

I then used the output `objpoints` and `imgpoints` to compute the camera calibration and distortion coefficients using the `cv2.calibrateCamera()` function.  I applied this distortion correction to the test image using the `cv2.undistort()` function and obtained this result: 

![alt text][image3]

### Perspective Transform
The code for this step is contained  IPython notebook located in "Advanced Lane Lines.ipynb" 

Here and example of undistorted and transformed image
![alt text][image1] 

### Color and Gradient Threshold

I used a combination of color and gradient thresholds to generate a binary image. You can find all steps in "Advanced Lane Lines.ipynb"
I found that the combination of following color channels and thresholds identifying pretty well the lane lines
1.Sobel threshold in x  with thresholds 20,200
2. Sobel threshold in y with thresholds 20,200
3. direction of gradient 
4. magnitute of gradient
5. S color channel with range 100 255
6. L color channel with range 120 255
Here's an example of my output for this step.  

![alt text][image2]



### Finding lane lines

The code for this step is contained  IPython notebook located in "Advanced Lane Lines.ipynb" and you can see there the output images for lane curvature detection
1. Identifying peaks in a histogram to detect lane lines
2. Identifying non zero pixels arround peaks 
3. Fitting 2 order polinomial to each line
4. Calculating distance of vehicle from center
5. Calculating lane curvature radiuses




### Pipeline (video)

Here's a [link to my video result](./project_video_output.mp4)

Final pipeline includes all steps above to plot the polinomials on the image and show the lane curvature radiuses on current time

---

### Discussion

The video pipeline worked pretty good in project_video.mp4 but fails on extra video 
and the problem I guess, first is the correct region of interest definition and also if more than 2 lanes appearing in image the pipeline doesn't work.
Still not clear how can we come on with general approach for all type of lanes

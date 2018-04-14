# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project you will detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images.  

---

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe the pipeline.

My pipeline consisted of 6 steps. 
1.change the img to hsv color space
[image1]: ./examples/step01_img.jpg "step01_img.jpg"

2.modify yellow and white pixels to white and else pixels to black
[image1]: ./examples/step02_h_mask.jpg "step02_h_mask.jpg"

3.get the gaussian_blur img
[image1]: ./examples/step05_gaussian_blur.jpg "step05_gaussian_blur.jpg"

4.get the edge of the img
[image1]: ./examples/step06_canny.jpg "step06_canny.jpg"

5.clip the img
[image1]: ./examples/step07_region_of_interest_img.jpg "step07_region_of_interest_img.jpg"

6.get the lines  
[image1]: ./examples/step08_hough_lines_img.jpg "step08_hough_lines_img.jpg"

7.get the result  
[image1]: ./examples/step09_weighted_img_img.jpg "step09_weighted_img_img.jpg"


draw_lines():
```python
    imshape = img.shape
    
    for line in lines:
        for x1,y1,x2,y2 in line:
            
            k = (y2-y1)/(x2-x1) #slope
            b = y1 - k * x1 # Intercept

            if ( k < 0.8  and  k > 0.5 ) or \
                ( k < -0.5  and  k > -0.8  ): 
                    
                if b > imshape[0] or b < (imshape[0] / 2):
                    cv2.line(img, (x1, y1), (x2, y2), color, thickness)

```python


![alt text][image1]


### 2.Potential shortcomings with my pipeline

The output lines are not completing when line segments are in the pictures


### 3. Possible improvements to my pipeline

Use the slope and the intercept to caclulate the lane lines

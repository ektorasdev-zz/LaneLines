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

My pipeline is constructed as follows:
    ### GrayScale
    First of all we make a copy of the image, so we do not modify the original. Then by using the cv2.cvtColor function we convert the
    image to grayscale.
    
    ### Gaussian Blur
    Then we take the grayscaled image and by adjusting a specific kernel size of 15 we create a gaussian smoothing.
    
    ### Canny
    Then on the blurred image we define low and high thresholds of 20 and 100 respectively and then apply a canny edge detection.
    
    ### Region of Interest
    Then with the canny edges we define the masking in the region we want to apply the lines.
    
    ### Hough Transform
    Then by taking the masked region, we apply parameters to create the Hough transform. The parameters applied to create the transform
    were the following. The distance resolution(rho) = 1, angular resoluton(theta) = np.pi/180, Hough intersection(threshold) = 10,
    minimum pixel number = 20, maximum pixel gap = 1.
        
    ### Draw_Lines()
    To apply the hough transform and draw the lines on the images, the draw_lines function was modified by firstly finding the slope and
    separating the right and left lanes. Then by finding the average of the x and y values of each line we apply the cv.line function which
    draws a red colored straight line on the left and right lanes.


### 2. Identify potential shortcomings with your current pipeline

Some potential shortcomings would be if for example the lines were not well colored on the image and so the algorithm wouldn't be able to draw an accurate space. Another example would if there was another car close to our car and so there wouldn't be enough space to mask the region and so the lines would not be created accurately.


### 3. Suggest possible improvements to your pipeline

An improvement would definitely be need in the draw lines function because the lanes can't be accurately classified in the challenge video
and the result is that it adentifies the concrete wall as a line and draws a line on that too. We can even try to make the lines more stable on the lanes because they are still a little shaky and that might affect the result in a curved road for example.

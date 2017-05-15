# Vehicle Detection Project

Introduction
---

The goals / steps of this project are the following:

* Perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a classifier Linear SVM classifier
* Optionally, you can also apply a color transform and append binned color features, as well as histograms of color, to your HOG feature vector. 
* Note: for those first two steps don't forget to normalize your features and randomize a selection for training and testing.
* Implement a sliding-window technique and use your trained classifier to search for vehicles in images.
* Run your pipeline on a video stream (start with the test_video.mp4 and later implement on full project_video.mp4) and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles.
* Estimate a bounding box for vehicles detected.

[//]: # (Image References)

[image1]: ./output_images/car_noncar.png "car_noncar"
[image2]: ./output_images/windows.png "windows"
[image3]: ./output_images/heatmap.png "heatmap"
[image4]: ./output_images/labels.png "labels"
[image5]: ./output_images/thresholded.png "thresholded"
[image6]: ./output_images/test_images.png "test_images"
[video1]: ./project_video_output.mp4 "Video"


Histogram of Oriented Gradients (HOG)
---

I started by reading in all the `vehicle` and `non-vehicle` images. I then explored different color spaces and different `skimage.hog()` parameters (`orientations`, `pixels_per_cell`, and `cells_per_block`).  I grabbed random images from each of the two classes and displayed them to get a feel for what the `skimage.hog()` output looks like.

Here is an example of car and non-car class using the `RGB` color space and HOG parameters of `orientations=9`, `pixels_per_cell=(8, 8)` and `cells_per_block=(2, 2)`:

![alt text][image1]

I tried various combinations of parameters before finalizing the HOG parameters. I settled on my final parameters based on the accuracy from SVM classifier. My final configuation was: YCrCb colorspace, 9 orientations, 8 pixels per cell, 2 cells per block, All channels for hog.

Classifier
---

I used a linear SVM classifier with default parameters. I used HOG features along with spatial intensity and channel intensity histogram features. I got test set accuracy of 99.38% with the following configuration:  

colorspace:  YCrCb 
orientations:  9 
pixels per cell:  8 
cells per block:  2 
hog channel:  ALL 
spatial size:  (32, 32) 
histogram bins:  32

Sliding Window Search
---

Removing False Positives
---

Discussion
---

Video Implementation
---
Here's a [link to my video result](./project_video_output.mp4)



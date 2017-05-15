# Vehicle Detection Project

Introduction
---

The goals / steps of this project are the following:

* Perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a classifier Linear SVM classifier
* Apply a color transform and append binned color features, as well as histograms of color, to HOG feature vector. 
* Normalize features and randomize a selection for training and testing.
* Implement a sliding-window technique and use the trained classifier to search for vehicles in images.
* Run the pipeline on a video stream and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles.
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

I tried various combinations of parameters before finalizing the HOG parameters. I settled on my final parameters based on the accuracy from SVM classifier. 

Classifier
---

I used a linear SVM classifier with default parameters. I used HOG features along with spatial intensity and channel intensity histogram features. 

I got test set accuracy of 99.38% with the following configuration:  
* colorspace:  YCrCb 
* orientations:  9 
* pixels per cell:  8 
* cells per block:  2 
* hog channel:  ALL 
* spatial size:  (32, 32) 
* histogram bins:  32

The code for this section can be found in 13th cell of vehicle_detection.ipynb

Sliding Window Search
---

The method find_cars in the cell 16 of vehicle_detection.ipynb combines HOG features extraction with sliding window search. Instead of performing feature extraction on each window individually, the HOG features are extracted for the entire image and then these features are subsampled according to the size of the window and the fed to the classifier. This saves alot of computation time. The method performs the classifier prediction on the HOG features for each window region and returns a list of rectangle objects corresponding to the windows that generated a positive prediction.

The image below shows output of find_cars on one of the test images:


![alt text][image2]


Removing False Positives
---

As we can see there is a false positive in the above image. I built a heat-map from these detections in order to combine overlapping detections and remove false positives. To make a heat-map, I simply added "heat" (+=1) for all pixels within windows where a positive detection is reported by the classifier. 

The heatmap for the above image look like this:


![alt text][image3]


I thresholded that heatmap to identify vehicle positions.  I then used `scipy.ndimage.measurements.label()` to identify individual blobs in the heatmap. 


The thresholded image for the above heatmap look like this:


![alt text][image4]



By using this technique the result of detection on some test images look like this:


![alt text][image5]



For thr video I integrated the heat map over several frames of the video, so that areas of multiple detections get "hot", while transient false positives stay "cool".

Discussion
---

Video Implementation
---
Here's a [link to my video result](./project_video_output.mp4)



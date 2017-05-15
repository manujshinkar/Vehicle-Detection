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

[image1]: ./images/undistort_output.png "Undistorted"
[image2]: ./images/undistorted.png "Road Transformed"
[image3]: ./images/gradient_threshold.png "Binary Example"
[image4]: ./images/warped.png "Warp Example"
[image5]: ./images/threshold_warped.png "Thresholded Warped"
[image6]: ./images/histogram.png "Histogram"
[image7]: ./images/sliding_window.png "Sliding Window"
[image8]: ./images/previous_polyfit.png "Previous Polyfit"
[image9]: ./images/lane_information.png "Lane Information"
[video1]: ./project_video_output.mp4 "Video"


Histogram of Oriented Gradients (HOG)
---

Classifier
---

Sliding Window Search
---

Removing False Positives
---

Discussion
---

Video Implementation
---
Here's a [link to my video result](./project_video_output.mp4)



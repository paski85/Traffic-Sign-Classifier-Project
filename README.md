#**Traffic-Sign-Classifier-Project**

In this project, you will use what you've learned about deep neural networks and convolutional neural networks to classify traffic signs. Specifically, you'll train a model to classify traffic signs from the German Traffic Sign Dataset.

---

###1. SETUP
Some issues getting Tensorflow-GPU working.
CUDA CuDNN vs. 5.1 dll required in CUDA folder
Restart of KERNEL necessary several times before CUDA was functioning.

###2. Data import and visualization
Class sizes are very uneven from 60 to 750.
Attempt to augment dataset using tf.image.random_flip_up_down(image, seed=None) or tflearn.data_augmentation.DataAugmentation (self) unsuccesful

###3. Data preparation
Grayscaling and normalization were helpful in bringing the accuracy from .87 to >.9






Sources:




Original frame is imported:

![Alt text](./Pipeline/1_import.png?raw=true "Original Input image")

Frame is grayscaled:

![Alt text](./Pipeline/2_grayscale.png?raw=true "Grayscaled")

Gaussian blur is applied to reduce noise:

![Alt text](./Pipeline/3_blur_gray.png?raw=true "Gaussian blur to reduce noise")

Canny Filter is applied to detect edges:

![Alt text](./Pipeline/4_canny.png?raw=true "Canny Filter")

ROI from (bottom_left) (max_x/2-x_res/50, .6*max_y) (max_x/2+x_res/50, .6*max_y) (bottom_right):

![Alt text](./Pipeline/5_canny_roi.png?raw=true "ROI applied to Canny Filter")

* Hough results are filtered according to slope ((y2-y1)/(x2-y2)) (positive right line/negative left line)
* Vertical and Horizontal slopes are filtered out
* The mean slope and standard dev is calculated
* Outliers of mean+2_standard_devs are excluded
* Mean slope is recalculated for left and right lines
* Mean y-intercept is calculated
* Lines starting from the bottom edge, going to .6*max_y are calculated using the mean left and right slope and y_intercept y=mx+b
* A circular buffer of the mean left and right slopes of the last ten frames is kept to filter out outliers

![Alt text](./Pipeline/6_lines_from_hough.png?raw=true "Hough Lines")

The resulting lines are overlaid onto the original input image

![Alt text](./Pipeline/7_overlaid.png?raw=true "Hough Lines applied on input image")


---

### Reflection



###2. Identify potential shortcomings with your current pipeline

* The current pipeline is jittery at times.


###3. Suggest possible improvements to your pipeline

* To improve performance a check on the line y-intercept and a ring buffer of sensible y-intercepts could be kept from frame to frame.
* y-intercepts can only change as fast as a lane change (e.g. 1000 pixels/s->25 pixels/frame-to-frame) 
* Confidence in the lane could be color-coded (e.g. how many hough lines are detected)



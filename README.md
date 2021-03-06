# **Behavioral Cloning**

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report


<!-- [//]: # (Image References)
center,left,right,steering,throttle,brake,speed
[image1]: ./examples/placeholder.png "Model Visualization"
[image2]: ./examples/placeholder.png "Grayscaling"
[image3]: ./examples/placeholder_small.png "Recovery Image"
[image4]: ./examples/placeholder_small.png "Recovery Image"
[image5]: ./examples/placeholder_small.png "Recovery Image"
[image6]: ./examples/placeholder_small.png "Normal Image"
[image7]: ./examples/placeholder_small.png "Flipped Image" -->

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.  

---
### Files Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* model.py containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network
* README.md summarizing the results

#### 2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing
```sh
python drive.py model.h5
```

#### 3. Submission code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

My model consists of a single convolution layer with 5x5 filter size and depths 15

The model includes RELU layers to introduce nonlinearity and the data is normalized in the model using a Keras lambda layer.

#### 2. Attempts to reduce overfitting in the model

The model was trained and validated on different data sets to ensure that the model was not overfitting. The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.

#### 3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually.

#### 4. Appropriate training data

Training data was chosen to keep the vehicle driving on the road. I used a combination of center lane driving, recovering from the left and right sides of the road by adding 0.4 and -0.3 to the steering angle of the that particular image respectively.

For details about how I created the training data, see the next section.

### Model Architecture and Training Strategy

#### 1. Solution Design Approach

The overall strategy for deriving a model architecture was to drive a car through any road condition being presented in either track.

My first step was to use a convolution neural network model similar to the the one created by Nvidia. I thought this model might be appropriate because it was applied on real life autonomous driving conditions. However, for our simulated case, I resulted to simplifying the architecture by reducing the convolutional and dense layers. In order to gauge how well the model was generalizing, I split my image and steering angle data into training and validation set. I found that my training set had a low MSE while the validation set had a high MSE implying my model was overfitting. To combat the overfitting, I modified the model by adding a dropout and max pooling layer followed by a convolution layer.

The final step was to run the simulator to see how well the car was driving around track one. There were a few spots where the vehicle fell off the track. This was resolved by augmenting the left and right image data, and also the steering angles. This improved our model.

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

#### 2. Final Model Architecture

The final model architecture `(model.py lines 56-62)` consisted of data preprocessing, Convolution2D, Dropout, MaxPooling2D and Dense layers. 3x3 filter sizes were used by the convolutional layer.



#### 3. Creation of the Training Set & Training Process

Here are examples of the original left, center and right camera images further processed:

<img src="rpt_imgs/left_original.png" width="250" /> <img src="rpt_imgs/center_original.png" width="250" /> <img src="rpt_imgs/right_original.png" width="250" />

Below are examples of augementation steps carried out on the center, left and right camera images such as cropping and resizing image to `(32,32,3)`:

<img src="rpt_imgs/left_crp_resized.png" width="200" /> <img src="rpt_imgs/center_crp_resized.png" width="200" /> <img src="rpt_imgs/right_crp_resized.png" width="200" />



I used an Adam optimizer and mean squared error metric as the loss function. Although the model was trained for 2 epochs, it performed very well and autonomously drove around the first track without skidding off the road.

Attached is a [Link to youtube video](https://youtu.be/pqeIWHmC8-M) of the car driving autonomously without leaving the road.

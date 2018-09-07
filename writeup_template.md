# **Behavioral Cloning** 

## Writeup 
---

**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/model_visual.png "Model Visualization"
[image2]: ./examples/left.jpg "left camera"
[image3]: ./examples/center.jpg "center camera"
[image4]: ./examples/right.jpg "right camera"
[image5]: ./examples/MSE_final.png "Mean Square Error"
[image6]: ./examples/placeholder_small.png "Normal Image"
[image7]: ./examples/placeholder_small.png "Flipped Image"

#### Files Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* model.py containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network 
* writeup_report.md or writeup_report.pdf summarizing the results
* video.mp4 - A video recording of vehicle driving autonomously one lap around the track one.

#### 2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing 
```sh
python drive.py model.h5
```

#### 3. Submission code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

### Model Architecture and Training St
gy

#### 1. An appropriate model architecture has been employed
This model is adapted from NVIDIA end-to-end behaviour learning model. The original model consists of 6 convolutional layers for feature extraction and 3 fully connected layers as "controller". This model requires relatively small training set, which is suitable in our application.


#### 2. Attempts to reduce overfitting in the model

The model contains dropout layers in order to reduce overfitting. The dropout rate is around 0.28. Dropout was added between fully connected layers. 

 The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.


#### 3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually.

#### 4. Appropriate training data

Training data was chosen to keep the vehicle driving on the road. I used a combination of 
* center lane driving
* extreme left turn (after bridge)
* counter turn (right turn)
* Sample data from Udacity

For details about how I created the training data, see the next section. 

### Model Architecture and Training Strategy

#### 1. Solution Design Approach

The overall strategy for deriving a model architecture was to ...

My first step was to use a convolution neural network model similar to the nvidia, thought this model might be appropriate because ...

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I found that my first model had a low mean squared error on the training set but a high mean squared error on the validation set. This implied that the model was overfitting.


Then I added dropout rate between layers to combat overfitting. 

The final step was to run the simulator to see how well the car was driving around track one. 

There were a few spots where the vehicle fell off the track... 
The first spot that the vehicle fell of the track was after the bridge where it didn't turn enough and went into the sand. 



To improve the driving behavior in these cases, I added a few more training data on the extreme turns to teach the model. 


At the end of the process, the vehicle is able to drive autonomously around the track 1 without leaving the road.


#### 2. Final Model Architecture

The final model architecture (model.py lines 18-24) consisted of a convolution neural network with the following layers and layer sizes ...

Here is a visualization of the architecture


![alt text][image1]

#### 3. Creation of the Training Set & Training Process

The basic edition of the training set only included the center lane. It handled the straining line and small turns well but couldn't turn properly
on larger turns. An example image of center lane driving was as following:
![alt text][image3]


Then I added the left and right sides of images to the training set and with a correction in the angle. The example images with
a turning angle of ~0.18 are shown as following:

![alt text][image2]
![alt text][image4]

Since the correction of turning angle was a intuitive guess, few iterations of tuning were done to get a proper value. 0.31 turns out to be a good guess in the current model archetecture.


To augment the data set, I flipped the images and reversed the angles. An example is shown below: 

To expand the size of training set, I also included the sample data provided by udacity course. This concludes to a 
data set of 58000. 10% of the data were excluded as validation data. 

An adam optimizer was used to choose the learning rate. 
### Results
As shown in video.mp4, the car is able to navigate correctly on test data without leaving the drivable portion of the track surface. The mse error on training and validation sets are shown in the following figure:
![alt text][image5]




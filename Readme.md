# Udacity Self-Driving Car Engineer Nanodegree

## Project 3 - Use Deep Learning to Clone Driving Behavior

### 1. Model Architecture Design Approach

First of all, it was taken for granted that the model architecture should be a variation of LeNet. That is, the model should consist of convolutional layers that elicit features from input images, and fully connected layers to fit features to expected output. 

A minialistic model with one convolutional layer (plus pooling and relu) and two fully connected layers was built and tested. It was shown that the model could fit a few sample input images, and output a steering angle in the correct direction. The model was then modified and tuned with a series of trials and errors, until finally could drive the car smoothly in endless laps.

Below is a list of things that have been excercised in order to achieve the final model. Note that data augmentation and model tuning experiments were carried out in parallel because sometimes it was not clear whether lack of good data or model flaw caused a problem.  

#### 1. Augmenting data by using side camera images: 
Images of all three camperas are utilised. When using a side camera image, the corresponding steering angle is modified towards the centre. This showed improvement on keeping the car at the centre of the road. 

#### 2. Augmenting data by flipping images left to right: 
Each input image is flipped left to right to fabricate a new input.

#### 3. Adding fully connected layers: 
Too many fully connected layers or neurons at each layer did not seem to have any impact on driving simulation, nor even validation error. The final model only kept 3 fully connected layer of 256, 128 and 1 neurons.

#### 4. Adding convolutional layers:
With 3 convolutional layers, training quickly converged after a couple of epoches, while validation error is relatively high. It was then found that the 3rd convolutional layer outputed all black images, thus it was removed since its neurons could not be activated. While the 2nd layer was proved to be helpful when in the image the road and adjacent area are similar in some image channels (such as similar satuation), usually during a section of road not clearly marked with lane lines.

#### 5. Adding correctional data:
During simulation the car sometimes went off the road due to under steering. Additionl training data of a few hundred images specific for the particular corner were created using the simulator.

### 2. Model Architecture
The model architecture is described by the table below. It is fairly simple, consisting only 2 convolutional and 3 fully connected layers. The convolutional layers are non-striding and only reduced in size by max pooling. This causes the adjacent fully connected layer to have a relatively large number of parameters. 

| Layer Type | Output Shape | Param # |
| :--- | :--- | ---: | :--- |
| Lambda | (None, 50, 160, 3) | 0 |
| Convolution 2D | (None, 48, 158, 16) | 448 |             
| MaxPooling 2D | (None, 24, 79, 16) | 0 |       
| Relu | (None, 24, 79, 16) | 0 |      
| Convolution 2D | (None, 22, 77, 8) | 1160 |         
| MaxPooling 2D | (None, 11, 38, 8) | 0 |
| Relu | (None, 11, 38, 8) | 0 |
| Flatten | (None, 3344) | 0 |
| Dropout | (None, 3344) | 0 |
| Dense | (None, 256) | 856320 |
| Dropout | (None, 256) | 0 |
| Dense | (None, 128) | 32896 |
| Dropout | (None, 128) | 0 |
| Dense | (None, 1) | 129 |
Total params: 890953

### 3. Data and Training
As discussed above, most of the training data came from project designer's sample data set. Images of all 3 camera were utilised, and augmented by flipping each image left to right. As a result, the model is trained against more than 40,000 distinct images. Additional data were gathered using the simulator (controlled by keyboard) for a couple of corners, to rectify under steering at those corners.

In the provided sample data set, the steering angle and speed are both 0, when the car was entering the corner. These inputs were not used for training.

![Provided sample image](./center_2016_12_01_13_31_13_177.jpg)

Additional data were created driving around this corner. The provided data also lacked images taken while the car is in the corner, like the one below:

![Additional training image](./center_2017_01_10_21_11_14_475.jpg)

The model was trained on an AWS EC2 Udacity CarND image. The weights were saved after 10 epoches of training. Each epoch took under 130 seconds to run.

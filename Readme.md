### 1. Model Architecture Design Approach

First of all, it was taken for granted that the model architecture should be a variation of LeNet. That is, the model should consist of convolutional layers that elicit features from input images, and fully connected layers to fit features to expected output. 

A minialistic model with one convolutional layer (plus pooling and relu) and two fully connected layers was built and tested. It was shown that the model could fit a few sample input images, and output a steering angle in the correct direction. The model was then modified and tuned with a series of trials and errors, until finally could drive the car smoothly in endless laps.

Below is a list of things that have been excercised in order to achieve the final model:

#### 1. Augmenting data by using side camera images: 
Images of all three camperas are utilised. When using a side camera image, the corresponding steering angle is modified towards the centre. This showed improvement on keeping the car at the centre of the road. 

#### 2. Augmenting data by flipping images left to right: 
Each input image is flipped left to right to fabricate a new input.

#### 3. Adding fully connected layers: 
Too many fully connected layers or neurons at each layer did not seem to have any impact on driving simulation, nor even validation error. The final model only kept three fully connected layer of 256, 128 and 1 neurons.

#### 4. Adding convolutional layers:

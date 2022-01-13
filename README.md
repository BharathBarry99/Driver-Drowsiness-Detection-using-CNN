# Driver Drowsiness Detection using CNN
 With the help of tensorflow and keras ,this model can detect if the driver is drowsy on not and prevent him from unexpected accidents.

 The code is shared as "Driver Drowsiness Detection using CNN.ipynb" (.ipynb file) and the dataset used is in the folder "IMAGES"
 
## Abstract 
According to the National Highway Traffic Safety Administration, 91,000 crashes involving drowsy drivers occur each year, resulting in 50,000 injuries and roughly 800 deaths. In addition, one out of every 24 adult drivers had fallen asleep behind the wheel in the last 30 days. According to studies, sleeping for more than 20 hours is similar to having a blood alcohol concentration of 0.08 percent. 
Here, i deceided to construct a neural network that can detect if eyes are closed and, when combined with computer vision, can detect if a real individual has had their eyes closed for more than 2 secondw. Anyone interested in better driving safety, including commercial and everyday drivers, automobile firms, and vehicle-insurance companies, can benefit from this technology.
For this project, we will collect data, analyse the data, pre-process the data, create a convolutional neural network, construct a model architecture, save the model, and create a webcam to monitor the driver's drowsiness.

## Face Recognition Library in Python
I used face recognition library from python to detect faces and manipulate the images for training and testing. Facial recognition is a method of recognizing or verifying a person's identification by looking at their face. People can be identified in pictures, films, or in real-time using facial recognition technology. Biometric security includes facial recognition. Voice recognition, fingerprint recognition, and ocular retina or iris recognition are all examples of biometric software. Although the technology is mostly utilised for security and law enforcement, there is growing interest in other applications.
Face recognition technology is well-known to many people thanks to FaceID, which is used to unlock iPhones (however, this is only one application of face recognition). Typically, facial recognition does not need a large database of images to identify an individual's identification; instead, it merely identifies and recognises one person as the device's only owner, while restricting access to others.


## Data collection
I used full facial data from a variety of sources, including UMass Amherst open eye face data and Nanjing University closed eye face data. The eyes were then cropped out of the dataset using a simple python script, leaving us with a total of over 4382 cropped eye images. We added a buffer to each image crop to capture not only the eye but also the area around it. This cropping feature will be used in the webcam section later.

## Data pre-processing 
Pre-processing is a necessary step before the data set is fed into the model. Each image of train and test set are converted into an appropriate matrix size and format that converts the class labels into a one-hot encoding vector. Gray scaling and lighting included.

![image](https://user-images.githubusercontent.com/97673902/149390646-d54ac650-6fd4-492f-a7a8-24b4028a70d1.png)


## Creating A Convolutional Neural Network

# Convolutional Layers:
This layer, rather than creating the entire image, produces sections of pixels, allowing for speedier models. This could be more or less dense than the original photos, depending on how many filters we use, but it will allow the model to learn more complex associations with fewer resources. We used 32 filters in total. Use at least one convolutional layer, and two or more is usually recommended. Two 3x3s pooled together followed by three 3x3s pooled together was the best setup for me. The use of a smaller filter size is becoming more common in CNNs. In truth, a double 3x3 layer is nearly identical to a 5x5 layer, but it is faster and often yields superior results. Pooling isn't always necessary or beneficial.

#Flatten
Flatten the image array so it can enter the dense layers.

# Dense Layers
More dense the layers are, the longer our model will take to train. As the number of neurons in these layers increases, the complexity of the relationships learned by the network will increase. Generally, the idea of convolutional layers is to avoid having to make an overly deep dense layer scheme. For our model we used three layers with relu activation at a decreasing rate of neurons (78, 78, 32). We also used a 30% dropout after each layer.

# Output Layer
Finally, because this a binary classification problem, make sure to use the sigmoid activation for our outer layer. Because we care more about forecasting the positive class (a sleeping driver) than the negative class (an awake driver), recall will be our most important statistic (sensitivity). The stronger the recall, the fewer sleeping motorists the programme incorrectly guesses are awake (false negatives). 
The only issue is that our positive class outnumbers our negative class by a large margin. As a result, it's preferable to utilise the F1 score or Precision-Recall AUC score, because they account for the number of times, we think a driver is sleeping but is actually awake (precision). Otherwise, our model will always assume we are sleeping and will be useless.

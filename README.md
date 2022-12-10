# Challenge - Computer Vision Intern


### Topic: Classifying the visibility of ID cards in photos.

### Resources: You can use any resources to complete this task.

### Deliverable: Jupyter notebook or a folder containing all your code and documentation.

### It should explain the steps you’ve taken

### The Task: EXPLORATION, ANALYSIS, MODELLING & OPERATIONALIZATION 


### The folder images inside data contains several different types of ID documents taken in different conditions and backgrounds.

### The goal is to use the images stored in this folder and to design an algorithm that identifies the visibility of the card in the photo (FULL_VISIBILITY, PARTIAL_VISIBILITY, NO_VISIBILITY).


### To understand what each visibility type means, consider the following examples :

![Example ids](https://user-images.githubusercontent.com/110006271/206835704-f83557cb-7516-4719-9ef7-25e06cc0630d.jpg)





### FULL_VISIBILITY PARTIAL_VISIBILITY NO_VISIBILITY


### FULL_VISIBILITY means the card is completely shown; PARTIAL_VISIBILITY means part of the card is clipped;

### while NO_VISIBILITY means the card does not appear in the image at all.

### We have provided you with the ground truth labels corresponding to each image data in folder
data, file gicsd_labels.csv.

### The name of each file is


### GICSD_{CARD_ID}_{BACKGROUND_ID}_{IMAGE_ID}, and you can use this information to make decisions about your approach if you so desire.


### Unfortunately, the sensor used when taking these photos was damaged and the photos are corrupted, as the images below show:


![Example 1](https://user-images.githubusercontent.com/110006271/206835779-5a129ac7-47b8-4ae7-9d84-a5d8ed65a98f.jpg)


### It’s up to you to figure out the best way of handling this situation, but to guide you through 
  
  this challenge you should refer to the following sub-tasks:

# a) Data Exploration

  --> i) Explore all the available data. What are your preliminary observations?

# b) Feature Engineering

  --> i) Utilizing some of your findings from part a) create a function that transforms an image (in the format of a numpy array) into a single-channel image.
  
  --> Explain the approach used to achieve this.

# c) Model Selection/Validation

  --> i) Create an ML model which classifies the visibility (FULL_VISIBILITY, PARTIAL_VISIBILITY, NO_VISIBILITY) of the card in the photo.
  
  --> This model must take a single-channel image as input. Justify the choices behind the model and assess the quality of your results.
  
  
  --> ii) Make a train.py module which pulls the raw ids from the CSV and generates the fitted model artifact.
  
     (it should be stored under the artifacts sub-directory).

# d) Operationalization
  
  --> i) Make a predict.py module and write a function that accepts the original RGB (3-channel) images and goes through the Feature Engineering and Inference pipelines to yield the predicted result.


# Step by step approach of this models:

  --> I have used multilogit regression without any extra transformations on the images, which yielded AUC on the training set,
  
  --> further oversampling and augmentation didn't raise the score much higher.

  --> The main approach to modelling would be to use a Convolutional Neural Network which can extract regional information and is much more robust to variations in the images.
  
  -> Given the time limitations of the task, relatively small amount of images we have (only 800 images in total of which 600 fall into training set) and strong variations in the background that is not evenly distributed among target classes, the best course of action would be to apply transfer learning so that the network can build on the already trained layers that recognize shapes, textures and forms.
  
  --> As a backbone I used ResNet50, which provides a deeper network at smaller computational expense by introducing skip connections which also mitigate the problem of vanishing gradient.

  --> The backbone is followed by three Dense layers with dropout for regularization and a dense output layer with softmax activation.

  --> Loss: Categorical cross entropy.
  
  
## Import all required packages

## Working directories and read the data

## **a) Data Exploration**

---


###i) Explore all the available data.

---


## Metadata are included in the image file name column of the dataset in the form 'GICSD_{CARD_ID}_{BACKGROUND_ID}_{IMAGE_ID}'.


## Checking the Images

### Result is only we've seeing noise.

### Image in the channel B is looks good in grayscale.

## Whether the actual image is always encoded in the **B** channel we make the following simplifying assumption:

#### The median (absolute) correlation among the rows in the image matrix is going to be maximum in the channel containing structured information.

### If a channel only contains random pixels, the median absolute correlation among the rows in the image matrix should be low. 

### On the other hand, when a channel encodes an actual image, we can expect the presence of some structured information to increase the medain absolute correlation.

### We can use this heuristics to see which channels contain the image we have to classify.

# Preliminary observations

---


## Total of 800 images available in the dataset All images have the same size of 192x192 pixels

### The image filenames are unique IDs matching to df.IMAGE_FILENAME df.LABEL values had whitespaces which were trimmed No missing values in .csv

### 646 out of 800 (0.801) images have ID cards with FULL_VISIBILITY

### 123 out of 800 (0.154) images have ID cards with PARTIAL_VISIBILITY

### 31 out of 800 (0.039) images have ID cards with NO_VISIBILITY

# Feature Engineering

### 4 images have an ax median correlation in a channel different from **B**.

### However, a visual inspection of these 4 images shows the relevant information is encoded in the **B** channel for them as well.

### Given that all the relevant information has been found in channel B for all the images in the dataset let's **assume** the following:  

### **Images in production setup will also contain useful information only in channel B**

### Inspecting the transformations above visually suggests that contrast stretching helps to distinguish between the background and the id card better than in the original image. it also doesn't distorting the information on the ID like in case of Histogram Equalization(HE) and Adaptive HE.

### Therefore it looks like a good approach to apply as part of image preprocessing.

## Train-test split

### Split the data into training and test set.

# Model

## The model is petty confidnt predicting.

## Model Evaluation:

  --> In this model for trained and test set. we've use AUC model to check the accuracy of this model evaluation.
  
  --> We ca see less accuracy of this model.
  
  --> We've to train it on more epochs.

  --> We've to use more model.fit_generator for more validation score.



## Model optimization:

---


## Add early stopping to prevent overfitting.

##Create a Deep CNN architecture from scratch, train it on more epochs.

## In this model i've use very less amount of CNN arichtecture used. 

## In future we've to use more CNN architecture for more validation score.


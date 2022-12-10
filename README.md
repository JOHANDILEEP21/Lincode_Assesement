# Challenge - Computer Vision Intern


# Topic: Classifying the visibility of ID cards in photos.

# Resources: You can use any resources to complete this task.

# Deliverable: Jupyter notebook or a folder containing all your code and documentation.

## It should explain the steps you’ve taken

# The Task: EXPLORATION, ANALYSIS, MODELLING & OPERATIONALIZATION 


## The folder images inside data contains several different types of ID documents taken in different conditions and backgrounds.

## The goal is to use the images stored in this folder and to design an algorithm that identifies the visibility of the card in the photo (FULL_VISIBILITY, PARTIAL_VISIBILITY, NO_VISIBILITY).


## To understand what each visibility type means, consider the following examples :

![Example ids](https://user-images.githubusercontent.com/110006271/206835704-f83557cb-7516-4719-9ef7-25e06cc0630d.jpg)





## FULL_VISIBILITY PARTIAL_VISIBILITY NO_VISIBILITY


## FULL_VISIBILITY means the card is completely shown; PARTIAL_VISIBILITY means part of the card is clipped;

## while NO_VISIBILITY means the card does not appear in the image at all.

##We have provided you with the ground truth labels corresponding to each image data in folder
data, file gicsd_labels.csv.

## The name of each file is


## GICSD_{CARD_ID}_{BACKGROUND_ID}_{IMAGE_ID}, and you can use this information to make decisions about your approach if you so desire.


## Unfortunately, the sensor used when taking these photos was damaged and the photos are corrupted, as the images below show:


![Example 1](https://user-images.githubusercontent.com/110006271/206835779-5a129ac7-47b8-4ae7-9d84-a5d8ed65a98f.jpg)


## It’s up to you to figure out the best way of handling this situation, but to guide you through 
  
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



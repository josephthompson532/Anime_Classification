# Image_Tag_Classification


## Purpose
The purpose of this project was to experiment using transfer learning with keras cor classification. Given a collected, labeled series of images, can we predict correctly if the image contains a given object. While, the scraping algorithm written here is setup to scrape any tag given to it in the form of an argument, this exchibition will focus on correctly classifying the presence of the character "Asuka Langely Soryu" from the hit Japanese TV show Evangelion. 

## Overview
To train a convolutional neural network using Keras, the images must be organized into a specific file structure: 
"{tag_name}/{test/train}/{example_of_label/not_example_of_label}"

### Scraping
Since there were no image repositories on kaggle and a multitude of other dataset repositories that had these images labeled, I created a scraping script using splinter and beautiful soup to scrape and label the images appropriately from an anime image repository "safebooru.org".

(NOTE/DISCLAIMER: While this imageboard is supposed to be only "safe for work" images, upon analysis it became evident this was not always so, as tends to be the case with any imageboard despite the moderators best efforts.)

The script is set up to scrape any tags given to it as an argument in the form of a list. You can scrape 1 tag at a time into the proper file structure, or 1,000, it makes no difference (with runtime being the exception).

### Exploratory Analysis of Image Dimensions
Once the data was scraped I looped through the images to see if there was an average image shape I could use for the images to save training time. There was quite a large spread of dimensions among the images, as is to be expected when scrpaing data from an imageboard. It is important to not undershoot the image dimension size, because the character we are searching for is more often than not, not centered in the middle of the frame. Using Seaborn, I plotted out the spread of the image dimension sizes. I chose a dimension size on the upper end of what we see in the spread of data: (1000,1500,3) to make sure the characters face is always somewhere in our image.

### Image Generator
Next, I created an image generator using keras for the training and validation sets. Traits it will alter include rotation 20 degrees, width and range shift of 0.1, shear range of 0.1, zoom_range of .1 and horizontal flip with mode set to nearest. The image data generator will rescale the data to between 0 and 1 as well.

# The Models
For the modeling portion of the project, I tested two model infrastructures, AlexNet and VGG19. In my models I used early stopping based on minimizing validation loss. Both models have a batch_size of 16. We are attempting binary classification between "Asuka present" and "Asuka not present". 

### Evaluation
To evaluate the model I used a confusion matrix and classification report. Our goal will be accuracy, as well as precision. While the model may not capture every instance of an Asuka image, all images it classifys as Asuka I want to be correctly her.

## Results

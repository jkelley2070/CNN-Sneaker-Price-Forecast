# CNN-Sneaker-Price-Forecast

## Goal
The goal of this project is create a after market sneaker price forecaster using convulutionary neural networks and transfer learning. We are going to be using vgg-16
model for transfer learning.

## Project Plan
The project plan can be found at the following link 
[ExcaliDraw](https://app.excalidraw.com/s/CmEgiggUrt/79jFijhFFDF)
(this link is subscription based and might not be avaiable in the future
so I am pushing the excalidraw and svg to this repo)
1. This describes in detail the plan for project
2. Well Illustrated Basics of Tensors, Neural Networks, and CNN
3. Explanations into transfer learning and the application to this problem


# FILE BREAKDOWN DATA

## Webscraping.ipynb
* This jupiter notebook covers static and dynamic webscraping 
* We are webscraping the data for better balancing and up to date information, i.e
there are datasets that exist for this problem, but creating our own allows us 
more control!
* The data is scraped from GOAT, a aftermarket, reselling site
    * Each sneaker on this website is unique, and contains high quality images
    and up to date price data so this is the perfect choice. 
    * Goat is dynamically loaded and all postings our listing on a single page,
    and loaded by infinitely scrolling
    * This infinitely scrolling caused some problems due to time complexity
    so the problem was solved slightly different
    * Instead of taking all sneakers and listing possible or up to a certain point,
    we took 25 popular models, and used goats search and filtering system
    to scape each model at a time

## Products_Updated.csv
    * The Webscraped data from 25 most popular models
    * Originally 25 csvs, but combined into 1
    * The data contains titles, image links, and prices in the format:
    Title Image Price  

# FILE BREAKDOWN DATA PREPROCESSING

## DataCleaning.ipynb
    * So we are have our Products_Updated but we must prepare it for our model
    * Part 1: Prepare Response
        * We must turn the prices into categories
        * We can do this to ways
            1. Balanced - Using Quantiles (Perfectly Distributed)
            2. Unbalanced - User Choise (Unknown Distribution)
        * We can create both of these vectors using one hot encoding and 
        some other techniques
        * We can store both vectors and the other df data in a file df allowing
        us to use in the future
    * Part 2: Prepare Images
        * These images have to downloaded from the link using python but
        before that we have to decide how to store it
        * Tensorflow binary is the best choice for this problem, due to csvs struggling with high dimensional data (They store it as a string), and
        the small storage size
        * We are going to need to write code to encode these things, and decode this things out of the binary, which can be tricky, 
        * While we are writing to this binary file we can
            * Download the image
            * Change the shape to (224,224)
            * Remove the alpha channel/make image rgb (224,224,4)->(224,224,3)
            * Store the Image, Title, Price, And Both Vectors in the binary
            * This will allow our model to be used very easy
##  Downloaded_Images_Binary.tfrecords
    * This stores all the Downloaded Images (224,224,3), Titles, Prices, And Both Vectors in the binary form
    * Much smaller file size
    * Can be decoded after


## First_Model.ipynb
    * 




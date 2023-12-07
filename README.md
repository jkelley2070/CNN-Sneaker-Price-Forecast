# CNN-Sneaker-Price-Forecast

## Goal
The goal of this project is create a after market sneaker price forecaster using a convulutionary neural network and two additional meta models!

## Project Plan
The project plan can be found at the following link 
[ExcaliDraw](https://app.excalidraw.com/s/CmEgiggUrt/79jFijhFFDF)
(this link is subscription based and might not be avaiable in the future
so I am pushing the excalidraw and svg to this repo)
1. This describes in detail the plan for project
2. Well Illustrated Basics of Tensors, Neural Networks, and CNN
3. Explanation of our model and the processes of how things were orginal modified
4. Introducing of stacking to the original model

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

## DataCleaningUpdated.ipynb
    * So we are have our Products_Updated but we must prepare it for our model
    * Part 1: Prepare Response
        * We must turn the vectors into categories
        * We can do this
            1. Balanced price- Using Quantiles (Perfectly Distributed)
            2. Unbalanced price - User Choise (Unknown Distribution)
            3. Model - 25 models
            4. Brand - 6 brands 
        * We can create these vectors using one hot encoding and some other techniques
    * Part 2: Prepare Images
        * These images have to downloaded from the link using python but
        before that we have to decide how to store it
        * Tensorflow binary is the best choice for this problem, due to csvs struggling with high dimensional data (They store it as a string), and the small storage size
        * We are going to need to write code to encode these things, and decode this things out of the binary, which can be tricky, 
        * While we are writing to this binary file we can
            * Download the image 
            * Change the shape to (224,224)
            * Remove the alpha channel/make image rgb (224,224,4)->(224,224,3)
            * Store the Image, Title, Price, And Both Vectors in the binary
            * This will allow our model to be used very easy

##  Downloaded_Images_Binary_Brands_Models.tfrecords
    * This stores all the Downloaded Images (224,224,3), Titles, Prices, And Vectors in the binary form
    * Much smaller file size
    * Can be decoded after using code found in Run_Model and Final_Scratch_Model


## Final_Scratch_Model (TRAINING) 
    * This is code for training the final scratch model!
    * Can be trained at the following colab link!
    [colab link!](https://colab.research.google.com/drive/1oebJ3ZSIFEuJZhumdY4aPh0Jyl7QZ38E?usp=sharing)
    * Many different models were tested, and this model was most affective for our data size, and type of image (consistent, no noise)
    * Note: There is lots of Redundant code for instructional and visualization purposes!
    * The module breaks down 
        * Decoding the Downloaded_Images_Binary.tfrecords
        * Loading the Data into Training and Testing
        * Shuffling the data to in sure randomness
        * Different Techniques that can be applied to the data
        * Training the data on the CNN model and making predictions
        * Code to save the model with the best weights and bias
        * Visualization of the performance of our model
    * There was a slight modification at the end, improving the performance of two of our features
    * It will take time to train these models so
    8 Models have been trained from this code, and are saved in Model_Keras_Files.zip

## Model_Keras_Files.zip
    * This zipped folder stores our keras models with ther corresponding weights and bias
    * Unzip before running Run_Model.ipynb

## Run_Model.ipynb (Predicting)
    * This is code for training the final scratch model!
    * Can be trained at the following colab link!
    [colab link!](https://colab.research.google.com/drive/1VnKqSBfDsStisIipzB2A7QEdRuAMELhe?usp=sharing)
    * This is the code for running the trained model 
    * The module breaks down 
        * Decoding the Downloaded_Images_Binary.tfrecords
        * Loading the Data into Training and Testing
        * Shuffling the data to insure randomness
        * Different Techniques that can be applied to the data
        * Making predictions on our already trained models
        * Saving these predictions to a DF and then a csv
        * Visualization of the performance of our model
    * Most of the code is taken from Final_Scratch_Model!
    * NOTE: The performance of this is going to skewed by 1-5%. The splitting of our original training and validation data was completely random, so when we run this code, even though it is completely random, training data has now been mixed with the validation data! The models were saved with best validation data, and have a balance between training and validation data

## CNN_Predicted_Probabilies.csv
 * This is a csv of predictions made by the model!
 * The format of it shows for our 4 respones
    *  Probabilites for each class | Actual Value one hot encoded




        




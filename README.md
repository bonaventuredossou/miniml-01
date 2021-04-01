# Practical Assignment 1
**Dealine**: 01.04.2021

**Name:** **Bonaventure F. P. Dossou
## Foreword
### Implementation of a Minimal Classification System

## Problem 1 - Done successfully
### Feature Extraction (Points 10)
We will start with extracting features from the images into the feature vector. For sake of simplicity the features were already calculated and are stored in the 001_fv.jpg and 002_fv.jpg files as red, green and blue channels. In order to solve the first problem please fill the feature vectors in the Training and Testing procedures in main.cpp file. The feature vector is a single channel column-matrix. It has nFeatures columns and 1 row. 

In order to check your implementation, the first feature vector of the 001_fv.jpg should be equal to [132, 12, 73]

> **Hint1:** In order to access pixels of a gray-scaled image ```img``` you can use OpenCV method ```img.at<byte>(y, x)```, where x and y are coordinates of the pixel. 

> **Hint 2:** In order to access pixels of an RGB color image ```img```, you can use OpenCV method ```img.at<Vec3b>(y, x)``` and to access the distingct color values: ```img.at<Vec3b>(y, x)[c]```, where c is the channel index from 0 to 2.
>  `First Feature vector == [132, 12, 73]`


## Problem 2 - Done successfully 
### Class Prior Probability (Points 25)
In order to apply the Bayes model we need to estimate the prior probabilities and the likelihoods from the training data. In this exersise we will estimate the prior probabilities. For this purpose we will use class `CPDFHistogram`. This class is designed to store, estimate and represent PDFs via histograms. Please study its implementation in the provided framework.

In `CBayes` class the prior probability is declared via smart pointer `std::shared_ptr<CPDFHistogram> m_pPrior;`, please see how it is initialized in the class constructor. In method `CBayes::addFeatureVec()` implement estimation of the prior probability. 

> **Hint:** Test your implementation with the `printPriorProbabilities()` function: if your implementation is correct, the output will be: `17.2%   0.4%    59.5%   9.9%    13.0%   0.0%`. Answer the question: Which class is not represented at the training image?

`Answer: The class that hasn't been represented in the training data is the class «car»`

`Submission Test PriorProbalities: 17.2%   0.4%    59.5%   9.9%    13.0%   0.0%`


## Problem 3 - Done Successfully
### The Bayes Classifier (Points 50)
Now in the `CBayes::addFeatureVec()` method you have complete implementation for estimating the prior probabilities and the likelihoods: thus the training procedure is complete. In this exercise, please finish the impmentation of the Bayes classifier in the `CBayes::getNodePotentials()` method. 

The resulting potentials should be stored in `res` variable, which is a one-column matrix. The values of the resulting node potentials are already initialized with the prior probabilities. Hence your task is to multiply these prior probabilities with the likelihoods for every class and every feature. The likelihoods are stored in the array `m_vPDF`. You can check in the `CBayes::addFeatureVec()` method how to access a histogram for specific feature and state. Use method `isEstimated()` of the class `CPDFHistogram` in order to detect states, for which no training samples were met during the training procedure. Set the potential for such classes to be equal to zero.

## Problem 4 - Done Successfully
### Decision Theory (Points 15)
Now, when both training and testing procedures are ready, we need to apply the decision theory in order to set proper label to every pixel of the testing image. 

In the testing procedure in the main.cpp file we classify the testing image using its features stored in the 002_fv.jpg file. The potentials for every pixel are returned from classifier into the `potentials` variable. Find the largest potential in `potentials` variable and assign the corresponding class label to the `classLabel` variable. Test your implementation. If everything is correct you should obtain 79,1% of accuracy and the class-map as follows:

![Solution](./renders/Bonaventure_Dossou_Solution.png)

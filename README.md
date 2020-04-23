# Data Science Challenge SDTSIA210 : Large scale face verification

From March to April 2020 I teamed up with Yoach Lacombe to compete in the Data Science challenge of the Machine Learning course at Télécom Paris in which we ranked 1st out of 126 participants. This repository contains our solution notebook solution. 

## Overview of the challenge

This challenge was designed by 

- Pavlo Mozharovskyi (pavlo.mozharovskyi@telecom-paris.fr)
- Umut Şimşekli (umut.simsekli@telecom-paris.fr)
- Attilio Fiandrotti (attilio.fiandrotti@telecom-paris.fr)
- Matthieu Labeau (matthieu.labeau@telecom-paris.fr)

Link to the original challenge introduction and starting kit : https://nbviewer.jupyter.org/urls/perso.telecom-paristech.fr/mozharovskyi/resources/challenge_SDTSIA_2020_start.ipynb

In this challenge, the goal is to build a fusion of algorithms in order to construct the best suited solution for comparison of a pair of images. This fusion is driven by qualities computed on each image.

Comparing of two images is done in two steps. 1st, a vector of features is computed for each image. 2nd, a simple function produces a vector of scores for a pair of images. The goal is to create a function that will compare a pair of images based on the information mentioned above, and decide whether two images belong to the same person.

### Training data:
The training set consist of two files, xtrain_challenge.csv and xtest_challenge.csv. File xtrain_challenge.csv contains one observation per row which contains following entries based on a pair of images:

- columns 1-13 - 13 qualities on first image;
- columns 14-26 - 13 qualities on second image;
- columns 27-37 - 11 matching scores between the two images.

File ytrain_challenge.csv contains one line with each entry corresponding to one observation in xtrain_challenge.csv, maintaining the order, and has '1' if a pair of images belong to the same person and '0' otherwise.

There are in total 1.068.504 training observations.

### Test data:
File xtest_challenge.csv has the same structure as file xtrain_challenge.csv.

There are in total 3.318.296 test observations.

### The performance criterion¶
The performance criterion is the prediction accuracy on the test set, which is a value between 0 and 1, the higher the better.


## Our solution and results

We ranked 1st out of 126 participants with an accuracy of 99.8837 % on the test set.
1. We used a Yeo-Johnson transformation to reduce the skweness in some of the features
2. We doubled the number of train data by symmetrizing the train set : for each row, we added the same row with the first image and the second image switched. 
3. We used sklearn's RandomizedSearchCV for parameter tuning on XGBoost.
4. We trained a first XGBoost classifier and used it to predict the probabilies of each label (0 or 1) on the test data.
5. Based on those probabilites, we added to the train set the part of the test data which was classified with 100% confidence by our classifier (about 99.3% of the test data). We then re-trained a new classifier on the new augmented train set and used it to predict the remaining test data. We iterate this step 3 times (after that the accuracy started decreasing). 

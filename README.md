# Data Science Challenge SDTSIA210

From March to April 2020 I teamed up with Yoach Lacombe to compete in the Data Science challenge of the Machine Learning course at Télécom Paris in which we ranked 1st out of 126 participants. This repository contains our solution notebook solution. 

The challenge was organized and designed by designed Pavlo Mozharovskyi, Attilio Fiandrotti, Matthieu Labeau researchers at Télécom Paris. Here is the link to the original starting kit : https://nbviewer.jupyter.org/urls/perso.telecom-paristech.fr/mozharovskyi/resources/challenge_SDTSIA_2020_start.ipynb

## Fusion of algorithms for face recognition

In this challenge, the goal is to build a fusion of algorithms in order to construct the best suited solution for comparison of a pair of images. This fusion is driven by qualities computed on each image.

Comparing of two images is done in two steps. 1st, a vector of features is computed for each image. 2nd, a simple function produces a vector of scores for a pair of images. The goal is to create a function that will compare a pair of images based on the information mentioned above, and decide whether two images belong to the same person.

## The properties of the dataset:
### Training data:
The training set consist of two files, xtrain_challenge.csv and xtest_challenge.csv.

File xtrain_challenge.csv contains one observation per row which contains following entries based on a pair of images:

- columns 1-13 - 13 qualities on first image;
- columns 14-26 - 13 qualities on second image;
- columns 27-37 - 11 matching scores between the two images.
File ytrain_challenge.csv contains one line with each entry corresponding to one observation in xtrain_challenge.csv, maintaining the order, and has '1' if a pair of images belong to the same person and '0' otherwise.

There are in total 1.068.504 training observations.

### Test data:
File xtest_challenge.csv has the same structure as file xtrain_challenge.csv.

There are in total 3.318.296 test observations.

## The performance criterion¶

The performance criterion is the prediction accuracy on the test set, which is a value between 0 and 1, the higher the better.

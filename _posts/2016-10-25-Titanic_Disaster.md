---
layout: post
title: "A Classification Analysis of Titanic Survivors"
---

## A Classification Analysis of Titanic Survivors

This project examines the probability of survival in the Titanic disaster using Classification models. Several models will be evaluated, such as Logistic, Gridsearch using Logistic, KNN, and Decision Trees. The dataset is accessed via a remote database, in which Exploratory Data Analysis is performed to select the features used in the models. The Jupyter Notebook and data set can be found [here.](https://github.com/adalal80/GA-DSI/blob/master/projects/projects-weekly/project-05/Project-5-Amish.ipynb)

### Exploratory Data Analysis

The following features are categorical variables: Pclass and Sex.
Age is a continuous variable, are binned into Child, Teenage, Young Adult, Adult, and Senior groups, thus categorical variables. Fare (see histogram below) will be normalized as it is skewed. Sibsp and Parch will be used as continuous variables.

![Histogram](https://github.com/adalal80/adalal80.github.io/blob/master/images/project5_histogram.png?raw=true)

### Model Validation

Features used in Model Validation: Pclass, Sex, Age_bins, Sibsp, Parch, and Fare (normalized). The class label is whether the person survived or not (survived).

#### 1. Logistic Regression

A logistic regression was used in the first model, with L2 as the penalty. The following are the confusion matrix, model score, and F1 score:

Confusion Matrix:

| 			   |not_survived | survived |     
|--------------|-------------|----------| 
| not_survived |     126     |    20    | 
| survived     |      31     |    57    | 


Model - Score: 0.78205

F1 Score     : 0.6909

#### 2. Gridsearch with Logistic Regression

A Gridsearch CV was used in the second model, which gave a penalty of L2. The following are the confusion matrix, model score, and F1 score:

Confusion Matrix:

| 			   |not_survived | survived |     
|--------------|-------------|----------| 
| not_survived |     124     |    22    | 
| survived     |      28     |    60    | 

Model - Score: 0.78632

F1 Score     : 0.70588

The model score and F1 score show a slight increase than the logistic model

#### 3. Gridsearch with KNN

Confusion Matrix:

A Gridsearch CV was used in the second model with KNN as the estimator. The following are the confusion matrix, model score, and F1 score:

| 			   |not_survived | survived |     
|--------------|-------------|----------| 
| not_survived |     124     |    22    | 
| survived     |      28     |    60    | 

Model - Score: 0.80341

F1 Score     : 0.70129

The model score faired better here than in the Gridsearch with logistic as the estimator, while the F1 score was slightly worse.


#### 4. Decision Trees

Decision Tree was used in the last model. The following are the confusion matrix, model score, and F1 score:

Confusion Matrix:

| 			   |not_survived | survived |     
|--------------|-------------|----------| 
| not_survived |     132     |    14    | 
| survived     |      28     |    60    | 


Model - Score: 0.82051

F1 Score     : 0.74074

ROC Curve for each model:

![ROC](https://github.com/adalal80/adalal80.github.io/blob/master/images/Project5_ROC.png?raw=true)


### Conclusion



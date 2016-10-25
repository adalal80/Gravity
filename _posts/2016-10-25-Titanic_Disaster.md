---
layout: post
title: "A Classification Analysis of Titanic Survivors"
---

## A Classification Analysis of Titanic Survivors

This project examines the probability of survival in the Titanic disaster using Classification models. Several models will be evaluated, such as Logistic, Gridsearch using Logistic, KNN, and Decision Trees. The dataset is accessed via a remote database, in which Exploratory Data Analysis is performed to select the features used in the models. The Jupyter Notebook and data set can be found [here.]()

### Exploratory Data Analysis

The following features are categorical variables: Pclass and Sex.
Age is a continuous variable, are binned into Child, Teenage, Young Adult, Adult, and Senior groups, thus categorical variables. Fare (see histogram below) will be normalized as it is skewed. Sibsp and Parch will be used as continuous variables.

![Histogram](https://github.com/adalal80/adalal80.github.io/blob/master/images/project5_histogram.png?raw=true)

### Model Validation

Features used in Model Validation: Pclass, Sex, Age_bins, Sibsp, Parch, Fare (normalized). The class label is whether the person survived or not (survived).

#### Logistic Regression

Confusion Matrix

| 			   |not_survived | survived |     
|--------------|-------------|----------| 
| not_survived |     126     |    20    | 
| survived     |      31     |    57    | 


Model - Score: 0.78205

F1 Score     : 0.6909

Coefficients:


#### Gridsearch with Logistic Regression
Confusion Matrix

| 			   |not_survived | survived |     
|--------------|-------------|----------| 
| not_survived |     124     |    22    | 
| survived     |      28     |    60    | 

Model - Score: 0.78632

F1 Score     : 0.70588

#### Gridsearch with KNN

Confusion Matrix

| 			   |not_survived | survived |     
|--------------|-------------|----------| 
| not_survived |     124     |    22    | 
| survived     |      28     |    60    | 

Model - Score: .80341

F1 Score     : 0.70129

#### Decision Trees
Confusion Matrix

Model - Score: 0.82051

F1 Score     : 0.74074

ROC Curve

![ROC](https://github.com/adalal80/adalal80.github.io/blob/master/images/Project5_ROC.png?raw=true)


### Conclusion



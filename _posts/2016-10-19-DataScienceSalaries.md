---
layout: post
title: "Predicting Data Scientist Salaries Using Logistic Regression"
---

#### Predicting Data Scientist Salaries Using Logistic Regression

#### Iowa Liquor Market Research for New Store Locations

Scenario involves being a data scientist contracted by a firm that is rapidly expanding. Looking for new data scientist is vital for the expansion. Management thinks the best way to gauge salary amounts is to take a look at what industry factors influence the pay scale for data scientist. The jupyter code can be found [here.](https://github.com/adalal80/GA-DSI/blob/master/projects/projects-weekly/project-04/scraping-project-4-starter_JPF.ipynb)

The following steps are taken in this analysis:

1. Scraping Indeed, Glassdoor, and Cost of Living index
2. Combining into separate Data Frames
3. Cleaning/Tidying Data
4. Plotting/Normalizing
5. Regressions

The cities scraped for this project were: Atlanta, Austin, Boston, Dallas, Detroit, Houston, Kansas City, Los Angeles, Minneapolis, Nashville, San Francisco, San Jose, and Washington DC.

The process was to perform a regression on glassdoor salaries, and then use the model to predict the data from Indeed. Findings from the regression found that incorporating Cost of Living Index with the median Salary found on glassdoor, with binning the titles into Entry-level, Mid-level, and Senior Level bins, and creating dummy variables for each city gave an AUC score of 0.86 (with 1 being perfect) and F1 score of 0.77. The AUC score is a metric that analyzes the relationship between false positives and True positives while running a classification regression. The F1 score looks at the accuracy of the model. 

What does this mean? Well, normalizing for cost of living, the salary is dependent on experience level and location. As the demand for data scientist is increasing, to attract the brightest minds, a company might be more inclined to overpay if the company is located outside of Bay Area, New York, Washington DC, and Boston (all had negative coefficients).

### Scraping Indeed, Glassdoor, and Cost of Living Index

1. Scraping Indeed

The scraper code used to pull informat from indeed, can be found in the jupiter notebook located [here.](https://github.com/adalal80/GA-DSI/blob/master/projects/projects-weekly/project-04/webscraping_indeed.py)

2. Glassdoor

The scraper code used to pull informat from Glassdoor, can be found [here.](https://github.com/adalal80/GA-DSI/blob/master/projects/projects-weekly/project-04/glassdoor-salary-scraper-master/scraper.py). This code was forked from [here.](https://github.com/ashalan/glassdoor-salary-scraper)

3. Cost of Living Index

The code to scrape for Cost of Living index from www.expatistan.com.

### Cleaning & Tidying the DataFrames

Extensive cleaning was performed to convert salaries into low salary, high salary and median salary, as well cleaning cities and titles, including binning into entry, mid, and senior-level bins. The jupyter notebook contains all the code for the cleaning.

### Visualizations

The distribution of entry-level, mid-level, and senior-level bins are: 90,663, and 378 respectively. The low sample size in entry-level bin compared to other bins is quite  low, and will be problematic when plotting the distribution.

The image below shows the histogram for median salaries. There is skewness in the data, most likely due to high disparity in salaries in cities where cost of living is high, such as San Francisco and New York.

![Median Salary](https://github.com/adalal80/adalal80.github.io/blob/master/images/Salary_Histogram.png?raw=true)


The image below shows the histogram for median salaries with cost of living factored in. 
![Median Salary Normalized](https://github.com/adalal80/adalal80.github.io/blob/master/images/Salary_Histogram_norm.png?raw=true)


### Assumptions

1) Normalizing salaries to adjust for Cost of Living, using NYC as base.
2) Used only experience, and cities as the features due not having access to skills in glassdoor.
3) There will be bias due to not having access to bonus or perks offered by companies.
4) Assumption is that each company in each market would offer similar bonus and perks, such that each company would pose an equal chance to hire a data scientist. In other words, they would be competitive in hiring for a data scientist.

### Regression

Target Variable

* Above_median (1 if above median or 0 below median)

Features:

* Cities (Dummy for each City)
* Entry-level (Dummy)
* Mid-level (Dummy)
* Senior-level (Dummy)


# Regression - Model 1

GridsearchCV was used to find the optimal penalty and C value, using logistic regression as the estimator.
GridsearchCV yielded: Penalty - L2, C - 0.9

            predicted_over_mean  predicted_under_mean
over_mean                   154                    31
under_mean                   55                   134
             precision    recall  f1-score   support

          0       0.81      0.71      0.76       189
          1       0.74      0.83      0.78       185

avg / total       0.77      0.77      0.77       374

AUC Score is: 0.858901758902

![Regression AUC - Reg1](https://github.com/adalal80/adalal80.github.io/blob/master/images/AUC_reg1.png?raw=true)

The coefficients of the logistic regression are:

| Variables          | Coefficients | 
|--------------------|--------------| 
| entry_bin          | -1.945187    | 
| mid_bin            | -0.206333    | 
| senior_bin         | 1.943905     | 
| City_atlanta       | -0.33349     | 
| City_austin        | 1.036828     | 
| City_boston        | -1.100968    | 
| City_dallas        | 1.645433     | 
| City_detroit       | 2.785725     | 
| City_houston       | 1.103457     | 
| City_kansas city   | 0.910086     | 
| City_los angeles   | 0.449568     | 
| City_minneapolis   | -0.09097     | 
| City_nashville     | -0.203721    | 
| City_new york      | -3.098401    | 
| City_san francisco | -1.837764    | 
| City_san jose      | 0.856329     | 
| City_seattle       | -0.30393     | 
| City_washington dc | -2.025796    | 
 

# Regression - Model 2

Since the indeed dataframe does not contain Houston and Kansas City, these must be dropped from the glassdoor dataframe. From there, we perform the same regression as we used in the previous regression. 126 observations were dropped.

GridsearchCV yielded: Penalty - L2, C - 0.9, same as earlier.

            predicted_over_mean  predicted_under_mean
over_mean                   154                    31
under_mean                   55                   134
             precision    recall  f1-score   support

          0       0.81      0.81      0.81       178
          1       0.78      0.78      0.78       154

avg / total       0.80      0.80      0.80       332

AUC Score is: 0.887786370932

![Regression AUC - Reg2](https://github.com/adalal80/adalal80.github.io/blob/master/images/AUC_reg2.png?raw=true)

The AUC score increased by approximately 0.03, which shows that this model performs better. The F1 score increased from 0.77 to 0.80, which shows the model score increased.

Using this new model  on the indeed dataframe as the test set, let's see how well this model pridects salaries.

            predicted_over_mean  predicted_under_mean
over_mean                    30                    17
under_mean                    8                    41
             precision    recall  f1-score   support

          0       0.71      0.84      0.77        49
          1       0.79      0.64      0.71        47

avg / total       0.75      0.74      0.74        96

AUC Score is: 0.753799392097

![Regression AUC - Indeed](https://github.com/adalal80/adalal80.github.io/blob/master/images/AUC_reg_indeed.png?raw=true)



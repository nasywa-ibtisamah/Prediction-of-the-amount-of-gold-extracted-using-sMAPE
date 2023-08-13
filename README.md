# Project Description

Hello there :wave:
I hope this project finds you well!

In this project, I will prepare a prototype of a machine learning model for a Company that specializes in developing efficient solutions for heavy industries.

The model that will be created should be able to predict the amount of gold extracted or obtained from gold ore. Relevant data about the extraction and purification process of gold ore is available for you to use.


**Objective**

The goal of this project is to predict the amount of gold extracted or obtained from gold ore. The model is expected to contribute to the creation of a more efficient production process and eliminate parameters that do not yield profits.

**Used Model**
1. Baseline
2. Linear Regression
3. Decision Tree regressor
4. Random Forest Regressor

# Steps

1. Data Overview
2. Data preprocessing
3. Exploratory Data Analysis
4. Dataset Preparation
5. Creating Machine Learning Model
6. Testing model on Test Set

## 1. Data Overview

**Technology Process (Stages)**
- `Rougher feed` - raw material for the flotation process
- `Rougher additions (reagent additions)` - flotation reagents, including:

    a. Xanthate — flotation collector or activator
    
    b. Sulphate — sodium sulphide, specific to this process
    
    c. Depressant — sodium silicate
    
    
- `Rougher process` - flotation
- `Rougher tails` - residue product
- `Float banks` - flotation units
- `Rougher Au` - rougher gold concentrate
- `Final Au` - final gold concentrate

**Available Parameters for Each Stage (Parameter Type)**
- `air amount` - volume of air
- `Fluid Levels` - liquid level (concentration)
- `Feed size` - particle size of the feed
- `Feed rate` - feed rate

**Feature Naming**
1. Values possible for [stage]
- `rougher` - flotation
- `primary_cleaner` - primary cleaning
- `secondary_cleaner` - secondary cleaning
- `final` - final characteristics
2. Values possible for [parameter_type]
- `input` - raw material parameter
- `output` - product parameter
- `state` - parameter indicating current stage characteristics
- `calculation` - calculated characteristic
3. Values possible for [parameter_name]
- `Au` - Gold
- `Ag` - Silver
- `Pb` - Lead

The method for naming existing features is as follows:
[stage].[parameter_type].[parameter_name]

Example: rougher.input.feed_ag

**Conclusion of Data Exploration Stage**

**df_train**
1. Only the "date" and "primary_cleaner.input.feed_size" columns have no missing values. Other columns contain missing values.

2. With a total of 53 columns, while the df_train dataset has 87 columns, there are 37 columns that are not present in the df_test dataset.

**df_test**
1. Only the "date" and "primary_cleaner.input.feed_size" columns have no missing values. Other columns contain missing values.
2. With a total of 53 columns, while the df_train dataset has 87 columns, there are 37 columns that are not present in the df_test dataset.

**df_full**

  1. Only the "date" and "primary_cleaner.input.feed_size" columns have no missing values. Other columns contain missing values.

  
**Function to calculate gold acquisition**

From the output recovery difference, a very small value of 9.303415616264301e-15 is obtained. Therefore, it can be concluded that the formula used is correct as the difference is extremely minor, and the calculation for rougher.output.recovery is considered reliable.

## 2. Pre-Processing Data

The following are data preprocessing steps I did in this project:
1. Analysis of Features Unavailable in test set

## 3. Exploratory Data Analysis
#### 1. How the concentration of metals (Au, Ag, Pb) changes depending on the purification stage
**Analysis Results**

1. The Gold (Au) component exhibits varying data distribution for each stage, with the highest concentration value in the final.output.concentrate stage.
2. The Silver (Ag) component displays a relatively centralized data distribution, with the highest concentration value in the final.output.concentrate stage.
3. The Lead (Pb) component also demonstrates a relatively centralized data distribution, with the highest concentration value in the rougher.output.concentrate stage.
#### 2. How the particle size distribution of the feed varies in both the training set and the test set. If the distribution varies significantly, the model evaluation will be inaccurate.
**Analysis Result**
From the above diagram, it can be observed that between df_test and df_train, there is a fairly similar density distribution for the rougher.input.feed_size feed particle size.
#### 3. Considering the total concentration of all substances at different stages: raw feed, rougher concentrate, and final concentrate. If there are abnormal values in the total distribution, an analysis will be performed to determine whether it's necessary to remove these abnormal values from both samples. The reasons and methods for eliminating these anomalies will be explained.
**Analysis Result**
1. The concentration data in all three stages exhibit anomalies, with a significant number of data points being 0.
2. Data points with a value of 0 will be removed, as they can be considered as outliers.

## 4. Dataset Preparation

The following are dataset preparation steps I did in this project:
1. Removing Outliers
2. Features Selection
3. Handling Missing Values in Target Variable
4. Defining Features and Target
5. Splitting dataset

## 5. Create Machine Learning Model

In this stage, the performed steps are as follows:
  1. Created of a function to calculate the final sMAPE.
2. Trained model using cross-validation. The best model with the smallest sMAPE value will be selected.


**Analysis Result**

The lowest sMAPE value in the train set is achieved by the DecisionTreeRegressor model with max_depth = 49, resulting in a score of 2.8141420682101164e-19 or 0.00000000000000000028141420682101164.

However, the result represents overfitting on the training model. Hence, we will use RandomForestRegressor instead to implement on Test Set. At depth 40 and n_estimator 100, the final smape score is 3.59.

**Interpretation of the sMAPE Value:**

The Symmetric Mean Absolute Percentage Error (sMAPE) is a metric used to measure the accuracy of a predictive model. It calculates the percentage difference between the actual and predicted values, and then averages these differences symmetrically.

In the context of my analysis, a sMAPE value of 3.59 indicates that, on average, the model's predictions have an error of approximately 3.59%. This means that the model's predictions are, on average, within 3.59% of the actual values. Lower sMAPE values indicate better model performance, as they represent a smaller average percentage error between predictions and actual values.

# General Conclusion


Despite the lowest sMAPE result when using the decision tree regressor model, overfitting actually occurred when applied to the test set. Therefore, the **RandomForestRegressor with max_depth 40 and n_estimators 100** was chosen to be applied to the test dataset.

The final sMAPE value on the test set is 8.544402388079245, indicates that, on average, the model's predictions have an error of approximately 8.54%. This means that the model's predictions are, on average, within 8.54% of the actual values.

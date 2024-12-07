## Introduction ##  
This project aims to analyze the data set of "Recipies and Ratings".  
This dataset has 17 features and 234429 examples. The relevant features have been listed below:

| Number | Feature | Description |
| ----------- | ----------- | ----------- |
| 1 | id | The index of the orders |
| 2 | minutes | The time used in minutes to make the meal |
| 3 | n_steps | The number of steps used to make the meal |
| 4 | nutrition | The detailed amount of nutrition components, including calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates |
| 5 | rating | The number of ratings of the orders |

This project will be divided into two parts:

Part 1: analyze the relation between the minutes used in making the meals and the ratings.  
Part 2: make a prediction model for the ratings.

## Data Cleaning and Exploratory Data Analysis ##  
### Data Cleaning ###  

**Step 1: split categorical features**  

The detailed amounts of nutrition components have been saved as strings in the feature "nutrition", so the first step of data cleaning will be splitting this feature into several quantitative features.  

**Step 2: fill NaN values**  

There are a lot of examples showing 0 in ratings since not everyone wants to rate their order, so the second step of data cleaning will be changing the 0 ratings to NaN and filling them with 5.0 since 5.0 is the majority number of the ratings. Below is the data after cleaning.  

|     id |   minutes |   n_steps |   calories |   total_fat |   sugar |   sodium |   protein |   saturated_fat |   carbohydrates |   rating | minutes_interval   |
|-------:|----------:|----------:|-----------:|------------:|--------:|---------:|----------:|----------------:|----------------:|---------:|:-------------------|
| 333281 |        40 |        10 |      138.4 |          10 |      50 |        3 |         3 |              19 |               6 |        4 | [40, 60)           |
| 453467 |        45 |        12 |      595.1 |          46 |     211 |       22 |        13 |              51 |              26 |        5 | [40, 60)           |
| 306168 |        40 |         6 |      194.8 |          20 |       6 |       32 |        22 |              36 |               3 |        5 | [40, 60)           |
| 306168 |        40 |         6 |      194.8 |          20 |       6 |       32 |        22 |              36 |               3 |        5 | [40, 60)           |
| 306168 |        40 |         6 |      194.8 |          20 |       6 |       32 |        22 |              36 |               3 |        5 | [40, 60)           |  

### Univariate Analysis ###  

First  


<iframe src="assets/uni-1.html" width="800" height="600" frameborder="0"></iframe>

### Bivariate Analysis ###  

### Aggregation Analysis ###
 

### Imputation ###  
This part is an additional explanation of the missing rating imputation.  

The technique used here imputes the missing values by grouping the examples based on the minute interval since the goal of this data analysis is to figure out the relation between the cooking minutes and the ratings.  

The mean values of minutes of different intervals have been listed below:  
| Interval | Mean of Minutes |
| ----------- | ----------- |
| (0, 20) | 4.72 |
| [20, 40) | 4.68 |
| [40, 60) | 4.67 |
| [60, 80) | 4.68 | 
| [80, 100) | 4.68 |
| [100, ∞) | 4.66 |  

Before the imputation, the distribution of ratings is shown below:  

After the imputation, the distribution of ratings is shown below:  


## Framing a Prediction Problem ##  
The rest of the parts of this project will focus on setting up a regression prediction model for the ratings based on some features in the dataset.  

There will be two models set up to predict the ratings. The first simpler one uses only 2 features, and the second one uses more features and polynomial regression.  

## Baseline Model ##  
This part aims to set up a prediction model based on 2 features. Here is how the model is set up:  

**Step 1: Training and Testing Data 

**Step 1: Select features**  

The features chosen here to set up a basic model are "minutes" and "n_steps" which represent the time complexity of making a meal.  

**Step 2: Split Training and Testing Data**  

Set 80% of examples as training data, and 20% of examples as testing data.

**Step 3: Make pipeline**  

To make the model more accurate, a StandardScaler() is added as the first step of the pipeline.  

After that, the pipeline fits the data using LinearRegression().  

**Step 4: Performance Evaluation**  

The performance of the model is evaluated by the mean square error.  

The training and testing mean square error is listed below:

| Training | Testing |
| -------- | ------- |
| 0.47 | 0.45 |  

We can see that the mean square error on the training and testing data has been an acceptable value. However, the model can still be optimized by adding more features and using non-linear regression.

## Final Model ##  

The final model will predict the ratings based on more valuables and use polynomial features in training.  

The steps of setting up this model are shown below:  

**Step 1: Add Features**

These features are added to the selected features:  
1. calories
2. protein
3. sodium

The remained features in nutrition can be represented by calories to some extent, so they are not selected.  

**Step 2: Split Training and Testing Data**  

Set 80% of examples as training data, and 20% of examples as testing data, and the random state is set as 23.  

**Step 3: Set up model**

The usage of the polynomial regression requires setting a scope of the degree as hyperparams. To shorten the training time, the scope of the degree is set from 1 to 12.  

Then, we use a pipeline to include the StandardScaler(), the PolynomialFeatures(), and the LinearRegression().  

Next, we include this pipeline in a GridSearchCV model. The parameters are set as below:  

| Parameter | Value |
| --------- | ----- |
| param_grid | polynomialfeatures__degree: range(1, 12) |
| cv | 5 |
| scoring | neg_mean_squared_error |  

**Step 4: Fit Data and Evaluate Performance**




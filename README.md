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
| 306168 |        40 |         6 |      194.8 |          20 |       6 |       32 |        22 |              36 |               3 |        5 | [40, 60)   

### Univariate Analysis ###  

First, let's see the distribution of different ratings as below:

<iframe src="assest/uni-1.html" width="800" height="600" frameborder="0"></iframe>  

Next, let's see the distribution of different minute intervals as below:  

<iframe src="assest/uni-2.html" width="800" height="600" frameborder="0"></iframe>  

### Bivariate Analysis ###  

<iframe src="assest/bi-1.html" width="800" height="600" frameborder="0"></iframe>

### Aggregation Analysis ###  

| minutes_interval   |   count |    mean |
|:-------------------|--------:|--------:|
| (0, 20)            |   52165 | 4.48011 |
| [20, 40)           |   71600 | 4.40978 |
| [40, 60)           |   43866 | 4.37327 |
| [60, ∞)            |   56949 | 4.28943 |
 
Before the imputation, the distribution of ratings is shown below:  

After the imputation, the distribution of ratings is shown below:  


## Framing a Prediction Problem ##  
The rest of the parts of this project will focus on setting up a multiclass classification prediction model for the ratings based on some features in the dataset.    

## Baseline Model ##  
This part aims to set up a prediction model based on 2 features. Here is how the model is set up:  

**Step 1: Training and Testing Data 

**Step 1: Select features**  

The features chosen here to set up a basic model are "minutes" and "n_steps" which represent the time complexity of making a meal.  

**Step 2: Split Training and Testing Data**  

Set 80% of examples as training data, and 20% of examples as testing data.



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



**Step 4: Fit Data and Evaluate Performance**




# Please give me a five-star rating #

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
Part 2: make a multiclass classification model for predicting the ratings.








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

First, let's see the amount distribution of different minute intervals as below:

<iframe src="assest/uni-1.html" width="800" height="400" frameborder="0"></iframe>   

Also, we can see the distribution of n_steps as below:  

<iframe src="assest/uni-2.html" width="800" height="400" frameborder="0"></iframe>  

### Bivariate Analysis ###  

Below is the mean of the ratings at every minute interval:  

<iframe src="assest/bi-1.html" width="800" height="400" frameborder="0"></iframe>   

We can see that the mean of ratings does not strictly decrease as the minutes increase, meaning that some customers are willing to give a high rating to the meals that take more time and are more exquisite.  

Next, we can see the mean of the n_steps at every minute intervals:  

<iframe src="assest/bi-2.html" width="800" height="400" frameborder="0"></iframe>  

We can see that the steps increase as the minutes increase, but slower after 20 minutes are taken.

### Aggregation Analysis ###  

Here is the detailed pivot table of the minutes interval and the ratings.

| minutes_interval   |   count |    mean |
|:-------------------|--------:|--------:|
| (0, 20)            |   52165 | 4.73114 |
| [20, 40)           |   71600 | 4.69728 |
| [40, 60)           |   43866 | 4.68821 |
| [60, ∞)            |   56949 | 4.69752 |  

### Imputation ###  

Here we choose to fill the NaN ratings with 5.0 since it is the majority, and it can be proven by the fact that most people tend to give a 5.0 rating even though the meal is bad.

Before the imputation, the distribution of ratings is shown below:  

<iframe src="assest/imp-1.html" width="800" height="400" frameborder="0"></iframe>  

After the imputation, the distribution of ratings is shown below:  

<iframe src="assest/imp-2.html" width="800" height="400" frameborder="0"></iframe>  

There is no 0 rating after imputation.  








## Framing a Prediction Problem ##  
The rest of the parts of this project will focus on setting up a multiclass classification model for predicting the ratings based on some features in the dataset.    









## Baseline Model ##  
This part aims to set up a prediction model based on 2 features. Here is how the model is set up:  

**Step 1: Select features**  

The quantitative features chosen here to set up a basic model are "minutes" and "n_steps" which represent the time complexity of making a meal. There are no categorical features selected.  

**Step 2: Split Training and Testing Data**  

Set 80% of examples as training data, and 20% of examples as testing data.  

**Step 3: Set up model**  

Use the K-Neighbors model to classify the ratings, and use GridSearchCV to find out the optimal amount of neighbors in the scope [3, 5]. The reason that the optimal amount of neighbors may not be 5 is that somebody will give a 5.0 rating even though the meal only deserves 3.0 or 2.0, or give a 3.0 to a perfect meal deserving a 5.0 rating. The actual distribution of the meals in the dataset may not have 5 rating intervals.

**Step 4: Fit Data and Evaluate Performance**  
The scores of the model on training and testing data are shown below:  

| Data | Score |
| ---- | ----- |
| Training | 0.7546698281236085 | 
| Testing | 0.7488200195921275 |









## Final Model ##  

The final model will predict the ratings based on more valuables.  

The steps of setting up this model are shown below:  

**Step 1: Add Features**

These features are added to the selected features:  
1. calories
2. total_fat
3. sugar
4. sodium
5. protein
6. saturated_fat
7. carbohydrates

These features will make the model predict the ratings not only based on the time and complexity but also the nutrition.  

**Step 2: Split Training and Testing Data**  

Set 80% of examples as training data, and 20% of examples as testing data, and the random state is set as 32. Using different   

**Step 3: Set up model**

Also use the K-Neighbors model to classify the ratings, and use GridSearchCV to find out the optimal amount of neighbors in the scope [3, 5].

**Step 4: Fit Data and Evaluate Performance**  
The scores of the model on training and testing data are improved as below:  

| Data | Score |
| ---- | ----- |
| Training | 0.799998886810936 | 
| Testing | 0.7517143111586072 |

There is a small but also valuable improvement after adding several features.



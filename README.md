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

## Data Cleaning and Exploratory Data Analysis  ##  
### Data Cleaning ###  

**Step 1: split categorical features**  

The detailed amounts of nutrition components have been saved as strings in the feature "nutrition", so the first step of data cleaning will be splitting this feature into several quantitative features.  

**Step 2: fill NaN values**  

There are a lot of examples showing 0 in ratings since not everyone wants to rate their order, so the second step of data cleaning will be changing the 0 ratings to NaN and filling them with the mean value after grouping by the interval of minutes.  

## Exploratory Data Analysis ##  

### Univariate Analysis ###  

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

## Baseline Model ##  


## Final Model

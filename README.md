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

| name                                 |     id |   minutes |   contributor_id | submitted   | tags                                                                                                                                                                                                                        |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | description                                                                                                                                                                                                                                                                                                                                                                       | ingredients                                                                                                                                                                    |   n_ingredients |          user_id |   recipe_id | date       |   rating | review                                                                                                                                                                                                                                                                                                                                           |   calories |   total_fat |   sugar |   sodium |   protein |   saturated_fat |   carbohydrates | minutes_interval   |
|:-------------------------------------|-------:|----------:|-----------------:|:------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|-----------------:|------------:|:-----------|---------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------:|------------:|--------:|---------:|----------:|----------------:|----------------:|:-------------------|
| 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings'] |        10 | ['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']                                                  | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour'] |               9 | 386585           |      333281 | 2008-11-19 |        4 | These were pretty good, but took forever to bake.  I would send it ended up being almost an hour!  Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut.  They did taste quite rich, though!  Made for My 3 Chefs.                                                                                   |      138.4 |          10 |      50 |        3 |         3 |              19 |               6 | [40, 60)           |
| 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11  | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                               |        12 | ['pre-heat oven the 350 degrees f', 'in a mixing bowl , sift together the flours and baking powder', 'set aside', 'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy', 'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft & chewy in the center', 'serve hot and enjoy !'] | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                    |              11 | 424680           |      453467 | 2012-01-26 |        5 | Originally I was gonna cut the recipe in half (just the 2 of us here), but then we had a park-wide yard sale, & I made the whole batch & used them as enticements for potential buyers ~ what the hey, a free cookie as delicious as these are, definitely works its magic! Will be making these again, for sure! Thanks for posting the recipe! |      595.1 |          46 |     211 |       22 |        13 |              51 |              26 | [40, 60)           |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']                                                                                                                                                                                                                                                                                                                              | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |  29782           |      306168 | 2008-12-31 |        5 | This was one of the best broccoli casseroles that I have ever made.  I made my own chicken soup for this recipe. I was a bit worried about the tsp of soy sauce but it gave the casserole the best flavor. YUM!                                                                                                                                  |      194.8 |          20 |       6 |       32 |        22 |              36 |               3 | [40, 60)           |
|                                      |        |           |                  |             |                                                                                                                                                                                                                             |           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |                                                                                                                                                                                                                                                                                                                                                                                   |                                                                                                                                                                                |                 |                  |             |            |          | The photos you took (shapeweaver) inspired me to make this recipe and it actually does look just like them when it comes out of the oven.                                                                                                                                                                                                        |            |             |         |          |           |                 |                 |                    |
|                                      |        |           |                  |             |                                                                                                                                                                                                                             |           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |                                                                                                                                                                                                                                                                                                                                                                                   |                                                                                                                                                                                |                 |                  |             |            |          | Thanks so much for sharing your recipe shapeweaver. It was wonderful!  Going into my family's favorite Zaar cookbook :)                                                                                                                                                                                                                          |            |             |         |          |           |                 |                 |                    |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']                                                                                                                                                                                                                                                                                                                              | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |      1.19628e+06 |      306168 | 2009-04-13 |        5 | I made this for my son's first birthday party this weekend. Our guests INHALED it! Everyone kept saying how delicious it was. I was I could have gotten to try it.                                                                                                                                                                               |      194.8 |          20 |       6 |       32 |        22 |              36 |               3 | [40, 60)           |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']                                                                                                                                                                                                                                                                                                                              | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 | 768828           |      306168 | 2013-08-02 |        5 | Loved this.  Be sure to completely thaw the broccoli.  I didn&#039;t and it didn&#039;t get done in time specified.  Just cooked it a little longer though and it was perfect.  Thanks Chef.                                                                                                                                                     |      194.8 |          20 |       6 |       32 |        22 |              36 |               3 | [40, 60)           |  


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




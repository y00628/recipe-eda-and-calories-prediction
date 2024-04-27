# recipe-eda-and-calories-prediction

**_Note_**: Combined repo recipe-dataset-analysis and repo recipe-calories-prediction into this new repo

# Part 1: Recipe Dataset Analysis

by Yosen Lin

**_Note_**: Exploratory Data Analysis Project for DSC 80 at UCSD

---

## Introduction

The data that I have access to is a subset of the raw data used in the original report, containing only the recipes and reviews posted since 2008, since the original data is quite large.

RAW_recipes.csv contains the recipes, while RAW_interactions.csv contains the reviews.

Question to investigate: Is there a correlation between the cooking time and average rating of recipes?

People should care about this dataset bacause a lot of people cook at home, and some of the information from this dataset (nutritional facts, rating, ingredients, etc.) can serve as a huge factor when choosing what to cook for a meal. Specifically, people should care about my question because people can decide what kind of meals to make given their time constraints, should there exist a relationship.

##### Number of rows: 83782

##### Relevant Columns:

minutes: number of minutes it takes to prepare each recipe

calories (#): number of calories for each recipe

sodium: the amount of sodium used for each recipe

rating: average rating for each recipe

---

## Cleaning and EDA

### Cleaning Data

Here are the steps I took to clean the data:

1. Left merge the recipes and rating datasets together so that the cooking times and the ratings are in the same dataset
2. Replace all ratings of 0 with np.nan in the merged dataset, as rating of 0 means the user did not rate.
3. Find the average rating per recipe as a Series and add this Seriesback to the merged recipes dataset
4. Convert the tags column from strings to lists
5. Convert nutrition column from strings to lists, then separate a list of nutritional labels to several different columns. This helps to detect if the missingness of a column has to do with nutritional columns.
6. Remove nutrition column as nutritional labels (calories, total sugar, etc.) are separated into different columns
7. Move rating to the last column
8. Convert nutritional labels from strings to floats (Quantify the labels)

|     | name                               |     id | minutes | contributor_id | submitted  | n_steps | n_ingredients | calories (#) | total fat (PDV) | sugar (PDV) | sodium (PDV) | protein (PDV) | saturated fat (PDV) | carbohydrates (PDV) | rating |
| --: | :--------------------------------- | -----: | ------: | -------------: | :--------- | ------: | ------------: | -----------: | --------------: | ----------: | -----------: | ------------: | ------------------: | ------------------: | -----: |
|   0 | 1 brownies in the world best ever  | 333281 |      40 |         985201 | 2008-10-27 |      10 |             9 |        138.4 |              10 |          50 |            3 |             3 |                  19 |                   6 |      4 |
|   1 | 1 in canada chocolate chip cookies | 453467 |      45 |        1848091 | 2011-04-11 |      12 |            11 |        595.1 |              46 |         211 |           22 |            13 |                  51 |                  26 |      5 |
|   2 | 412 broccoli casserole             | 306168 |      40 |          50969 | 2008-05-30 |       6 |             9 |        194.8 |              20 |           6 |           32 |            22 |                  36 |                   3 |      5 |
|   3 | millionaire pound cake             | 286009 |     120 |         461724 | 2008-02-12 |       7 |             7 |        878.3 |              63 |         326 |           13 |            20 |                 123 |                  39 |      5 |
|   4 | 2000 meatloaf                      | 475785 |      90 |        2202916 | 2012-03-06 |      17 |            13 |          267 |              30 |          12 |           12 |            29 |                  48 |                   2 |      5 |

Note: 'tags', 'ingredients', 'description', 'steps' columns not shown due to space constraints.

### Univariate Analysis

<iframe src="assets/cooking-time-uni.html" width=800 height=600 frameBorder=0></iframe>

As you can see, most of the recipes take no more than 150 minutes to prepare. For the recipes that take no more than 150 minutes to prepare, most of the them take about 20 to 50 minutes to prepare. However, as shown on the graph, some can take as long as 10000000 to 100000000 minutes to prepare.

### Bivariate Analysis

<iframe src="assets/calories-min-scatter.html" width=800 height=600 frameBorder=0></iframe>

As you can see, the bottom-left corner of the graph takes is the most dense part of the scatterplot. Notice that there are some data points at the top-left corner of the plot, meaning that the recipe does not have a lot of calories even though it takes a long time to prepare that recipe. On the other hand, there are some data points at the bottom-right corner of the plot, meaning that the recipe has a lot of calories even though it does not take a long time to prepare that recipe.

Note: Recipes that take more than 500000 minutes to prepare or has more than 500000 calories are not on the scatterplot

### Aggregate Analysis

The table below shows the average calories for different cooking time and rating intervals. This table can be used as a source to explore if the average cooking time and the rating has anything to do with the number of calories of a recipe.

| rating_bins   | (-0.0001, 20.0] | (20.0, 50.0] | (50.0, 150.0] | (150.0, 250.0] | (250.0, 1000.0] | (1000.0, 5000.0] | (5000.0, 10000.0] | (10000.0, 100000.0] | (100000.0, 1000000.0] | (1000000.0, 10000000.0] |
| :------------ | --------------: | -----------: | ------------: | -------------: | --------------: | ---------------: | ----------------: | ------------------: | --------------------: | ----------------------: |
| (-0.001, 1.0] |         400.879 |      395.288 |       551.068 |         418.95 |         462.239 |          457.717 |             760.7 |                 nan |                   nan |                     nan |
| (1.0, 2.0]    |         379.876 |      409.657 |       549.739 |        620.968 |         371.727 |          1717.21 |               nan |                 nan |                   nan |                     nan |
| (2.0, 3.0]    |         324.398 |      407.104 |       573.432 |        575.752 |          426.47 |          459.271 |               nan |              440.95 |                   nan |                     nan |
| (3.0, 4.0]    |         338.281 |      406.587 |       516.855 |        576.618 |         490.755 |          573.749 |            374.95 |             394.575 |                 836.2 |                     nan |
| (4.0, 5.0]    |         322.155 |       405.16 |       539.795 |        628.879 |         489.456 |          660.235 |            2307.1 |             584.973 |                  69.4 |                   407.4 |
| nan           |         453.324 |       432.27 |       610.069 |         598.55 |         621.055 |          871.246 |           223.967 |             574.578 |                  75.2 |                     nan |

---

The table below shows the average cooking time for different rating intervals. Notice that recipes that have ratings higher than 3 tend to have longer average cooking time in this table. Also notice that recipes without a rating tend to take significantly longer time to prepare comparing to those with ratings.

| rating_bins   | minutes |
| :------------ | ------: |
| (-0.001, 1.0] | 95.9151 |
| (1.0, 2.0]    | 94.7684 |
| (2.0, 3.0]    | 97.0264 |
| (3.0, 4.0]    | 112.166 |
| (4.0, 5.0]    | 112.124 |
| nan           | 228.719 |

---

## Assessment of Missingness

### NMAR Analysis

I found out that there are 3 columns with missing values in my dataset:

|             | number of missing entries |
| :---------- | ------------------------: |
| name        |                         1 |
| description |                        70 |
| rating      |                      2609 |

I believe that the description column is NMAR, since people tend to ignore the description when rating a recipe (unless the experience of making/tasting the recipe is so unforgettable that a user would want to comment). Additional data like time it takes to write a description may be able to explain the missingness.

### Missingness Dependency

I was wondering if the missingness of the rating column has anything to do with the number of calories.

<iframe src="assets/cal-missing.html" width=800 height=600 frameBorder=0></iframe>

We got a P-value of 5.821920986766768e-09 using K-S Statistic. Our result implies that the missingness of the rating column depends on calories (#) column.

I was also wondering if the missingness of the rating column has anything to do with sodium (PDV) column.

<iframe src="assets/sodium-missing.html" width=800 height=600 frameBorder=0></iframe>

We got a P-value of 0.11517155899608289 using K-S Statistic. Our result implies that the missingness of the rating column does not depend on calories (#) column.

## Hypothesis/Permutation Testing

Null Hypothesis: In the population, the average cooking time of recipes with rating more than 3 and that of recipes with rating no more than 3 have the same distribution, and the observed differences in our samples are due to random chance.

Alternate Hypothesis: In the population, the average cooking time of recipes with rating more than 3 is longer than that of recipes with rating no more than 3, on average. The observed differences in our samples cannot be explained by random chance alone.

Test Statistic: Signed difference in group means

Significance Level: 5%

This statistic is reasonable because not only did I want to know if there exists a difference between the 2 disdtributions, I also wanted to know if one has a lower mean than the other.

5% is a common choice for significance level.

<iframe src="assets/permutation-test-rating-min.html" width=800 height=600 frameBorder=0></iframe>

Under the null hypothesis, the chance of us seeing differences as extreme as the observed statistic is close to 60% (way higher than the alpha value of 5%). Thus, we failed to reject the null hypothesis.

---

# Part 2: Recipe Calories Prediction

by Yosen Lin

**_Note_**: Model Building and Prediction Project (Project 5) for DSC 80 at UCSD

---

## Problem Identification

The data that I have access to is a subset of the raw data used in the original report, containing only the recipes and reviews posted since 2008, since the original data is quite large.

RAW_recipes.csv contains the recipes, while RAW_interactions.csv contains the reviews.

The prediction problem I have is predicting the number of calories for each recipe using certain features like sugar (PDV), ingredients, and total fat (PDV) for example. The type of prediction problem in this case is a regression problem. The response variable here is calories (#), as it is one of the most important nutritional values amongst all the features provided in this dataset. I am using both RMSE and R-squared for my metric, as my prediction problem is a regression problem.

The features used are: ingredients, n_ingredients, n_steps, rating, total fat (PDV), saturated fat (PDV), sodium (PDV), carbohydrates (PDV), protein (PDV), sugar (PDV), and minutes.

---

## Baseline Model

For my model, there is one nominal feature (ingredients), while the rest (10) are quantitative features. For ingredients, I wrote a custom function that detects whether if 'sugar' is part of the ingredients of each recipe, as sugar can add on to the number of calories. I then transformed the number of ingredients (n_ingredients) with np.log. The final component of the model is a DecisionTreeRegressor(). The RMSE I got was about 266.34, while the R-squared was about 0.842. The baseline model had a decent performance since it achieved an R-squared score of 0.8 as a baseline model. I believe that the model can do a better job through more transformations and tuning.

---

## Final Model

In addition to the transformation for the nominal feature ingredients, some new features were transformed version of n_ingredients and n_steps, both of which were transformed using QuantileTransformer, as both of the features are more like discrete variables. Another new feature was the transformation of the rating column with StandardScaler(), as rating does not play that big of a role comparing to other features.

The modeling algorithm I chose was DecisionTreeRegressor(), which is the same as the baseline model. I tuned n_quantiles for both of the transformers in the preprocessing ColumnTransformer and max_depth for DecisionTreeRegressor().The hyperparameters that ended up performing the best are:

max_depth=11, n_quantiles for n_ingredients=12, n_quantiles for n_steps=9

The most optimal values above were found GridSearchCV, with the parameter cv set to 5.

The final model's performance is an improvement over the baseline model since the RMSE of the final model is lower than that of baseline model, and the final model has a higher R-squared than the baseline model. Below describes the performances:

Baseline Model - RMSE: 266.34, R-squared: 0.842

Final Model - RMSE: 200.90, R-squared: 0.910

---

## Fairness Evaluation

My choice of Group X and Y are recipes that have ratings higher than 3 and recipes that does not have ratings higher than 3 respectively, as rating does not have that big of an impact on the numer of calories comparing to other variables. For evaluation metric I chose R-squared since the problem I am dealing with is a Regression Problem.

Below are the details of the permutation test used for model fairness evaluation:

Null Hypothesis: Our model is fair. Recipes with ratings higher than 3 and recipes with ratings at most 3 have roughly the same R-squared scores, and any differences are due to random chance.

Alternate Hypothesis: Our model is unfair. Its R-squared for recipes with ratings at most 3 is lower than its R-sqaured for recipes with ratings higher than 3.

Significance Level: alpha=0.05 (Reject null when p-value is smaller than 0.05)

Resulting p-value: 0.35

Conclusion:
Since the p-value (around 35%) is way larger than the threshold 5%, we failed to reject the null hypothesis. Thus, recipes with ratings higher than 3 and recipes with ratings at most 3 have roughly the same R-squared scores, and any differences are due to random chance.

<iframe src="assets/fairness_hypo_test_updated.html" width=800 height=600 frameBorder=0></iframe>

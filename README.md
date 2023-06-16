# recipe-calories-prediction

by Yosen Lin

***Note***: Model Building and Prediction Project (Project 5) for DSC 80 at UCSD

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

<iframe src="assets/fairness_hypo_test.html" width=800 height=600 frameBorder=0></iframe>
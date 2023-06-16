# recipe-calories-prediction

by Yosen Lin

***Note***: Model Building and Prediction Project (Project 5) for DSC 80 at UCSD

---

## Problem Identification

The data that I have access to is a subset of the raw data used in the original report, containing only the recipes and reviews posted since 2008, since the original data is quite large.

RAW_recipes.csv contains the recipes, while RAW_interactions.csv contains the reviews.

The prediction problem I have is predicting the number of calories for each recipe using certain features like sugar (PDV), ingredients, and total fat (PDV) for example. The type of prediction problem in this case is a regression problem. The response variable here is calories (#), as it is one of the most important nutritional values amongst all the features provided in this dataset. I am using both RMSE and R-squared for my metric, as my prediction problem is a regression problem.


---

## Baseline Model

For my model, there is one nominal feature (ingredients), while the rest (10) are quantitative features. For ingredients, I wrote a custom function that detects whether if 'sugar' is part of the ingredients of each recipe, as sugar can add on to the number of calories. I then transformed the number of ingredients (n_ingredients) with np.log. The final component of the model is a DecisionTreeRegressor(). The RMSE I got was about 266.34, while the R-squared was about 0.842. The baseline model had a decent performance since it achieved an R-squared score of 0.8 as a baseline model. I believe that the model can do a better job through more transformations and tuning.
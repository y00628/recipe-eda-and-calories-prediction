# recipe-calories-prediction

by Yosen Lin

***Note***: Model Building and Prediction Project (Project 5) for DSC 80 at UCSD

---

## Problem Identification

The data that I have access to is a subset of the raw data used in the original report, containing only the recipes and reviews posted since 2008, since the original data is quite large.

RAW_recipes.csv contains the recipes, while RAW_interactions.csv contains the reviews.

The prediction problem I have is predicting the number of calories for each recipe using certain features like sugar (PDV), ingredients, and total fat (PDV) for example. The type of prediction problem in this case is a regression problem. The response variable here is calories (#), as it is one of the most important nutritional values amongst all the features provided in this dataset. I am using both RMSE and R-squared for my metric, as my prediction problem is a regression problem.
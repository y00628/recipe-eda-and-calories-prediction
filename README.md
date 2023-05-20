# Recipe Dataset Analysis

by Yosen Lin

***Note***: Exploratoy Data Analysis Project for DSC 80 at UCSD

---

## Introduction

In this project, we studied the effectiveness of spice challenges in building team morale.
The data that I have access to is a subset of the raw data used in the original report, containing only the recipes and reviews posted since 2008, since the original data is quite large.

RAW_recipes.csv contains the recipes, while RAW_interactions.csv contains the reviews.

I was investigating the correlation between the cooking time and average rating of recipes. People 

##### Number of rows: 83782

##### Relevant Columns: 
minutes: number of minutes it takes to prepare each recipe
calories (#): number of calories for each recipe 
sodium: the amount of sodium used for each recipe 
rating: average rating for each recipe

---

## Cleaning and EDA

### Univariate Analysis

<iframe src="assets/cooking-time-uni.html" width=800 height=600 frameBorder=0></iframe>


As you can see, most of the recipes take no more than 150 minutes to prepare. For the recipes that take no more than 150 minutes to prepare, most of the them take about 20 to 50 minutes to prepare. However, as shown on the graph, some can take as long as 10000000 to 100000000 minutes to prepare.

### Bivariate Analysis

<iframe src="assets/calories-min-scatter.html" width=800 height=600 frameBorder=0></iframe>

As you can see, the bottom-left corner of the graph takes is the most dense part of the scatterplot. Notice that there are some data points at the top-left corner of the plot, meaning that the recipe does not have a lot of calories even though it takes a long time to prepare that recipe. On the other hand, there are some data points at the bottom-right corner of the plot, meaning that the recipe has a lot of calories even though it does not take a long time to prepare that recipe.

Note: Recipes that take more than 500000 minutes to prepare or has more than 500000 calories are not on the scatterplot

### Aggregate Analysis

| rating_bins   |   (-0.0001, 20.0] |   (20.0, 50.0] |   (50.0, 150.0] |   (150.0, 250.0] |   (250.0, 1000.0] |   (1000.0, 5000.0] |   (5000.0, 10000.0] |   (10000.0, 100000.0] |   (100000.0, 1000000.0] |   (1000000.0, 10000000.0] |
|:--------------|------------------:|---------------:|----------------:|-----------------:|------------------:|-------------------:|--------------------:|----------------------:|------------------------:|--------------------------:|
| (-0.001, 1.0] |           400.879 |        395.288 |         551.068 |          418.95  |           462.239 |            457.717 |             760.7   |               nan     |                   nan   |                     nan   |
| (1.0, 2.0]    |           379.876 |        409.657 |         549.739 |          620.968 |           371.727 |           1717.21  |             nan     |               nan     |                   nan   |                     nan   |
| (2.0, 3.0]    |           324.398 |        407.104 |         573.432 |          575.752 |           426.47  |            459.271 |             nan     |               440.95  |                   nan   |                     nan   |
| (3.0, 4.0]    |           338.281 |        406.587 |         516.855 |          576.618 |           490.755 |            573.749 |             374.95  |               394.575 |                   836.2 |                     nan   |
| (4.0, 5.0]    |           322.155 |        405.16  |         539.795 |          628.879 |           489.456 |            660.235 |            2307.1   |               584.973 |                    69.4 |                     407.4 |
| nan           |           453.324 |        432.27  |         610.069 |          598.55  |           621.055 |            871.246 |             223.967 |               574.578 |                    75.2 |                     nan   |

---

The table above shows the average calories for different cooking time and rating intervals. This table can be used as a source to explore if the average cooking time and the rating has anything to do with the number of calories of a recipe.


| rating_bins   |   minutes |
|:--------------|----------:|
| (-0.001, 1.0] |   95.9151 |
| (1.0, 2.0]    |   94.7684 |
| (2.0, 3.0]    |   97.0264 |
| (3.0, 4.0]    |  112.166  |
| (4.0, 5.0]    |  112.124  |
| nan           |  228.719  |

The table above shows the average cooking time for different rating intervals. Notice that recipes that have ratings higher than 3 tends to have longer average cooking time in this table. Also notice that recipes without a rating tends to take significantly longer time to prepare comparing to those with ratings.

---

## Assessment of Missingness

Here's what a Markdown table looks like. Note that the code for this table was generated _automatically_ from a DataFrame, using





## Hypothesis Testing


---
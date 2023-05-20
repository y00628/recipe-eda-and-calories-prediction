# Recipe Dataset Analysis

by Yosen Lin

***Note***: Exploratoy Data Analysis Project for DSC 80 at UCSD

---

## Introduction

In this project, we studied the effectiveness of spice challenges in building team morale.
The data that I have access to is a subset of the raw data used in the original report, containing only the recipes and reviews posted since 2008, since the original data is quite large.

RAW_recipes.csv contains the recipes, while RAW_interactions.csv contains the reviews.

I was investigating the correlation between the cooking time and average rating of recipes. People 

Number of rows: 83782
Relevant Columns: 
minutes: number of minutes it takes to prepare each recipe
calories (#): number of calories for each recipe 
sodium: the amount of sodium used for each recipe 
rating: average rating for each recipe

---

## Cleaning and EDA

<iframe src="assets/cooking-time-uni.html" width=800 height=600 frameBorder=0></iframe>

| rating_bins   |   (-0.0001, 20.0] |   (20.0, 50.0] |   (50.0, 150.0] |   (150.0, 250.0] |   (250.0, 1000.0] |   (1000.0, 5000.0] |   (5000.0, 10000.0] |   (10000.0, 100000.0] |   (100000.0, 1000000.0] |   (1000000.0, 10000000.0] |
|:--------------|------------------:|---------------:|----------------:|-----------------:|------------------:|-------------------:|--------------------:|----------------------:|------------------------:|--------------------------:|
| (-0.001, 1.0] |           400.879 |        395.288 |         551.068 |          418.95  |           462.239 |            457.717 |             760.7   |               nan     |                   nan   |                     nan   |
| (1.0, 2.0]    |           379.876 |        409.657 |         549.739 |          620.968 |           371.727 |           1717.21  |             nan     |               nan     |                   nan   |                     nan   |
| (2.0, 3.0]    |           324.398 |        407.104 |         573.432 |          575.752 |           426.47  |            459.271 |             nan     |               440.95  |                   nan   |                     nan   |
| (3.0, 4.0]    |           338.281 |        406.587 |         516.855 |          576.618 |           490.755 |            573.749 |             374.95  |               394.575 |                   836.2 |                     nan   |
| (4.0, 5.0]    |           322.155 |        405.16  |         539.795 |          628.879 |           489.456 |            660.235 |            2307.1   |               584.973 |                    69.4 |                     407.4 |
| nan           |           453.324 |        432.27  |         610.069 |          598.55  |           621.055 |            871.246 |             223.967 |               574.578 |                    75.2 |                     nan   |

---

---

## Assessment of Missingness

Here's what a Markdown table looks like. Note that the code for this table was generated _automatically_ from a DataFrame, using





## Hypothesis Testing


---
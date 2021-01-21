---
layout: post
title:      "The Need for Decision Tree Visualization"
date:       2021-01-21 23:18:53 +0000
permalink:  the_need_for_decision_tree_visualization
---


Recently I was trying to make the best Random Forest model that i can for the Tanzanian water pump predictor (https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/).

The score I used to evaluate the performance of the model is AUC, since one can always adjust the predicted outcome by sliding the threshold probability. I kept getting AUC of 0.85 to 0.90, so I tried different method to improve that.

I have tried diferent max_features:
![](https://raw.githubusercontent.com/zjluoxk/2020_Water_Table/main/images/auc_max_features_dropped.png)

I have tried different n_estimators:
![](https://raw.githubusercontent.com//zjluoxk/2020_Water_Table/main/images/auc_n_estimators_dropped.png)

I also tried to limit the amount of features I provided to the Random Forest estimator:
![](https://raw.githubusercontent.com//zjluoxk/2020_Water_Table/main/images/drop_self_identifying_auc.png)

As far as I can see, there is no major improvement. Then the thought hit me, maybe that's all the data can do. So maybe I can use the model to see which features have the most impact instead.

Therefore I made ranking of the features after using bunch of Recursive Feature Elimination models:
![](https://raw.githubusercontent.com//zjluoxk/2020_Water_Table/main/images/drop_self_identifying.png)

And here's the AUC:
![](https://raw.githubusercontent.com//zjluoxk/2020_Water_Table/main/images/feature_selection_auc.png)

All the evidence points to simple model can do almost the same level of prediction as a complex model. So I thought, maybe I should just visualize a simple, maybe 2 tree, forest. But to my dismal, most the models that's easy accessible to Googling are numerical decision tree models, in which all categorical values have been encoded. This makes the tree uninterpretable even if visualize.

Here is a snip:

nstaller >  -0.81

|   |   |   |   |   |   |   |   |   |   |   |--- truncated branch of depth 8

|   |   |   |   |   |   |   |   |   |--- installer >  -0.68

|   |   |   |   |   |   |   |   |   |   |--- class: 1.0

|   |   |   |   |   |   |   |   |--- quantity_group >  0.22

|   |   |   |   |   |   |   |   |   |--- quantity_group <= 1.46

|   |   |   |   |   |   |   |   |   |   |--- installer <= -0.69

|   |   |   |   |   |   |   |   |   |   |   |--- truncated branch of depth 8

|   |   |   |   |   |   |   |   |   |   |--- installer >  -0.69

|   |   |   |   |   |   |   |   |   |   |   |--- truncated branch of depth 4

|   |   |   |   |   |   |   |   |   |--- quantity_group >  1.46

|   |   |   |   |   |   |   |   |   |   |--- installer <= -0.68

|   |   |   |   |   |   |   |   |   |   |   |--- class: 2.0

|   |   |   |   |   |   |   |   |   |   |--- installer >  -0.68

|   |   |   |   |   |   |   |   |   |   |   |--- truncated branch of depth 3

|   |   |   |   |   |   |   |--- amount_tsh >  -0.18

|   |   |   |   |   |   |   |   |--- class: 2.0

|   |   |   |   |   |   |--- installer >  -0.67

|   |   |   |   |   |   |   |--- installer <= 2.36

|   |   |   |   |   |   |   |   |--- installer <= 0.11


All these features are supposed to be categorical values. But are now not recognizable!


There needs to be categorical Random Forest algorithm easily available!




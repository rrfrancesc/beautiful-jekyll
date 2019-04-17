---
layout: post
title: Machine Learning
subtitle: Predective Classification Models with Random Forest
image: /img/Random_Forest_0.png
tags: [machine learning, random forest, decision tree]
---

I build predictive models about **policy renewal** using Logistic Regression and Random Forest.  
If a company interacts with every single customer, the cost would be too much. Focusing retention efforts on a small subset of high risk policies is a much more effective strategy.

In this post, I’m going to focus on **Random Forest as a classification method**. Unlike *logistic regression*, random forest is better at fitting non-linear data. It can also work well even if there are correlated features, which can be a problem for interpreting logistic regression.

**Random forest** uses *multiple decision trees* to make predictions. *Single decision trees* on their own can be very effective at learning non-linear relationships (low bias, but high variance). Here is an exemple of a simple tree with 3 only features:

![rf1](http://i68.tinypic.com/28wds8j.png)

Due to their high variance, they can tend to over-fit. Random forest reduces this variance by averaging many trees (at the sacrifice of a slight increase in the bias).

In this case, I fit the model to 14 features. So by default, **randomForest() R function** will set mtry = sqrt(14) = 3.74 rounded down = 3. Also, by default random forest generates 500 trees, but 200 would be enough as errors rate do not decrease as we can see in next plot:

![rf3](http://i68.tinypic.com/nwms1h.png)

After I fit the model, let's take a look at the confusion matrix to see how well the model made predictions on the validation set. The accuracy is pretty good!

![rf2](http://i68.tinypic.com/2nizhxj.png)

And in the next plot, we can study the importance of each feature in the prediction model:
![rf4](http://i64.tinypic.com/acfk45.png)

***

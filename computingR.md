---
layout: page
title: Computing with R
subtitle: Powerful tool for insurance analytics...
---

<br>

<img src="http://i67.tinypic.com/2e5vabq.png" width="150">

I began using **R** for data visualisation, and, over time, it has become integral to my workflow. It’s just so flexible, and the more you get immersed in the R world, the more you realise what you can do with it.

At *ERM Re* [(ERM)](http://ermgrupo.com), I'm doing a lot of reinsurance consulting work in **R**. Here you can see some examples of the projects developed.

<br>

## STOP LOSS Reinsurance: 
### Pricing Computing risk premium...
*Parametric Model* using a **LOG NORMAL distribution** to fit the empiric data. Their two parameters are the mean and the sd.

Function to compute the reinsurance pure premium:
```{r}
E <- function (yinf,ysup,par1,par2,premium) {as.numeric(integrate(function(x) (x-yinf) * premium * dlnorm(x,par1,par2), lower=yinf,upper=ysup)$value + (1-plnorm(ysup,par1,par2)) * (ysup-yinf) * premium)}
```
<img src="http://i67.tinypic.com/2w24lg7.png" width="600">
<br>

<img src="http://i68.tinypic.com/16gal2d.jpg" width="600">
* * *
<br>

## Claims Reserving: 
### Using the ChainLadder Package in R...
The *MackChainLadder model* uses the chain ladder approach for predicting ultimate and IBNR values for each row (in this case accident year) for a cumulative loss triangle. The default method of the model predicts the ultimate values using chain ladder ratios with the assumption of no tail factor, and the standard error of the ultimates are approximated using a log linear model. The model also has the option to use two other ratios: the simple average and the weighted average of the development ratios.

<img src="http://i67.tinypic.com/30msuvk.png" width="660">
<br>

The *BootChainLadder* is a model that provides a predicted distribution for the IBNR values for a claims triangle. First, the development factors are calculated and then they are used in a backwards recursion to predict values for the past loss triangle. Then the predicted values and the actual values are used to calculate Pearson residuals. Using the adjusted residuals and the predicted losses from before, the model solves for the actual losses in the Pearson formula and forms a new loss triangle. The steps for predicting past losses and residuals are then repeated for this new triangle. After that, the model uses chain ladder ratios to predict the future losses, calculates the ultimate and IBNR values like in the previous Mack model. This cycle is performed N times. The IBNR for each origin period is calculated from each triangle (N times) and used to form a predictive distribution, from which summary statistics are obtained such as mean, prediction error and quantiles.

<img src="http://i66.tinypic.com/ju97ag.png" width="660">
* * *
<br>

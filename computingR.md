---
layout: page
title: Computing with R
subtitle: Powerful tool for insurance analytics...
---

<br>

<img src="https://i.ibb.co/p0sQxV1/R.png" width="150">

I began using **R** for data visualisation, and, over time, it has become integral to my workflow. It’s just so flexible, and the more you get immersed in the R world, the more you realise what you can do with it.

At *ERSM Re* [(ERSM)](http://ersmgrupo.com), I'm doing a lot of reinsurance consulting work in **R**. Here you can see some examples of the projects developed.

<br>
<br>

## POPULATION PYRAMID ANUMATED PLOT: 
### Video: data manipulation with **tydiverse** packages to get data ready for plotting ...

Original data:
head(data) 

| Index | Region |  Gender | Date | De_0_a_4 | De_05_a_9 | De_10_a_14 | De_15_a_19|  .... |
| ----- | -------| --------|------|----------|-----------|------------|-----------|-------|
|  256  | Africa | Female  | 1950 |   19129  |   14824   |   12918    |    11518  |       |
|   257 | Africa | Female  | 1955 |   21773  |   16776   |   14196    |    12489  |       |
|   258 | Africa | Female  | 1960 |   24786  |   19431   |   16075    |    13654  |       |
|   259 | Africa | Female  | 1965 |   28271  |   22415   |   18794    |    15555  |       |
|   260 | Africa | Female  | 1970 |   32033  |   25841   |   21732    |    18208  |       |
|   261 | Africa | Female  | 1975 |   36719  |   29543   |   25136    |    21172  |       |

Use **pivot_longer()** to get in the same column all the values from different ages... 
```{r}
data_1 <- data %>%
  dplyr::filter(Region %in% c("Africa","Asia","Europe")) %>%
  tidyr::pivot_longer(cols=-c(Index,Region,Country_code,Gender,Date), names_to="Age", values_to="Population") %>%
  dplyr::group_by(Region, Gender, Date, Age) %>%
  dplyr::summarise(n = sum(Population)) %>%
  dplyr::ungroup(Gender) %>%
  dplyr::mutate(freq = n / sum(n))
```
Now, the data is ready for plotting... 

 |Region |Gender  |  Date| Age        |    n|   freq|
 |-------|--------|------|------------|-----|-------| 
 | Africa| Female | 1950 | De_0_a_4   |19129| 0.0840|
 | Africa| Female | 1950 | De_05_a_9  |14824| 0.0651|
 | Africa| Female | 1950 | De_10_a_14 |12918| 0.0567|
 | Africa| Female | 1950 | De_15_a_19 |11518| 0.0506|
 | Africa| Female | 1950 | De_20_a_24 |10091| 0.0443|
 | Africa| Female | 1950 | De_25_a_29 | 8668| 0.0381|

Population pyramid plot:
- **facet_wrap()** to make a plot for each region.
- **transition.states()** from **gganimate** package to move along eacy year.

```{r}
p <- ggplot(data_1, aes(x = Age, fill = Gender,
                 y = ifelse(test = Gender == "Male", yes = -freq, no = freq))) + 
  geom_bar(stat="identity", alpha=.65) +
  scale_y_continuous(labels=scales::percent_format(accuracy=1)) +
  facet_wrap(~Region) +
  scale_fill_viridis_d(option="D") +
  coord_flip() + 
  theme_minimal() +
  theme(panel.spacing=unit(2,"lines"), axis.title=element_text(size=18), plot.title=element_text(size=22), 
        strip.text=element_text(size=18), axis.text=element_text(size=11), 
        panel.border=element_rect(color="gray85", fill=NA)) +
  labs(title = "Population Pyramid", subtitle="From 1950 to 2020", x = "Age", y = "\nPercent of population") +
  geom_text(aes(x=max(Age), y=max(freq), label=as.factor(Date)), alpha=0.3, hjust=1, vjust=0.75, col="gray", size=8) +
  transition_states(as.factor(Date), state_length=50)
```
### Video of the animated plot:
<iframe width="784" height="442" src="https://youtube.com/embed/bUbdwCe2qts" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<br>
* * *
<br>

## STOP LOSS Reinsurance: 
### Pricing Computing risk premium...
*Parametric Model* using a **LOG NORMAL distribution** to fit the empiric data. Their two parameters are the mean and the sd.

Function to compute the reinsurance pure premium:
```{r}
E <- function (yinf,ysup,par1,par2,premium) {as.numeric(integrate(function(x) (x-yinf) * premium * dlnorm(x,par1,par2), lower=yinf,upper=ysup)$value + (1-plnorm(ysup,par1,par2)) * (ysup-yinf) * premium)}
```
<img src="https://i.ibb.co/DLJKtBW/SL-1.png" width="600">
<br>

<img src="https://i.ibb.co/DLJKtBW/SL-2.png" width="600">
<br>
* * *
<br>

## Claims Reserving: 
### Using the ChainLadder Package in R...
The *MackChainLadder model* uses the chain ladder approach for predicting ultimate and IBNR values for each row (in this case accident year) for a cumulative loss triangle. The default method of the model predicts the ultimate values using chain ladder ratios with the assumption of no tail factor, and the standard error of the ultimates are approximated using a log linear model. The model also has the option to use two other ratios: the simple average and the weighted average of the development ratios.

<img src="https://i.ibb.co/0CVMtvS/Mack-Chain-Ladder.png" width="660">
<br>

The *BootChainLadder* is a model that provides a predicted distribution for the IBNR values for a claims triangle. First, the development factors are calculated and then they are used in a backwards recursion to predict values for the past loss triangle. Then the predicted values and the actual values are used to calculate Pearson residuals. Using the adjusted residuals and the predicted losses from before, the model solves for the actual losses in the Pearson formula and forms a new loss triangle. The steps for predicting past losses and residuals are then repeated for this new triangle. After that, the model uses chain ladder ratios to predict the future losses, calculates the ultimate and IBNR values like in the previous Mack model. This cycle is performed N times. The IBNR for each origin period is calculated from each triangle (N times) and used to form a predictive distribution, from which summary statistics are obtained such as mean, prediction error and quantiles.

<img src="https://i.ibb.co/Kqr96bc/Booststrap-Chain-Ladder.png" width="660">
<br>
* * *
<br>

## ReIns Package: 
### An R new package with powerful tools for Reinsurance data analysis...
The *ReIns package* contains implementations of:
- Basic extreme value theory (EVT) estimators and graphical.
- EVT estimators and graphical methods adapted for censored and/or truncated data.
- Splicing of mixed Erlang distributions with EVT distributions (Pareto, GPD).
- Value-at-Risk (VaR), Conditional Tail Expectation (CTE) and excess-loss premium estimates.

It's very useful for fitting claims distributions. One usually wants a fit for the whole distribution. ReIns package proposes the splicing of a Mixed Erlang (ME) distribution for the body and an extreme value distribution, i.e. Pareto or GPD, for the tail. Also, it provides some tools to see how well the spliced distribution fits the data:

<img src="https://i.ibb.co/X3PTts9/ReIns1.png" width="800">
<br>
* * *
<br>

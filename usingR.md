---
layout: page
title: Using R
subtitle: Designing optimal interactive applications...
---

<br>

<img src="http://i67.tinypic.com/2e5vabq.png" width="150">

At *ERM Re*, I'm doing a lot of reinsurance consulting work in **R**. Here you can see some examples of the projects developed.
<br>

<br>

## 3D Analysis: 
### Working with data visualization in 3D...
Building a 3D graphic using **R** and the **rgl package**. RGL is a 3D graphics package that produces a real-time interactive 3D plot. It allows to interactively rotate, zoom the graphics and select regions.

<img src="http://i65.tinypic.com/9s7xwj.png" width="600">
<img src="http://i63.tinypic.com/25tiaad.png" width="600">
* * *
<br>
 
## Spatial Analysis: 
### Leaflet package for map data visualization...
**Leaflet** package lets you create interactive maps right from the R console. It provides a simple and fast way to host *interactive maps* online in R, requiring only a few lines of code for a basic web map. Interactive panning and zooming allows for an explorative view on your pinpointed location and it has therefore a great integration in a workflow with *Shiny*.

<img src="http://i63.tinypic.com/2nvt6vk.png" width="600">
<br>

<img src="http://i67.tinypic.com/111809e.png" width="600">
<br>

<img src="http://i64.tinypic.com/xpc5c6.png" width="600">
* * *
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



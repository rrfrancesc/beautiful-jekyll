---
layout: page
title: Visualization in R
subtitle: Designing interactive applications for Data Visualization...
---

<br>

<img src="https://i.ibb.co/p0sQxV1/R.png" width="150">

At *ERSM Re* [(ERSM)](http://ersmgrupo.com), I'm doing a lot of reinsurance consulting work in **R**. Here you can see some examples of the projects developed.
<br>

<br>


## geom_area() from ggplot2: 
### Using an area plot to study evolution along time... 

With the **purrr** package one can make n plots at the same time with data coming from a list with n elements.  

From *ggplot2*, **geom_area** is great to compare positions along time. In this case, I'm plotting the percentage of quotes that an insurance company is the cheapest along time; and I'm plotting at the same time as many plots as types of covers, with the **map** function from *purrr*. 

```{r}
# plot <- purrr::map2(data_4$data, data_4$Cobertura, .f = function(x,y) { data.frame(x) %>%
    dplyr::count(Fecha_Estudio, Top_1_Cheap_Cia) %>% 
    tidyr::complete(Fecha_Estudio, Top_1_Cheap_Cia, fill=list(n=0) ) %>%
    dplyr::left_join(data.frame(x) %>% group_by(Fecha_Estudio) %>% dplyr::count(Fecha_Estudio, name="total_mes"), by="Fecha_Estudio") %>%  
    dplyr::mutate(percent=n/total_mes) %>%
    ggplot2::ggplot(aes(Fecha_Estudio, percent, fill=Top_1_Cheap_Cia)) + 
    ggplot2::geom_area(color="gray90") +
    scale_fill_viridis(discrete=TRUE) + 
    ggplot2::labs(title=y, x="Mes", y="Porcentaje", subtitle="Porcentaje de cotizaciones más económicas") + 
    ggplot2::scale_y_continuous(labels=percent_format()) + 
    ggplot2::scale_x_date(breaks = unique(data_3$Fecha_Estudio)) + 
    ggplot2::theme(axis.text.x=element_text(colour="gray30",size=9,angle=45, hjust=1)) })

# egg::ggarrange(plots=list(plot[[1]],plot[[2]],plot[[3]]), ncol=1)
```
The result is a clear data visualization in a few lines of code, using the **tidyverse** packages!! 

<img src="https://i.ibb.co/RBcpJPn/Rplot10.png" width="630" height="700">
* * *
<br>

## 3D Analysis: 
### Working with data visualization in 3D...
Building a 3D graphic using **R** and the **rgl package**. RGL is a 3D graphics package that produces a real-time interactive 3D plot. It allows to interactively rotate, zoom the graphics and select regions.

<img src="https://i.ibb.co/120F46H/3d.png" width="600">
<img src="https://i.ibb.co/JFgvcFs/3d2.png" width="600">
* * *
<br>

## Using Plotly in R: 
### Interactive charts...
The **Plotly package** is one of the best R tools to create beautiful and interactive data visualizations.
**Plotly’s R package** is very useful to make interactive heatmaps, geographic map visualizations, and sliders. And it's very easy to turn static ggplot2 visualizations into interactive Plotly visualizations with just one line of code. Here, some examples:

<img src="https://i.ibb.co/XLYL8Cd/Plotly1.png" width="600">
<br>

<img src="https://i.ibb.co/WWHQqCm/Plotly2.png" width="700">
<br>

<img src="https://i.ibb.co/LC7rHZh/Plotly3.png" width="600">
* * *
<br>

## Spatial Analysis: 
### Leaflet package for map data visualization...
**Leaflet** package lets you create interactive maps right from the R console. It provides a simple and fast way to host *interactive maps* online in R, requiring only a few lines of code for a basic web map. Interactive panning and zooming allows for an explorative view on your pinpointed location and it has therefore a great integration in a workflow with *Shiny*.

<img src="https://i.ibb.co/k2TgC60/spatial-1.png" width="700">
<br>

<img src="https://i.ibb.co/6YZpJTP/spatial-3.png" width="600">
<br>

<img src="https://i.ibb.co/HTPnTQh/spatial-4.png" width="600">
* * *
<br>

## Heat Maps: 
### ggplot2 package for data visualization...
A **heatmap** is a literal way of visualizing a table of numbers, where you substitute the numbers with colored cells. So, it is basically a table that has colors in place of numbers. Colors correspond to the level of the measurement. It’s very useful for finding highs and lows and sometimes, patterns.

In this example, it shows the expected XL Premium of a Reinsurance Treaty, depending on Priority and Capacity.

<img src="https://i.ibb.co/N6b2Zg5/Heat-Map.png" width="700">
<br>

Another example, with frequency of use by Product, Sex and Age - Health Insurance.

<img src="https://i.ibb.co/YyHLDWf/Heat-Map-2.png" width="900">
* * *

<br>

## Visual Results with gauge() function: 
### Nice and easy way to visualize your results in a Shiny App...
**flexdashboard** package provides this function to easily *compare reactive results*. A gauge displays a numeric value on a meter that runs between specified minimum and maximum values. Only allows custom colored sectors (e.g. "success", "warning", "danger"). By default all values are colored using the "success" theme color.

Function used:
```{r}
gauge(round(table_AA()$Por_Rtdo_Reas_1[1],2), min=-5, max=20, symbol = '%', label= "Prog_Act.", 
sectors = gaugeSectors(success = c(7.5, 20), warning = c(2.5, 7.5), danger = c(-5, 2.5)))
```
<img src="https://i.ibb.co/938MgZF/gauge-1.png" width="900">
* * *
<br>

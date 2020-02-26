---
layout: post
title: Profit Commission in Proportional Treaties
subtitle: An interactive App to calculate any Reinsurance Profit Commission...
image: /img/profit.jpg
tags: [reinsurance, R, rmarkdown, shiny]
---

On the face of it, a PC is quite simple; it rewards the Reinsured for successfully creating a profit for the reinsurers by rebating an agreed percentage of the profit the treaty has generated during the year.

But, we need to deal with the fact that individual policies ceded to the treaty may still be running when the PC calculation is made and there are bound to be outstanding claims that may take months or even years to settle.

The hardest item deals with the question of the *carry-forward of deficits from previous years*.  Contracts will specify for how many years any deficits may be carried forward.  The most common examples are 3, 5 or to extinction. So, if the total income minus the total outgo results in a negative figure, that figure will be carried forward to the profit commission calculation of the next underwriting year (note: not the next calculation that adjusts the current year) PC.  The deficit will be carried forward for the next 3 or 5 underwriting years, or until it is cancelled out by subsequent profitable years, whichever happens first.

This APP provides **an easy way to compute difficult PC, with many years and many reinsurers**, with different conditions for each reinsurer and year.

**Some images from this tool:**
* * *
#### Shiny App...
![shiny1](https://i.ibb.co/hLjDPNh/Capt-1.png)
* * *
#### Loading Data...
![rshiny2](https://i.ibb.co/bs0pxS5/Capt-2.png)

#### Results Visualization...
![rshiny3](https://i.ibb.co/VS1YNzK/Capt-3.png)
![rshiny4](https://i.ibb.co/TPqJCY1/Capt-4.png)

#### PC Account...
![rshiny5](https://i.ibb.co/rsTg008/Capt-6.png)

#### VIDEO to see how it works...
<iframe width="560" height="315" src="https://www.youtube.com/embed/QI6P_lrFMo0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

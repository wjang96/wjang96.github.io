---
layout: post
title:  "Bubble Plots to Visualize Singapore EC & Condos Transactions"
date:   2023-08-30 20:53:58 +0800
categories: R Leaflet
---

Embed an **interactive map** onto any website! This is in continuation of the previous dataset created in the previous post. Create a bubble plot map using R to unlock visualise transactions data!

## Leaflet and Bubble Plots using R
From our previous dataset, a transaction rental record would be tagged as ‘Low’, Average’, High’, ‘Extreme’ according to the percentile category it falls under during the Quarter. These 4 categories would be represented with different bubble colours in the interactive map.
To add bubbles in specific locations, we use the `addCircles` function. The parameters lng and lat refer to the longitude and latitude. The radius determines the size of the bubble, which we set to be proportional to the square root of the average price. We can also display a pop up when the user’s mouse hovers over the bubble. In our case we display the project name, average price, district.
{% include bubbleprop.html %}

---
layout: post
title:  "Bubble Plots to Visualize Singapore EC & Condos rents figure"
date:   2023-08-30 20:53:58 +0800
categories: R Leaflet
---

Embed an **interactive map** onto any website! This is in continuation of the previous [dataset][dataset] created in the previous post. Create a bubble plot map using R to visualise transactions data!

## Dataset Preparation
From our previous post, we have prepared a dataset that consists of the average rents of 3 bedrooms EC and Condos. A transaction rental record have been tagged as `‘Low’, Average’, High’, ‘Extreme’` according to the percentile category it falls under during the transaction's Quarter. These 4 categories would then be represented with different bubble colours in the interactive map.

## Leaflet and Bubble Plots using R
To add bubbles in specific locations, we use the `addCircles` function. The parameters lng and lat refer to the longitude and latitude. The radius determines the size of the bubble, which we set to be proportional to the square root of the average price. We define a colour palette to categorise our `‘Low’, Average’, High’, ‘Extreme’` rental records. We can also display a pop up when the user’s mouse hovers over the bubble. In our case we display the project name, average price, district.
{% include bubbleprop.html %}
[dataset]: https://github.com/wjang96/URA-transactions-index/blob/main/Output_File/transactions_three_bedder_23q3.csv

---
layout: post
title:  "With an input address, what is your Region, Planning Area & Subzone classified by URA Singapore?"
date:   2023-09-28 20:53:58 +0800
categories: Geopandas GoogleAPI
---

URA release a masterplan every few years and boundaries might change. With property transactions data coming in everyday, how do you identify an address is categorised under the right Planning Area & Region quickly and accurately?

The objective of this post is to explain how to classify a property address with the right Region, Planning Area and Subzone by URA standards.

**A photo of the URA masterplan seperated by Region**
![DF_wideformat]({{ '/assets/regionmap.png' | relative_url }}) 

**A photo of the URA masterplan seperated by Planning Area**
![DF_wideformat]({{ '/assets/planningareamap.png' | relative_url }}) 

Before we start, we need some sample data with Property addresses. To achieve our objective, we also need the Latitude and Longtitude information along with the Property addresses. The data you are working with may come with Latitude and Longtitude information or in another format like SVY21. You may make use of [conversion script][gitrepo] to convert to  Latitude and Longtitude if necessary. 

If the data source you are working on do not have any geocoding information, you may make use of Google Geocoding API to get the Latitude and Longtitude.

{: class="table-of-content"}
* TOC
{:toc}

## 1. Use Google Geocoding API to get the Lat & Long (skip this step if it is not relevant for you)
```python
import googlemaps
from datetime import datetime
import pandas as pd
import json
import csv

#place your googlemaps API key between the '' in next step
gmaps = googlemaps.Client(key='PUT YOUR API KEY')
header = ('"input address","formatted address","Latitude",\"Longitude"')
newdata = []
newdatacsv = []
newdata1 = []
json_data = []

#create a text file with addresses on each line and replace "addresses.txt" with the path to the file
file =open("C:\\Users\\weijin.ang/\\Code\\property_addresses.txt", 'r', encoding = 'utf8')
for line in file:
    line1 = gmaps.geocode(line)
    #extract the relevent values
    lat = line1[0]["geometry"]["location"]["lat"]
    long = line1[0]["geometry"]["location"]["lng"]
    lat = str(lat)
    long = str(long)
    formadd = line1[0]["formatted_address"]
    formadd=str(formadd)
    csvline = '"' + line + '",'+'"' + formadd + '",' + lat +',' +long
    newdatacsv.append(csvline)
print(newdatacsv)

#write the data to csv
with open("C:\\Users\\weijin.ang/\\Code\\property_addresses_with_lat_long.csv", "w+", encoding = 'utf8') as newdatafile:
    newdatafile.write(header + "\n")
    for line2 in newdatacsv:
        newdatafile.write(line2 + "\n")
```




[gitrepo]: https://github.com/cgcai/SVY21

---
layout: post
title:  "URA transactions index"
date:   2023-09-18 21:03:36 +0530
categories: Python Jupyter
---

This repo give insights of rental costs statistics of non-landed private properties (EC & Condos) in Singapore

## Output file 1
1. Price Index by Singapore Districts & No. of Bedroom in June 2023


## Output file 2

2. Price Index by Project & No. of Bedroom in June 2023


## Step
1. Source File is extracted from URA API call - https://www.ura.gov.sg/maps/api/#private-residential-properties-rental-contract (Please register for account and obtain API key)
2. For this API, data is refreshed on a quarterly basis by URA
3. Since it is a simple API, API call is made via Postman and JSON file is obtained
4. Python is used for converting JSON to CSV file and further performing data analysis such as caclulating percentile at districts, noofbedroom level
5. The output file is useful for drawing commentary insights. You may also combine datasets for further analytical purposes such as time-series trend lines.


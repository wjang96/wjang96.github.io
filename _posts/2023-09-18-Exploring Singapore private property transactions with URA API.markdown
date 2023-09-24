---
layout: post
title:  "Exploring Singapore private property transactions with URA API"
date:   2023-08-18 20:53:58 +0800
categories: Python Jupyter
---

Unlocking data insights based on the **rental figures of private non-landed residential properties** in Singapore!
API source: https://www.ura.gov.sg/maps/api/#private-residential-property
Transaction data is published by URA. Update Frequency: End of day of every 15th of the month. If it is a public holiday, the data will be updated on the following working day. 
Retrieval is based on quarterly period. Reference period for data retrieval is required


## Output file 1
1. Price Index by Singapore Districts & No. of Bedroom in June 2023

Eg.

| Bedroom         | 1                | 1                | 1                |2               | 2                | 2                | 
| --------------- | ---------------- | ---------------- | ---------------- |--------------- | ---------------- | ---------------- |
| rental_district | rental_rent_25th | rental_rent_50th | rental_rent_75th | rental_rent_25th | rental_rent_50th | rental_rent_75th |
| `D01 Boat Quay / Raffles Place / Marina` | 4300 | 4900 | 5500 | 5950 | 6850 | 8000 |
| `D02 Chinatown / Tanjong Pagar`          | 3800 | 4400 | 4800 | 4800 | 5500 | 6275 |
| `D03 Alexandra / Commonwealth`           | 3600 | 3900 | 4200 | 4800 | 5300 | 5800 |

## Output file 2

Eg.

| Project | noOfBedRoom | rental_rent| mean_areaSqft| y | x |
| --------------- | ---------------- | ---------------- | ---------------- |---------------- | ---------------- |
| `HILLVIEW HEIGHTS` | 2 | 3666.66 | 950 | 38125.62339 | 20467.25374 |
| `HILLVIEW HEIGHTS` | 3 | 3950 | 1200 | 38125.62339 | 20467.25374 |
| `HILLVIEW HEIGHTS` | 4 | 5750 | 1650 | 38125.62339 | 20467.25374 |

**Steps:**
1. Source File is extracted from URA API call - https://www.ura.gov.sg/maps/api/#private-residential-properties-rental-contract (Please register for account and obtain API key)
2. For this API, data is refreshed on a quarterly basis by URA
3. No need to perform API call on a separate IDE
4. Python is used for converting JSON to CSV file and further performing data analysis such as caclulating percentile at districts, noofbedroom level
5. The output file is useful for drawing commentary insights for Singapore Residental rental market on a quarterly basis. You may also combine datasets for further analytical purposes such as time-series trend lines.

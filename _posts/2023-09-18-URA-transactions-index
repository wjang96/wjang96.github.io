This repo give insights of rental costs statistics of non-landed private properties (EC & Condos) in Singapore

**Output file #1:**
1. Price Index by Singapore Districts & No. of Bedroom in June 2023

Eg.

| Bedroom         | 1                | 1                | 1                |2               | 2                | 2                | 
| --------------- | ---------------- | ---------------- | ---------------- |--------------- | ---------------- | ---------------- |
| rental_district | rental_rent_25th | rental_rent_50th | rental_rent_75th | rental_rent_25th | rental_rent_50th | rental_rent_75th |
| `D01 Boat Quay / Raffles Place / Marina` | 4300 | 4900 | 5500 | 5950 | 6850 | 8000 |
| `D02 Chinatown / Tanjong Pagar`          | 3800 | 4400 | 4800 | 4800 | 5500 | 6275 |
| `D03 Alexandra / Commonwealth`           | 3600 | 3900 | 4200 | 4800 | 5300 | 5800 |

**Output file #2:**

2. Price Index by Project & No. of Bedroom in June 2023

Eg.

| Project | noOfBedRoom | rental_rent| mean_areaSqft| 
| --------------- | ---------------- | ---------------- | ---------------- |
| `HILLVIEW HEIGHTS` | 2 | 3666.66 | 950 |
| `HILLVIEW HEIGHTS` | 3 | 3950 | 1200 |
| `HILLVIEW HEIGHTS` | 4 | 5750 | 1650 |

**Steps:**
1. Source File is extracted from URA API call - https://www.ura.gov.sg/maps/api/#private-residential-properties-rental-contract (Please register for account and obtain API key)
2. For this API, data is refreshed on a quarterly basis by URA
3. Since it is a simple API, API call is made via Postman and JSON file is obtained
4. Python is used for converting JSON to CSV file and further performing data analysis such as caclulating percentile at districts, noofbedroom level
5. The output file is useful for drawing commentary insights. You may also combine datasets for further analytical purposes such as time-series trend lines.


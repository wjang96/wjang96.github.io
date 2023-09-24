---
layout: post
title:  "Exploring Singapore private property transactions with URA API Part 1"
date:   2023-08-18 20:53:58 +0800
categories: Python Jupyter
---


API source: https://www.ura.gov.sg/maps/api/#private-residential-property
Transaction data is published by URA. Update Frequency: End of day of every 15th of the month. If it is a public holiday, the data will be updated on the following working day. 
Retrieval is based on quarterly period. Reference period for data retrieval is required

Creating your **REST API GET Request** can be hassle-free and easy with Python! The entire process can be completed by following a 9-step guide. I constructed a GET request from URA's web API to fetch rental contract data in `.json` format and converted the dataset in `.csv` format for the ease of data load into the database. You can find the .py file stored in my [github repository][gitrepo] as well.

**Below is a 9-step guide (80-line code) on how I constructed the GET request in python to fetch data from URA's web API.**

{: class="table-of-content"}
* TOC
{:toc}

## 1. Register an account with URA to obtain your access key
Find out more here:
```python
https://www.ura.gov.sg/maps/api/#introduction
```

## 2.  Import the required libraries
```python
import json
import requests
import csv
import pandas as pd
```
These `import` statements load Python code that allow us to work with the data output in JSON format and the HTTP protocol. <br>

## 3. Set up the HTTP GET request to retrieve a daily token
A valid token needs to be generated to gain access to the data via URA's web API

```python
# Enter the YearQuarter you wish to extract the data from the API call
refperiod = '23q3'

api_accesskey = 'Key in your access key'
api_url_base= 'https://www.ura.gov.sg/uraDataService/insertNewToken.action'

headers = {'Content-Type': 'application/json',
           'AccessKey': api_accesskey}

def get_token():

    response = requests.get(api_url_base, headers=headers)

    if response.status_code == 200:
        return json.loads(response.content.decode('utf-8'))
    else:
        return None
    
token_info = get_token()

if token_info is not None:
    print("Here's your token: "+'\n'+token_info['Result'])    
else:
    print('[!] Request Failed')
```


## 4. Send GET Request to retrieve data based on refPeriod
To retrieve a list of median rentals of private non-landed residential properties, send GET Request to URA API:
```python
api_url_base2= 'https://www.ura.gov.sg/uraDataService/invokeUraDS?service=PMI_Resi_Rental&'

headers2 = {'Content-Type': 'application/json',
           'AccessKey': api_accesskey,
           'Token': token_info['Result']}

params = {'refPeriod' : refperiod}

def get_data():

    response = requests.get(api_url_base2, params=params, headers=headers2)

    if response.status_code == 200:
        return json.loads(response.content.decode('utf-8'))
    else:
        return None
    
data_info = get_data()

if data_info is not None:
    print("Success! json dataset to convert to csv is embedded in data_info['Result']")   
else:
    print('[!] Request Failed')
```

## 5. Flatten nested data in json file
The data retrieved from URA's web API is in a nested json format. We will need to flatten the nested data using json_normalize.

```python
from pandas.io.json import json_normalize
data = data_info['Result']
flattendata = json_normalize(data,'rental',['project','street','y','x'],errors='ignore')
```

```

```
## 8. Convert json data to .csv file, removing the index number

```python
#convert json data to .csv file, removing the index number
flattendata.to_csv('transaction_resi_converted_raw_csv_' + refperiod + '.csv', index=False)
```

And it's completed! 

[gitrepo]: https://github.com/wjang96/URA-transactions-index

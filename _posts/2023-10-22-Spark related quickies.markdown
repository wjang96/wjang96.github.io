![image](https://github.com/wjang96/wjang96.github.io/assets/72901512/7b805b90-810a-4f11-8457-c30fe8d5d9d8)---
layout: post
title:  "Spark related quickies for building ETL pipelines"
date:   2023-10-22 20:53:58 +0800
categories: Spark Databricks
---

Interesting FAQs & lessons from building ETL pipelines related to spark, dataframe, spark sql, configurations.

There are many resources out there to build your own ETL pipeline using spark. These days, there are many web-based platform for working with Spark and one of the most popular one is Databricks. It allows any user to start your own data engineering project at a relatively low-cost and an easy-to-manage automated cluster management.

Get started to build your own ETL pipeline using a simple architecture like below and at the same, enhance your understanding with Spark!
![DF_wideformat]({{ '/assets/databricks_1.png' | relative_url }}) 

**How do get the list of all spark configurations?**

Use spark context directly in the Databricks notebook to call the getAll function.
```python
sc.getConf().getAll()
```
Another way is via spark instance in the Databricks
```python
spark.sparkContext.getConf().getAll()
```
**How to set a configuration property permanently for all Spark applications run on the same cluster?**

It is possible by modifying the spark-defaults.conf file, located in the spark configuration directory.

When you’re working in Databricks, it’s easier. It is via cluster configuration, under Advanced settings, and inside the Spark tab. 
Refer to Figure 1 sequential numbers in red color to check step by step way to do that.

![DF_wideformat]({{ '/assets/databricks_2.png' | relative_url }}) 

Underneath, the Databricks makes the changes to the same spark-defaults.conf file which is abstracted for Databrick’s users for the sake of 
simplicity.

Note that, modifying the spark-defaults.conf file will affect all spark applications running on the cluster, thus make sure only the intended properties you can make changes to.

**With so many `select` methods using Spark, which is the better one to use?**

The first `select` method below is simple. However, the other 3 select methods allow you to apply column based functions like for eg. alias (changing column name). This give you more flexibility.

```python
#1
df_selected = df.select("id", "name", "location", "country", "lat", "lng", "alt)
#2
df_selected = df.select(df.id, df.name, df.location, df.country, df.lat, df.lng, df.alt)
#3
df_selected = df.select(df["id"], df["name"], df["location"], df["country"], df["lat"], df["lng"], df["alt])
#4
from pyspark.sql.functions import col
df_selected = df.select(col("id").alias("location_id"), col("name"), col("location"), col("country"), col("lat"), col("lng"), col("alt))
```

**Why is databricks magic commands so important & useful?**

Below list is not an exhaustive list but shows you the list of various useful magic commands you can use in Databricks notebook. Essentially, magic commands allow you to write code in multiple languages using the same notebook!
```python
%run: runs a Python file or a notebook.
%sh: executes shell commands on the cluster nodes.
%fs: allows you to interact with the Databricks file system.
%sql: allows you to run SQL queries.
%scala: switches the notebook context to Scala.
%python: switches the notebook context to Python.
```
Examples of using magic commands:
1. Use magic command %fs to check if the file is written as in dbfs
![DF_wideformat]({{ '/assets/databricks_3.png' | relative_url }})

2.Use magic command %run to run your configuration file or common python functions file
![DF_wideformat]({{ '/assets/databricks_4.png' | relative_url }})

**When to use `.groupBy` vs `.agg` method?**
You are not able to use `.groupBy` method if you are intending to perform more than 1 aggregration after the `.groupBy` method.
```python
# this won't work
demo_df\
  .groupBy("driver_name") \
  .sum("points") \
  .countDistinct("race_name") \
  .show()
```
Instead, consider using the `.agg` method.
```python
demo_df\
  .groupBy("driver_name") \
  .agg(sum("points"), countDistinct("race_name") \
  .show()
```

**What is the difference between `createOrReplaceTempView` vs `createOrReplaceGlobalTempView` vs `permanent view`?

| View         | Description                | Scenario                |
| --------------- | ---------------- | ---------------- | 
| `createOrReplaceTempView` | A temporary view is only available within a spark session and within the notebook. If you detach the notebook from the cluster and reattach it, this view is not going to be available. | When your scope is only just a notebook → create the temp view and you only need to access it in this notebook|
| `createOrReplaceGlobalTempView` | A global view compared to a temporary view is available across the whole application and in databricks context, this means the global view is available within all the the notebooks attached to the same cluster.| When you have other notebooks working on the same view|
| `permanent` | Even if you detach notebook from clsuter or terminate cluster and restart, the permanent view would still exist | When you have some pipelines accessing to the views directly, eg. monitoring dashboards|


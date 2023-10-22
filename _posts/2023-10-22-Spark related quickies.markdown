---
layout: post
title:  "Spark related quickies for building ETL pipelines"
date:   2023-10-22 20:53:58 +0800
categories: Spark Databricks
---

Interesting FAQs & lessons from building ETL pipelines related to spark, dataframe, spark sql, configurations.

There are many resources out there to build your own ETL pipeline using spark. There are many web-based platform for working with Spark and one of the
most popular one is Databricks. It allows any user to start your own data engineering project at a relatively low-cost and an easy-to-manage automated 
cluster management.

Get started to build your own ETL pipeline using a simple architecture like below!
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

Note that, modifying the spark-defaults.conf file will affect all spark applications running on the cluster, thus make sure only the intended properties 
you can make changes to.


---
layout:     post
title:      "Pyspark Tricks"
subtitle:   "Learning From Work Assignments"
date:       2017-11-10
author:     "BoyuanZH"
header-img: "img/post-bg-building.jpg"
tags:
    - Pyspark
    - Study Notes
---
#### Work with Date Type Data
1. ```pyspark.sql.functions.unix_timestamp(timestampString, format = 'yyyy-MM-dd HH:mm:ss')```

	This ```unix_timestamp``` can convert string type in the format of date, to timestamp type.
	
	Example:
	
	```
	from pyspark.sql.functions import unix_timestamp
	df = spark.createDataFrame([("11/25/1991",), ("11/24/1991",), ("11/30/1991",)], ['date_str'])
	df2 = df.select('date_str', from_unixtime(unix_timestamp('date_str', 'MM/dd/yyy')).alias('date'))
	df2 DataFrame[date_str: string, date: timestamp]
	df2.show()
+----------+--------------------+
|  date_str|                date|
+----------+--------------------+
|11/25/1991|1991-11-25 00:00:...|
|11/24/1991|1991-11-24 00:00:...|
|11/30/1991|1991-11-30 00:00:...|
+----------+--------------------+
	```

2. The ```mapValues``` **(only applicable on pair RDD)** transformation is like a map (can be applied on any RDD) transform but it has one difference that when we apply map transform on pair RDD we can access the key and value both of this RDD but in case of “mapValues” transformation, it will transform the values by applying some function and key will not be affected.
	
	Example: Following two expression has same output.
	
	```
	rdd3_mapped.reduceByKey(lambda x,y: x+y)
	```
	```
	rdd3_mapped.groupByKey().mapValues(sum)
	```
	
	**Here in `groupByKey` transformation lot of shuffling in the data is required to get the answer, so it is better to use `reduceByKey` in case of large shuffling of data.**
	
3. 
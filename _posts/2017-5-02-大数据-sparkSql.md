---
layout: post
title: sparkSql
categories:  大数据平台开发
tags: [sparkSql]
fullview: true
---

# Spark SQL
### 概述
Spark SQL是Spark的一个组件，用于结构化数据的计算。Spark SQL提供了一个称为DataFrames的编程抽象，DataFrames可以充当分布式SQL查询引擎。

### DataFrames
DataFrame是一个分布式的数据集合，该数据集合以命名列的方式进行整合。DataFrame可以理解为关系数据库中的一张表，也可以理解为R/Python中的一个data frame。DataFrames可以通过多种数据构造，例如：结构化的数据文件、hive中的表、外部数据库、Spark计算过程中生成的RDD等。DataFrame的API支持4种语言：Scala、Java、Python、R。

### SQLContext
Spark SQL程序的主入口是SQLContext类或它的子类。除了基本的SQLContext，也可以创建HiveContext。

### 创建DataFrames
使用SQLContext，spark应用程序（Application）可以通过RDD、Hive表、JSON格式数据等数据源创建DataFrames

### DataFrame操作
	val sc: SparkContext // An existing SparkContext.
	val sqlContext = new org.apache.spark.sql.SQLContext(sc)

	// Create the DataFrame
	val df = sqlContext.read.json("examples/src/main/resources/people.json")

	// Show the content of the DataFrame
	df.show()
	// age  name
	// null Michael
	// 30   Andy
	// 19   Justin

	// Print the schema in a tree format
	df.printSchema()
	// root
	// |-- age: long (nullable = true)
	// |-- name: string (nullable = true)

	// Select only the "name" column
	df.select("name").show()
	// name
	// Michael
	// Andy
	// Justin

	// Select everybody, but increment the age by 1
	df.select(df("name"), df("age") + 1).show()
	// name    (age + 1)
	// Michael null
	// Andy    31
	// Justin  20

	// Select people older than 21
	df.filter(df("age") > 21).show()
	// age name
	// 30  Andy

	// Count people by age
	df.groupBy("age").count().show()
	// age  count
	// null 1
	// 19   1
	// 30   1

### 运行SQL查询程序
Spark Application可以使用SQLContext的sql()方法执行SQL查询操作，sql()方法返回的查询结果为DataFrame格式。

	val sqlContext = ...  // An existing SQLContext
	val df = sqlContext.sql("SELECT * FROM table")

### DataFrames与RDDs的相互转换
Spark SQL支持两种RDDs转换为DataFrames的方式：

* 使用反射获取RDD内的Schema
	* 当已知类的Schema的时候，使用这种基于反射的方法会让代码更加简洁而且效果也很好。
* 通过编程接口指定Schema
	* 通过Spark SQL的接口创建RDD的Schema，这种方式会让代码比较冗长。
	* 这种方法的好处是，在运行时才知道数据的列以及列的类型的情况下，可以动态生成Schema		

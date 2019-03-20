---
title: Postgresql from Spark, how to query?
tags: ["Scala", "Tutorial", "Spark", "Postgresql"]
date: 2019-01-07
excerpt: How to query Postgresql from Spark? Dependencies, passing configurations, executing queries, solution to the famous "No Suitable Driver" problem.
---

## Introduction

![Scala Logo](/assets/scala_logo.png)
![Postgresql Logo](/assets/postgresql_logo.png)

This article will cover how to query Postgresql from Spark, using Scala. To know more about Scala, check out any of [the previous Scala articles](https://leobenkel.com/category/scala/).

## Dependencies

Below, find dependencies needed to add to the `build.sbt` file.

```Scala
libraryDependencies += "org.postgresql" % "postgresql" % "42.2.5"

libraryDependencies += "org.apache.spark" %% "spark-mllib" % sparkVersion % Provided
```

To make sure this is the correct version of `org.postgresql`, check [MavenRepository](https://mvnrepository.com/artifact/org.postgresql/postgresql).



## Which configurations are needed ?
### How to pass the configurations to the Spark job?
## As configuration in spark-submit
## Query Postgresql from Spark
## Exception in thread "main" java.sql.SQLException: No suitable driver
### Like this:
### Related articles

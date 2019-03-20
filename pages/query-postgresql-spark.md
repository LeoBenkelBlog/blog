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

To be able to query Postgresql from Spark, a few configurations must be provided to the Spark job:

* **URL** to the database, which should be of the form: `jdbc:postgresql://[HOST]:[PORT]`
* **User** to log in if the database has the authentication enabled ( which should be )
* **Password** to log in if the database has the authentication enabled ( which should be )
* **Database** if the URL does not contains it already

### How to pass the configurations to the Spark job?

There are three options:

* As configuration using environment variables
* As arguments passed to the jar
* Or, fetched from another endpoint

Only the first option, using environment variables, will be discussed here.

For explanations about the other options, please request them in the comments below.

## As configuration in spark-submit

The idea is to have the configuration stored in the environment variables. After that, call it when starting the Spark job as in the example below:

```Bash
spark-submit \
   --class com.myOrganization.myProject.MyMainClass \
   --master ... \
   --deploy-mode ... \
   --num-executors ... \
   --driver-memory ... \
   --executor-memory ... \
   --conf spark.executor.cores=... \
   --conf spark.serializer=org.apache.spark.serializer.KryoSerializer \
   ... other configurations ...
   --conf spark.postgresql_url=${POSTGRES_URL} \
   --conf spark.postgresql_user=${POSTGRES_USER} \
   --conf spark.postgresql_password=${POSTGRES_PASSWORD} \
   /path/to/my/jar.jar \
   --argument value \
   --argument2 value2
```

All the `...` should be replaced by the proper values. Find below, what each of the environment variables should contain:

* Use `POSTGRES_URL` for the **URL** of the form:
    * `jdbc:postgresql://[HOST]:[PORT]/[DATABASE_NAME]`
* Set `POSTGRES_USER` to the **username** to log in
* `POSTGRES_PASSWORD` is the **password** to log in

## Query Postgresql from Spark

Here is a snippet of code to query a table in Postgresql from Spark:

```Scala
// Get the configurations from spark
val spark: SparkSession = ???
val conf: RuntimeConfig = spark.conf

// Retrieve the JDBC configurations
val jdbcUrl = conf.get("spark.postgres_url")
val jdbcUser = conf.get("spark.postgresql_user")
val jdbcPassword = conf.get("spark.postgresql_password")

// Table to query
val tableName = "Table to fetch"

// Tell spark which driver to use
val driver = "org.postgresql.Driver"

// Load the class
Class.forName(driver)

val df = spark
  .sqlContext
  .read
  .format("jdbc")
  .option("driver", driver)
  .option("url", jdbcUrl)
  .option("user", jdbcUser)
  .option("password", jdbcPassword)
  .option("dbtable", tableName)
  .load()
```

In order to use this code, it is required that Spark must already be started and running. This is not the purpose of this article and is assumed to be already known and done.

The configuration set in the previous section of this article can be read from `SparkSession`, and then `spark.conf`.

Using the `RuntimeConfig`, retrieve the configuration passed above which should contains the right credentials and URL to the Postgresql database from the environment variables.

After this, set which table will be fetched. It will be translated to `SELECT * FROM [tableName]` by `SparkSql`.

Then, make sure that `Spark` knows which driver to use to perform the query. Since, Postgresql is being queried, the Driver here is `org.postgresql.Driver`.

And finally, all the components are gathered so the query can be run. `df` will be a `DataFrame` containing the entirety of the table. Then, it is possible to use traditional `Spark` methods to `filter`, `select` and transform the data as if the Postgresql table was any other `DataFrame`.

## `Exception in thread "main" java.sql.SQLException: No suitable driver`

The Spark job will throw this exception if any of these are missed:

* Did not update the `build.sbt` file with the right dependency.
* Did not call `Class.forName(driver)` before running the query.
* Did not set `option("driver", ...)`.

If the issue persists, please leave a comment below.

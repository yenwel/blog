+++
title = "Building a valid Json in a PySpark"
description = "How to build a valid Json document based on PySpark schema syntax"
date = 2023-01-08
draft = false
slug = "valid-json-in-pyspark"

[taxonomies]
categories = ["data-engineering"]
tags = ["pyspark","json","tutorial"]

[extra]
comments = true
+++

This article is meant for data engineers with some experience in Python and preferably also Pyspark. It will demonstrate how to build a valid Json from the columns of a Spark dataframe. 

## Why build a valid Json document in PySpark  
PySpark is a mature framework and API to do data engineering in a scalable way. Since it is based on the Python language it is possible to reuse a lot of that ecosystem also. One gap I encountered while doing data engineering with PySpark was when I used it to build dataframes on top of REST API calls. One important difference using the Python API and the PySpark API is that in order to be able to make use of the scale out architecture of a Spark cluster you need to implement some parts explicitly in the PySpark API. Otherwise your code will only run locally in Python in your notebook on the driver node in your Spark Cluster and that work will not be distributed to the Spark Cluster. Explicitly shipping Python code can be done aided by User Defined Functions (UDFs). Also for calling REST API in a scalable way can be done via an UDF as demonstrated [here](https://github.com/jamesshocking/Spark-REST-API-UDF). So that is a solved issue and this article does not go further into depth on that. It documents how to use the schema API of PySpark to explicitly define a schema for the output of a REST API call. However when it comes to the input of a REST API call a valid Json may be also sometimes be needed. This article provides this piece of that puzzle. When defining an UDF you may experience difficulties including serialization code. Moreover preparing valid Json strings in a dataframe before using it in a UDF may help debugging and understanding the inputs for your UDF since you can perform analysis on your input columns in the dataframe.

## How to build the valid Json document

Imagine that we want to use a [petstore api](https://petstore.swagger.io/#/) to upload our pets from our datalake.

Let's start by defining our datalake of pets as follows:

    from pyspark.sql import Row
    rowspets =[
        Row( petid = "1", petcategoryid = "1", petcategoryname = "Small", petname = "Fifi", petphotourl = "https://google.com/Fifi.png", pettagid = "1", pettagname = "red"),
        Row( petid = "2", petcategoryid = "2", petcategoryname = "Big", petname = "Rénée", petphotourl = "https://google.com/Réne.png", pettagid = "2", pettagname = "green")
    ]

    dfpets = spark.createDataFrame(rowspets)

We see that in order to add our pets to the petstore we need to use the POST verb and use a specifically formatted json for our pet

    {
        "id": 0,
        "category": {
            "id": 0,
            "name": "string"
        },
        "name": "doggie",
        "photoUrls": [
            "string"
        ],
        "tags": [
            {
            "id": 0,
            "name": "string"
            }
        ],
        "status": "available"
    }

We can use the type system of pyspark to define a template expression to create the body for our request as follows:

    from pyspark.sql.functions import lit, col, to_json, struct, array
    from pyspark.sql.types import IntegerType

    petbodycolexpr = to_json(
        struct(
            col("petid").cast(IntegerType()).alias("id"),
            struct(
                col("petcategoryid").cast(IntegerType()).alias("id"),
                col("petcategoryname").alias("name")
            ).alias("category"),
            udf_encodejson(col("petname")).alias("name"),
            array(
                udf_encodejson(col("petphotourl"))
            ).alias("photoUrls"),
            array(
                struct(
                    col("pettagid").cast(IntegerType()).alias("id"),
                    col("pettagname").alias("name")
                )
            ).alias("tags"),
            lit("available").alias("status")
        )
    ).alias("body")

    petbodycolexpr

Take notice how we can work with other pyspark functions (e.g. for casting an string to an int) and user defined functions to cleanup certain strings that may contain weird characters that are not allowed in a valid json document. The to_json function of the pyspark framework does not seem to handle this. We can then use the pyspark struct function to do object templating and the pyspark array function for list templating. As content we can use the columns in our dataframe or literals defined outside our dataframe with the lit or col pyspark functions. Finally we can give everything in our template a name using an alias.

This results in the following column expression:

    Column<'to_json(struct(CAST(petid AS INT) AS id, struct(CAST(petcategoryid AS INT) AS id, petcategoryname AS name) AS category, <lambda>(petname) AS name, array(<lambda>(petphotourl)) AS photoUrls, array(struct(CAST(pettagid AS INT) AS id, pettagname AS name)) AS tags, available AS status)) AS body'>

We can then use this json template on our dataframe to see the input and the result of our API call side by side:

    dfexecute = dfpets \
        .withColumn("body",petbodycolexpr) \
        .select("*",
        udf_callAPI(
            lit(url),
            lit(verb),
            lit(username),
            lit(password),
            col("body")
            ).alias("statuscode")
    )

## Summary

As you can see the type system on a spark system is very expressive and parallels can be made to how a json document is structured. This allows for templating dataframes as jsondocuments in a very flexible manner.
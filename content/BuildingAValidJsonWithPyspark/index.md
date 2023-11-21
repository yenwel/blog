+++
title = "Building a valid Json in a PySpark"
description = "How to build a valid Json document based on PySpark schema syntax"
date = 2023-12-10
draft = false
slug = "valid-Json-in-PySpark"

[taxonomies]
categories = ["data-engineering"]
tags = ["PySpark","Json","tutorial"]

[extra]
comments = true
+++

This article is meant for data engineers with some experience in Python and preferably also PySpark. It will demonstrate how to build a valid Json from the columns of a Spark dataframe. 

## Why build a valid Json document in PySpark  
PySpark is a mature framework and API to do data engineering in a scalable way. Since it is based on the Python language it is possible to reuse a lot of that ecosystem also. One gap I encountered while doing data engineering with PySpark was when I used it to build dataframes on top of REST API calls. One important difference using the Python API and the PySpark API is that in order to be able to make use of the scale out architecture of a Spark cluster you need to implement some parts explicitly in the PySpark API. Otherwise your code will only run locally in Python in your notebook on the driver node in your Spark Cluster and that work will not be distributed to the Spark Cluster. Explicitly shipping Python code can be done aided by User Defined Functions (UDFs). Also for calling REST API in a scalable way can be done via an UDF as demonstrated [here](https://github.com/jamesshocking/Spark-REST-API-UDF). So that is a solved issue and this article does not go further into depth on that. It documents how to use the schema API of PySpark to explicitly define a schema for the output of a REST API call. However when it comes to the input of a REST API call a valid Json may be also sometimes be needed. This article provides this piece of that puzzle. When defining an UDF you may experience difficulties including serialization code. Moreover preparing valid Json strings in a dataframe before using it in a UDF may help debugging and understanding the inputs for your UDF since you can perform analysis on your input columns in the dataframe.

## How to build the valid Json document

Imagine that we want to use a [petstore api](https://petstore.swagger.io/#/) to upload our pets from our datalake.

Let's start by defining our datalake of pets as follows:

    from PySpark.sql import Row
    rowspets =[
        Row( petid = "1", petcategoryid = "1", petcategoryname = "Big", petname = "Bite", petphotourl = "https://en.wikipedia.org/wiki/Nile_crocodile#/media/File:NileCrocodile.jpg", pettagid = "1", pettagname = "green"),
        Row( petid = "2", petcategoryid = "2", petcategoryname = "Medium", petname = "Jason", petphotourl = "https://en.wikipedia.org/wiki/Cat#/media/File:Orange_tabby_cat_sitting_on_fallen_leaves-Hisashi-01A.jpg", pettagid = "2", pettagname = "orange"),
        Row( petid = "3", petcategoryid = "3", petcategoryname = "Small", petname = "Sparky", petphotourl = "https://en.wikipedia.org/wiki/Rose-ringed_parakeet#/media/File:Rose-ringed_Parakeet_(Psittacula_krameri)-_Female_on_a_Neem_(Azadirachta_indica)_tree_at_Hodal_Iws_IMG_1279.jpg", pettagid = "1", pettagname = "green")
    ]

    dfpets = spark.createDataFrame(rowspets)

![live view of our petstore](petstore.png)

We see that in order to add our pets to the petstore we need to use the POST verb and use a specifically formatted Json for our pet

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

We can use the type system of PySpark to define a template expression to create the body for our request as follows:

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

Take notice how we can work with other PySpark functions (e.g. for casting an string to an int) and user defined functions to cleanup certain strings that may contain weird characters that are not allowed in a valid Json document. The to_Json function of the PySpark framework does not seem to handle this. We can then use the PySpark struct function to do object templating and the PySpark array function for list templating. As content we can use the columns in our dataframe or literals defined outside our dataframe with the lit or col PySpark functions. Finally we can give everything in our template a name using an alias.

To summarize the equivalence between Json and our PySpark Object Notation:
* Json [] is PySpark array()
* Json {} is PySpark struct()
* Json key : val is PySpark col("val").alias("key") or lit("lit").alias("key")

This results in the following column expression:

    Column<'to_json(struct(CAST(petid AS INT) AS id, struct(CAST(petcategoryid AS INT) AS id, petcategoryname AS name) AS category, <lambda>(petname) AS name, array(<lambda>(petphotourl)) AS photoUrls, array(struct(CAST(pettagid AS INT) AS id, pettagname AS name)) AS tags, available AS status)) AS body'>

We can then use this Json template on our dataframe to see the input and the result of our API call side by side:

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

As you can see the type system on a spark system is very expressive and parallels can be made to how a Json document is structured. This allows for templating dataframes as Jsondocuments in a very flexible manner.
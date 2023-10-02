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
PySpark is a mature framework and API to do data engineering in a scalable way. Since it is based on the Python language it is possible to reuse a lot of that ecosystem also. One gap I encountered while doing data engineering with PySpark was when I used it to build dataframes on top of REST API calls. One important difference using the Python API and the PySpark API is that in order to be able to make us of the scale out architecture of a Spark cluster you need to implement some parts explicitly in the PySpark API. Otherwise your code will only run locally in Python in your notebook on the driver node in your Spark Cluster and that work will not be distributed to the Spark Cluster. Explicitly shipping Python code can be done aided by User Defined Functions (UDFs). Also for calling REST API in a scalable way can be done via an UDF as demonstrated [here](https://github.com/jamesshocking/Spark-REST-API-UDF). So that is a solved issue and this article does not go further into debt onto that. It documents how to use the schema API of PySpark to explicitly define a schema for the output of a REST API call. However when it comes to the input of REST API call a valid Json may be also sometimes be needed. This article provides this piece of that puzzle.

## How to build the valid Json document

    from pyspark.sql.functions import to_json, struct, array

    def getbodycolexpr(colattlistpar):
        bodycolexpr = to_json(struct(
            lit(jiraassetobjectid).cast(StringType()).alias("objectTypeId"),
            array(
            [
                struct(lit(colatt["id"]).alias("objectTypeAttributeId"),
                array(
                    struct(
                        udfencodejson(
                            col(
                                colatt["column"]
                            )
                        ).alias("value") if colatt["type"] == "Text" else 
                        col(
                            colatt["column"]
                        ).cast(StringType()).alias("value")
                    )
                ).alias("objectAttributeValues")) for colatt in colattlistpar
            ]).alias("attributes")
        )).alias("body")
        return bodycolexpr
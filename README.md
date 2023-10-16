# Practical Data Science on AWS Cloud Specialization

Reference: <a href="https://www.deeplearning.ai/courses/practical-data-science-specialization/">Practical Data Science on AWS Cloud Specialization</a>

1. [Course 1: Analyze Datasets and Train ML Models using AutoML](#1)
   1. [Intro to Practical Data Science](#2)
   2. [Working with data](#3)
   3. 
Course 2: Build, Train, and Deploy ML Pipelines using BERT
Course 3: Optimize ML Models and Deploy Human-in-the-Loop Pipelines

<a name="1"></a>
## Course 1: Analyze Datasets and Train ML Models using AutoML

<a name="2"></a>
### Intro to Practical Data Science

The whole idea is to go from local to cloud to handle large datasets. 

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/overview.PNG)

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/ML-Workflow.PNG)

#### Scale up vs. Scale out 

One of the biggest benefits of developing and running data science projects in the Cloud is the agility and elasticity that the Cloud offers. Maybe your model training takes too long because it consumes all of the CPU resources of the compute instance you have chosen. You can switch to using a compute instance that has more CPU resources, or even switch up to a GPU-based compute instance. This is referred to as scaling up or instead of training your model on a single CPU instance, say you want to perform **distributed model training in parallel across various compute instances**. This is referred to as **scaling out**. 

**Data Exploration**: 

For data exploration, we can use Amazon S3 and AWS Glue to ingest and catalog the data, and then explore the data with SQL queries using Amazon Athena.

The project we will be working on in this specialization would be:

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/project.PNG)

 A great resource to explore product reviews are e-commerce sites. You can use the review text as the input feature for the model training and the sentiment as a label for model training. The sentiment class is usually expressed as an integer value for model training such as 1 for positive sentiment, 0 for neutral sentiment, and -1 for negative sentiment:
 
![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/product-review.PNG)

<a name="3"></a>
### Working with data

#### Data lake

One of the largest advantages of performing data science in the cloud is that you can store and process virtually any amount of data. The **infrastructure scales elastically with the size of your data.**

Data lake as the centralized and secure repository can store, discover, and share virtually any amount and any type of your data. You can ingest data in its raw format without any prior data transformation. Whether it's structured relational data in the form of CSV or TSV files, semi-structured data such as JSON or XML files, or unstructured data such as images, audio, and media files. 

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/data%20lakes.PNG)

**Data lakes are often built on top of object storage, such as Amazon S3.** 

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/data%20lakes%20on%20S3.PNG)

**File storage vs. block storage vs. object storage**: 

**File storage** stores and manages data as individual files organized in hierarchical file folder structures. In contrast, **block storage** stores and manages data as individual **chunks called blocks**. Each block receives a unique identifier, but no additional metadata is stored with that block. With **object storage**, data is stored and managed as objects, which consists of the **data itself, any relevant metadata**, such as when the object was last modified, and a unique identifier. **Object storage is particularly helpful for storing and retrieving growing amounts of data of any type, hence it's the perfect foundation for data lakes.**

**With a data lake in place, you can now use this **centralized data repository to enable data warehousing analytics and also machine learning.**

#### AWS Data Wrangler 

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/wrangler.PNG)

#### AWS Glue

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/register%20data%20with%20glue.PNG)

Amazon Athena 

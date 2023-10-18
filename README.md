# Practical Data Science on AWS Cloud Specialization 

Reference: <a href="https://www.deeplearning.ai/courses/practical-data-science-specialization/">Practical Data Science on AWS Cloud Specialization</a>

1. [Course 1: Analyze Datasets and Train ML Models using AutoML](#1)
   1. [Intro to Practical Data Science](#2)
   2. [Working with data](#3)
      1. [Data ingestion and exploration](#4)
         1. [Data lake](#5)
         2. [AWS Data Wrangler](#6)
         3. [AWS Glue](#7)
         4. [Amazon Athena](#8)
      2. [Data visualization](#9)
   3. [Statistical bias and feature importance](#10) 

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

<a name="4"></a>
#### Data ingestion and exploration]

<a name="5"></a>
##### Data lake

One of the largest advantages of performing data science in the cloud is that you can store and process virtually any amount of data. The **infrastructure scales elastically with the size of your data.**

Data lake as the centralized and secure repository can store, discover, and share virtually any amount and any type of your data. You can ingest data in its raw format without any prior data transformation. Whether it's structured relational data in the form of CSV or TSV files, semi-structured data such as JSON or XML files, or unstructured data such as images, audio, and media files. 

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/data%20lakes.PNG)

**Data lakes are often built on top of object storage, such as Amazon S3.** 

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/data%20lakes%20on%20S3.PNG)

**File storage vs. block storage vs. object storage**: 

**File storage** stores and manages data as individual files organized in hierarchical file folder structures. In contrast, **block storage** stores and manages data as individual **chunks called blocks**. Each block receives a unique identifier, but no additional metadata is stored with that block. With **object storage**, data is stored and managed as objects, which consists of the **data itself, any relevant metadata**, such as when the object was last modified, and a unique identifier. **Object storage is particularly helpful for storing and retrieving growing amounts of data of any type, hence it's the perfect foundation for data lakes.**

**With a data lake in place, you can now use this **centralized data repository to enable data warehousing analytics and also machine learning.**

<a name="6"></a>
##### AWS Data Wrangler 

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/wrangler.PNG)

useful link: https://github.com/aws/aws-sdk-pandas

<a name="7"></a>
##### AWS Glue

This **data catalog service** is used to register or catalog the data stored in S3. **similar to taking inventory in a shop**, you need to know what data is stored in your S3 data lake, or bucket (as an individual container for objects). Using the Data Catalog Service, you create a reference to the data, basically S3 to table mapping. The **AWS Glue table**, which is created inside an AWS Glue database, **only contains the metadata information such as the data schema**. It's important to note that **no data is moved**. All the data remains in your S3 location. You catalog where to find the data and which schema should be used, to query the data. Instead of manually registering the data, you can also use **AWS Glue Crawler**. A Crawler can be used and set up to run on a schedule or to automatically find new data, which includes inferring the data schema and also to update the data catalog. 

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/register%20data%20with%20glue.PNG)

**How to register the data?**

You can use the AWS Data Wrangler tool:

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/register%20data%20with%20glue%202.PNG)

The catalog.create_CSV_table function will only store the schema and the metadata in the AWS Glue Data Catalog table that you specify. **The actual data again remains in your S3 bucket**. Now you can query the data stored in S3, using a tool called Amazon Athena

<a name="8"></a>
##### Amazon Athena 

Athena is 
+ an interactive queries service that lets you run standard SQL queries to explore your data. \
+ Athena is serverless, which means you don't need to set up any infrastructure to run those queries,
+ no matter how large the data is that you want to query, you can simply type your SQL query, referencing the dataset schema you provided in the **AWS Glue Data Catalog.**
+ No data is loaded or moved, 

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/quering%20the%20data.PNG) 

**Again, this database and table only contains the metadata of your data.** The data still resides in S3, and when you run this Python command, AWS Data Wrangler will send this SQL query to Amazon Athena. Athena then runs the query on the specified dataset and stores the results in S3, and it also returns the results in a Pandas DataFrame, as specified in the command shown here.

Given this simplicity, you might wonder what is so special about this, and I have to admit the SQL query I've shown here was fairly simple. But just imagine building highly complex analytical queries to run against not just gigabytes, but potentially terabytes, or petabytes of data. Using Athena, you don't have to worry about any compute and memory resources to support this query, because Athena will automatically scale out and split the query into simpler queries to run in parallel against your data. **Athena is based on Presto, an open-source distributed SQL engine**, developed for this exact use case, running interactive queries against data sources of all sizes. And remember, no installation or infrastructure setup is needed, and no data movement is required. Just register your data with AWS Glue and use Amazon Athena to explore your datasets from the comfort of your Python environment.

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/quering%20the%20data%202.PNG)

<a name="9"></a>
#### Data visualization 

Depending on what kind of data you are exploring and what kind of relationships in the data you're looking for, the type of visualizations you use might be different.

Popular Python data analysis and visualization tools
+ Pandas
+ Numpy
+ Matplotlib
+ Seaborn 

<a name="10"></a>
### Statistical bias and feature importance

We use the following AWS tools to perform bias detection on our training data sets:
+ SageMaker Data Wrangler and
+ SageMaker Clarify 

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/bias.PNG)

Causes of the statistical bias:

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/bias%20causes.PNG)

+ Activity bias is caused by the human-generated content in social media, the reason is that a very small percentage of people actively participate in social media platforms so the data collected is not representative of the entire population
+ Societal bias, also caused by human-generated content, not only on social media but these biases could also be generated because of preconceived notions in society because all humans have unconscious bias
+ Selection bias (**feedback loop**) can be introduced by the ML itself. Take, for example, a streaming service. You want to watch a movie on the streaming service and the streaming service makes a few recommendations for you, and you decide to watch Dancing with Wolves. You like the movie and you rate it high. From then on, the streaming service is recommending you the movies that have wolves in them. It's partly because of the **feedback** you provided to the service. But in reality, maybe you watched that movie because you like the actors in the movie, and you don't even particularly like wolves. Situations like this could result in selection bias, that includes a feedback loop, that involves both the model consumers and the machine learning model itself.
+ Data drift happens, especially when the data distribution significantly varies from the distribution of the training data that was used to initially train the model. This is called data drift and also data shift. There are several different variations of data drift. Sometimes the distribution of the **independent variables or the features** that make up your dataset can change. That's called covariant drift. Sometimes the **data distribution of your labels or the targeted variables** might change. That's the second one, which is prior probability drift. Sometimes the relationship between the two, that is the relationship between the features and the labels can change as well. That's called concept drift. Concept drift, also called as concept shift, can happen when the definition of the label itself changes based on a particular feature, like age or geographical location. 

Measuring statistical bias

When we talk about these metrics, it's important to understand that these metrics are applicable to a particular facet of your dataset. A facet is a sensitive feature in your dataset, that you want to analyze for these imbalances. Let's take, for example, the product review dataset. In that dataset or product category, there could be a facet, or a feature of interest for you, that you want to analyze for imbalances.

Metrics used to measure imbalance in data:
+ Class imbalance (CI)
+ Difference in proportions of labels (DPL)

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/CI.PNG)

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/DPL.PNG)

More metrics: https://docs.aws.amazon.com/sagemaker/latest/dg/clarify-measure-data-bias.html

Detect statistical bias with Sagemaker Data Wrangler

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/sagemaker%20data%20wrangler.PNG)

Data Wrangler provides you with capabilities to connect to various different sources for your data, visualize the data, and transform the data, by applying any number of transformations in the Data Wrangler environment, and, detect statistical bias in your data sets, and generate reports about the bias detected in those data sets. It also provides capabilities to provide feature importance calculations on your training data set.

Detect statistical bias with Amazon SageMaker Clarify

+ it can perform bias detection in trained and deployed models
  
![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/clarify.PNG)

We use the clarify library from the Sagemaker SDK:

      from sagemaker import clarify
      
      clarify_processor = clarify.SageMakerClarifyProcessor(
         role = role,
         instance_count = 1,
         instance_type = 'ml.c5.2xlarge',
         sagemaker_session = sess)
      
      bias_report_output_path = 'my S3 path'

Some points:

+ SageMaker Clarify Processor is a construct that allows you to scale the bias detection process into a distributed cluster: instance_count represents the number of nodes that are included in the cluster, and instance_type represents the processing capacity of each individual node in the cluster.

The next step is to configure the data config object on the Clarify library:

      bias_data_config = clarify.DataConfig(
         s3_data_input_path = ...,
         s3_output_path = ...,
         label = 'sentiment',
         headers = df_balanced.columns.to_list(),
         dataset_type = 'text/csv') 
         

      bias_config = clarify.BiasConfig(
         label_values_or_threshold=[...],
         facet_name = 'product_category')

Once you have configured those three objects, you are ready to run the pre-training bias method on the Clarify processor:

      clarify_processor.run_pre_training_bias(
         data_config = ...,
         data_bias_config = ...,
         methods = ['CL', 'DPL', ...],
         wait = True,
         logs = True)

   

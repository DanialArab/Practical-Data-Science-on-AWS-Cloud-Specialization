# Practical Data Science on AWS Cloud Specialization

Reference: <a href="https://www.deeplearning.ai/courses/practical-data-science-specialization/">Practical Data Science on AWS Cloud Specialization</a>

Course 1: Analyze Datasets and Train ML Models using AutoML
Course 2: Build, Train, and Deploy ML Pipelines using BERT
Course 3: Optimize ML Models and Deploy Human-in-the-Loop Pipelines

## Analyze Datasets and Train ML Models using AutoML

![](https://github.com/DanialArab/images/blob/main/Practical-DS-with-AWS/ML-Workflow.PNG)

### Scale up vs. Scale out 

One of the biggest benefits of developing and running data science projects in the Cloud is the agility and elasticity that the Cloud offers. Maybe your model training takes too long because it consumes all of the CPU resources of the compute instance you have chosen. You can switch to using a compute instance that has more CPU resources, or even switch up to a GPU-based compute instance. This is referred to as scaling up or instead of training your model on a single CPU instance, say you want to perform **distributed model training in parallel across various compute instances**. This is referred to as **scaling out**. 

### Data exploration

For data exploration, we can use Amazon S3 and AWS Glue to ingest and catalog the data, and then explore the data with SQL queries using Amazon Athena.


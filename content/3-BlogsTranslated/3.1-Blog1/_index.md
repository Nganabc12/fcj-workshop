---
title: "Blog 1: Machine Learning Pipelines"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Understanding Machine Learning Pipelines: The Journey to Bring AI Models into Reality

## Original Article Information

| Item | Details |
|------|---------|
| **Original Title** | Machine Learning Pipelines |
| **Original Author** | Accenture |
| **Published Date** | July 27, 2022 |
| **Original Source** | https://docs.aws.amazon.com/whitepapers/latest/accenture-ai-scaling-ml-and-deep-learning-models/machine-learning-pipelines.html |
| **Translated by** | Nguyễn Hoàng Sơn |
| **Translation Published** | June 9, 2026 |
| **Translated Blog** | https://www.facebook.com/share/p/18qaf9Rky8/ |

---

## Introduction

While exploring AI and Machine Learning technologies on AWS, I came across an AWS Whitepaper that explains how Machine Learning models are developed and deployed at an enterprise scale. What impressed me most was not the complexity of Machine Learning algorithms, but a practical question:

**How can an AI model be moved from a personal computer to a production environment where it can serve millions of users?**

Previously, I believed that building an AI application mainly involved collecting data, training a model with Python or Jupyter Notebook, and completing the project. However, the AWS Whitepaper highlights that developing the model itself is only a small part of the entire process. Most of the work lies in designing the infrastructure, automating workflows, deploying the model, and maintaining a reliable production environment.

This is why **Machine Learning Pipelines** play a critical role in modern MLOps. They automate the entire Machine Learning lifecycle, from data collection and preprocessing to model training, deployment, monitoring, and continuous improvement.

---

> **Note:** This article is translated and summarized from the AWS Whitepaper **"Accenture Enterprise AI: Scaling Machine Learning and Deep Learning Models"** for educational and learning purposes only. All copyrights belong to **Amazon Web Services (AWS)** and **Accenture**.


That is why the concept of **Machine Learning Pipelines** was born.

---

## What problem does the Machine Learning Pipeline architecture solve?

According to the article, for an AI model to run smoothly in reality, it needs to go through an automated assembly line (pipeline). Instead of running each step manually, a good Pipeline will link all these tasks together into a fully automated loop.

**Core steps in the Pipeline include:**

- **Data Ingestion:** Automatically pull the latest raw data from massive storage repositories.
- **Data Preprocessing:** Clean, standardize formatting, and perform Feature Engineering on the data.
- **Training & Tuning:** Let the AI relearn from the new data to become smarter, while automatically performing Hyperparameter tuning.
- **Deployment:** Bring the trained AI model to servers as Endpoints to serve users in real-time or via batch processing.

![Machine Learning Process](/images/3-BlogsTranslated/blog1-1.png)

---

## Technology Selection for Pipeline Stages

When applying this model on AWS, we need to map the above steps with corresponding Cloud services. Below is a summary table of commonly considered technologies:

| Pipeline Stage | Core AWS Services | Main Function in the System |
| ----------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Storage & Data Ingestion** | Amazon S3, AWS Lake Formation, Amazon RDS | Provides a centralized Data Lake, storing raw data and processed data. |
| **Data Preprocessing** | AWS Glue, Amazon SageMaker Data Wrangler | Runs ETL (Extract, Transform, Load) jobs to clean data at scale. |
| **Model Training** | Amazon SageMaker Training Instances, EC2 | Provisions server clusters with powerful GPUs to train AI, then automatically shuts them down when finished. |
| **Deployment & Inference** | Amazon SageMaker Endpoints, API Gateway, AWS Lambda | Packages the model into a REST API for the application's Frontend/Backend to invoke. |

![Machine Learning Engineering](/images/3-BlogsTranslated/blog1-2.png)

---

## Breaking Down Components in the MLOps System

Similar to breaking down an application into Microservices, an AI system in Production is also divided into loosely coupled modules:

### 1. Data Storage Hub
Instead of using a regular relational database, the AI system utilizes **Amazon S3** as its foundation.
- Stores terabytes of unstructured image, text, and CSV data.
- Stores artifacts (the model's `.tar.gz` weight files) after the training process is completed.

### 2. Orchestration Layer
For the steps (Ingestion -> Processing -> Training) to run automatically, we need an orchestration tool like **AWS Step Functions** or **SageMaker Pipelines**. 
- This system operates on an *event-driven* model. For example: When a new data file is uploaded to S3, it automatically triggers a Lambda function to initiate the entire model retraining workflow.

> *Only allow external applications to invoke the AI model through a single endpoint (API Gateway) → Ensures traffic control and strict security.*

---

## Automation and Infrastructure as Code

To manage AI infrastructure, Cloud engineers often use Infrastructure as Code (IaC) to define the Pipeline. Here is an example of an automated configuration creating an S3 Bucket to hold Training data using **AWS CloudFormation**:

```yaml
Resources:
  MLTrainingDataBucket:
    Type: 'AWS::S3::Bucket'
    Properties:
      BucketName: !Sub '${AWS::StackName}-ml-training-data'
      VersioningConfiguration:
        Status: Enabled
      LifecycleConfiguration:
        Rules:
          - Id: TransitionToGlacier
            Status: Enabled
            Transitions:
              - TransitionInDays: 90
                StorageClass: GLACIER
Outputs:
  TrainingBucketName:
    Value: !Ref MLTrainingDataBucket
    Export:
      Name: !Sub '${AWS::StackName}-TrainingBucket'
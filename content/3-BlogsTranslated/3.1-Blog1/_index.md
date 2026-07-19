---
title: "Blog 1: Machine Learning Pipelines"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Understanding Machine Learning Pipelines: The Journey to Bring AI Models into Reality

*Original post link: [AWS Study Group Facebook Group](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2178072669624360/?rdid=xF88278FD6QFnlfz#)*


While exploring AI/ML technical documents on AWS, I read a whitepaper about scaling Machine Learning models. What caught my attention wasn't the complex machine learning algorithms, but an extremely practical problem: **How do we bring an AI model from a personal computer to a production environment so millions of users can utilize it?**

Previously, when hearing about AI, I immediately thought of Data Scientists downloading data to their machines, writing Python code (like Jupyter Notebook) to train the AI to become smart, and that's it.

However, the AWS article pointed out a harsh reality: Creating a high-quality AI model only accounts for about 20% of the workload. The remaining 80% of the effort lies in building an infrastructure system to maintain and operate that model. 

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
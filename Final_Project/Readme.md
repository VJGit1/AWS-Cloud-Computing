# Predicting the next FIFA World Cup Champion

This is the final project for DATS 6450, developed by:
* Joshua Gray
* Vaijayanti Deshmukh
* Lasya Raghavendra

## 🎯 Project Scope

This project aims to design and deploy a scalable AWS-based machine learning environment capable of predicting the next FIFA World Cup champion using historical and contemporary football data. [cite: 6]

The system integrates data engineering, analytics, and machine learning pipelines across three separate AWS accounts, each managed by a different team member to ensure balanced collaboration and modular responsibility. [cite: 7]

## ☁️ AWS Architecture

Our project uses a secure, multi-account pipeline that separates the duties of each team member.

* **Account 1: Data Engineer (Lasya)**
    * **AWS Lambda** ingests raw data from public sources (Kaggle, FIFA.com). 
    * **Shared S3 Bucket** stores all raw data.
    * **Amazon DynamoDB** tracks metadata for the ingestion process (e.g., data source, timestamps). 

* **Account 2: Data Analyst (Vaijayanti)**
    * **AWS Glue** jobs run on the raw data in S3 to transform it and create predictive features. 
    * **Key Engineered Features** include Team Performance (Recent Form, H2H Record), Player Strength (Star Player Factor), and Match Context (Host Advantage). 
    *Processed data is saved back to the **Shared S3 Bucket**. 
    * **Amazon Athena** is used to make the clean feature set queryable for analysis. 

* **Account 3: ML Engineer (Joshua)**
    * **Amazon SageMaker Studio** reads the clean features from S3 to train and evaluate the prediction model. 
    * The trained model is deployed to a live **EC2 Endpoint** to serve real-time predictions. 
    * **Amazon QuickSight** is used to build a "World Cup Insights" dashboard for visualizing predictions and statistics. 


## 🏆 Expected Outcomes

1.  **A Trained & Deployed Prediction Model:** A model trained in SageMaker (Account 3) and deployed as a live EC2 Endpoint. 
2.  **An Interactive "Insights" Dashboard:** A "World Cup Insights" dashboard, built in QuickSight (Account 3), to visualize model predictions and allow users to analyze team and player statistics.
3.  **A Clean & Queryable Feature Set:** A production-ready, clean dataset of engineered features, processed by AWS Glue (Account 2), and made queryable for analysts via Amazon Athena. 
4.  **A Secure, Multi-Account Pipeline:** A governed and secure data pipeline using VPC Peering and IAM Roles that separates the duties of Data Engineering (Account 1), Data Analysis (Account 2), and ML Engineering (Account 3). 
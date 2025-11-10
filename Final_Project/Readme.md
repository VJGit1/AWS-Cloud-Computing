# Predicting the next FIFA World Cup Champion

This is the final project for DATS 6450, developed by:
* Joshua Gray
* Vaijayanti Shrikant Deshmukh
* Lasya Raghavendra

## 🎯 Project Scope

[cite_start]This project aims to design and deploy a scalable AWS-based machine learning environment capable of predicting the next FIFA World Cup champion using historical and contemporary football data. [cite: 6]

[cite_start]The system integrates data engineering, analytics, and machine learning pipelines across three separate AWS accounts, each managed by a different team member to ensure balanced collaboration and modular responsibility. [cite: 7]

## ☁️ AWS Architecture

Our project uses a secure, multi-account pipeline that separates the duties of each team member.

* **Account 1: Data Engineer (Lasya)**
    * [cite_start]**AWS Lambda** ingests raw data from public sources (Kaggle, FIFA.com). [cite: 9, 10, 14]
    * [cite_start]**Shared S3 Bucket** stores all raw data. [cite: 11, 14]
    * [cite_start]**Amazon DynamoDB** tracks metadata for the ingestion process (e.g., data source, timestamps). [cite: 12, 14]

* **Account 2: Data Analyst (Vaijayanti)**
    * [cite_start]**AWS Glue** jobs run on the raw data in S3 to transform it and create predictive features. [cite: 15]
    * [cite_start]**Key Engineered Features** include Team Performance (Recent Form, H2H Record), Player Strength (Star Player Factor), and Match Context (Host Advantage). [cite: 17]
    * [cite_start]Processed data is saved back to the **Shared S3 Bucket**. [cite: 16]
    * [cite_start]**Amazon Athena** is used to make the clean feature set queryable for analysis. [cite: 28]

* **Account 3: ML Engineer (Joshua)**
    * [cite_start]**Amazon SageMaker Studio** reads the clean features from S3 to train and evaluate the prediction model. [cite: 18]
    * [cite_start]The trained model is deployed to a live **EC2 Endpoint** to serve real-time predictions. [cite: 26]
    * [cite_start]**Amazon QuickSight** is used to build a "World Cup Insights" dashboard for visualizing predictions and statistics. [cite: 27]

[cite_start] [cite: 18]

## 🏆 Expected Outcomes

1.  [cite_start]**A Trained & Deployed Prediction Model:** A model trained in SageMaker (Account 3) and deployed as a live EC2 Endpoint. [cite: 26]
2.  [cite_start]**An Interactive "Insights" Dashboard:** A "World Cup Insights" dashboard, built in QuickSight (Account 3), to visualize model predictions and allow users to analyze team and player statistics. [cite: 27]
3.  [cite_start]**A Clean & Queryable Feature Set:** A production-ready, clean dataset of engineered features, processed by AWS Glue (Account 2), and made queryable for analysts via Amazon Athena. [cite: 28]
4.  [cite_start]**A Secure, Multi-Account Pipeline:** A governed and secure data pipeline using VPC Peering and IAM Roles that separates the duties of Data Engineering (Account 1), Data Analysis (Account 2), and ML Engineering (Account 3). [cite: 29]
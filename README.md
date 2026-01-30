# 🚀 AWS Glue CI/CD Pipeline (CloudFormation + Python SDK)

## 📌 Project Overview

This project implements a complete **CI/CD pipeline for AWS Glue** using **GitHub Actions**.  
The pipeline automates deployment, execution, and monitoring of Glue Jobs and Glue Crawlers.

Infrastructure is implemented using:
- **CloudFormation (YAML)**
- **Python SDK (boto3)**

---

## 🏗️ End-to-End Flow

# 🚀 AWS Glue CI/CD Pipeline (CloudFormation + Python SDK)

## 📌 Project Overview

This project implements a complete **CI/CD pipeline for AWS Glue** using **GitHub Actions**.  
The pipeline automates deployment, execution, and monitoring of Glue Jobs and Glue Crawlers.

Infrastructure is implemented using:
- **CloudFormation (YAML)**
- **Python SDK (boto3)**

---

## 🏗️ End-to-End Flow

GitHub Push (main)
|
v
GitHub Actions CI/CD
|
v
Upload Glue Script to S3
|
v
Deploy Glue Job (CloudFormation)
|
v
Run Glue Job (Wait until SUCCESS)
|
v
Run Airline Crawler (Wait + Validate)
|
v
Run Customers Crawler (Wait + Validate)
|
v
Glue Data Catalog Tables
|
v
Amazon Athena

---

## 📁 Repository Structure
.
├── .github/workflows/
│ └── ci.yml # GitHub Actions CI/CD pipeline
│
├── glue_job.py # AWS Glue ETL job script
├── template.yaml # Glue Job CloudFormation template
├── crawler-template.yaml # Glue Crawlers CloudFormation template
├── deployment.py # Python SDK (boto3) deployment script
├── README.md # Project documentation


---

## ⚙️ CI/CD Pipeline Details

The pipeline is triggered on every push to the **main** branch.

### Pipeline Steps

1. Checkout repository
2. Configure AWS credentials
3. Upload Glue ETL script to S3
4. Deploy Glue Job using CloudFormation
5. Trigger Glue Job and wait until it **SUCCEEDS**
6. Run **Airline** Glue Crawler
7. Validate Airline crawler execution
8. Run **Customers** Glue Crawler
9. Validate Customers crawler execution
10. Mark pipeline success

Pipeline **fails automatically** if:
- Glue Job fails or stops
- Any crawler fails

---

## 🧪 Glue Job Execution Logic

- Glue Job is triggered once per pipeline run
- Pipeline continuously polls job status
- Job must reach `SUCCEEDED`
- Prevents concurrent execution issues

---

## 🗂️ Glue Crawlers Execution Strategy

Crawlers are executed **one by one** (not parallel):

1. Airline crawler
2. Customers crawler

For each crawler:
- Trigger crawler
- Wait until crawler state becomes `READY`
- Validate last crawl status
- Pipeline fails if status is `FAILED`

---

## 🗃️ S3 Data Locations


---

## ⚙️ CI/CD Pipeline Details

The pipeline is triggered on every push to the **main** branch.

### Pipeline Steps

1. Checkout repository
2. Configure AWS credentials
3. Upload Glue ETL script to S3
4. Deploy Glue Job using CloudFormation
5. Trigger Glue Job and wait until it **SUCCEEDS**
6. Run **Airline** Glue Crawler
7. Validate Airline crawler execution
8. Run **Customers** Glue Crawler
9. Validate Customers crawler execution
10. Mark pipeline success

Pipeline **fails automatically** if:
- Glue Job fails or stops
- Any crawler fails

---

## 🧪 Glue Job Execution Logic

- Glue Job is triggered once per pipeline run
- Pipeline continuously polls job status
- Job must reach `SUCCEEDED`
- Prevents concurrent execution issues

---

## 🗂️ Glue Crawlers Execution Strategy

Crawlers are executed **one by one** (not parallel):

1. Airline crawler
2. Customers crawler

For each crawler:
- Trigger crawler
- Wait until crawler state becomes `READY`
- Validate last crawl status
- Pipeline fails if status is `FAILED`

---

## 🗃️ S3 Data Locations
s3://airport-airline-operations-analytics-platform/silver/airline/
s3://airport-airline-operations-analytics-platform/silver/customers/


Glue Crawlers scan these paths and create tables.

---

## 🧠 Infrastructure as Code Approach

### 1️⃣ CloudFormation (YAML)
- `template.yaml` provisions Glue Job
- `crawler-template.yaml` provisions Glue Crawlers
- Declarative and repeatable infrastructure

### 2️⃣ Python SDK (boto3)
- `deployment.py` provisions infrastructure programmatically
- Demonstrates SDK-based alternative to CloudFormation
- Useful for dynamic or conditional deployments

---

## 🔐 Prerequisites

- AWS Account
- IAM user with permissions:
  - AWS Glue
  - Amazon S3
  - AWS CloudFormation
- GitHub Secrets configured:
  - `AWS_ACCESS_KEY_ID`
  - `AWS_SECRET_ACCESS_KEY`
  - `AWS_DEFAULT_REGION`

---

## 📊 Final Output

- Glue Job executed successfully
- Glue Crawlers completed sequentially
- Glue Data Catalog tables created
- Tables visible in Amazon Athena

---

## ✅ Conclusion

This project demonstrates a **production-grade AWS Glue CI/CD pipeline** with:
- Sequential orchestration
- Failure handling
- CloudFormation-based IaC
- Python SDK-based deployment

---



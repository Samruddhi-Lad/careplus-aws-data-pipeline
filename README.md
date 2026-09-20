# CarePlus AWS Data Pipeline

## 📌 Project Overview

The **CarePlus AWS Data Pipeline** is an end-to-end cloud data engineering project that collects support ticket and application log data, processes it using AWS services, stores the transformed data in analytical systems, and makes it available for reporting through Power BI.

The project demonstrates practical implementation of **data ingestion, ETL, data quality, cloud storage, data warehousing, and business intelligence**.

---

## 🏗️ Architecture

```text
MySQL Database
      │
      ▼
Amazon S3 - Raw Data
      │
      ├──────────────► AWS Lambda
      │                    │
      │                    ▼
      │              Processed Parquet
      │
      └──────────────► AWS Glue
                           │
                           ▼
                    Processed Data
                           │
                    ┌──────┴──────┐
                    ▼             ▼
                 Athena        Redshift
                    │             │
                    └──────┬──────┘
                           ▼
                       Power BI
                       Dashboard
```

---

## 🔄 Data Pipeline

### 1. Data Ingestion

Support ticket data is extracted from a **MySQL database** and uploaded to Amazon S3.

Raw data is stored in:

```text
support-tickets/raw/
support-logs/raw/
```

### 2. Data Processing

AWS services are used to process and transform the raw data.

**Support Tickets:**

* AWS Glue performs ETL processing.
* Data quality and column transformations are applied.
* Processed data is stored in Amazon S3.

**Application Logs:**

* AWS Lambda processes raw log files.
* Invalid and duplicate records are removed.
* Logs are converted into Parquet format.
* Snappy compression is used for efficient storage.

Processed data is stored in:

```text
support-tickets/processed/
support-logs/processed/
```

### 3. Data Catalog and Querying

AWS Glue Data Catalog is used to catalog processed data.

Amazon Athena is used to query the processed log data.

Database:

```text
careplus_db
```

### 4. Data Warehouse

Processed data is loaded into **Amazon Redshift** for analytical querying.

Main tables:

```text
public.support_tickets
public.support_logs
```

### 5. Visualization

Power BI connects to the analytical data to create dashboards for monitoring support tickets and application logs.

---

## ☁️ AWS Services Used

| Service           | Purpose                                  |
| ----------------- | ---------------------------------------- |
| Amazon S3         | Cloud storage for raw and processed data |
| AWS Lambda        | Serverless log processing                |
| AWS Glue          | ETL processing for support tickets       |
| Glue Data Catalog | Metadata management                      |
| Amazon Athena     | SQL-based data analysis                  |
| Amazon Redshift   | Data warehouse                           |
| Power BI          | Data visualization and dashboards        |

---

## 🛠️ Technologies

* Python
* SQL
* MySQL
* Amazon S3
* AWS Lambda
* AWS Glue
* Amazon Athena
* Amazon Redshift
* Parquet
* PyArrow
* Power BI
* Git & GitHub

---

## 🧹 Data Quality

The pipeline includes data quality handling during processing.

Examples include:

* Duplicate record removal
* Invalid record filtering
* Negative response-time filtering
* Schema/column handling
* Conversion of raw logs into structured Parquet data

Example log processing:

```text
105 records parsed
      ↓
9 duplicate records removed
      ↓
7 invalid negative response-time records removed
      ↓
89 valid records processed
```

---

## 📊 Dashboard

The processed data is used to build Power BI dashboards for:

### Support Tickets

The dashboard can be used to analyze:

* Ticket volume
* Ticket status
* Priority
* Issue categories
* Support channels
* Agent activity
* Resolution information

### Application Logs

The log dashboard can be used to analyze:

* Response time
* CPU usage
* Log levels
* Error events
* Application components
* Ticket/session activity

---

## 📁 Repository Structure

```text
careplus-aws-data-pipeline/
│
├── README.md
├── .gitignore
│
├── architecture/
│
├── code/
│   └── support_tickets_ingestion_to_S3.ipynb
│
├── sql/
│   └── careplus_support_db.sql
│
└── dashboard/
```

---

## 🔐 Security

Sensitive information is excluded from the GitHub repository.

The `.gitignore` file prevents files such as:

```text
.env
AWS credentials
local CSV files
JSON data
Parquet files
Python cache files
```

from being committed accidentally.

---

## 🎯 Project Objectives

The main objectives of this project are to demonstrate:

* Cloud-based data ingestion
* ETL pipeline development
* Serverless data processing
* Data quality management
* Data lake storage using Amazon S3
* Analytical querying using Athena
* Data warehousing using Redshift
* Business intelligence using Power BI
* End-to-end AWS data engineering workflow

---

## 🚀 Key Learning Outcomes

Through this project, I worked with:

* AWS cloud services
* Data ingestion pipelines
* ETL and ELT concepts
* Data lake architecture
* Parquet data format
* Serverless processing
* Data quality techniques
* SQL analytics
* Cloud data warehousing
* Power BI visualization

---

## 👩‍💻 Author

**Samruddhi Lad**

Aspiring Data Engineer

GitHub: [Samruddhi-Lad](https://github.com/Samruddhi-Lad)

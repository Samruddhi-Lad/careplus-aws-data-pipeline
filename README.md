# CarePlus AWS Data Pipeline

## 📌 Project Overview

**CarePlus AWS Data Pipeline** is an end-to-end cloud data engineering project designed to ingest, process, transform, store, and analyze **support ticket and application log data** using AWS services.

The pipeline demonstrates practical implementation of:

* Data ingestion
* ETL processing
* Data quality
* Cloud data lake storage
* Serverless processing
* Data cataloging
* SQL analytics
* Cloud data warehousing
* Business intelligence

---

## 🏗️ Architecture

```text
                    ┌──────────────────┐
                    │   MySQL Database │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │    Amazon S3     │
                    │    Raw Data      │
                    └────────┬─────────┘
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼                             ▼
     ┌─────────────────┐          ┌─────────────────┐
     │   AWS Lambda    │          │    AWS Glue     │
     │  Log Processing │          │ Ticket ETL      │
     └────────┬────────┘          └────────┬────────┘
              │                            │
              ▼                            ▼
     ┌─────────────────┐          ┌─────────────────┐
     │ Processed Logs  │          │ Processed       │
     │     Parquet     │          │ Ticket Data     │
     └────────┬────────┘          └────────┬────────┘
              │                            │
              └──────────────┬─────────────┘
                             ▼
                    ┌──────────────────┐
                    │ Glue Data Catalog│
                    │    + Athena      │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Amazon Redshift  │
                    │  Data Warehouse  │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │     Power BI     │
                    │    Dashboard     │
                    └──────────────────┘
```

---

## 🔄 End-to-End Data Flow

### 1. Data Source

The project uses a local **MySQL database** containing CarePlus support ticket data and application log data.

Database:

```text
careplus_support_db
```

---

### 2. Data Ingestion to Amazon S3

Raw data is uploaded to Amazon S3 and organized using separate prefixes.

```text
support-tickets/raw/
support-logs/raw/
```

Amazon S3 acts as the central cloud storage layer for raw and processed data.

---

### 3. Support Ticket ETL

AWS Glue is used to process the support ticket data.

The Glue ETL workflow:

```text
Raw CSV
   ↓
Amazon S3
   ↓
AWS Glue
   ↓
Data Transformation
   ↓
Data Quality Handling
   ↓
Processed Data
   ↓
Amazon S3
```

Processed ticket data is stored under:

```text
support-tickets/processed/
```

The Glue job used in the project is:

```text
automate_etl_support_tickets
```

---

### 4. Application Log Processing

AWS Lambda is used to process application log files.

The workflow is:

```text
Raw Log Files
     ↓
Amazon S3
     ↓
AWS Lambda
     ↓
Validation & Cleaning
     ↓
Parquet Conversion
     ↓
Snappy Compression
     ↓
Processed Logs
```

Processed logs are stored under:

```text
support-logs/processed/
```

The processed data uses the **Parquet** format for efficient analytical processing.

---

## 🧹 Data Quality

Data quality checks are applied during log processing.

The pipeline handles:

* Duplicate records
* Invalid records
* Negative response times
* Schema/column handling
* Data type conversion
* Structured Parquet output

### Example

For one processed log file:

```text
105 records parsed
        ↓
9 duplicate records removed
        ↓
7 negative response-time records removed
        ↓
89 valid records processed
```

This ensures that invalid records are not passed to the analytical layer.

---

## 📚 Data Catalog and Querying

AWS Glue Data Catalog is used to maintain metadata for the processed data.

Amazon Athena is used to query the processed log data using SQL.

Athena database:

```text
careplus_db
```

Processed log table:

```text
support_logs_processed
```

---

## 🏢 Data Warehouse

Amazon Redshift is used as the analytical data warehouse.

Main tables:

```text
public.support_tickets
public.support_logs
```

The processed data can then be queried for reporting and analytical use cases.

---

## 📊 Power BI Dashboard

Power BI is used as the visualization layer.

### Support Ticket Dashboard

The ticket dashboard can provide insights into:

* Ticket volume
* Ticket status
* Priority
* Issue categories
* Support channels
* Agent activity
* Resolution information

### Application Log Dashboard

The log dashboard can provide insights into:

* Response time
* CPU usage
* Log levels
* Error events
* Application components
* Ticket activity
* Session activity

---

## ☁️ AWS Services Used

| AWS Service               | Purpose                               |
| ------------------------- | ------------------------------------- |
| **Amazon S3**             | Stores raw and processed data         |
| **AWS Lambda**            | Processes application logs            |
| **AWS Glue**              | Performs ETL on support ticket data   |
| **AWS Glue Data Catalog** | Maintains metadata                    |
| **Amazon Athena**         | Queries processed data using SQL      |
| **Amazon Redshift**       | Stores analytical data                |
| **Power BI**              | Creates dashboards and visualizations |

---

## 🛠️ Technologies Used

* Python
* SQL
* MySQL
* Amazon S3
* AWS Lambda
* AWS Glue
* AWS Glue Data Catalog
* Amazon Athena
* Amazon Redshift
* Parquet
* PyArrow
* Power BI
* Git
* GitHub

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

### Folder Description

| Folder/File     | Description                                               |
| --------------- | --------------------------------------------------------- |
| `README.md`     | Project documentation                                     |
| `.gitignore`    | Prevents sensitive/unnecessary files from being committed |
| `architecture/` | Architecture diagrams                                     |
| `code/`         | Data ingestion and processing notebooks                   |
| `sql/`          | Database and SQL scripts                                  |
| `dashboard/`    | Power BI dashboard screenshots/files                      |

---

## 🔐 Security

Sensitive credentials and local data are intentionally excluded from the repository.

The `.gitignore` file excludes:

```text
.env
.env.*
.aws/
*.csv
*.json
*.parquet
*.log
__pycache__/
.ipynb_checkpoints/
```

AWS credentials and other secrets should never be committed to GitHub.

---

## 🎯 Project Objectives

The main objectives of this project are to demonstrate an end-to-end AWS data engineering workflow.

### Key objectives

* Build a cloud-based data ingestion pipeline
* Store raw data in Amazon S3
* Process data using AWS Lambda and AWS Glue
* Apply data quality checks
* Convert log data to Parquet
* Catalog data using AWS Glue Data Catalog
* Query data using Amazon Athena
* Load analytical data into Amazon Redshift
* Create business dashboards using Power BI
* Manage the project using Git and GitHub

---

## 📈 Key Learning Outcomes

Through this project, I gained practical experience with:

* AWS cloud services
* Data lake concepts
* ETL pipelines
* Serverless data processing
* Data quality handling
* Parquet data format
* SQL-based analytics
* Cloud data warehousing
* AWS Glue
* AWS Lambda
* Amazon Athena
* Amazon Redshift
* Power BI
* Git and GitHub

---

## 🚀 Future Improvements

Possible future improvements include:

* Automating the complete pipeline using event-driven triggers
* Adding AWS Step Functions for workflow orchestration
* Adding more automated data quality checks
* Implementing monitoring and alerting
* Adding incremental data processing
* Improving dashboard refresh automation
* Adding infrastructure as code using Terraform or AWS CloudFormation

---

## 👩‍💻 Author

**Samruddhi Lad**

Aspiring Data Engineer

GitHub: [Samruddhi-Lad](https://github.com/Samruddhi-Lad)

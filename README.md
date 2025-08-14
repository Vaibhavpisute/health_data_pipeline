# 🏥 Health Data Pipeline

[![Apache Spark](https://img.shields.io/badge/Apache%20Spark-FDEE21?style=flat-square&logo=apachespark&logoColor=black)](https://spark.apache.org/)
[![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=flat-square&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/)
[![Apache Airflow](https://img.shields.io/badge/Apache%20Airflow-017CEE?style=flat-square&logo=Apache%20Airflow&logoColor=white)](https://airflow.apache.org/)
[![Python](https://img.shields.io/badge/python-3670A0?style=flat-square&logo=python&logoColor=ffdd54)](https://www.python.org/)

A comprehensive big data analytics solution for healthcare and insurance data processing, designed to detect fraudulent claims and analyze prescription/treatment trends at scale.

## 📋 Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Data Pipeline Flow](#data-pipeline-flow)
- [Project Structure](#project-structure)
- [Configuration](#configuration)
- [Monitoring](#monitoring)
- [Contributing](#contributing)
- [License](#license)

## 🔍 Overview

This project addresses the critical challenge of fraudulent claims in the healthcare insurance sector by implementing a robust, scalable data pipeline architecture. Built on AWS cloud infrastructure, it processes large-scale healthcare data using distributed computing technologies to provide actionable insights and automated fraud detection capabilities.

### Key Objectives

- **Fraud Detection**: Identify suspicious patterns in insurance claims using advanced analytics
- **Trend Analysis**: Monitor prescription and treatment trends across different demographics
- **Data Quality**: Ensure data integrity through comprehensive validation and quality checks
- **Scalability**: Handle large volumes of healthcare data efficiently
- **Automation**: Provide end-to-end automated data processing workflows

## 🏗️ Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Oracle RDBMS  │───▶│   Apache Spark  │───▶│    Amazon S3    │
│  (Source Data)  │    │ (ETL Processing)│    │ (Data Storage)  │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                │
                                ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│ Apache Airflow  │◀───│      Hive       │───▶│   Redshift      │
│ (Orchestration) │    │ (Data Warehouse)│    │  (Analytics)    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## ✨ Features

### Data Processing
- **ETL Pipelines**: Robust Extract, Transform, Load processes using PySpark
- **Incremental Loading**: Efficient handling of new and updated records
- **Data Quality Assurance**: Comprehensive validation and cleansing workflows
- **Query Optimization**: Performance-tuned queries using Spark and Hive best practices

### Analytics & Insights
- **Fraud Detection**: Advanced algorithms to identify suspicious claim patterns
- **Prescription Analytics**: Trend analysis for medication prescriptions
- **Treatment Pattern Analysis**: Healthcare service utilization insights
- **Risk Assessment**: Automated scoring for insurance claim risks

### Automation & Orchestration
- **Workflow Scheduling**: Automated job execution using Apache Airflow
- **Pipeline Monitoring**: Real-time monitoring and alerting
- **Error Handling**: Robust error recovery and notification systems
- **Reporting**: Automated generation of analytical reports

## 🛠️ Tech Stack

### Big Data & Processing
- **Apache Spark**: Distributed data processing engine
- **PySpark**: Python API for Spark
- **Apache Hive**: Data warehouse software for querying large datasets
- **HDFS**: Distributed file system for data storage

### Cloud Infrastructure
- **Amazon S3**: Scalable object storage
- **Amazon Redshift**: Cloud data warehouse
- **AWS EC2**: Compute instances for processing
- **AWS IAM**: Identity and access management

### Orchestration & Monitoring
- **Apache Airflow**: Workflow orchestration platform
- **AWS CloudWatch**: Monitoring and logging service

### Database
- **Oracle Database**: Source system for healthcare data
- **Amazon RDS**: Managed relational database service

## 📋 Prerequisites

- Python 3.8+
- Apache Spark 3.2+
- Apache Airflow 2.0+
- AWS CLI configured with appropriate permissions
- Oracle Client (for database connectivity)
- Docker (optional, for containerized deployment)

### AWS Permissions Required
- S3: Read/Write access
- Redshift: Full access
- EC2: Launch and manage instances
- IAM: Role management
- CloudWatch: Logging and monitoring

## 🚀 Installation

### 1. Clone the Repository
```bash
git clone https://github.com/Vaibhavpisute/health_data_pipeline.git
cd health_data_pipeline
```

### 2. Set Up Python Environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 3. Configure AWS Credentials
```bash
aws configure
# Enter your AWS Access Key ID, Secret Access Key, Region, and Output format
```

### 4. Set Up Environment Variables
```bash
cp .env.example .env
# Edit .env file with your configuration values
```

### 5. Initialize Airflow
```bash
airflow db init
airflow users create \
    --username admin \
    --firstname Admin \
    --lastname User \
    --role Admin \
    --email admin@example.com
```

## 💻 Usage

### Starting the Pipeline

1. **Start Airflow Services**
```bash
# Start the web server (default port 8080)
airflow webserver --port 8080

# In another terminal, start the scheduler
airflow scheduler
```

2. **Access Airflow UI**
Navigate to `http://localhost:8080` and log in with your admin credentials.

3. **Trigger Data Pipeline**
```bash
# Trigger the main ETL pipeline
airflow dags trigger health_data_etl_pipeline

# Or trigger via Python script
python scripts/trigger_pipeline.py
```

### Running Individual Components

```bash
# Run data ingestion
python src/ingestion/data_ingestion.py

# Run data transformation
python src/transformation/data_transformation.py

# Run fraud detection analysis
python src/analytics/fraud_detection.py
```

## 🔄 Data Pipeline Flow

1. **Data Ingestion**
   - Extract data from Oracle RDBMS
   - Validate data quality and schema
   - Store raw data in S3 (Bronze layer)

2. **Data Transformation**
   - Clean and standardize data formats
   - Apply business rules and calculations
   - Create curated datasets (Silver layer)

3. **Data Loading**
   - Load processed data into Hive tables
   - Create optimized views for analytics
   - Store final datasets (Gold layer)

4. **Analytics & Reporting**
   - Run fraud detection algorithms
   - Generate trend analysis reports
   - Update dashboards and visualizations

## 📁 Project Structure

```
health_data_pipeline/
├── src/
│   ├── ingestion/           # Data ingestion modules
│   ├── transformation/      # Data transformation logic
│   ├── analytics/          # Analytics and ML models
│   └── utils/              # Utility functions
├── dags/                   # Airflow DAG definitions
├── configs/                # Configuration files
├── scripts/                # Utility scripts
├── tests/                  # Unit and integration tests
├── docs/                   # Documentation
├── requirements.txt        # Python dependencies
├── .env.example           # Environment variables template
└── README.md              # This file
```
### Pipeline Configuration
Edit `configs/pipeline_config.yaml` to customize:
- Data source connections
- Processing parameters
- Output destinations
- Scheduling intervals

## 📊 Monitoring

### Airflow Monitoring
- Access the Airflow web interface for DAG monitoring
- View task logs and execution history
- Set up email alerts for failed tasks

### AWS CloudWatch
- Monitor S3 storage usage and costs
- Track Redshift query performance
- Set up custom metrics and alarms

### Data Quality Checks
- Automated data validation reports
- Schema drift detection
- Data freshness monitoring

---

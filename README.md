# 📦 AWS Data Engineering Overview

> 📚 Motivation: In life you can choose who you want to be; be very careful with that choice.

🌅 [**AWS Certified Data Engineer – Associate（DEA-C01）**](https://www.udemy.com/course/aws-certified-data-engineer-associate-dea-c01/?couponCode=ST16MT230625B)

## 0. Preface

In modern data architecture, AWS provides a comprehensive set of tools to support the full data lifecycle — from ingestion and storage to processing and orchestration. 

**🔁 Data Ingestion**

| Type            | Service     | Description |
|-----------------|-------------|-------------|
| **Batch**       | AWS Glue | Crawlers automatically infer schemas; Glue ETL jobs (Spark-based) handle transformations. |
|                 | AWS DMS  | Supports full load and CDC (Change Data Capture) to migrate databases into **Amazon S3**, **Redshift**, or **Aurora**. |

**🗃️ Data Storage**

| Category         | Service               | Description |
|------------------|------------------------|-------------|
| Data Lake     | Amazon S3 | Object storage with partitioning, versioning, and lifecycle policies. Integrated with **Glue Data Catalog**. |
|                  | AWS Lake Formation | Centralized access control with fine-grained permissions. |
| Data_Warehouse| Amazon Redshift    | Columnar storage, MPP engine, Spectrum enables direct querying of S3 data. |
| Relational    | Amazon RDS / Aurora | Managed OLTP databases with read replicas and global database support. |

**⚙️ Data Processing & ETL**

| Category           | Service                  | Description |
|--------------------|---------------------------|-------------|
| Batch Processing | AWS Glue ETL         | Serverless Spark for ETL in **Python** or **Scala**. |
|                    | Amazon EMR            | Custom big data platform with **Spark**, **Hive**, **Hadoop**, and spot instance support. |
| **Orchestration**   | AWS Step Functions     | Serverless state machine for orchestrating workflows. |
|  /ˌɔː.kɪˈstreɪ.ʃən/  | Amazon MWAA (Airflow) | Fully managed Airflow for DAG-based job scheduling. |

✅ **Data Services (7 hours)**

[AWS Free- login](https://signin.aws.amazon.com/signin?client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fcanvas&redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3FhashArgs%3D%2523%26isauthcode%3Dtrue%26state%3DhashArgsFromTB_ap-southeast-2_4006ae5d2b7eed51&page=resolve&code_challenge=f9CZpqfFaFLi3LHpmKeNB0PfdFV7GbPKBE3FMsgIZqg&code_challenge_method=SHA-256&backwards_compatible=true) 

## S1 - Introduction

- Signup for AWS Free Trial

<div align="center">
  <a href="docs/pdf/AllSlides_v3.3_Data+Engineer.pdf" target="_blank">
    <img src="docs/images/pdf-cover.jpg" alt="Slides Preview" width="700">
  </a>
</div>


## S2 - Data Ingestion

- S3 = Simple Storage Service, simple object storage  
- Buckets (containers for storage) and objects (files)

<div align="left">
  <img src="docs/AWS-DI-S3.webp" alt="image" width="300">
</div>


[**our-first-bucket-202507**](https://ap-southeast-1.console.aws.amazon.com/s3/buckets/our-first-bucket-202507?region=ap-southeast-1&bucketType=general)

<div align="center">
  <img src="docs/image%201.png" alt="image" width="700">
</div>

#### 🧠 Glue ≈ Spark + Hive Metastore + Airflow

- After finishing each service module, **take the quiz immediately**.
- Draw architecture diagrams like:
- `Glue ➝ S3 ➝ Athena`
- `S3 ➝ Redshift Spectrum`

#### AWS Glue?

AWS Glue is a **serverless data integration service** designed to help you **discover, prepare, move, and integrate data** from various sources for analytics and application development. It's primarily used for building **data warehouses**, **data lakes**, and **data pipelines**.

<div align="center">
  <img src="docs/image%202.png" alt="image" width="700">
</div>

<div align="center">
  <img src="docs/image%203.png" alt="image" width="700">
</div>

<div align="center">
  <img src="docs/image%204.png" alt="image" width="700">
</div>

> AWS Glue is a fully managed serverless data integration service. It helps you discover, prepare, transform, and combine data from multiple sources for analytics, machine learning, and application development.

<div align="center">
  <img src="docs/AWS-Glue-1-structure.png" alt="structure" width="700">
</div>

#### ✅ In One Sentence:

> Glue is AWS’s serverless data engineering platform that handles ETL, metadata management, orchestration [ˌɔːkɪˈstreɪʃn], and connectivity, making it ideal for building data lakes and pipelines

<div align="center">
  <img src="docs/df1fd758ba7182d09bf63c2f0e661b18.png" alt="Glue Feature" width="700">
</div>

#### Key Features & Benefits

- **Serverless:** No servers to provision or manage. Glue **auto-scales** based on your workload, and you **pay only for consumption**.
- **ETL  Capabilities:** Offers robust ETL functionalities, supporting diverse **data sources** and **targets**. You can use **PySpark** or **Scala** for ETL scripts or the visual interface in **Glue Studio**.
- **Data Catalog:** A **persistent metadata repository** that's a core Glue component. It stores **metadata** for all your data assets, including **table definitions**, **schemas**, and **location information**, facilitating data discovery and sharing.
- **Crawlers:** Automatically connect to your data sources, **infer data schemas**, and populate the **Data Catalog**, greatly simplifying schema management.
- **Glue Studio:** A **graphical interface** for visually creating, running, and monitoring ETL jobs with minimal code.
- **AWS Service Integration:** Seamlessly integrates with other AWS services like **S3**, **Redshift**, **RDS**, **Lake Formation**, and **SageMaker** for end-to-end data solutions.

#### Core Components

| Component | Description |
| --- | --- |
| **AWS Glue Data Catalog** | Stores all **metadata**, including **table definitions**, **schemas**, and data **locations**. |
| **AWS Glue Crawlers** | Automatically **scan data sources**, **infer schemas**, and **update the Data Catalog**. |
| **AWS Glue ETL Jobs** | Execute **PySpark** or **Scala** scripts to perform **data transformations** and processing. |
| **AWS Glue Studio** | A **visual interface** for building, running, and monitoring **ETL jobs**. |
| **AWS Glue DataBrew** | (Part of the Glue suite) A **visual data preparation tool** for cleaning and normalising data **without code**. |
| **AWS Glue Data Quality** | Helps **assess and improve** the **quality of your data**. |

## S3 - Querying with Athena

Serverless SQL querying on S3, SerDe, Partitioning

S3 bucket → Crawler → Data Catalog → Athena → Quicksight

Federated Query

<div align="left">
  <img src="docs/image%205.png" alt="Athena" width="350">
</div>

| Topic | Key Point | Why It Matters for the Exam |
| --- | --- | --- |
| **1. Querying Data** | SQL on S3 | Athena lets you run SQL directly on S3 data (no ETL needed) |
|  | Partitioning | Reduces data scanned and cost; common exam topic |
|  | Parquet / ORC | Columnar formats = faster queries, lower costs |
| **2. Federated Queries** | Query across RDS, DynamoDB, etc. | Athena can query non-S3 sources using connectors (via Lambda) |
|  | IAM Role for Connector | Secure access is key; know how roles work with connectors |
| **3. Performance & Cost** | Pay-per-Scan ($5/TB) | Exam may ask how to reduce cost – partitioning + columnar files |
|  | Partition Projection | Avoids full metadata scans, boosts performance |
|  | Compression & Format | Use Parquet/ORC for columnar compression |
| **3. Workgroups** | Query isolation & cost control | Used to manage query cost, access, and results per team |
|  | Query metrics & audit logs | For governance and troubleshooting |

## S4 - AWS Glue Deep Dive

<div align="left">
  <img src="docs/image%206.png" alt="Glue Deep Dive" width="350">
</div>

1. Stateful vs Stateless

Data Ingestion in AWS

- Amazon Kinesis
- AWS Data Pipeline
- AWS Glue

| Module | Description | Why Learn It |
| --- | --- | --- |
| ✅ Data Lakes with S3 | Building data lakes with S3, lifecycle policies, versioning | S3 is the core of the data lake – **must-know** |
| ✅ Glue Basics & ETL | Glue ETL concepts: Jobs, Crawlers, Scripts | Glue is **high-frequency** on the exam |
| ✅ Athena [əˈθiːnə] | Serverless SQL querying on S3, SerDe, Partitioning | Common with S3 – fast, cost-effective querying |
| ✅ Redshift | Data warehousing, distribution/sort keys, Spectrum | Focus on storage architecture and **Redshift + S3** |

### AWS Action

AWS Glue Action Dashboard

[ap-southeast-1.console.aws.amazon.com](https://ap-southeast-1.console.aws.amazon.com/glue/home?region=ap-southeast-1#/v2/getting-started)

<div align="center">
  <img src="docs/image%207.png" alt="AWS Console" width="750">
</div>

[Complete AWS Certified Data Engineer Associate - DEA-C01](https://www.udemy.com/course/aws-certified-data-engineer-associate-dea-c01/?couponCode=LETSLEARNNOW)

## 2. AWS Certified Data Engineer – Associate (DEA-C01)

[AWS Certified Data Engineer – Associate (DEA-C01)](https://www.coursera.org/specializations/exam-prep-aws-certified-data-engineer-associate?utm_source=chatgpt.com)

| 排名 | 认证 | 市场认可度说明 |
| --- | --- | --- |
| 1 | [AWS Certified Cloud Practitioner](https://3lexw.medium.com/aws-certified-cloud-practitioner-clf-c01-%E8%AD%89%E7%85%A7%E8%80%83%E8%A9%A6%E5%BF%83%E5%BE%97-b3b9987b5d59) | Entry-level certificates have the widest coverage and are required for many cross-functional or non-technical positions. |
| 2 | AWS Certified Data Engineer – Associate (DEA-C01) | 2024 持证量仍在累积中；但在主流大厂的 Data Engineer 岗位中，认可度正快速提升。 |

## 3. Exam

| Domain | Weight | Key Services & Topics |
| --- | --- | --- |
| **Data Ingestion** | 20% | Batch vs. streaming; AWS Glue; AWS DMS; Kinesis Data Streams & Firehose |
| **Data Storage** | 20% | Data lake vs. data warehouse; Amazon S3; Redshift; DynamoDB; RDS/Aurora |
| **Data Processing & ETL** | 30% | AWS Glue ETL; EMR (Hive, Spark); Lambda; Step Functions; MWAA |
| **Analytics & Machine Learning** | 15% | Athena; QuickSight; SageMaker (notebooks, training, endpoints) |
| **Security, Monitoring & Optimization** | 15% | IAM roles/policies; KMS encryption; CloudWatch & CloudTrail; cost controls |

### 🔍 AWS Glue vs. Amazon EMR – Comparison Table

| Feature / Aspect | **AWS Glue** | **Amazon EMR** |
| --- | --- | --- |
| **Type** | Serverless ETL service | Managed cluster-based big data platform |
| **Use Case** | Simplified ETL (Extract-Transform-Load) | Custom big data processing (Spark, Hive, Presto, etc.) |
| **Language Support** | PySpark, Python, Scala (limited) | PySpark, Spark, Hive, Presto, HBase, Flink, Hadoop, etc. |
| **Infrastructure** | Fully managed, no cluster management | Requires cluster provisioning & tuning |
| **Startup Time** | Slow (several minutes) | Faster if using persistent clusters |
| **Cost Model** | Pay per job (DPU/hour) | Pay per instance-hour |
| **Scalability** | Auto-scales jobs | Manual or auto-scaling clusters |
| **Orchestration** | Glue Workflows, triggers | Use Step Functions, Airflow, or native scheduling |
| **Metadata Catalog** | Built-in Glue Data Catalog (Hive-compatible) | Use Glue Catalog or Hive Metastore |
| **Connectors** | JDBC, MongoDB, Kafka, Redshift, S3 | Wide range via Spark or custom setup |
| **Skill Level Needed** | Beginner to Intermediate | Intermediate to Advanced |
| **Best For** | Fast serverless ETL, less infrastructure hassle | Complex, large-scale data pipelines with full control |

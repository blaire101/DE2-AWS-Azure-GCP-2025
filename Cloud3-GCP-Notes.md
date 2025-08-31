# 📦 GCP Data Engineering Overview

In modern data architecture, GCP provides a comprehensive set of tools to support the full data lifecycle — from ingestion and storage to processing and orchestration. 

[Google Professional Data Engineer Certification](https://cloud.google.com/certification/data-engineer)

| Exam - Domain | Weight | Key Services & Topics |
| :--- | --- | --- |
| **Data Ingestion** | 20% | Batch vs. streaming; Cloud Data Fusion; Datastream (CDC); Pub/Sub |
| **Data Storage** | 20% | Data lake vs. data warehouse; Cloud Storage; BigQuery; Firestore; Cloud SQL/AlloyDB |
| **Data Processing & ETL** | 30% | Dataflow (Beam pipelines); Dataproc (Spark, Hadoop, Hive); Cloud Functions; Cloud Composer |
| **Analytics & Machine Learning** | 15% | BigQuery ML; Looker / Looker Studio; Vertex AI (training, endpoints) |
| **Security, Monitoring & Optimization** | 15% | IAM roles/policies; CMEK encryption; Cloud Logging & Cloud Monitoring; cost optimization |

---

## 1. Cloud Storage (GCS)

- Buckets (containers for storage)  
- Objects (files)

<div align="center">
  <img src="docs/GCP-Cloud-Storage-logo.png" alt="structure" width="300">
</div>

---

## 2. Cloud Data Fusion

Cloud Data Fusion is a **serverless data integration service** to **discover, prepare, move, and integrate data** from various sources for analytics and application development. It is widely used for building **data pipelines**, **data lakes**, and **data warehouses**.  

- **Fully-managed ETL service**  
- Designed to make it easy to **build & orchestrate pipelines**  
- **Visual interface**: Drag & drop ETL without code  
- **Integrations**: Cloud Storage, BigQuery, Cloud SQL, Firestore  

<div align="center">
  <img src="docs/GCP-Data-Fusion.png" alt="structure" width="700">
</div>

| Component | Description |
| --- | --- |
| **Cloud Data Catalog** | Stores all **metadata**, including **table definitions**, **schemas**, and data **locations**. |
| **Cloud Data Fusion Pipelines** | Automatically **ingest, transform, and load** data from multiple sources. |
| **Dataprep (Trifacta)** | Visual tool for **data preparation** and cleaning. |
| **Cloud Composer (Airflow)** | Workflow orchestration for **ETL pipelines**. |

---

## 3. Querying with BigQuery

BigQuery is a **Serverless Data Warehouse** that can be used to query and analyze massive datasets using standard SQL.  

<div align="center">
  <img src="docs/GCP-BigQuery.png" alt="structure" width="600">
</div>

| Topic | Key Point | Why It Matters for the Exam |
| --- | --- | --- |
| **1. Querying Data** | SQL on structured/unstructured data | BigQuery lets you run SQL directly on data (including GCS external tables) |
|  | Partitioning & Clustering | Reduces data scanned and cost; common exam topic |
|  | Parquet / ORC / Avro | Columnar formats = faster queries, lower costs |
| **2. Federated Queries** | Query Cloud SQL, Bigtable, Sheets | BigQuery can query non-GCS sources |
|  | IAM Role for connectors | Secure access is key; know how roles work with connectors |
| **3. Performance & Cost** | On-demand ($5/TB scanned) or flat-rate slots | Exam may ask how to optimize cost – partitioning, clustering, storage tiers |
| **4. Governance** | Data Catalog, Access Control | Used for schema management & permissions |

---

## 4. Dataflow & Dataproc

### Dataflow (Apache Beam)

- **Serverless streaming & batch processing**  
- Unified model for pipelines  
- Supports SQL, Java, Python  

### Dataproc

- Managed **Spark / Hadoop / Hive** clusters  
- Good for **legacy workloads** or custom Spark ML pipelines  

---

## 5. Serverless Compute with Cloud Functions

Use cases： 

```mermaid
flowchart TD
    subgraph EventSource
        A1[GCS Upload]
        A2[Firestore Change]
        A3[Pub/Sub Message]
    end

    subgraph GCPFunctions
        L1[Trigger]
        L2[Cloud Function]
        L3[Process Data]
    end

    subgraph TargetServices
        T1[Store in GCS]
        T2[Update Firestore / Bigtable]
        T3[Publish Notification via Pub/Sub]
    end

    A1 --> L1
    A2 --> L1
    A3 --> L1
    L1 --> L2
    L2 --> L3
    L3 --> T1
    L3 --> T2
    L3 --> T3

    classDef green fill:#b5e7a0,stroke:#2e8b57,stroke-width:2px;
    classDef orange fill:#ffe6b3,stroke:#e67e00,stroke-width:2px;
    classDef purple fill:#dabfff,stroke:#6a0dad,stroke-width:2px;
    classDef blue fill:#cfe2ff,stroke:#0056b3,stroke-width:2px;
    classDef gray fill:#e0e0e0,stroke:#888888,stroke-width:2px;
    classDef pink fill:#ffd6e7,stroke:#cc3366,stroke-width:2px;

    class A1,T1 green;
    class A2,T2 orange;
    class A3 purple;
    class L1 gray;
    class L2,L3 blue;
    class T3 pink;

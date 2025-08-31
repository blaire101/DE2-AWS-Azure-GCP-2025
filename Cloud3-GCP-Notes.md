# 📦 GCP Data Engineering Overview

In modern data architecture, GCP provides a comprehensive set of tools to support the full data lifecycle — from ingestion and storage to processing and orchestration.  

[Google Cloud Certified: Professional Data Engineer](https://cloud.google.com/certification/data-engineer)

| Exam - Domain | Weight | Key Services & Topics |
| :--- | --- | --- |
| **Data Ingestion** | 20% | Batch vs. streaming; Datastream; Pub/Sub; Data Fusion |
| **Data Storage** | 20% | Data lake vs. data warehouse; Cloud Storage; BigQuery; Firestore; Cloud SQL |
| **Data Processing & ETL** | 30% | Dataflow; Dataproc; Cloud Functions; Composer; Spark on GKE |
| **Analytics & Machine Learning** | 15% | BigQuery SQL; Looker; Vertex AI |
| **Security, Monitoring & Optimization** | 15% | IAM; CMEK/KMS; Cloud Logging & Monitoring; Dataplex & Data Catalog |

---

## 1. GCS = Google Cloud Storage

- Buckets (like S3 containers)
- Objects (files/blobs)

<div align="center">
  <img src="docs/GCP-Cloud-Storage.png" alt="structure" width="700">
</div>

---

## 2. Data Fusion

Cloud Data Fusion is a **serverless data integration service** designed to help you **discover, prepare, move, and integrate data**. It's primarily used for **pipelines** feeding **data warehouses** and **data lakes**.

- **Fully-managed ETL/ELT service**
- **Visual drag-and-drop UI**
- **Integrations**: GCS, BigQuery, Cloud SQL, Pub/Sub

<div align="center">
  <img src="docs/GCP-Data-Fusion.png" alt="structure" width="300">
</div>

| Component | Description |
| --- | --- |
| **Cloud Data Catalog** | Metadata, schemas, governance. |
| **Wrangler** | UI for data exploration and transformation. |
| **Pipelines** | Batch or streaming jobs, run on Dataflow/Spark. |

---

## 3. Querying with BigQuery

BigQuery is a **serverless, petabyte-scale data warehouse** with SQL interface.  

<div align="center">
  <img src="docs/GCP-BigQuery.svg" alt="structure" width="200">
</div>

| Topic | Key Point | Why It Matters |
| --- | --- | --- |
| **1. Querying Data** | SQL on GCS or native tables | No infrastructure to manage |
|  | Partitioning & Clustering | Reduce cost and latency |
| **2. External Tables** | Query data in GCS directly | Avoids ETL for raw files |
| **3. Performance & Cost** | Storage cheap, compute billed per TB scanned | Partitioned + columnar files lower cost |
| **4. ML Integration** | BigQuery ML | Train models directly in SQL |
| **5. Governance** | Dataplex & IAM | Centralized metadata and fine-grained access |

---

## 4. Dataflow & Dataproc

### Cloud Dataflow
- Serverless Apache Beam pipelines  
- Batch + Streaming (unified model)  
- Auto-scaling  

### Dataproc
- Managed Hadoop/Spark/Flink  
- Flexible for lift-and-shift workloads  
- Pay per VM  

---

## 5. Serverless Compute with Cloud Functions

Use cases： 

```mermaid
flowchart TD
    subgraph EventSource
        A1[GCS Upload]
        A2[Firestore/Cloud SQL Change]
        A3[Pub/Sub Topic]
    end

    subgraph CloudFunctions
        L1[Trigger]
        L2[Function]
        L3[Process Data]
    end

    subgraph TargetServices
        T1[Store in GCS]
        T2[Update BigQuery / Firestore]
        T3[Send Notification via Pub/Sub / Cloud Tasks]
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
```

---

## 6. Data Streaming

- **Pub/Sub** (Kafka-like pub-sub messaging)  
- **Dataflow Streaming** (real-time ETL with Beam/Flink)  
- **Cloud Functions** for lightweight transforms  
- **Dataproc + Spark Streaming** for advanced scenarios  

---

## 7. Storage with GCS

- Partitioning (prefix/structured paths)  
- Storage classes (Standard / Nearline / Coldline / Archive)  
- Object Versioning  
- CMEK encryption with Cloud KMS  
- IAM & ACLs  
- Event Notifications (to Pub/Sub)  

---

## 8. Other Storage Services

- **Persistent Disks**  
- **Filestore (NFS)**  
- **Backup & DR**  

---

## 9. Firestore / Bigtable / Cloud SQL

- Firestore = NoSQL document DB  
- Bigtable = Wide-column DB (low latency, high throughput)  
- Cloud SQL = Managed MySQL/Postgres/SQL Server  
- AlloyDB = Advanced PostgreSQL-compatible  

---

## 10. BigQuery Data Warehouse

BigQuery is a fully managed **MPP** analytics warehouse.  

<div align="center">
  <img src="docs/GCP-BigQuery.png" alt="Diagram" width="700">
</div>

✅ BigQuery vs Hive vs SparkSQL

| Feature | BigQuery | Hive | SparkSQL |
|--------|----------|------|----------|
| Type | Managed MPP Data Warehouse | Hadoop SQL Engine | In-memory distributed SQL |
| Storage | Columnar + GCS | HDFS | HDFS/S3/GCS |
| Latency | Fast | Slow | Fast |
| Deployment | Fully managed | Self-hosted Hadoop | Self-hosted Spark |

```mermaid
flowchart TB
    %% ===== Color classes =====
    classDef core fill:#ffe5e5,stroke:#cc0000,stroke-width:2px,color:#000;
    classDef ops fill:#fff2cc,stroke:#aa7a00,stroke-width:2px,color:#000;
    classDef features fill:#e6ffe6,stroke:#1b7f1b,stroke-width:2px,color:#000;
    classDef bg_clients fill:#e6f3ff,stroke:none;
    classDef bg_cluster fill:#fff8f0,stroke:none;
    classDef bg_ops fill:#f4e6ff,stroke:none;
    classDef bg_features fill:#f0fff4,stroke:none;

    %% ===== Clients =====
    subgraph C["Clients & Connectivity"]
        BI["🧑‍💻 Looker / BI Tools / SQL clients"]
        ODBC["🔌 ODBC / JDBC"]
    end
    class C bg_clients

    %% ===== BigQuery Cluster =====
    subgraph BQ["BigQuery Engine"]
        L["🧠 Control Plane<br>(Job orchestration, query planner)"]
        W1["🧩 Worker Node 1<br>(Dremel slot execution)"]
        W2["🧩 Worker Node 2<br>(Dremel slot execution)"]
        W3["🧩 Worker Node 3<br>(Dremel slot execution)"]
    end
    class BQ bg_cluster

    %% ===== Features =====
    subgraph F["Key Features"]
        F1["📦 Columnar storage (Colossus)"]
        F2["⚡ Serverless MPP"]
    end
    class F bg_features

    %% ===== Ops =====
    subgraph G["Security & Operations"]
        SEC["🔐 IAM / VPC-SC / CMEK (KMS)"]
        BAK["🧷 Automated backup & DR"]
        SHARE["🔁 External tables / Data sharing"]
    end
    class G bg_ops

    BI --> ODBC --> BQ
    L --> W1
    L --> W2
    L --> W3

    SEC --- BQ
    BAK --- BQ
    SHARE --- L

    class BI,ODBC,L,W1,W2,W3 core
    class SEC,BAK,SHARE ops
    class F1,F2 features
```

---

## 11. Other Database Services

```mermaid
flowchart TB
    CloudSQL[Cloud SQL]:::relational
    AlloyDB[AlloyDB]:::relational
    Firestore[Firestore]:::nosql
    Bigtable[Bigtable]:::nosql
    Spanner[Cloud Spanner]:::special
    Memorystore[Memorystore - Redis/Memcached]:::nosql

    subgraph Relational
        CloudSQL
        AlloyDB
    end

    subgraph NoSQL
        Firestore
        Bigtable
        Memorystore
    end

    subgraph Specialized
        Spanner
    end

    CloudSQL -->|Migration| AlloyDB

    %% Styles
    classDef relational fill:#d0f0fd,stroke:#007acc,stroke-width:2px;
    classDef nosql fill:#fde2d0,stroke:#cc5200,stroke-width:2px;
    classDef special fill:#e6d0fd,stroke:#7e3ff2,stroke-width:2px;
```

---

## 12. Compute Services

```mermaid
flowchart TD
    LB[Cloud Load Balancer]
    LB --> GCE1[GCE VM 1]
    LB --> GCE2[GCE VM 2]
    MIG[Managed Instance Group] --> GCE1
    MIG --> GCE2
    GCE1 --> DB[(Cloud SQL)]
    GCE2 --> DB
```

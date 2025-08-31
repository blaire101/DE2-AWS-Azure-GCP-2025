# 📦 Azure Data Engineering Overview

In modern data architecture, Azure provides a comprehensive set of tools to support the full data lifecycle — from ingestion and storage to processing and orchestration. 

[Microsoft Certified: Azure Data Engineer Associate (DP-203)](https://learn.microsoft.com/en-us/certifications/azure-data-engineer/)

| Exam - Domain | Weight | Key Services & Topics |
| :--- | --- | --- |
| **Data Ingestion** | 20% | Batch vs. streaming; Azure Data Factory; Event Hubs; Data Share |
| **Data Storage** | 20% | Data lake vs. data warehouse; Azure Data Lake Storage (ADLS); Synapse; Cosmos DB; Azure SQL Database |
| **Data Processing & ETL** | 30% | Data Factory pipelines; Synapse Spark pools; HDInsight; Azure Functions; Azure Databricks |
| **Analytics & Machine Learning** | 15% | Synapse SQL; Power BI; Azure Machine Learning |
| **Security, Monitoring & Optimization** | 15% | RBAC & Managed Identity; Key Vault; Azure Monitor; Cost Management |

---

## 1. ADLS = Azure Data Lake Storage

- Containers (similar to buckets)
- Blobs (objects/files)

<div align="center">
  <img src="docs/Azure-ADLS-logo.png" alt="structure" width="300">
</div>

---

## 2. Azure Data Factory

Azure Data Factory is a **serverless data integration service** designed to help you **discover, prepare, move, and integrate data** from various sources for analytics and application development. It's widely used for building **data lakes**, **data warehouses**, and **data pipelines**.

- **Fully-managed ETL/ELT service**
- Visual drag-and-drop pipeline builder
- Rich **integration**: ADLS, Synapse, Azure SQL, Cosmos DB

<div align="center">
  <img src="docs/Azure-DataFactory.png" alt="structure" width="700">
</div>

| Component | Description |
| --- | --- |
| **Data Catalog (Purview)** | Centralized **metadata**, schema registry, governance. |
| **Integration Runtimes** | Compute used to move/transform data. |
| **Mapping Data Flows** | Visual, Spark-based transformation. |
| **ADF Studio** | Browser UI for building pipelines. |

---

## 3. Querying with Synapse SQL

Azure Synapse Analytics provides a **serverless + dedicated SQL pool** to query and analyze data across data lake and warehouse.  

<div align="center">
  <img src="docs/Azure-Synapse.png" alt="structure" width="600">
</div>

| Topic | Key Point | Why It Matters for the Exam |
| --- | --- | --- |
| **1. Querying Data** | SQL on ADLS (serverless pool) | Run SQL directly on Parquet/CSV without ingestion |
|  | Partitioning & Clustering | Reduces data scanned and cost |
|  | Parquet / ORC | Columnar formats = faster queries |
| **2. Federated Queries** | Query across Azure SQL, Cosmos DB | Integration with Synapse SQL pools |
| **3. Performance & Cost** | Dedicated pool vs. serverless | Exam often asks about workload isolation, cost models |
| **4. Governance** | Purview integration | Metadata, lineage, security |

---

## 4. Azure Databricks & Synapse Spark

### Azure Databricks
- Collaborative Spark platform for **advanced ETL/ML**.  
- Supports **batch + streaming**.  

### Synapse Spark Pools
- Integrated Spark runtime within Synapse.  
- Great for **big data transformations** without separate cluster mgmt.  

---

## 5. Serverless Compute with Azure Functions

Use cases： 

```mermaid
flowchart TD
    subgraph EventSource
        A1[ADLS Blob Upload]
        A2[Cosmos DB Change Feed]
        A3[Event Hub Stream]
    end

    subgraph AzureFunctions
        L1[Trigger]
        L2[Function App]
        L3[Process Data]
    end

    subgraph TargetServices
        T1[Store in ADLS]
        T2[Update Cosmos DB / Azure SQL]
        T3[Send Notification via Event Grid / Service Bus]
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

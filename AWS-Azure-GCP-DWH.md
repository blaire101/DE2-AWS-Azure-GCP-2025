# ☁️ Cloud Data Warehouse Comparison (AWS Redshift vs Azure Synapse vs GCP BigQuery)

---

## 1. Basics
**Q1. What are AWS Redshift, Azure Synapse, and GCP BigQuery?**

| Type | English |
| --- | --- |
| AWS Redshift | A **<mark>PB-scale</mark> <mark>MPP</mark> <mark>data warehouse</mark>** optimized for **<mark>OLAP</mark>**, part of the **<mark>AWS ecosystem</mark>**. |
| Azure Synapse | Microsoft’s **<mark>cloud data warehouse</mark>** (formerly **<mark>SQL DW</mark>**), integrates with **<mark>Azure ecosystem</mark>** and **<mark>Power BI</mark>**. |
| GCP BigQuery | Fully **<mark>serverless</mark> <mark>data warehouse</mark>**, **<mark>pay-per-query</mark>**, deeply tied to **<mark>Google Cloud</mark>** and **<mark>AI/ML</mark>**. |

---

## 2. Architecture
**Q2. How do they handle architecture and scaling?**

| Type | English |
| --- | --- |
| AWS Redshift | **<mark>Cluster-based</mark>**, with **<mark>Leader Node</mark>** + **<mark>Compute Nodes</mark>**. Scaling = **<mark>resize cluster</mark>** or use **<mark>Serverless</mark>**. |
| Azure Synapse | Uses **<mark>DWU (Data Warehouse Units)</mark>** for compute, scale up/down by changing DWUs. |
| GCP BigQuery | Fully managed, **<mark>elastic scaling</mark>**, no infrastructure to manage. |

---

## 3. Storage & Distribution
**Q3. How is data distributed and stored?**

| Type | English |
| --- | --- |
| AWS Redshift | **<mark>Columnar storage</mark>**. Distribution = **<mark>KEY</mark> / <mark>EVEN</mark> / <mark>ALL</mark> / <mark>AUTO</mark>**. |
| Azure Synapse | Table distribution = **<mark>Hash</mark> / <mark>Round-robin</mark> / <mark>Replicated</mark>**. |
| GCP BigQuery | Automatically partitions and distributes data. Supports **<mark>partitioned</mark> & <mark>clustered tables</mark>**. |

---

## 4. Query Processing
**Q4. How do queries run?**

| Type | English |
| --- | --- |
| AWS Redshift | SQL engine with **<mark>Leader Node</mark> planning** + **<mark>MPP execution</mark>** on compute nodes. |
| Azure Synapse | **<mark>T-SQL</mark>** interface, distributed query engine over **<mark>DWUs</mark>**. |
| GCP BigQuery | **<mark>Dremel engine</mark>**, runs queries on distributed **<mark>slots</mark>**, serverless execution. |

---

## 5. Loading & Integration
**Q5. How is data loaded and integrated?**

| Type | English |
| --- | --- |
| AWS Redshift | **<mark>COPY</mark>** from **<mark>S3</mark>**, integration with **<mark>Glue</mark>**, **<mark>Spectrum</mark>** for querying S3 directly. |
| Azure Synapse | **<mark>COPY INTO</mark>** from **<mark>Azure Blob</mark> / <mark>Data Lake</mark>**, pipelines with **<mark>ADF (Data Factory)</mark>**. |
| GCP BigQuery | Load from **<mark>GCS (Google Cloud Storage)</mark>**, **<mark>streaming inserts</mark>**, pipelines with **<mark>Dataflow</mark> / <mark>Dataproc</mark>**. |

---

## 6. Performance & Optimization
**Q6. How is performance optimized?**

| Type | English |
| --- | --- |
| AWS Redshift | Optimize with **<mark>Distribution Key</mark> / <mark>Sort Key</mark> / <mark>VACUUM</mark> / <mark>WLM</mark>**. |
| Azure Synapse | Optimize with **<mark>Table distribution strategy</mark> / <mark>Statistics</mark> / <mark>Materialized views</mark>**. |
| GCP BigQuery | Optimize with **<mark>partitioned</mark> & <mark>clustered tables</mark>**, **<mark>caching</mark>**, **<mark>slots reservation</mark>**. |

---

## 7. Pricing
**Q7. How is pricing handled?**

| Type | English |
| --- | --- |
| AWS Redshift | Based on **<mark>node type</mark>**, **<mark>cluster size</mark>**, **<mark>on-demand</mark> / <mark>serverless</mark> usage**. |
| Azure Synapse | Based on **<mark>DWU per hour</mark>** + storage costs. |
| GCP BigQuery | **<mark>On-demand query</mark> (per TB scanned)** or **<mark>flat-rate slots</mark>**. Storage billed separately. |

---

## 8. Security
**Q8. How do they handle security?**

| Type | English |
| --- | --- |
| AWS Redshift | **<mark>IAM</mark>**, **<mark>VPC</mark>**, **<mark>KMS encryption</mark>**, **<mark>SSL/TLS</mark>**, **<mark>FGAC</mark> (fine-grained access control)**. |
| Azure Synapse | **<mark>Azure AD</mark>** integration, **<mark>RBAC</mark>**, **<mark>Managed VNET</mark>**, **<mark>TDE encryption</mark>**. |
| GCP BigQuery | **<mark>IAM</mark>**, **<mark>VPC-SC</mark>**, **<mark>CMEK encryption</mark>**, **<mark>row-level</mark> & <mark>column-level security</mark>**. |

---

## 9. Advanced & Scenarios
**Q9. How would you design an e-commerce analytics warehouse in each platform?**

| Type | English |
| --- | --- |
| AWS Redshift | **<mark>Fact/dimension schema</mark>** with **<mark>Distribution</mark> / <mark>Sort Keys</mark>**, data loaded via **<mark>COPY</mark>** from **<mark>S3</mark>**. |
| Azure Synapse | **<mark>Star schema</mark>**, **<mark>Hash-distributed fact tables</mark>**, **<mark>Replicated dimension tables</mark>**. |
| GCP BigQuery | **<mark>Partitioned</mark> & <mark>clustered fact tables</mark>**, ingestion from **<mark>GCS</mark>**, accelerated by **<mark>BI Engine</mark>**. |

**Q10. Compare in one line each.**

| Type | English |
| --- | --- |
| AWS Redshift | Best if you are in **<mark>AWS ecosystem</mark>**, strong integration with **<mark>S3</mark>** & **<mark>Glue</mark>**. |
| Azure Synapse | Best for **<mark>Azure shops</mark>**, integrates with **<mark>Power BI</mark>** and **<mark>ADF</mark>**. |
| GCP BigQuery | Best for **<mark>ad-hoc analytics</mark>** at scale, **<mark>serverless</mark>** with **<mark>ML/AI integration</mark>**. |

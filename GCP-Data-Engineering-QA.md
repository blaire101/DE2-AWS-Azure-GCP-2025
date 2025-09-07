# 📚 GCP Data Engineering Q&A  

```mermaid
flowchart LR
    classDef src fill:#d0f0fd,stroke:#007acc,stroke-width:2px,color:#000,font-weight:bold
    classDef lake fill:#fde2d0,stroke:#cc5200,stroke-width:2px,color:#000,font-weight:bold
    classDef etl fill:#e6d0fd,stroke:#7e3ff2,stroke-width:2px,color:#000,font-weight:bold
    classDef wh fill:#fff3bf,stroke:#d48806,stroke-width:2px,color:#000,font-weight:bold
    classDef srv fill:#d9f7be,stroke:#389e0d,stroke-width:2px,color:#000,font-weight:bold

    subgraph Source["📥 Data Sources"]
        DB[(MySQL Orders)]:::src
        CSV[(GCS CSV Logs)]:::src
    end

    subgraph Lake["🪣 Data Lake (GCS)"]
        RAW[Raw Zone]:::lake
        STG[Staging Zone]:::lake
    end

    subgraph ETL["⚙️ Processing"]
        DF[Dataflow Batch ETL]:::etl
    end

    subgraph Warehouse["🏛️ BigQuery Data Warehouse"]
        FACT[Fact_Orders]:::wh
        DIM[Dim_Customers]:::wh
        AGG[Sales_Aggregates]:::wh
    end

    subgraph Serving["📊 Analytics"]
        LS[Looker Studio]:::srv
    end

    DB --> RAW
    CSV --> RAW
    RAW --> DF --> STG
    STG --> FACT
    STG --> DIM
    FACT --> AGG
    FACT --> LS
    DIM --> LS
    AGG --> LS
```

- [1. BigQuery (Core Data Warehouse)](#1-bigquery-core-data-warehouse)
  - [Q1. What is BigQuery?](#q1-what-is-bigquery)
  - [Q2. BigQuery Architecture](#q2-bigquery-architecture)
  - [Q3. Storage & Data Modeling](#q3-storage--data-modeling)
  - [Q4. Query Execution & Slots](#q4-query-execution--slots)
  - [Q5. Partitioning vs Clustering](#q5-partitioning-vs-clustering)
  - [Q6. External vs Native Tables](#q6-external-vs-native-tables)
  - [Q7. BigQuery Caching](#q7-bigquery-caching)
  - [Q8. Materialized Views vs Scheduled Queries](#q8-materialized-views-vs-scheduled-queries)
  - [Q9. Query Optimization Best Practices](#q9-query-optimization-best-practices)
  - [Q10. Common Pitfalls](#q10-common-pitfalls)

- [2. Cost & Security](#2-cost--security)
  - [Q11. Pricing Models](#q11-pricing-models)
  - [Q12. Cost-saving Techniques](#q12-cost-saving-techniques)
  - [Q13. Security in BigQuery](#q13-security-in-bigquery)

- [3. Data Modeling & ETL](#3-data-modeling--etl)
  - [Q14. Schema Evolution](#q14-schema-evolution)
  - [Q15. Slowly Changing Dimensions](#q15-slowly-changing-dimensions)
  - [Q16. CDC](#q16-cdc)
  - [Q17. Batch Loading](#q17-batch-loading)

- [4. Dataflow (ETL/Streaming Layer)](#4-dataflow-etlstreaming-layer)
  - [Q18. What is Dataflow?](#q18-what-is-dataflow)
  - [Q19. Dataflow Architecture](#q19-dataflow-architecture)
  - [Q20. Batch vs Streaming](#q20-batch-vs-streaming)
  - [Q21. Event-time vs Processing-time](#q21-event-time-vs-processing-time)
  - [Q22. Windowing & Triggers](#q22-windowing--triggers)
  - [Q23. Stateful Example](#q23-stateful-example)
  - [Q24. Shuffle & Streaming Engine](#q24-shuffle--streaming-engine)
  - [Q25. Monitoring](#q25-monitoring)

- [5. Integration & Real-time](#5-integration--real-time)
  - [Q26. Pub/Sub Basics](#q26-pubsub-basics)
  - [Q27. Pub/Sub → Dataflow → BQ](#q27-pubsub--dataflow--bq)
  - [Q28. Batch ETL Pipeline](#q28-batch-etl-pipeline)
  - [Q29. Migration from Hadoop](#q29-migration-from-hadoop)
  - [Q30. E-commerce Analytics](#q30-e-commerce-analytics)

- [6. Cloud Data Fusion (Visual ETL)](#6-cloud-data-fusion-visual-etl)
  - [Q31. What is Cloud Data Fusion?](#q31-what-is-cloud-data-fusion)
  - [Q32. Data Fusion Features](#q32-data-fusion-features)
  - [Q33. Use Cases](#q33-use-cases)

- [7. Dataproc (Managed Spark/Hadoop)](#7-dataproc-managed-sparkhadoop)
  - [Q34. What is Dataproc?](#q34-what-is-dataproc)
  - [Q35. Dataproc Architecture](#q35-dataproc-architecture)
  - [Q36. When to Use](#q36-when-to-use)
  - [Q37. Cost & Optimization](#q37-cost--optimization)
  - [Q38. Pitfalls](#q38-pitfalls)

- [✅ Final Summary](#-final-summary)

- [🎯 Goal](#-goal)

## 🎯 Goal

For a **Data Engineer role focusing on GCP Data Warehouse & ETL**.

* Deep focus on **BigQuery (core warehouse)**
* Solid understanding of **ETL (batch & streaming with Dataflow)**
* Cover **Batch ETL Pipelines & Integration Scenarios**

## 1. BigQuery (Core Data Warehouse)

<div align="center">
  <img src="docs/GCP-BigQuery.png" alt="Diagram" width="500">
</div>

### Q1. What is BigQuery?

- BigQuery is a **<mark>serverless</mark>**, **<mark>fully managed</mark>**, **<mark>cloud data warehouse</mark>** optimized for OLAP.  
- It separates **<mark>storage (Colossus</mark>, Google’s next-gen file system, similar to HDFS)** and **<mark>Compute (slots)</mark>** using the **<mark>Dremel execution engine</mark>**.

```mermaid
flowchart TB
    classDef storage fill:#eaf4ff,stroke:#2980b9,stroke-width:1.5px,color:#000
    classDef compute fill:#f0fff0,stroke:#27ae60,stroke-width:1.5px,color:#000
    classDef schema  fill:#fff0f6,stroke:#c2185b,stroke-width:1.5px,color:#000
    classDef cache   fill:#fdf5e6,stroke:#8e44ad,stroke-width:1.5px,color:#000

    %% BigQuery as a container
    subgraph BQ["🏛️ BigQuery"]
      direction LR
      B[💾 Storage<br/>Colossus + Capacitor]:::storage
      C[⚡ Compute<br/>Dremel + Slots]:::compute
      D[🗂️ Schema<br/>Partition + Clustering]:::schema
      E[📊 Caching & Views]:::cache

      %% 隐形连线，确保它们在一行
      B --- C
      C --- D
      D --- E
    end

    %% 可选：外部链接
    %% Client --> BQ
    %% BQ --> Downstream
```

✅ BigQuery vs Hive vs SparkSQL

| Feature | BigQuery | Hive | SparkSQL |
|--------|----------|------|----------|
| Type | Managed MPP Data Warehouse | Hadoop SQL Engine | In-memory distributed SQL |
| Storage | Columnar + GCS | HDFS | HDFS/S3/GCS |
| Latency | Fast | Slow | Fast |
| Deployment | Fully managed | Self-hosted Hadoop | Self-hosted Spark |

### Q2. BigQuery Architecture

```mermaid
flowchart TD
    classDef storage fill:#e6f2ff,stroke:#004080,stroke-width:2px,color:#000,font-weight:bold
    classDef compute fill:#fff0e6,stroke:#993300,stroke-width:2px,color:#000,font-weight:bold
    classDef client  fill:#e6ffe6,stroke:#006600,stroke-width:2px,color:#000,font-weight:bold

    subgraph Client["🧑‍💻 Client Layer"]
    U1["BI Tools - Looker, Data Studio"]:::client
    U2["APIs and SDKs"]:::client
    U3["Console or CLI"]:::client
    U1 --- U2
    U2 --- U3
    end

    subgraph Compute["⚡ Dremel Execution Engine"]
    Q1["SQL Parser"]:::compute
    Q2["Execution Tree - Fan-out/Fan-in"]:::compute
    Q3["Slots - Virtual CPUs"]:::compute
    Q1 --- Q2
    Q2 --- Q3
    end

    subgraph Storage["☁️ Colossus Storage"]
    T1["Tables - Capacitor Columnar"]:::storage
    P1["Partitions and Clusters"]:::storage
    T1 --- P1
    end

    Client --> Compute
    Compute --> Storage
```

### Q3. Storage & Data Modeling

* Partitioning = split table into **chunks** (date/int).
* Clustering = sort **inside each partition** (customer\_id, product\_id).
* Schema = **Star schema** recommended.

### Q4. Query Execution & Slots

```mermaid
flowchart LR
    A[SQL Query] --> B[Fan-out to Slots]
    B --> C[Parallel Execution]
    C --> D[Fan-in Aggregation]
    D --> E[Final Result]
```

### Q5. Partitioning vs Clustering

* Partitioning = reduce scanned data.
* Clustering = speed filtering/sorting.
* Best = combine both.

### Q6. External vs Native Tables

* **Native**: stored in BigQuery’s **Colossus**.
* **External**: data in **GCS/BigLake/Sheets**. Query via federation.
* Trade-off: flexibility vs performance.

```mermaid
flowchart TB
    classDef client fill:#e6ffe6,stroke:#006600,stroke-width:2px,color:#000,font-weight:bold
    classDef native fill:#eaf4ff,stroke:#2980b9,stroke-width:2px,color:#000,font-weight:bold
    classDef external fill:#fff0f6,stroke:#c2185b,stroke-width:2px,color:#000,font-weight:bold
    classDef trade fill:#fdf5e6,stroke:#8e44ad,stroke-width:1.5px,color:#000

    %% Client in the center
    C[🧑‍💻 Query<br/>Client/BI Tool]:::client

    %% BigQuery container
    subgraph BQ["🏛️ BigQuery"]
      direction TB
      N[💾 Native Table<br/>Colossus Storage]:::native
      X[🌐 External Table<br/>GCS / BigLake / Sheets]:::external
    end

    %% Place Client in middle linking to both
    C --> N
    C --> X

    N --> R1[⚡ Fast performance<br/>Optimized storage]:::trade
    X --> R2[🔄 Flexible federation<br/>But slower]:::trade
```

### Q7. BigQuery Caching

* Query results cached 24h.
* No cost if rerun unchanged query.

### Q8. Materialized Views vs Scheduled Queries

* MV = precomputed, auto-refresh.
* SQ = periodic query into table.

Q1. What is the difference between a <mark>Materialized View</mark> and a <mark>Scheduled Query</mark> in BigQuery?

- **<mark>Materialized View</mark>**: <mark>Precomputed</mark>, <mark>auto-refresh</mark>, <mark>incremental updates</mark>, best for <mark>frequently queried aggregations</mark>.  
- **<mark>Scheduled Query</mark>**: <mark>Periodic execution</mark>, writes results to a <mark>table</mark>, best for <mark>daily/weekly reports</mark>.  

Q2. In which scenarios would you choose a <mark>Materialized View</mark> over a <mark>Scheduled Query</mark> (and vice versa)?

- **Use <mark>MV</mark>**: <mark>Dashboard</mark> needs <mark>real-time fast query</mark> of the same aggregation.  
- **Use <mark>SQ</mark>**: Business requires <mark>daily snapshot reports</mark> (e.g., <mark>yesterday’s sales</mark>).  

```mermaid
flowchart TB
    classDef mv fill:#eaf4ff,stroke:#2980b9,stroke-width:2px,color:#000,font-weight:bold
    classDef sq fill:#fff0f6,stroke:#c2185b,stroke-width:2px,color:#000,font-weight:bold
    classDef use fill:#fdf5e6,stroke:#8e44ad,stroke-width:1.5px,color:#000

    C[🧑‍💻 Query Client/BI Tool]

    subgraph BQ["🏛️ BigQuery"]
      direction TB
      MV[📊 Materialized View<br/>Auto-refresh, Incremental]:::mv
      SQ[⏱️ Scheduled Query<br/>Runs on Schedule]:::sq
    end

    C --> MV
    C --> SQ

    MV --> U1[⚡ Fast repeated aggregations<br/>Dashboards, low latency]:::use
    SQ --> U2[📅 Periodic snapshots<br/>Daily/weekly reports]:::use
```

### Q9. Query Optimization Best Practices

* Avoid `SELECT *`.
* Use partition filters.
* Monitor with `INFORMATION_SCHEMA.JOBS`.

### Q10. Common Pitfalls

* Unpartitioned scans → \$\$\$.
* Too many streaming inserts.
* Misusing clustering.

| Pitfall | Explanation | Cost/Performance Impact | Best Practice |
|---------|-------------|--------------------------|---------------|
| **Unpartitioned scans** | Query runs over the entire table without filtering by partition | 🚨 Very high cost (pay per TB scanned) + slow queries | Use **Partitioning** (e.g., by date) and always filter on partition column |
| **Too many streaming inserts** | Writing rows in real-time with streaming API | 🚨 Expensive vs batch loads + quota limits | Prefer **Batch load from GCS**; if real-time needed, use **Pub/Sub + Dataflow** to micro-batch |
| **Misusing clustering** | Choosing low-cardinality fields (e.g., boolean) for clustering | 🚨 No performance benefit, still pay for scan | Use **high-cardinality, frequently filtered fields** (e.g., `user_id`, `product_id`) for clustering |

## 2. Cost & Security

```mermaid
flowchart TB
    classDef main fill:#ffe8cc,stroke:#b03a2e,stroke-width:2px,font-weight:bold,color:#000
    classDef pricing fill:#eaf4ff,stroke:#2874a6,stroke-width:1.5px
    classDef saving fill:#f0fff0,stroke:#229954,stroke-width:1.5px
    classDef security fill:#fff0f6,stroke:#8e44ad,stroke-width:1.5px

    A[💰 Cost & 🔒 Security]:::main
    B[💵 Pricing Models]:::pricing
    C[📉 Cost-saving]:::saving
    D[🛡️ Security]:::security
    A --> B
    A --> C
    A --> D
```

### Q11. Pricing Models

* On-demand: \$5/TB scanned.
* Flat-rate: reserved **slots**.
* Storage: active vs long-term.

### Q12. Cost-saving Techniques

* Partition tables.
* Compressed formats.
* Avoid SELECT \*.
* Monitor queries.

### Q13. Security in BigQuery

* IAM (project/dataset/table).
* Row/Column-level policies.
* CMEK, VPC-SC.

## 3. Data Modeling & ETL

```mermaid
flowchart TB
    classDef main fill:#ffe8cc,stroke:#6c3483,stroke-width:2px,font-weight:bold,color:#000
    classDef schema fill:#eaf4ff,stroke:#2874a6,stroke-width:1.5px
    classDef scd fill:#f0fff0,stroke:#27ae60,stroke-width:1.5px
    classDef cdc fill:#fff0f6,stroke:#c2185b,stroke-width:1.5px
    classDef batch fill:#fdf5e6,stroke:#8e44ad,stroke-width:1.5px

    A[🧩 Data Modeling & ETL]:::main
    B[📐 Schema Evolution]:::schema
    C[🕰️ SCD Types]:::scd
    D[🔄 CDC Pipelines]:::cdc
    E[📥 Batch Load]:::batch
    A --> B
    A --> C
    A --> D
    A --> E
```

### Q14. Schema Evolution

* Add = easy.
* Drop/change = new table + view.

### Q15. Slowly Changing Dimensions

* Type1 = overwrite.
* Type2 = new row with valid\_from/to.
* Type3 = new column.

### Q16. CDC

* Use **Datastream/Dataflow** to apply DB changes into BQ.

### Q17. Batch Loading

* `bq load` or Dataflow.
* From GCS (Parquet/Avro preferred).

## 4. Dataflow (ETL/Streaming Layer)

```mermaid
flowchart TB
    classDef main fill:#ffe8cc,stroke:#196f3d,stroke-width:2px,font-weight:bold,color:#000
    classDef beam fill:#eaf4ff,stroke:#1f618d,stroke-width:1.5px
    classDef window fill:#f0fff0,stroke:#27ae60,stroke-width:1.5px
    classDef state fill:#fff0f6,stroke:#c2185b,stroke-width:1.5px
    classDef shuffle fill:#fdf5e6,stroke:#8e44ad,stroke-width:1.5px
    classDef monitor fill:#e8f8f5,stroke:#148f77,stroke-width:1.5px

    A[⚙️ Dataflow]:::main
    B[🌊 Apache Beam]:::beam
    C[⏱️ Windowing & Triggers]:::window
    D[📈 Stateful Processing]:::state
    E[🔀 Shuffle/Streaming Engine]:::shuffle
    F[📡 Monitoring]:::monitor
    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
```

### Q18. What is Dataflow?

* Serverless ETL for **batch & streaming**, built on **Apache Beam**.

### Q19. Dataflow Architecture

* Sources: Pub/Sub, GCS, DB.
* Pipeline: PCollection → PTransform → Window.
* Sinks: BQ, Bigtable, GCS.

### Q20. Batch vs Streaming

* Batch = daily/hourly.
* Streaming = near real-time.

### Q21. Event-time vs Processing-time

* Event-time = when happened.
* Processing-time = when processed.

### Q22. Windowing & Triggers

* Fixed, Sliding, Session windows.
* Triggers control partial results.

### Q23. Stateful Example

* Count per user clicks in 5 min window.

### Q24. Shuffle & Streaming Engine

* Shuffle offloaded → backend.
* Streaming engine stores state externally.

### Q25. Monitoring

* Stackdriver Logging + Metrics.

## 5. Integration & Real-time

```mermaid
flowchart TB
    classDef main fill:#ffe8cc,stroke:#154360,stroke-width:2px,font-weight:bold,color:#000
    classDef pubsub fill:#eaf4ff,stroke:#1f618d,stroke-width:1.5px
    classDef pipeline fill:#f0fff0,stroke:#27ae60,stroke-width:1.5px
    classDef batch fill:#fff0f6,stroke:#c2185b,stroke-width:1.5px
    classDef migrate fill:#fdf5e6,stroke:#8e44ad,stroke-width:1.5px
    classDef usecase fill:#e8f8f5,stroke:#148f77,stroke-width:1.5px

    A[🔗 Integration & Real-time]:::main
    B[📩 Pub/Sub Basics]:::pubsub
    C[⚡ Realtime Pipeline]:::pipeline
    D[📂 Batch ETL]:::batch
    E[🚚 Migration from Hadoop]:::migrate
    F[🛒 E-commerce Analytics]:::usecase
    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
```

### Q26. Pub/Sub Basics

* GCP real-time messaging.
* Producers → Topics → Subscribers → Dataflow → BQ.

### Q27. Pub/Sub → Dataflow → BQ

* Streaming ETL.

### Q28. Batch ETL Pipeline

* GCS → Dataflow/Dataproc → BQ.

### Q29. Migration from Hadoop

* HDFS → GCS, Hive → Dataproc.

### Q30. E-commerce Analytics

* Real-time orders (Pub/Sub).
* Sessionization (Dataflow).
* Star schema (BQ).
* Visualization (Looker).

| **Dimension** | Cloud Data Fusion (CDF) | Dataflow (Apache Beam) | Dataproc (Spark/Hadoop) |
|---|---|---|---|
| **Development model** | <mark>Low-code</mark>, visual pipelines, drag-and-drop | <mark>Code-first</mark> (Java/Python/SQL via <mark>Beam</mark> SDKs) | <mark>Code-first</mark> (<mark>Spark</mark>/Scala/PySpark, Hive) |
| **Primary paradigm** | <mark>Visual ETL/ELT</mark>, multi-source batch integration | <mark>Streaming</mark> + batch ETL with <mark>state</mark>, <mark>windows</mark>, <mark>triggers</mark> | <mark>Large-scale batch</mark>, existing <mark>Spark/Hadoop</mark> workloads |
| **Runtime / engine** | Runs on <mark>Dataproc/Spark</mark> via Profiles | Managed <mark>Beam runner</mark> (Dataflow) | Managed <mark>Spark/Hadoop</mark> clusters or Serverless |
| **Latency profile** | Minutes-level (cluster spin-up, scheduling) | <mark>Seconds / sub-seconds</mark> for streaming; efficient batch | Minutes to hours for batch; streaming via Spark Structured Streaming |
| **Streaming strength** | Good for standardized batch; can read Pub/Sub | <mark>Strongest</mark>: exactly-once sinks, stateful processing | Possible, but more ops effort; better for batch |
| **Connectors** | <mark>Rich catalog</mark>: JDBC, SaaS, GCS, <mark>BigQuery</mark>, Pub/Sub | Beam I/O connectors (broad, code-driven) | Spark ecosystem connectors; <mark>BigQuery connector</mark>, JDBC |
| **Ops & cost levers** | Low build effort; runtime uses Dataproc. Use <mark>temporary clusters</mark> and right-sized <mark>profiles</mark> | Serverless <mark>autoscaling</mark>, batching, efficient windows/triggers | <mark>Ephemeral clusters</mark>, <mark>preemptible workers</mark>, autoscaling; tuning needed |
| **Best fit** | <mark>Low-code teams</mark>, many sources, standardized batch, governance | <mark>Low-latency real-time</mark>, complex stateful ETL, portable logic | <mark>Existing Spark assets</mark>, custom libs, heavy offline batch |
| **Typical example** | SaaS/JDBC + files → cleanse/joins → BigQuery | Pub/Sub → Dataflow (sessionization/state) → BigQuery | HDFS/Parquet → Spark jobs → BigQuery via connector |

## 6. Cloud Data Fusion (Visual ETL)

### Q31. What is Cloud Data Fusion?

* Managed **visual data integration** service (built on CDAP).
* Low-code ETL pipelines.
* Runtime = Dataflow (streaming) or Dataproc (batch).

### Q32. Data Fusion Features

* Wrangler for data prep.
* Error handling: dead-letter, retry.
* Schema drift alerts.
* CI/CD export + deploy.

### Q33. Use Cases

* DB → BigQuery batch ingestion.
* GCS CSV → Wrangler → BQ.
* Pub/Sub → BQ streaming.

## 7. Dataproc (Managed Spark/Hadoop)

### Q34. What is Dataproc?

* Managed Hadoop/Spark clusters.
* Supports Spark, Hive, Pig, Presto.
* Bridge for **legacy workloads**.

### Q35. Dataproc Architecture

* Master/Worker VMs.
* Uses **GCS as HDFS**.
* Clusters = ephemeral or long-running.

### Q36. When to Use

* Lift & shift Hadoop/Spark.
* Complex batch ETL.
* PySpark ML/ETL pipelines.

### Q37. Cost & Optimization

* Pay per VM-minute.
* Ephemeral clusters → cost savings.
* Prefer GCS over HDFS.

### Q38. Pitfalls

* Leaving clusters idle.
* Using HDFS instead of GCS.
* Poor Spark tuning.

# ✅ Final Summary

* **BigQuery** → Data Warehouse Core.
* **Dataflow** → Batch + Streaming ETL (Apache Beam).
* **Pub/Sub** → Real-time ingestion.
* **Cloud Data Fusion** → Visual low-code ETL (runs on Dataflow/Dataproc).
* **Dataproc** → Legacy Spark/Hadoop bridge.
* Together → End-to-end **GCP Data Platform** (batch + streaming + migration).

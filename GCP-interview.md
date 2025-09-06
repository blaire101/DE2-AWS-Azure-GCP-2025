# 📚 GCP Data Engineering Interview Q&A

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

## 🎯 Goal
For a **Data Engineer role focusing on GCP Data Warehouse & ETL**.  
- Deep focus on **BigQuery (core warehouse)**  
- Solid understanding of **ETL (batch & streaming with Dataflow)**  
- Mention **Pub/Sub (real-time ingestion)**  
- Cover **Batch ETL Pipelines & Integration Scenarios**

## 1. BigQuery (Core Data Warehouse)

### Q1. What is BigQuery?

- BigQuery is a **<mark>serverless</mark>**, **<mark>fully managed</mark>**, **<mark>cloud data warehouse</mark>** optimized for OLAP.  
- It separates **<mark>storage (Colossus</mark>, Google’s next-gen file system, similar to HDFS)** and **<mark>Compute (slots)</mark>** using the **<mark>Dremel execution engine</mark>**.

### Q2. BigQuery Architecture

```mermaid
flowchart TD

%% ===== Styles =====
classDef storage fill:#e6f2ff,stroke:#004080,stroke-width:2px,color:#000,font-weight:bold
classDef compute fill:#fff0e6,stroke:#993300,stroke-width:2px,color:#000,font-weight:bold
classDef client  fill:#e6ffe6,stroke:#006600,stroke-width:2px,color:#000,font-weight:bold

%% ===== Client Layer: subgraph with nodes forced horizontal via hidden links =====
subgraph Client["🧑‍💻 Client Layer"]
U1["BI Tools - Looker, Data Studio"]:::client
U2["APIs and SDKs"]:::client
U3["Console or CLI"]:::client
U1 --- U2
U2 --- U3
end

%% ===== Compute Layer =====
subgraph Compute["⚡ Dremel Execution Engine"]
Q1["SQL Parser"]:::compute
Q2["Execution Tree - Fan-out/Fan-in"]:::compute
Q3["Slots - Virtual CPUs"]:::compute
Q1 --- Q2
Q2 --- Q3
end

%% ===== Storage Layer =====
subgraph Storage["☁️ Colossus Storage"]
T1["Tables - Capacitor Columnar<br>columnar storage format"]:::storage
P1["Partitions and Clusters"]:::storage
T1 --- P1
end

%% ===== Vertical flow between the three frames =====
Client --> Compute
Compute --> Storage

%% ===== Hide the helper horizontal links so only the frames and vertical arrows remain =====
linkStyle 0 stroke-width:0px,fill:none
linkStyle 1 stroke-width:0px,fill:none
linkStyle 2 stroke-width:0px,fill:none
linkStyle 3 stroke-width:0px,fill:none
linkStyle 4 stroke-width:0px,fill:none
```

### Q3. Storage & Data Modeling

* **Partitioning**: ingestion-time, date/datetime, int range
* **Clustering**: sort by customer\_id, product\_id
* **Schema design**: star schema (fact + dimension) recommended

> - Partitioning:  = Splitting the table into “big chunks” (e.g., by date).
> - Clustering:  = Within each chunk, sorting the data (e.g., by user, product) to make “precise lookups” faster.

### Q4. Query Execution & Slots

```mermaid
flowchart TD
    A[SQL Query] --> B[Fan-out to Slots]
    B --> C[Parallel Execution on Slots]
    C --> D[Fan-in Aggregation]
    D --> E[Final Result]
```

Queries broken into stages executed on **<mark>slots</mark>**.
Dremel tree → fan-out parallelism → fan-in aggregation.

### Q5. Partitioning vs Clustering

* **Partitioning** reduces scanned data (by date/int).
* **Clustering** improves performance for filtering/sorting on clustered columns.
* Best practice: combine both.

### Q6. External vs Native Tables

* **Native**: stored in BigQuery’s **Colossus**.
* **External**: data in **GCS/BigLake/Sheets**. Query via federation.
* Trade-off: flexibility vs performance.

### Q7. BigQuery Caching

Query results cached 24 hours.
No charge if exact query reruns on unchanged data.

### Q8. Materialized Views vs Scheduled Queries

* **Materialized views**: precomputed, auto-refreshed.
* **Scheduled queries**: run at intervals, save to table.

### Q9. Query Optimization Best Practices

* Avoid **SELECT \***
* Use **partition filters**
* Choose correct **distribution of data**
* Monitor with **INFORMATION\_SCHEMA.JOBS**

### Q10. Common Pitfalls

* Running queries on unpartitioned tables → high cost
* Overusing streaming inserts (expensive)
* Misusing clustering (only effective when filtering on clustered columns)

## 2. Cost & Security

### Q11. Pricing Models

* **On-demand**: \$5/TB scanned
* **Flat-rate**: reserved **slots** for predictable workloads
* Storage: active vs long-term (cheaper after 90 days)

### Q12. Cost-saving Techniques

* Partition tables
* Use compressed formats (Parquet, ORC)
* Avoid SELECT \*
* Monitor query usage

### Q13. Security in BigQuery

* **IAM**: project/dataset/table level
* **Row/Column-level security**
* **CMEK encryption**
* **VPC-SC** for perimeter security

## 3. Data Modeling & ETL

### Q14. Schema Evolution in BigQuery

* Add columns is easy
* Deleting/changing requires new table
* Use **versioning + views** to manage evolution

### Q15. Slowly Changing Dimensions (SCD)

* **Type 1**: overwrite
* **Type 2**: add new row with valid\_from / valid\_to
* **Type 3**: add new column

### Q16. CDC (Change Data Capture)

Use **Dataflow or Datastream** to capture DB changes and apply into BigQuery.

### Q17. Batch Loading into BigQuery

* Via **bq load** or Dataflow batch
* From **GCS (CSV, Parquet, ORC, Avro)**
* Recommended: Parquet/Avro (compressed, schema support)

## 4. Dataflow (ETL/Streaming Layer)

### Q18. What is Dataflow?

A **<mark>serverless</mark>** data processing service for **batch & streaming ETL**, based on **<mark>Apache Beam</mark>**.

### Q19. Dataflow Architecture

```mermaid
flowchart TD
    subgraph Source["📥 Sources"]
        Pub[Pub/Sub]
        GCS[Google Cloud Storage]
        DB[Cloud SQL / Bigtable]
    end

    subgraph Pipeline["⚡ Apache Beam Pipeline"]
        PC[PCollections]
        PT[PTransforms]
        WN[Windowing & Triggers]
    end

    subgraph Sink["📤 Sinks"]
        BQ[BigQuery]
        BT[Bigtable]
        GCS2[GCS]
    end

    Source --> Pipeline --> Sink
```

---

### Q20. Batch vs Streaming in Dataflow

* **Batch**: GCS → Dataflow → BigQuery (daily/hourly)
* **Streaming**: Pub/Sub → Dataflow → BigQuery (near real-time)

---

### Q21. Event-time vs Processing-time

* **Event-time**: when event happened
* **Processing-time**: when processed
* Important for late-arriving data

---

### Q22. Windowing & Triggers

* **Fixed windows** (every 5 min)
* **Sliding windows** (e.g., 5 min window every 1 min)
* **Session windows** (user activity gaps)
* Triggers decide when partial results are emitted

---

### Q23. Stateful Processing Example

Maintain counters per key (e.g., number of clicks per user in last 5 mins).

---

### Q24. Dataflow Shuffle & Streaming Engine

* Shuffle service → offloads shuffle to backend
* Streaming engine → moves state/shuffle from workers to service → autoscaling

---

### Q25. Monitoring & Debugging

* **Stackdriver (Cloud Logging)**
* **Cloud Monitoring** for metrics (latency, throughput, backlogs)

---

## 5. Integration & Real-time

### Q26. Pub/Sub Basics

Pub/Sub is GCP’s **<mark>real-time messaging service</mark>** for ingestion.
Producers publish → Subscribers consume → Dataflow processes → BigQuery stores.

---

### Q27. Pub/Sub → Dataflow → BigQuery Pipeline

```mermaid
flowchart LR
    P[Pub/Sub Topic] --> D[Dataflow Streaming Job]
    D --> B[BigQuery Table]
    D --> M[Monitoring/Alerts]
```

---

### Q28. Batch ETL Pipeline

* Source: GCS (daily files)
* Process: Dataflow batch / Dataproc Spark
* Sink: BigQuery (fact & dimension tables)

---

### Q29. Migration from Hadoop

* HDFS → GCS
* Hive/Spark → Dataproc
* Move reporting → BigQuery

---

### Q30. E-commerce Analytics Pipeline

* Ingest: Pub/Sub (real-time orders)
* Transform: Dataflow (ETL, sessionization)
* Store: BigQuery star schema (orders, customers, products)
* Visualize: Looker / BI Engine

---

# ✅ Final Summary

* **BigQuery**: <mark>Data Warehouse core</mark> (serverless, scalable, slot-based execution)
* **Dataflow**: <mark>ETL engine</mark> (batch + streaming with Apache Beam)
* **Pub/Sub**: <mark>real-time ingestion</mark> layer
* **Dataproc**: bridge for legacy Spark/Hadoop
* Together: End-to-end **GCP Data Platform** for batch + real-time analytics


# Google Cloud Professional Data Engineer — Q&A (Q1–Q319)

## 1. Machine Learning & TensorFlow
- [Q1: TensorFlow Overfitting Prevention](#q1-tensorflow-overfitting-prevention)
- [Q2: Retraining Recommendation Model](#q2-retraining-recommendation-model)
- [Q7: Predict Housing Prices](#q7-predict-housing-prices)
- [Q14: Unsupervised Anomaly Detection](#q14-unsupervised-anomaly-detection)
- [Q27: Speeding Up Model Training](#q27-speeding-up-model-training)
- [Q203: Faster TensorFlow Training](#q203-faster-tensorflow-training)
- [Q204: BigQuery ML + Vertex AI for Streaming](#q204-bigquery-ml--vertex-ai-for-streaming)
- [Q243: Handling Nulls in BigQueryML](#q243-handling-nulls-in-bigqueryml)
- [Q245: Next Step in ML Lifecycle](#q245-next-step-in-ml-lifecycle)

---

## 2. BigQuery Basics

### A) Query Patterns & SQL Features

* [Q5: Partitioning vs Clustering](#q5-partitioning-vs-clustering)
* [Q8: Deduplication with ROW\_NUMBER window function](#q8-deduplication-with-row_number-window-function)
* [Q9: Wildcard Tables](#q9-wildcard-tables)
* [Q53: Slow GROUP BY due to data skew](#q53-slow-group-by-due-to-data-skew)
* [Q56: Legacy SQL over sharded tables — use `TABLE_DATE_RANGE`](#q56-legacy-sql-over-sharded-tables--use-table_date_range)

### B) Ingestion, Freshness & Consistency

* [Q15: Streaming inserts are eventually consistent (wait before query)](#q15-streaming-inserts-are-eventually-consistent-wait-before-query)
* [Q24: Convert STRING to TIMESTAMP with new table](#q24-convert-string-to-timestamp-with-new-table)
* [Q48: CSV import mismatch — fix file encoding (BigQuery defaults to UTF-8)](#q48-csv-import-mismatch--fix-file-encoding-bigquery-defaults-to-utf-8)

### C) Governance & Access Control

* [Q10: Restrict access in BigQuery (IAM roles, dataset isolation)](#q10-restrict-access-in-bigquery-iam-roles-dataset-isolation)
* [Q40: Enforce regional access — dataset-per-region + IAM on datasets](#q40-enforce-regional-access--dataset-per-region--iam-on-datasets)

### D) Admin, Performance & Workload Mgmt

* [Q233: Troubleshooting BigQuery slot contention](#q233-troubleshooting-bigquery-slot-contention)
* [Q239: Concurrency issues with slots](#q239-concurrency-issues-with-slots)

### E) Data Modeling & Table Design

* [Q60: Replace sharded tables with one partitioned table](#q60-replace-sharded-tables-with-one-partitioned-table)
* [Q252: Designing customer–product–subscription model](#q252-designing-customerproductsubscription-model)

### F) Integration & BI (Looker Studio / Tools)

* [Q4: Disable caching in Data Studio report (data missing for <1h)](#q4-disable-caching-in-data-studio-report-data-missing-for-1h)
* [Q25: Stackdriver Logging + advanced filter for BQ insert jobs](#q25-stackdriver-logging--advanced-filter-for-bq-insert-jobs)
* [Q36: Use a view to simplify columns for BI and cut query cost](#q36-use-a-view-to-simplify-columns-for-bi-and-cut-query-cost)
* [Q39: Data Studio on BigQuery — build filtered, fast reports](#q39-data-studio-on-bigquery--build-filtered-fast-reports)
* [Q43: Expose `FullName` via a BigQuery view (avoid reshaping data)](#q43-expose-fullname-via-a-bigquery-view-avoid-reshaping-data)
* [Q46: Keep frequently updated reference data via BigQuery external table (GCS)](#q46-keep-frequently-updated-reference-data-via-bigquery-external-table-gcs)
* [Q55: ODBC access — use Standard SQL view + service account](#q55-odbc-access--use-standard-sql-view--service-account)

### G) Views & Materialized Views

* [Q248: Filtering rows with views vs materialized views](#q248-filtering-rows-with-views-vs-materialized-views)


## 3. Cost & Security
- [Q11: Pricing Models](#q11-pricing-models)
- [Q12: Cost-Saving Techniques](#q12-cost-saving-techniques)
- [Q13: Security in BigQuery](#q13-security-in-bigquery)
- [Q200: PII Protection](#q200-pii-protection)
- [Q215: CMEK Sharing](#q215-cmek-sharing)
- [Q238: Per-User Crypto-Deletion](#q238-per-user-crypto-deletion)

---

## 4. Data Modeling & ETL
- [Q14: SCD Types](#q14-scd-types)
- [Q16: CDC Pipelines](#q16-cdc-pipelines)
- [Q17: Batch Loading](#q17-batch-loading)
- [Q223: Dataform Assertions](#q223-dataform-assertions)
- [Q252: Data Warehouse Design](#q252-data-warehouse-design)

---

## 5. Dataflow & Pipelines
- [Q5: Handling Corrupted CSV Data](#q5-handling-corrupted-csv-data)
- [Q11: Basket Abandonment with Session Window](#q11-basket-abandonment-with-session-window)
- [Q212: Dataflow Firewall Troubleshooting](#q212-dataflow-firewall-troubleshooting)
- [Q253: Dataflow Internal IP Only](#q253-dataflow-internal-ip-only)
- [Q254: Dataflow Performance Optimization](#q254-dataflow-performance-optimization)

---

## 6. Dataplex / Data Mesh / Governance
- [Q210: Dataplex Design for Data Products](#q210-dataplex-design-for-data-products)
- [Q217: Secure BigQuery Sharing with Policy Tags](#q217-secure-bigquery-sharing-with-policy-tags)
- [Q240: Dataplex Permissions](#q240-dataplex-permissions)
- [Q244: Analytics Hub Sharing](#q244-analytics-hub-sharing)
- [Q247: Data Mesh with Dataplex](#q247-data-mesh-with-dataplex)

---

## 7. Pub/Sub & Messaging
- [Q20: Duplicate Messages](#q20-duplicate-messages)
- [Q224: Dataflow Lag in Pub/Sub](#q224-dataflow-lag-in-pubsub)
- [Q228: Reprocessing Pub/Sub Messages](#q228-reprocessing-pubsub-messages)

---

## 8. Cloud SQL / Spanner / Databases
- [Q3: Scaling Patient Records](#q3-scaling-patient-records)
- [Q197: ACID-Compliant Database](#q197-acid-compliant-database)
- [Q218: Cloud SQL Disaster Recovery](#q218-cloud-sql-disaster-recovery)
- [Q236: HA Cloud SQL Multi-Region](#q236-ha-cloud-sql-multi-region)

---

## 9. Cloud Storage & Data Lake
- [Q19: Storage Costs with Dataproc](#q19-storage-costs-with-dataproc)
- [Q241: Cloud Storage RPO Design](#q241-cloud-storage-rpo-design)
- [Q249: Cost Optimization for Raw Data](#q249-cost-optimization-for-raw-data)
- [Q251: Retention Policy Lock](#q251-retention-policy-lock)
- [Q257: Autoclass for Data Lake](#q257-autoclass-for-data-lake)

---

## 10. Governance & IAM
- [Q10: Restricting Access in BigQuery](#q10-restricting-access-in-bigquery)
- [Q232: Resource Location Policy](#q232-resource-location-policy)
- [Q226: Pub/Sub Isolation with VPC-SC](#q226-pubsub-isolation-with-vpc-sc)

---


## 1. Machine Learning & TensorFlow

#### Q1: TensorFlow Overfitting Prevention


**Question:**  
Your company built a TensorFlow neural-network model with a large number of neurons and layers. The model fits well for the training data. However, when tested against new data, it performs poorly. What method can you employ to address this?

- **Answer:** A. Apply **regularization techniques** such as dropout, L1/L2 penalties, or early stopping.  
  - Overfitting means the model memorizes training data but fails to generalize.  
  - **Dropout** randomly disables neurons during training, preventing co-adaptation.  
  - **L1/L2 regularization** penalizes overly complex weights.  
  - **Early stopping** halts training once validation loss stops improving.  

## 2. BigQuery Basics

### A) Query Patterns & SQL Features

#### Q5: Partitioning vs Clustering

**Question:**  
Your team wants to optimize query performance and cost in BigQuery. What is the difference between partitioning and clustering, and how can they be combined?

- **Answer:**  
  - **Partitioning** reduces the amount of data scanned by filtering on partition keys (e.g., date).  
  - **Clustering** organizes data inside partitions based on specified columns, improving filtering and sorting.  
  - **Best Practice:** Combine both. Example: Partition by `order_date` and cluster by `user_id`. This minimizes scanned data and speeds up queries.

#### Q8: Deduplication with ROW_NUMBER window function

Question:  
You are building a new real-time data warehouse using **BigQuery streaming inserts**. Since there’s no guarantee that data will only be sent once, but you do have a **unique ID** for each row and an **event timestamp**, you want to ensure that **duplicates are not included** when querying. Which query type should you use?

- **Answer:**  
  Use the **ROW_NUMBER** window function with `PARTITION BY unique_id` and filter on `row_number = 1`.

**Explanation (English):**  
- BigQuery streaming inserts may produce **duplicate rows**.  
- To deduplicate, you partition by the **unique ID** and order by timestamp.  
- Then select only the **first row** (`row_number = 1`).  
- Example:  

```sql
  SELECT *
  FROM (
    SELECT *, ROW_NUMBER() OVER(PARTITION BY unique_id ORDER BY event_ts DESC) AS rn
    FROM mytable
  )
  WHERE rn = 1;
```

#### Q9: Wildcard Tables in BigQuery

**Question:**  
You need to query across multiple tables in BigQuery whose names share a prefix (e.g., `gsod*`). Which query syntax should you use?

- **Answer:**  
  Use **backticks with a wildcard** in the table name.  
  Example:  
  
```sql
  SELECT * 
  FROM `bigquery-public-data.noaa_gsod.gsod*`
  WHERE _TABLE_SUFFIX BETWEEN '2010' AND '2012';
```

#### Q53: Slow GROUP BY due to data skew

Question:  
Your users report that a simple query with `GROUP BY country` in BigQuery is running very slowly. The table is large, and the query plan shows imbalance in stage execution. What is the most likely cause of the delay?

**Answer:**  
  The **slowdown** is caused by **<mark>data skew</mark>** — most rows in the table have the **<mark>same value</mark>** in the `country` column, leading to **<mark>uneven slot usage</mark>** and slow aggregation.

**Explanation:**  
- In distributed systems like BigQuery, `GROUP BY` requires data to be **<mark>shuffled by key</mark>**.  
- If one key (e.g., `"US"`) dominates, a **<mark>single reducer node</mark>** gets overloaded.  
- <mark>Best Practice:</mark>  
  - Pre-aggregate or bucket the data.  
  - Use **<mark>approximate aggregate functions</mark>** (like `APPROX_TOP_COUNT`) when exact results are not critical.  
  - Consider **<mark>clustering/partitioning</mark>** strategies to distribute load more evenly.  

#### Q56: Legacy SQL over sharded tables — use `TABLE_DATE_RANGE`

Question:  
Your Firebase Analytics integration automatically creates daily tables in BigQuery (e.g., `app_events_20240815`, `app_events_20240816`). You need to query across the past 30 days using Legacy SQL. What function should you use?

- Answer:  
  Use the <mark>`TABLE_DATE_RANGE`</mark> function in <mark>Legacy SQL</mark>.  
  Example:  

```sql
  SELECT event_name, COUNT(*)
  FROM TABLE_DATE_RANGE([mydataset.app_events_],
                        TIMESTAMP("2024-08-01"),
                        TIMESTAMP("2024-08-30"))
  GROUP BY event_name;
```

**Explanation (English):**

* Legacy SQL requires <mark>`TABLE_DATE_RANGE`</mark> to scan <mark>date-suffixed sharded tables</mark>.
* Modern <mark>Standard SQL</mark> supports wildcards with <mark>`_TABLE_SUFFIX`</mark>, which is recommended.
* <mark>Best Practice:</mark>

  * For new pipelines, avoid table sharding — use a <mark>single partitioned table</mark>.
  * Partitioned tables are easier to query and scale better.


#### Q10: Restrict access in BigQuery (IAM roles, dataset isolation)

Question:  
Your company is in a highly regulated industry. One requirement is to ensure individual users have access only to the minimum amount of information required to do their jobs. How should you enforce this requirement in BigQuery? (Choose three)

* **Answer:**  
  <mark>Restrict access by role (IAM)</mark>,  
  <mark>Restrict dataset access to approved users</mark>,  
  <mark>Segregate data across multiple datasets/tables</mark>.

**Explanation (English):**

* BigQuery uses <mark>IAM roles</mark> to control access.  
* Best practice is the <mark>least privilege principle</mark>:  
  * Grant only the roles needed (e.g., <mark>`roles/bigquery.dataViewer`</mark>).  
  * Assign access at <mark>dataset or table level</mark>, not project-wide.  
  * Separate <mark>sensitive data</mark> into different datasets/tables to limit visibility.  
* Extra: <mark>Encryption</mark> and <mark>audit logs</mark> help compliance, but do not enforce row/column-level restrictions.


#### Q15: Consistency in BigQuery Streaming Inserts

**Question:**
Your application streams data into BigQuery, and analysts complain that some records appear missing when querying right after insertion. How should you handle this?

* **Answer:**
  <mark>**Wait twice the average streaming latency before querying.**</mark>

  * Streaming inserts are **eventually consistent**.
  * Queries executed immediately after insertion may not see all rows.
  * Waiting allows BigQuery to fully commit the records.

#### Q213: Dashboard Performance with Filters

**Question:**
Your company's `customer_order` table in BigQuery stores 10 PB of order history for 10 million customers. A dashboard allows support staff to filter by `country_name` and `username`. Queries are slow when applying filters. How should you redesign the table?

* **Answer:**
  <mark>**Cluster the table by `country_name` and `username`.**</mark>

  * Clustering organizes rows by frequently filtered fields, reducing scanned data.
  * Partitioning is not ideal here because `country_name` and `username` have high cardinality.
  * Clustering improves query performance while keeping costs lower.

#### Q239: Concurrency Issues with BigQuery Slots

**Question:**
Your analyst team runs ad hoc queries and scheduled pipelines in BigQuery. With the recent addition of hundreds of non-time-sensitive SQL pipelines, users encounter frequent quota errors. About 1500 queries run concurrently during peak times. How should you resolve the concurrency issue?

* **Answer:**
  **Update SQL pipelines to run as <mark>batch queries</mark>, and run <mark>ad-hoc</mark> queries as <mark>interactive jobs</mark>.**

  * Batch queries queue for execution and reduce contention.
  * Interactive queries remain available for urgent user needs.
  * This balances concurrency without increasing slot reservations.

#### Q233: Troubleshooting BigQuery Slot Contention

**Question:**
You suspect query slowness in BigQuery is due to job queuing or slot contention. How can you identify where the performance issue occurs?

* **Answer:**
  **Query the <mark>INFORMATION\_SCHEMA</mark> and use <mark>admin resource charts</mark>.**

  * Run queries against `INFORMATION_SCHEMA.JOBS` to review job performance and slot usage.
  * Combine with BigQuery admin charts to visualize slot allocation and job queuing.
  * This helps diagnose contention and optimize workload management.

**Knowledge :** When queries slow down, it may be due to slot contention. To diagnose:

- Query INFORMATION\_SCHEMA.JOBS for metrics like total\_slot_ms, creation\_time, end\_time.
- Check Admin Resource Charts in the BigQuery console for slot usage and queuing trends.

#### Q248: Filtering rows with views / materialized views in BigQuery

Question:
You have an inventory of VM data stored in a BigQuery table. You want to prepare the data for regular reporting in the most cost-effective way. You need to exclude VM rows with fewer than 8 vCPU in your report.

Answer:
Use a <mark>**view**</mark> with a filter to drop rows with fewer than 8 vCPUs.

* <mark>**View**</mark>: Good for lightweight, frequently changing queries. No storage cost, just logic.
* <mark>**Materialized view**</mark>: Better for pre-aggregated, stable queries where performance matters. Has extra storage cost but gives faster query results.
* In this case, <mark>**a simple view**</mark> is the most cost-effective solution.

---

#### Q252: Designing Customer–Product–Subscription Model in BigQuery

Question:
You are designing a data warehouse in BigQuery to analyze sales data for a telecommunication service provider. You need to create a data model for customers, products, and subscriptions. All customers, products, and subscriptions can be updated monthly, but you must maintain a historical record of all data. You plan to use the visualization layer for current and historical reporting. You need to ensure that the data model is simple, easy-to-use, and cost-effective.

Answer:
Use a <mark>**denormalized**</mark>, <mark>**append-only**</mark> model with <mark>**nested and repeated fields**</mark>, and include an <mark>**ingestion timestamp**</mark> to track historical data.

1. <mark>**Denormalized**</mark>: Put customers, products, and subscriptions together in one table to reduce joins.
2. <mark>**Append-only**</mark>: Insert new rows instead of overwriting old ones, to maintain history.
3. <mark>**Nested/repeated fields**</mark>: Capture multiple subscriptions per customer efficiently.
4. <mark>**Ingestion timestamp**</mark>: Track both current and historical states for reporting.

**Example Schema**

```sql
-- One denormalized table: customer_product_subscription
CREATE OR REPLACE TABLE telco.sales_data AS
SELECT
  customer_id,
  customer_name,
  ARRAY<STRUCT<
    product_id STRING,
    product_name STRING,
    subscriptions ARRAY<STRUCT<
      subscription_id STRING,
      start_date DATE,
      end_date DATE,
      status STRING
    >>
  >> AS products,
  ingestion_ts TIMESTAMP
FROM UNNEST([
  STRUCT(
    "C001" AS customer_id,
    "Alice" AS customer_name,
    [
      STRUCT("P100", "Mobile Plan", [
        STRUCT("S1001", DATE "2024-01-01", DATE "2024-12-31", "Active"),
        STRUCT("S1002", DATE "2025-01-01", NULL, "Active")
      ]),
      STRUCT("P200", "Internet", [
        STRUCT("S2001", DATE "2023-06-01", DATE "2024-05-31", "Expired")
      ])
    ] AS products,
    CURRENT_TIMESTAMP() AS ingestion_ts
  )
]);
```


**Example Queries**

**1. Count current active subscriptions**

```sql
SELECT
  customer_id,
  customer_name,
  COUNTIF(sub.status = "Active") AS active_subscriptions
FROM telco.sales_data, UNNEST(products) p, UNNEST(p.subscriptions) sub
WHERE sub.end_date IS NULL OR sub.end_date > CURRENT_DATE()
GROUP BY customer_id, customer_name;
```

**2. Retrieve historical records by ingestion timestamp**

```sql
SELECT
  customer_id,
  p.product_name,
  sub.subscription_id,
  sub.start_date,
  sub.end_date,
  ingestion_ts
FROM telco.sales_data, UNNEST(products) p, UNNEST(p.subscriptions) sub
WHERE customer_id = "C001"
ORDER BY ingestion_ts DESC;
```

### F) Integration & BI (Looker Studio / Tools)

#### Q4: Disable caching in Data Studio report (data missing for <1h)

Question:  
You create an important report for your large team in Google Data Studio (Looker Studio). The report uses **BigQuery** as its data source. You notice that visualizations are not showing data that is **less than 1 hour old**. What should you do?

- **Answer:**  
  Disable caching by editing the **report settings** in Data Studio.  

**Explanation (English):**  
- Data Studio caches query results for up to **1 hour** by default.  
- This cache helps reduce **query cost** and improve **dashboard performance**.  
- But it also means **fresh data** (e.g., streaming inserts, recent loads) won’t appear until cache expires.  
- Solution: turn off caching or lower the cache refresh interval in **report settings**.  
- ⚠️ Trade-off: disabling cache may **increase BigQuery costs** and make dashboards slower.  

  

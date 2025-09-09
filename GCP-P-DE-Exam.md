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

* **Answer:**

  * <mark>Partitioning</mark> reduces the amount of data scanned by filtering on partition keys (e.g., date).
  * <mark>Clustering</mark> organizes data inside partitions based on specified columns, improving filtering and sorting.
  * <mark>Best Practice:</mark> Combine both. Example: Partition by `order_date` and cluster by `user_id`. This minimizes scanned data and speeds up queries.

---

#### Q8: Deduplication with ROW\_NUMBER window function

**Question:**
You are building a new real-time data warehouse using <mark>BigQuery streaming inserts</mark>. Since there’s no guarantee that data will only be sent once, but you do have a <mark>unique ID</mark> for each row and an <mark>event timestamp</mark>, you want to ensure that <mark>duplicates</mark> are not included when querying. Which query type should you use?

* **Answer:**
  Use the <mark>ROW\_NUMBER</mark> window function with `PARTITION BY unique_id` and filter on `row_number = 1`.

**Explanation:**

* Streaming inserts may produce <mark>duplicate rows</mark>.
* To deduplicate:

  * Partition by <mark>unique ID</mark>.
  * Order by <mark>event timestamp</mark>.
  * Select only the <mark>first row</mark>.

```sql
SELECT *
FROM (
  SELECT *, ROW_NUMBER() OVER(PARTITION BY unique_id ORDER BY event_ts DESC) AS rn
  FROM mytable
)
WHERE rn = 1;
```

---

#### Q9: Wildcard Tables in BigQuery

**Question:**
You need to query across multiple tables in BigQuery whose names share a prefix (e.g., `gsod*`). Which query syntax should you use?

* **Answer:**
  Use <mark>wildcards</mark> in the table name with <mark>backticks</mark>.

```sql
SELECT * 
FROM `bigquery-public-data.noaa_gsod.gsod*`
WHERE _TABLE_SUFFIX BETWEEN '2010' AND '2012';
```

**Explanation:**

* <mark>`_TABLE_SUFFIX`</mark> pseudo-column lets you filter specific tables.
* <mark>Best Practice:</mark> Prefer <mark>partitioned tables</mark> instead of sharded ones when designing new pipelines.

---

#### Q53: Slow GROUP BY due to data skew

**Question:**
Your users report that a simple query with `GROUP BY country` in BigQuery is running very slowly. The table is large, and the query plan shows imbalance in stage execution. What is the most likely cause?

* **Answer:**
  The slowdown is caused by <mark>data skew</mark> — most rows in the table have the <mark>same value</mark> in the `country` column, leading to <mark>uneven slot usage</mark>.

**Explanation:**

* BigQuery distributes data by <mark>shuffling keys</mark>.
* If one key dominates (e.g., `"US"`), a <mark>single reducer</mark> gets overloaded.
* <mark>Best Practice:</mark>

  * Pre-aggregate or bucket data.
  * Use <mark>approximate functions</mark> like `APPROX_TOP_COUNT`.
  * Apply <mark>clustering/partitioning</mark> to balance load.

---

#### Q56: Legacy SQL over sharded tables — use `TABLE_DATE_RANGE`

**Question:**
Your Firebase Analytics integration automatically creates daily tables (e.g., `app_events_20240815`). You need to query across the past 30 days in Legacy SQL. What function should you use?

* **Answer:**
  Use the <mark>`TABLE_DATE_RANGE`</mark> function in <mark>Legacy SQL</mark>.

```sql
SELECT event_name, COUNT(*)
FROM TABLE_DATE_RANGE([mydataset.app_events_],
                      TIMESTAMP("2024-08-01"),
                      TIMESTAMP("2024-08-30"))
GROUP BY event_name;
```

**Explanation:**

* Legacy SQL requires <mark>`TABLE_DATE_RANGE`</mark>.
* Standard SQL supports <mark>wildcards</mark> with <mark>`_TABLE_SUFFIX`</mark>.
* <mark>Best Practice:</mark> Use <mark>partitioned tables</mark> instead of sharding.

---

### B) Ingestion, Freshness & Consistency

#### Q15: Consistency in BigQuery Streaming Inserts

**Question:**
Your application streams data into BigQuery, and analysts complain that some records appear missing when querying right after insertion. How should you handle this?

* **Answer:** <mark>Wait twice the average streaming latency before querying</mark>.

**Explanation:**

* Streaming inserts are <mark>eventually consistent</mark>.
* Queries executed too early may not return all rows.
* Wait a short buffer time for data to fully commit.

---

#### Q24: Convert STRING to TIMESTAMP with new table

**Question:**
You have a table where `event_time` is stored as a <mark>STRING</mark>. Analysts need it as a <mark>TIMESTAMP</mark>. How should you provide it without affecting the raw table?

* **Answer:**
  Create a <mark>new table</mark> with `CAST(event_time AS TIMESTAMP)`.

```sql
CREATE OR REPLACE TABLE mydataset.cleaned_events AS
SELECT
  event_id,
  CAST(event_time AS TIMESTAMP) AS event_ts
FROM mydataset.raw_events;
```

**Explanation:**

* Keeps <mark>raw data</mark> intact.
* Provides analysts with <mark>cleaned schema</mark>.
* <mark>Best Practice:</mark> Always separate raw and transformed data layers.

---

#### Q48: CSV import mismatch — fix file encoding

**Question:**
Your CSV import into BigQuery succeeded, but the imported data does not match the source file byte-to-byte. What is the most likely cause?

* **Answer:**
  BigQuery <mark>defaults to UTF-8 encoding</mark>. If the source file uses another encoding, mismatches occur.

**Explanation:**

* Always ensure <mark>CSV file encoding = UTF-8</mark>.
* If not, convert the file before loading.
* <mark>Best Practice:</mark> Standardize file encoding across pipelines.

---

### C) Governance & Access Control

#### Q10: Restrict access in BigQuery (IAM roles, dataset isolation)

**Question:**
Your company is in a highly regulated industry. One requirement is to ensure users have access only to the <mark>minimum information</mark> needed. How should you enforce this in BigQuery? (Choose three)

* **Answer:**

  * <mark>Restrict access by IAM role</mark>
  * <mark>Restrict dataset access</mark>
  * <mark>Segregate data across datasets/tables</mark>

**Explanation:**

* BigQuery uses <mark>IAM roles</mark> for access control.
* <mark>Least privilege principle</mark>:

  * Assign <mark>dataset/table-level</mark> roles, not project-wide.
  * Separate <mark>sensitive data</mark> into dedicated datasets.
* <mark>Audit logs</mark> and <mark>encryption</mark> add compliance but do not enforce row/column-level access.

---

#### Q40: Enforce regional access — dataset-per-region + IAM

**Question:**
You created regional tables for a company policy where employees should only access data for their own region. How do you enforce this?

* **Answer:**

  * Store tables in <mark>separate datasets per region</mark>.
  * Grant <mark>IAM access</mark> only to the relevant dataset.

**Explanation:**

* <mark>Dataset-level IAM</mark> is easier to maintain than table-level rules.
* Avoid duplicating tables into one dataset with complex filters.
* <mark>Best Practice:</mark> use <mark>dataset-per-region</mark> for clear boundaries.

---

### D) Admin, Performance & Workload Mgmt

#### Q233: Troubleshooting BigQuery slot contention

**Question:**
You suspect BigQuery query slowness is due to <mark>slot contention</mark>. How can you confirm?

* **Answer:**

  * Query <mark>INFORMATION\_SCHEMA.JOBS</mark>
  * Use <mark>BigQuery admin resource charts</mark>

**Explanation:**

* INFORMATION\_SCHEMA shows <mark>job queuing and slot usage</mark>.
* Admin charts visualize <mark>slot allocation</mark>.
* Together, they help identify contention.

---

#### Q239: Concurrency issues with BigQuery slots

**Question:**
Your analysts run ad hoc queries, and you have 1500 scheduled jobs at peak, causing <mark>quota errors</mark>. How do you resolve concurrency?

* **Answer:**

  * Run pipelines as <mark>batch queries</mark>.
  * Keep ad hoc as <mark>interactive queries</mark>.

**Explanation:**

* Batch jobs queue until slots free up, reducing pressure.
* Interactive queries remain responsive.
* <mark>Best Practice:</mark> Reserve slots only if workloads are predictable.

---

### E) Data Modeling & Table Design

#### Q60: Replace sharded tables with one partitioned table

**Question:**
You have 3 years of daily log tables (e.g., `LOGS_20210101`). Queries fail when scanning >1000 tables. How do you fix this?

* **Answer:**
  Convert to a <mark>partitioned table</mark>.

**Explanation:**

* Partitioned tables scale better and avoid query limits.
* Easier to manage retention policies.
* <mark>Best Practice:</mark> Never use sharded tables for long-term pipelines.

---

#### Q252: Designing customer–product–subscription model

（已经写在上面，不重复）

---

### F) Integration & BI (Looker Studio / Tools)

#### Q4: Disable caching in Data Studio report (data missing for <1h)

（已写，不重复）

---

#### Q25: Stackdriver Logging + advanced filter for BQ insert jobs

**Question:**
Your team suspects some BigQuery insert jobs are failing. How can you identify the failed jobs?

* **Answer:**
  Use <mark>Stackdriver (Cloud Logging)</mark> with <mark>advanced filters</mark>.

**Explanation:**

* Search `resource.type="bigquery_resource"` and `protoPayload.methodName="jobservice.insert"` in logs.
* Filter by <mark>status.errorResult</mark> to find failures.
* <mark>Best Practice:</mark> Always set up log-based alerts for job failures.

---

#### Q36: Use a view to simplify columns for BI and cut query cost

**Question:**
Your BI team struggles with too many columns in a large table and high query costs. What should you do?

* **Answer:**
  Create a <mark>view</mark> exposing only the needed columns.

**Explanation:**

* Views reduce <mark>query cost</mark> by limiting scanned columns.
* BI users see a <mark>simplified schema</mark>.
* <mark>Best Practice:</mark> Provide curated views for business users.

---

#### Q39: Data Studio on BigQuery — build filtered, fast reports

**Question:**
You need to create dashboards in Data Studio on BigQuery with <mark>fast performance</mark>. What design should you use?

* **Answer:**

  * Pre-filter and aggregate data in <mark>BigQuery views</mark>.
  * Use <mark>clustering</mark> or <mark>materialized views</mark> if queries repeat.

**Explanation:**

* Avoid exposing raw wide tables to BI tools.
* Reduce <mark>data scanned</mark> before visualization.
* <mark>Best Practice:</mark> Build a BI-friendly semantic layer.

---

#### Q43: Expose `FullName` via a BigQuery view

**Question:**
You need a `FullName` field (`FirstName + LastName`) in a `Users` table. How do you provide it without altering the schema?

* **Answer:**
  Create a <mark>view</mark> that concatenates the fields.

```sql
CREATE OR REPLACE VIEW mydataset.v_users AS
SELECT
  FirstName,
  LastName,
  CONCAT(FirstName, " ", LastName) AS FullName
FROM mydataset.users;
```

**Explanation:**

* Keeps <mark>raw table</mark> unchanged.
* Avoids <mark>storage cost</mark> of duplicating data.
* <mark>Best Practice:</mark> Use views for derived fields.

---

#### Q46: Keep frequently updated reference data via BigQuery external table

**Question:**
You have a dataset of prices updated every 30 minutes. How should you expose it to BigQuery for cheap queries?

* **Answer:**
  Store it in <mark>Cloud Storage</mark> and use a <mark>federated external table</mark>.

**Explanation:**

* Avoid frequent re-loads into BigQuery.
* External table reflects updates directly.
* <mark>Best Practice:</mark> Use for small, frequently refreshed reference data.

---

#### Q55: ODBC access — use Standard SQL view + service account

**Question:**
Your team will connect to BigQuery via ODBC, but your current view is in <mark>Legacy SQL</mark>. How do you ensure compatibility?

* **Answer:**

  * Create a <mark>Standard SQL view</mark>
  * Use a <mark>service account</mark> for ODBC authentication

**Explanation:**

* ODBC requires <mark>Standard SQL</mark> syntax.
* Service accounts provide <mark>secure, controlled access</mark>.

---

### G) Views & Materialized Views

#### Q248: Filtering rows with views vs materialized views

（已写，不重复）


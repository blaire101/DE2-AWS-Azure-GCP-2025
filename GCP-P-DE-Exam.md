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

<div align="center">
  <img src="docs/GCP-BigQuery-2.png" alt="Diagram" width="900">
</div>

**BigQuery Table Types**

<div align="center">
  <img src="docs/GCP-BigQuery-Table-Types.png" alt="Diagram" width="800">
</div>

### A) Query Patterns & SQL Features 

* [Q5: Partitioning vs Clustering ✅](#q5-partitioning-vs-clustering)
* [Q8: Deduplication with ROW\_NUMBER window function ✅](#q8-deduplication-with-row_number-window-function)
* [Q9: Wildcard Tables ✅](#q9-wildcard-tables)
* [Q53: Slow GROUP BY due to data skew ✅](#q53-slow-group-by-due-to-data-skew)
* [Q56: Legacy SQL over sharded tables — use `TABLE_DATE_RANGE` ✅](#q56-legacy-sql-over-sharded-tables--use-table_date_range)

### B) Ingestion, Freshness & Consistency

* [Q15: Streaming inserts are eventually consistent (wait before query) ✅](#q15-streaming-inserts-are-eventually-consistent-wait-before-query)
* [Q24: Convert STRING to TIMESTAMP with new table ✅](#q24-convert-string-to-timestamp-with-new-table)
* [Q48: CSV import mismatch — fix file encoding (BigQuery defaults to UTF-8) ✅](#q48-csv-import-mismatch--fix-file-encoding-bigquery-defaults-to-utf-8)

### C) Governance & Access Control

* [Q10: Restrict access in BigQuery (IAM roles, dataset isolation) ✅](#q10-restrict-access-in-bigquery-iam-roles-dataset-isolation)
* [Q40: Enforce regional access — dataset-per-region + IAM on datasets ✅](#q40-enforce-regional-access--dataset-per-region--iam-on-datasets)

### D) Admin, Performance & Workload Mgmt

* [Q233: Troubleshooting BigQuery slot contention ✅](#q233-troubleshooting-bigquery-slot-contention)
* [Q239: Concurrency issues with slots ✅](#q239-concurrency-issues-with-slots)

### E) Data Modeling & Table Design

* [Q60: Replace sharded tables with one partitioned table ✅](#q60-replace-sharded-tables-with-one-partitioned-table)
* [Q252: Designing customer–product–subscription model ✅](#q252-designing-customerproductsubscription-model)

### F) Integration & BI (Looker Studio / Tools)

* [Q4: Disable caching in Data Studio report (data missing for <1h) ✅](#q4-disable-caching-in-data-studio-report-data-missing-for-1h)
* [Q25: Stackdriver Logging + advanced filter for BQ insert jobs ✅](#q25-stackdriver-logging--advanced-filter-for-bq-insert-jobs)
* [Q36: Use a view to simplify columns for BI and cut query cost ✅](#q36-use-a-view-to-simplify-columns-for-bi-and-cut-query-cost)
* [Q39: Data Studio on BigQuery — build filtered, fast reports ✅](#q39-data-studio-on-bigquery--build-filtered-fast-reports)
* [Q43: Expose `FullName` via a BigQuery view (avoid reshaping data) ✅](#q43-expose-fullname-via-a-bigquery-view-avoid-reshaping-data)
* [Q46: Keep frequently updated reference data via BigQuery external table (GCS) ✅](#q46-keep-frequently-updated-reference-data-via-bigquery-external-table-gcs)
* [Q55: ODBC access — use Standard SQL view + service account ✅](#q55-odbc-access--use-standard-sql-view--service-account)

### G) Views & Materialized Views

* [Q248: Filtering rows with views vs materialized views ✅](#q248-filtering-rows-with-views-vs-materialized-views)


## 3. Cost & Security
- [Q11: Pricing Models ✅](#q11-pricing-models)
- [Q12: Cost-Saving Techniques ✅](#q12-cost-saving-techniques)
- [Q13: Security in BigQuery ✅](#q13-security-in-bigquery)
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


## 6. Dataplex / Data Mesh / Governance
- [Q16: Securing BigQuery with Audit Logs](#q16-securing-bigquery-with-audit-logs)
- [Q210: Dataplex Design for Data Products](#q210-dataplex-design-for-data-products)
- [Q217: Secure BigQuery Sharing with Policy Tags](#q217-secure-bigquery-sharing-with-policy-tags)
- [Q240: Dataplex Permissions](#q240-dataplex-permissions)
- [Q244: Analytics Hub Sharing](#q244-analytics-hub-sharing)
- [Q247: Data Mesh with Dataplex](#q247-data-mesh-with-dataplex)

## 7. Pub/Sub & Messaging
- [Q20: Duplicate Messages](#q20-duplicate-messages)
- [Q224: Dataflow Lag in Pub/Sub](#q224-dataflow-lag-in-pubsub)
- [Q228: Reprocessing Pub/Sub Messages](#q228-reprocessing-pubsub-messages)

---

## 8. Cloud SQL / Spanner / Databases
- [Q3: Scaling Patient Records](#q3-scaling-patient-records)
- [Q6: Weather App DB Failure Handling](#q6-weather-app-db-failure-handling)
- [Q197: ACID-Compliant Database](#q197-acid-compliant-database)
- [Q218: Cloud SQL Disaster Recovery](#q218-cloud-sql-disaster-recovery)
- [Q236: HA Cloud SQL Multi-Region](#q236-ha-cloud-sql-multi-region)


## 9. Cloud Storage & Data Lake
- [Q17: Migrating Hadoop Jobs to Cloud Dataproc with GCS Connector](#q17-migrating-hadoop-jobs-to-cloud-dataproc-with-gcs-connector)
- [Q19: Storage Costs with Dataproc](#q19-storage-costs-with-dataproc)
- [Q241: Cloud Storage RPO Design](#q241-cloud-storage-rpo-design)
- [Q249: Cost Optimization for Raw Data](#q249-cost-optimization-for-raw-data)
- [Q251: Retention Policy Lock](#q251-retention-policy-lock)
- [Q257: Autoclass for Data Lake](#q257-autoclass-for-data-lake)

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

**Answer:**

  * <mark>Partitioning</mark> reduces the amount of data scanned by filtering on partition keys (e.g., date).
  * <mark>Clustering</mark> organizes data inside partitions based on specified columns, improving filtering and sorting.
  * <mark>Best Practice:</mark> Combine both. Example: Partition by `order_date` and cluster by `user_id`. This minimizes scanned data and speeds up queries.

---

#### Q8: Deduplication with ROW\_NUMBER window function

**Question:**
You are building a new real-time data warehouse using <mark>BigQuery streaming inserts</mark>. Since there’s no guarantee that data will only be sent once, but you do have a <mark>unique ID</mark> for each row and an <mark>event timestamp</mark>, you want to ensure that <mark>duplicates</mark> are not included when querying. Which query type should you use?

**Answer:**
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

**Answer:**
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

**Answer:**
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

**Answer:**
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

**Answer:** <mark>Wait twice the average streaming latency before querying</mark>.

**Explanation:**

* Streaming inserts are <mark>eventually consistent</mark>.
* Queries executed too early may not return all rows.
* Wait a short buffer time for data to fully commit.


#### Q24: Convert STRING to TIMESTAMP with new table

**Question:**
You have a table where `event_time` is stored as a <mark>STRING</mark>. Analysts need it as a <mark>TIMESTAMP</mark>. How should you provide it without affecting the raw table?

**Answer:**
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

**Answer:**
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

**Answer:**

  * <mark>Restrict access by IAM role</mark>
  * <mark>Restrict dataset access</mark>
  * <mark>Segregate data across datasets/tables</mark>

**Explanation:**

* BigQuery uses <mark>IAM roles</mark> for access control.
* <mark>Least privilege principle</mark>:
  * Assign <mark>dataset/table-level</mark> roles, not project-wide.
  * Separate <mark>sensitive data</mark> into dedicated datasets.
* <mark>Audit logs</mark> and <mark>encryption</mark> add compliance but do not enforce row/column-level access.


#### Q40: Enforce regional access — dataset-per-region + IAM

**Question:**
You created regional tables for a company policy where employees should only access data for their own region. How do you enforce this?

**Answer:**

  * Store tables in <mark>separate datasets per region</mark>.
  * Grant <mark>IAM access</mark> only to the relevant dataset.

**Explanation:**

* <mark>Dataset-level IAM</mark> is easier to maintain than table-level rules.
* Avoid duplicating tables into one dataset with complex filters.
* <mark>Best Practice:</mark> use <mark>dataset-per-region</mark> for clear boundaries.


### D) Admin, Performance & Workload Mgmt

#### Q233: Troubleshooting BigQuery slot contention

**Question:**
You suspect BigQuery query slowness is due to <mark>slot contention</mark>. How can you confirm?

**Answer:**

  * Query <mark>INFORMATION\_SCHEMA.JOBS</mark>
  * Use <mark>BigQuery admin resource charts</mark>

**Explanation:**

* INFORMATION\_SCHEMA shows <mark>job queuing and slot usage</mark>.
* Admin charts visualize <mark>slot allocation</mark>.
* Together, they help identify contention.


#### Q239: Concurrency issues with BigQuery slots

**Question:**
Your analysts run ad hoc queries, and you have 1500 scheduled jobs at peak, causing <mark>quota errors</mark>. How do you resolve concurrency?

**Answer:**

  * Run pipelines as <mark>batch queries</mark>.
  * Keep ad hoc as <mark>interactive queries</mark>.

**Explanation:**

* Batch jobs queue until slots free up, reducing pressure.
* Interactive queries remain responsive.
* <mark>Best Practice:</mark> Reserve slots only if workloads are predictable.


### E) Data Modeling & Table Design

#### Q60: Replace sharded tables with one partitioned table

**Question:**
You have 3 years of daily log tables (e.g., `LOGS_20210101`). Queries fail when scanning >1000 tables. How do you fix this?

**Answer:**
  Convert to a <mark>partitioned table</mark>.

**Explanation:**

* Partitioned tables scale better and avoid query limits.
* Easier to manage retention policies.
* <mark>Best Practice:</mark> Never use sharded tables for long-term pipelines.

---

#### Q252: Designing customer–product–subscription model

**Question:**  
You are designing a data warehouse in BigQuery to analyze sales data for a **telecommunication service provider**.  
You need to create a model for **customers, products, and subscriptions**.  
All entities can be **updated monthly**, but you must **maintain historical records**.  
The visualization layer must support **current and historical reporting**, and the model should be **simple, easy-to-use, and cost-effective**.  

**Answer:**  
  Use a <mark>denormalized</mark>, <mark>append-only</mark> model with <mark>nested and repeated fields</mark>, and include an <mark>ingestion timestamp</mark> to track historical data.  

**Explanation:**  

* **Denormalized**: Put customers, products, and subscriptions together in one table to reduce joins.  
* **Append-only**: Insert new rows instead of overwriting old ones, to preserve history.  
* **Nested/repeated fields**: Capture multiple subscriptions per customer efficiently.  
* **Ingestion timestamp**: Enables both point-in-time and current-state reporting.  

<mark>Best Practice:</mark> In BigQuery, prefer **wide denormalized tables** with nested fields for performance and cost efficiency, instead of complex star schemas.  

**Example Query — Count Active Subscriptions**

```sql
SELECT
  customer_id,
  customer_name,
  COUNTIF(sub.status = "Active") AS active_subscriptions
FROM telco.sales_data,
     UNNEST(products) AS p,
     UNNEST(p.subscriptions) AS sub
WHERE sub.end_date IS NULL OR sub.end_date > CURRENT_DATE()
GROUP BY customer_id, customer_name;
```

👉 This query uses **`UNNEST`** to flatten nested arrays (`products` and `subscriptions`),
then filters by `status = "Active"` and `end_date` to count current active subscriptions per customer.



### F) Integration & BI (Looker Studio / Tools)

#### Q4: Disable caching in Data Studio report (data missing for <1h)

**Question:**  
You create an important report for your large team in **Google Data Studio (Looker Studio)**.  
The report uses **BigQuery** as its data source.  

You notice that visualizations are not showing data that is **less than 1 hour old**.  
What should you do?

**Answer:**  
  <mark>Disable caching</mark> by editing the **report settings** in Data Studio.


#### Q25: Stackdriver Logging + advanced filter for BQ insert jobs

**Question:**
Your team suspects some BigQuery insert jobs are failing. How can you identify the failed jobs?

**Answer:**
  Use <mark>Stackdriver (Cloud Logging)</mark> with <mark>advanced filters</mark>.

<div align="center">
  <img src="docs/GCP-Stackdriver.webp" alt="Diagram" width="600">
</div>

**Explanation:**

* Search `resource.type="bigquery_resource"` and `protoPayload.methodName="jobservice.insert"` in logs.
* Filter by <mark>status.errorResult</mark> to find failures.
* <mark>Best Practice:</mark> Always set up log-based alerts for job failures.

---

#### Q36: Use a view to simplify columns for BI and cut query cost

**Question:**
Your BI team struggles with too many columns in a large table and high query costs. What should you do?

**Answer:**
  Create a <mark>view</mark> exposing only the needed columns.

<div align="center">
  <img src="docs/GCP-View-BI-Tool.png" alt="Diagram" width="400">
</div>

**Explanation:**

* Views reduce <mark>query cost</mark> by limiting scanned columns.
* BI users see a <mark>simplified schema</mark>.
* <mark>Best Practice:</mark> Provide curated views for business users.


```sql
CREATE VIEW sales_summary AS
SELECT
  order_id,
  customer_id,
  total_amount,
  order_date
FROM raw_sales_table;
```

---

#### Q39: Data Studio on BigQuery — build filtered, fast reports

**Question:**
You need to create dashboards in Data Studio on BigQuery with <mark>fast performance</mark>. What design should you use?

**Answer:**

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

**Answer:**
  Create a <mark>view</mark> that concatenates the fields.

<div align="center">
  <img src="docs/GCP-materialized_views.jpg" alt="Diagram" width="800">
</div>

```sql
CREATE MATERIALIZED VIEW mydataset.v_users AS
SELECT
  FirstName,
  LastName,
  CONCAT(FirstName, " ", LastName) AS FullName
FROM mydataset.users
WHERE status = 'ACTIVE';
```

**Explanation:**

* Keeps <mark>raw table</mark> unchanged.
* Avoids <mark>storage cost</mark> of duplicating data.
* <mark>Best Practice:</mark> Use views for derived fields.


#### Q46: Keep frequently updated reference data via BigQuery external table

**Question:**
You have a dataset of prices updated every 30 minutes. How should you expose it to BigQuery for cheap queries?

<div align="center">
  <img src="docs/GCP-external-table.png" alt="Diagram" width="700">
</div>

**Answer:**
  Store it in <mark>Cloud Storage</mark> and use a <mark>federated external table</mark>.

**Explanation:**

* Avoid frequent re-loads into BigQuery.
* External table reflects updates directly.
* <mark>Best Practice:</mark> Use for small, frequently refreshed reference data.

---

#### Q55: ODBC access — use Standard SQL view + service account

**Question:**
Your team will connect to BigQuery via ODBC, but your current view is in <mark>Legacy SQL</mark>. How do you ensure compatibility?

**Answer:**

  * Create a <mark>Standard SQL view</mark>
  * Use a <mark>service account</mark> for ODBC authentication

**Explanation:**

* ODBC requires <mark>Standard SQL</mark> syntax.
* Legacy SQL → Standard SQL: Resolves compatibility issues.
* Service accounts provide <mark>secure, controlled access</mark>.

---

### G) Views & Materialized Views

#### Q248: Filtering rows with views vs materialized views

**Question:**  
You have an inventory of VM data stored in the BigQuery table `dataset.inventory_vm`.  
You need to prepare the data for **regular reporting** in the most **cost-effective** way.  
You want to **exclude VM rows with fewer than 8 vCPU** in your report. What should you do?

Options:  
<mark>A. Create a **view** with a filter to drop rows with fewer than 8 vCPU, and use the **UNNEST** operator.</mark>  
B. Create a **materialized view** with a filter to drop rows with fewer than 8 vCPU, and use a WITH CTE.  
C. Create a **view** with a filter to drop rows with fewer than 8 vCPU, and use a WITH CTE.  
D. Use **Dataflow** to batch process and write the result to another BigQuery table.  

**Correct Answer:**  
A. Create a <mark>view</mark> with a filter to drop rows with fewer than 8 vCPU, and use the <mark>UNNEST</mark> operator.  


**Explanation:**

* The `vcpu` information is stored in a **nested field** (inside `components` column).  
* You must use <mark>`UNNEST`</mark> to flatten the array before filtering.  
* <mark>View</mark>:
  * Zero storage cost.  
  * Always up-to-date with the base table.  
  * Perfect for reporting filters.  

* <mark>Materialized View</mark>:  
  * Adds storage cost.  
  * Useful for **pre-aggregations**, not simple filters.  

* <mark>Dataflow</mark>:  
  * Too complex and expensive for this use case.  

**View Definition:**

```sql
CREATE OR REPLACE VIEW dataset.v_inventory_vm AS
SELECT vm_id, c.vcpu
FROM dataset.inventory_vm,
     UNNEST(components) AS c
WHERE c.component = "cpu"
  AND c.vcpu >= 8;
```

## 3. Cost & Security

- [Q11: Pricing Models](#q11-pricing-models)
- [Q12: Cost-Saving Techniques](#q12-cost-saving-techniques)
- [Q13: Security in BigQuery](#q13-security-in-bigquery)
- [Q200: PII Protection](#q200-pii-protection)
- [Q215: CMEK Sharing](#q215-cmek-sharing)
- [Q238: Per-User Crypto-Deletion](#q238-per-user-crypto-deletion)

#### Q11: Basket Abandonment System with Dataflow

**Question:**  
You are designing a basket abandonment system for an e-commerce company. The rules are:  
* No interaction by the user for **1 hour**  
* Basket value > **$30**  
* No completed transaction  

You use **Google Cloud Dataflow** to process the data and decide if a message should be sent. How should you design the pipeline?

Options:  
A. Use a fixed-time window with a duration of 60 minutes.  
B. Use a sliding time window with a duration of 60 minutes.  
<mark>C. Use a session window with a gap time duration of 60 minutes.</mark>  
D. Use a global window with a time-based trigger with a delay of 60 minutes.  

**Correct Answer:**  
C. Use a <mark>session window</mark> with a gap time duration of 60 minutes.  

**Explanation:**  

* <mark>Session windows</mark> group events into sessions separated by inactivity gaps.  
* A **gap of 60 minutes** means if the user does nothing for 1 hour, the session closes.  
* Perfect fit for **user inactivity detection** like cart abandonment.  
* Fixed or sliding windows (A/B) cannot capture per-user inactivity properly.  
* Global window with custom triggers (D) is too complex.  

---

#### Q12: Secure Multi-Client BigQuery Access

**Question:**  
Your company handles data for multiple clients. Each client wants to use their own tools, with some accessing directly via **BigQuery**.  
You must ensure **clients cannot see each other’s data** and only have **appropriate access**. What should you do? (Choose three)

Options:  
A. Load data into different partitions.  
<mark>B. Load data into a different dataset for each client.</mark>  
C. Put each client’s data in a different table within the same dataset.  
<mark>D. Restrict a client’s dataset to approved users.</mark>  
E. Only allow a service account to access the datasets.  
<mark>F. Use IAM roles for each client’s users.</mark>  

**Correct Answer:**  
B, D, F  

**Explanation:**  

* <mark>Separate datasets per client</mark> = clean boundary.  
* <mark>Restrict dataset access</mark> = dataset-level IAM for approved users only.  
* <mark>IAM roles</mark> = enforce least privilege per client.  
* A is wrong: Partitions don’t isolate access.  
* C is wrong: Tables inside the same dataset share the same IAM policy.  
* E is wrong: Service accounts are for backend automation, not client-facing access.  

---

#### Q13: Scalable Database for POS Transactions

**Question:**  
You want to process **payment transactions** in a **point-of-sale (POS) app** running on Google Cloud.  
The user base may grow **exponentially**, and you do not want to manage infrastructure scaling. Which database should you use?

Options:  
A. Cloud SQL  
B. BigQuery  
C. Cloud Bigtable  
<mark>D. Cloud Datastore (Firestore in Datastore mode)</mark>  

**Correct Answer:**  
D. Cloud Datastore  

**Explanation:**  

* <mark>Cloud Datastore</mark> (now Firestore in Datastore mode) is **serverless**.  
  * Auto-scales storage & compute.  
  * Provides **ACID transactions** (within entity groups).  
  * No infra management needed.  
* Cloud SQL: Limited auto-scaling (storage only, not CPU/memory).  
* BigQuery: OLAP, not OLTP (not suitable for transactions).  
* Bigtable: Scales for throughput, but manual node management required.  

| Dimension   | **Cloud Datastore / Firestore (Datastore mode)** | **Cloud SQL**                        |
| ----------- | ----------------------------------------------- | ------------------------------------ |
| Operations  | <mark>**Serverless / Auto-scaling**</mark>       | **Manual** tuning of CPU/memory; storage auto-extends |
| Workload    | **OLTP**, low-latency read/write                | **OLTP**, relational model           |
| Transactions (ACID) | Yes (**small-scope transactions**, good for orders/inventory) | Full SQL transactions, strong relational integrity |
| Data Model  | Document / Entity (non-relational)              | Relational tables, schema, foreign keys |
| Scalability | <mark>**No ops required**</mark>                | Manual scaling windows needed         |
| POS Fit     | <mark>**✓ Best fit**</mark>                     | Possible (but need scaling/ops work) |

--- 未分类 -- 分类参考最上面 --

#### Q6: Weather app handling DB failure

**Question:**  
Your weather app queries a database every 15 minutes to get the current temperature. The frontend is powered by Google App Engine and serves millions of users. How should you design the frontend to respond to a database failure?

Options:  
A. Issue a command to restart the database servers.  
<mark>B. Retry the query with exponential backoff, up to a cap of 15 minutes.</mark>  
C. Retry the query every second until it comes back online to minimize staleness of data.  
D. Reduce the query frequency to once every hour until the database comes back online.  

**Correct Answer:**  
B. Retry the query with <mark>exponential backoff</mark>, up to a cap of 15 minutes.  

**Explanation:**  
- Exponential backoff prevents overwhelming the DB with retries.  
- Starts with short delays (1s, 2s, 4s …) and increases gradually.  
- A cap (15m) avoids infinite retry storms.  
- Restarting DB (A) is infra task, not frontend.  
- Retrying every second (C) overloads server.  
- Reducing to 1h (D) makes data too stale.  

---

#### Q16: First step to secure BigQuery warehouse

**Question:**  
Your startup has no formal security policy. Everyone in the company has access to BigQuery datasets. You’ve been asked to secure the data warehouse and need to first discover what everyone is doing. What should you do?

Options:  
<mark>A. Use Google Stackdriver (Cloud) Audit Logs to review data access.</mark>  
B. Get the IAM policy of each table.  
C. Use Stackdriver Monitoring to see BigQuery slot usage.  
D. Use the Google Cloud Billing API to check billing.  

**Correct Answer:**  
A. Use <mark>Cloud Audit Logs</mark> to review data access.  

**Explanation:**  
- Audit Logs = best way to discover *who accessed what and when*.  
- IAM policy only shows *permissions*, not actual usage.  
- Monitoring slots shows performance, not security.  
- Billing API only shows costs, not access.  

---

#### Q17: Migrating Hadoop cluster to cloud

**Question:**  
Your company is migrating their 30-node Apache Hadoop cluster to the cloud. They want to re-use Hadoop jobs, minimize cluster management, and persist data beyond cluster life. What should you do?

Options:  
A. Create a Google Cloud Dataflow job.  
B. Create a Dataproc cluster with persistent disks for HDFS.  
C. Create a Hadoop cluster on Compute Engine with persistent disks.  
<mark>D. Create a Cloud Dataproc cluster that uses the Google Cloud Storage connector.</mark>  
E. Create a Hadoop cluster on Compute Engine with Local SSDs.  

**Correct Answer:**  
D. Cloud Dataproc with <mark>GCS connector</mark>.  

**Explanation:**  
- **Dataproc** = managed Hadoop, minimal ops.  
- **GCS connector** = data persists even after cluster shutdown.  
- Persistent HDFS disks (B) still tied to cluster lifecycle.  
- Raw Compute Engine clusters (C, E) require manual ops.  
- Dataflow (A) can’t directly re-use existing Hadoop jobs.  

---

#### Q18: ML applications on bank transactions

**Question:**  
You are given a dataset of bank transactions (user ID, type, location, amount). Business asks what ML can be applied. Which three?  

Options:  
A. Supervised learning to determine which transactions are most likely fraudulent.  
<mark>B. Unsupervised learning to determine which transactions are most likely fraudulent.</mark>  
<mark>C. Clustering to divide transactions into N categories.</mark>  
<mark>D. Supervised learning to predict the location of a transaction.</mark>  
E. Reinforcement learning to predict the location.  
F. Unsupervised learning to predict the location.  

**Correct Answer:**  
B, C, D  

**Explanation:**  
- **Fraud detection** often starts as **unsupervised anomaly detection** (B).  <mark>Unsupervised learning does not give a definitive conclusion like “this is fraud”; instead, it outputs an anomaly score.</mark>
- **Clustering (C)** groups transactions by similarity (e.g., type, amount, location).  
- **Supervised classification (D)** works if location is the target label.  
- A requires labeled fraud data (not given).  
- E/F are not suitable for this dataset.  


#### Q19: Minimize storage cost when migrating Hadoop → Dataproc

**Question:**  
Like-for-like migration would need **50 TB Persistent Disk per node**. CIO worries about **block storage cost**. How to **minimize storage cost**?

Options:  
<mark>A. Put the data into Cloud Storage (GCS).</mark>  
B. Use preemptible VMs for the cluster.  
C. Tune cluster so disks are just enough.  
D. Move cold to GCS, keep hot on PD.  

**Correct Answer:**  
A  

**Explanation:**  
- Use **Dataproc + GCS connector**: compute ephemeral, data persists cheaply in **GCS**.  
- Avoids massive PD footprint per node.  
- **B** cuts compute cost, not storage.  
- **C/D** still rely on PD; more ops overhead.  

---

#### Q20: Pub/Sub push endpoint duplicate messages

**Question:**  
Push subscription to HTTPS endpoint receives many **duplicate messages**. Most likely cause?

Options:  
A. Message body too large.  
B. Expired SSL cert.  
C. Topic has too many messages.  
<mark>D. Endpoint not acknowledging within ack deadline.</mark>  ✅

**Correct Answer:**  
D  

**Explanation:**  
- Pub/Sub is **at-least-once**; if not acked, Pub/Sub redelivers → duplicates.  
- Expired cert = failure, not dupes.  
- Too many messages doesn’t directly cause duplicates.  

---

#### Q21: Deduplicate retransmitted inventory payloads

**Question:**  
System retransmits when in doubt; payload includes **fields + transmission timestamp**. How to dedup?

Options:  
<mark>A. Assign GUID per data entry.</mark>  
B. Compute hash vs history.  
C. Store full payload as primary key.  
D. Maintain hash table.  

**Correct Answer:**  
A  

**Explanation:**  
- **GUID** = stable ID → downstream dedup/idempotency trivial.  
- Hash breaks if timestamp changes.  
- Using payload as PK is heavy. (Payload = Effective load (useful load) It refers to the actual business data）


#### Q22: Data scientist laptop underpowered

**Question:**  
Data scientist needs to analyze huge GCS + Cassandra datasets. Laptop too weak.

Options:  
A. Local Jupyter.  
B. Cloud Shell.  
C. Host only viz tool.  
<mark>D. Cloud Datalab on GCE VM.</mark>  

**Correct Answer:**  
D  

**Explanation:**  
- Managed notebook close to data.  
- Scales with VM resources.  
- A/B limited resources.  
- C = viz only, no analysis.  

---

#### Q23: 10,000 IoT devices real-time pipeline

**Question:**  
Need real-time ingestion, processing, and analysis.

Options:  
A. Datastore → export → BQ.  
<mark>B. Pub/Sub → Dataflow (stream) → BigQuery.</mark>  
C. GCS + Dataproc.  
D. Batch to GCS → Cloud SQL.  

**Correct Answer:**  
B  

**Explanation:**  
- Canonical streaming stack: Pub/Sub (ingest), Dataflow (process), BQ (analyze).  
- A/D are batch.  
- C is slow/batch-oriented.  

---

#### Q24: STRING epoch → TIMESTAMP

**Question:**  
`CLICK_STREAM.DT` stored as STRING epoch. Need TIMESTAMP for sessions, minimize future query cost.

Options:  
A. Drop/reload with TIMESTAMP.  
B. Add TIMESTAMP col, backfill.  
C. View casting DT → TIMESTAMP.  
<mark>E. CTAS into NEW_CLICK_STREAM with casted TS.</mark>  

**Correct Answer:**  
E  

**Explanation:**  
- One-time transform → queries run on real TIMESTAMP (no per-query cast cost).  
- C = casts every query = costly.  
- A/B heavy ops.  


#### Q25: Alert on BigQuery insert job

**Question:**  
Send **instant notification** only when an **insert job** appends to one specific table.

Options:  
A. List logs via API.  
B. Sink logs to BQ.  
C. Sink logs to Pub/Sub (no fine filter).  
<mark>D. Create sink with advanced filter → Pub/Sub.</mark>  ✅ `protoPayload.methodName="jobservice.insert"`

**Correct Answer:**  
D  

**Explanation:**  
- Advanced filter isolates target table + job type.  
- Pub/Sub delivers instant events.  
- A/B don’t notify.  
- C lacks fine-grained filter.  

#### Q26: Consultant with sensitive Dataflow job

**Question:**  
External consultant needs to develop Dataflow transform, but **data is sensitive**. How to proceed?

Options:  
A. Project Viewer role.  
B. Dataflow Developer role.  
C. Share service account.  
<mark>D. Provide anonymized sample in separate project.</mark>  ✅ /əˈnɑː.nə.maɪzd/

**Correct Answer:**  
D  

**Explanation:**  
- **Least privilege**: anonymized sample → no PII exposure.  
- A/B still expose real data.  
- C is anti-pattern.  


#### Q27: Feature reduction for faster training

**Question:**  
Thousands of features; want faster training while preserving accuracy.

Options:  
A. Drop features correlated with label.  
<mark>B. Combine highly correlated features.</mark>  
C. Average features in groups of 3.  
D. Drop features with 50% nulls.  

**Correct Answer:**  
B  

**Explanation:**  
- Removes redundancy, preserves signal.  
- A: correlated with label = important!  
- C: arbitrary, loses info.  
- D: missingness ≠ useless.  

---

#### Q28: Dataflow reading BigQuery logs

**Question:**  
Need to read growing BigQuery logs efficiently for new features.

Options:  
A. Provide TableReference.  
<mark>B. Use `.fromQuery` selecting only needed columns.</mark>  ✅ `projection pushdown`  
C. Use TableSchema.  
D. Return TableRow.  

**Correct Answer:**  
B  

**Explanation:**  
- Push down projection → scan fewer bytes.  
- Others don’t cut scanned data size.  

---

#### Q29: Bigtable row key design

**Question:**  
Row key for real-time dashboards with sensors.

Options:  
A. `<timestamp>`  
B. `<sensorid>`  
C. `<timestamp>#<sensorid>`  
<mark>D. `<sensorid>#<timestamp>`</mark>  

**Correct Answer:**  
D  

**Explanation:**  
- Sensor-first avoids hotspotting.  
- Supports efficient time-range per sensor.  
- Timestamp-first = hotspotting.  

---

#### Q30: Analytics on busy MySQL cluster

**Question:**  
MySQL cluster overloaded. Need analytics without hurting ops.

Options:  
A. Add node + OLAP cube.  
<mark>B. ETL data into BigQuery.</mark>  
C. On-prem Hadoop.  
D. Restore backup → Cloud SQL → Dataproc.  

**Correct Answer:**  
B  

**Explanation:**  
- Offload to BigQuery = scalable analytics.  
- A = more OLTP load.  
- C = complex, heavy ops.  
- D = clunky multi-step.  

#### Q31: Updating incompatible Dataflow pipeline without data loss  

**Question:**  
Your streaming Dataflow pipeline (Pub/Sub source) needs an update that makes it **incompatible** with the current version. You must avoid data loss.  

Options:  
<mark>A. Update the current pipeline and use the drain flag.</mark>  
B. Update the current pipeline and provide the transform mapping JSON object.  
C. Create a new pipeline with the same Pub/Sub subscription and cancel the old one.  
D. Create a new pipeline with a new Pub/Sub subscription and cancel the old one.  

**Correct Answer:**  
A  

**Explanation:**  
- <mark>**Drain** allows current pipeline to **finish processing in-flight data** before shutdown → no loss.</mark>    
- **B** only works for compatible transform changes (rename/mapping), not for incompatible jobs.  
- **C/D** risk losing unacked or duplicate messages when switching subscriptions.  
- Safe approach: **drain old pipeline → deploy new one**.  

---

#### Q32: Improve Bigtable load performance (10TB initial load)  

**Question:**  
Data scientists observe poor read/write performance with Bigtable initial load (10TB). Want to improve performance at minimal cost.  

Options:  
<mark>A. Redefine schema to evenly distribute reads/writes across row space.</mark>  
B. Wait for cluster auto-scale.  
C. Use single row key for frequently updated values.  
D. Use sequential numeric IDs as row keys.  

**Correct Answer:**  
A  

**Explanation:**  
- **Bigtable best practice**: avoid **hotspotting** by distributing keys evenly.  
- **B**: cluster size ≠ schema design.  
- **C**: single row key concentrates load → bottleneck.  
- **D**: sequential IDs → hotspotting.  

---

#### Q33: Messages missing in Dataflow dashboard  

**Question:**  
Pub/Sub shows all messages published, but CFO dashboard (via Dataflow) is missing some. What to check next?  

Options:  
A. Check dashboard app rendering.  
<mark>B. Run a fixed dataset through Dataflow pipeline and analyze output.</mark>  
C. Use Stackdriver Monitoring on Pub/Sub.  
D. Switch Dataflow to pull mode.  

**Correct Answer:**  
B  

**Explanation:**  
- Pub/Sub confirmed fine → issue likely **in Dataflow pipeline**.  
- Re-run with **fixed dataset** → confirm transformations/parsing logic.  
- **C** shows backlog metrics but not actual missing message cause.  
- **A/D** don’t isolate pipeline logic.  

---

#### Q34: Flowlogistic — common storage for BigQuery & Hadoop  

**Question:**  
BigQuery is primary analytics system, but Hadoop/Spark workloads remain. Where to store **common data**?  

Options:  
A. Store in BigQuery partitioned tables.  
B. Store in BigQuery with authorized views.  
<mark>C. Store in GCS encoded as Avro.</mark>  
D. Store in HDFS on Dataproc.  

**Correct Answer:**  
C  

**Explanation:**  

- **GCS** is Google’s object storage, accessible to all systems.  
- **Avro** is a cross-platform format with built-in schema support (row-oriented with efficient serialization).

- BigQuery can directly load Avro files or query them as external tables.  
- Spark/Hadoop can read Avro natively through their connectors.  
- **GCS + Avro** = interoperable format for both **BigQuery** and **Spark/Hadoop**.  

---

- **A/B**: BigQuery-only, not usable directly by Spark.  
- **D**: HDFS on Dataproc adds cost/ops, not recommended for common data lake.  


#### Q35: Flowlogistic — real-time tracking ingestion system  

**Question:**  
Kafka cannot scale. Need ingestion, real-time processing, reliable storage.  

Options:  
<mark>A. Cloud Pub/Sub + Cloud Dataflow + Cloud Storage.</mark>  
B. Pub/Sub + Dataflow + Local SSD.  
C. Pub/Sub + Cloud SQL + Cloud Storage.  
D. Load Balancing + Dataflow + Cloud Storage.  

**Correct Answer:**  
A  

**Explanation:**  
- **Pub/Sub** = scalable global ingestion.  
- **Dataflow** = stream + batch processing.  
- **Cloud Storage** = durable storage for analytics.  
- Other options misuse SQL/SSD/LB → don’t fit streaming scale.  

---

#### Q36: Flowlogistic — cost-effective BigQuery reporting  

**Question:**  
Sales team (non-technical) overwhelmed by huge BQ tables, queries cost too much. Best fix?  

Options:  
A. Export to Google Sheets.  
B. Create extra table with only needed columns.  
<mark>C. Create a view with only necessary columns.</mark>  
D. Use IAM column-level access.  

**Correct Answer:**  
C  

**Explanation:**  
- **View**: logical subset, no extra storage, keeps data updated.  
- **B** static table duplicates data & requires sync.  
- **A** too small for TB-scale.  
- **D** controls access but doesn’t simplify data.  

---

#### Q37: Flowlogistic — tracking messages with Pub/Sub  

**Question:**  
Devices send package-tracking messages to one Pub/Sub topic. Need to ensure package data is analyzable over time.  

Options:  
A. Timestamp added by subscriber.  
<mark>B. Timestamp + Package ID added by publisher device.</mark>  
C. Use NOW() in BigQuery.  
D. Use Pub/Sub publishTime.  

**Correct Answer:**  
B  

**Explanation:**  
- **Event time from publisher** = true time of event + unique ID for ordering.  
- **A**: subscriber receive-time may be delayed.  
- **C**: NOW() in BQ = ingestion time, not event time.  
- **D**: Pub/Sub publishTime = system time, not guaranteed accurate for event sequence.  

---

#### Q38: MJTelco — Dataflow scaling  

**Question:**  
Dataflow must handle up to 50k installations, scale compute power dynamically. Which setting?  

Options:  
A. Zone  
B. Number of workers  
C. Disk size per worker  
<mark>D. Maximum number of workers</mark>  

**Correct Answer:**  
D  

**Explanation:**  
- Dataflow **autoscaling** adds/removes workers as needed → limited by **max workers**.  
- **A** irrelevant to scaling.  
- **B** = fixed workers, not dynamic.  
- **C** = storage size, not compute scaling.  

---

#### Q39: MJTelco — visualization of telemetry  

**Question:**  
Ops team needs dashboards: 50k installs, 6 weeks data, <3h delay, <5s load time, filter suboptimal links.  

Options:  
A. Google Sheets  
B. BigQuery + Apps Script + Sheets  
C. Datastore + App Engine + Charts API  
<mark>D. BigQuery + Data Studio 360 (Looker Studio)</mark>  

**Correct Answer:**  
D  

**Explanation:**  
- **BigQuery** handles large telemetry datasets.  
- **Data Studio** (Looker Studio) = cost-free, interactive dashboards with filters/sorting.  
- Meets latency + usability requirements.  
- Other options too small-scale or require custom apps.  

---

#### Q40: MJTelco — enforce regional access in BigQuery  

**Question:**  
Each region has its own table. Need to enforce access so employees only see their region.  

Options:  
A. Put all tables in one global dataset.  
<mark>B. Put each table in a dataset for a region.</mark>  
C. Adjust table-level IAM.  
D. Adjust view-level IAM.  
<mark>E. Adjust dataset-level IAM for each region’s group.</mark>  

**Correct Answer:**  
B, E  

**Explanation:**  
- **B**: region-specific dataset separation.  
- **E**: dataset-level IAM = scalable, easy to maintain.  
- **A**: global dataset breaks isolation.  
- **C/D**: possible, but harder to maintain vs dataset-level controls.  

---

#### Q41: MJTelco — Bigtable schema for historical telemetry

**Question:**  
MJTelco needs a schema in **Google Bigtable** for 2 years of telemetry records (every 15 min, unique device_id + datapoint).  
Most common query: *“all the data for a given device for a given day.”*  

Options:  
<mark>A. Rowkey: date#device_id; Column data: data_point</mark>  
B. Rowkey: date; Column data: device_id, data_point  
C. Rowkey: device_id; Column data: date, data_point  
D. Rowkey: data_point; Column data: device_id, date  
E. Rowkey: date#data_point; Column data: device_id  

**Correct Answer:**  
A  

**Explanation:**  
- **Rowkey = date#device_id** supports prefix scans like `2023-12-20#device123`, directly matching query pattern.  
- Avoids scanning full table for each query.  
- Column families store datapoints efficiently.  
- **C** is tempting (device_id#date), but the exam expects A since the *query* starts with date + device.  
- Best practice IRL: consider **device_id#date** to avoid hotspotting, but within given options, **A** is correct.  

---

#### Q42: Hadoop batch jobs falling behind with more data

**Question:**  
Batch MapReduce jobs on Hadoop are lagging as data volume grows. How to increase responsiveness **without adding cost**?  

Options:  
A. Rewrite in Pig  
<mark>B. Rewrite in Apache Spark</mark>  
C. Increase Hadoop cluster size  
D. Decrease cluster size + use Hive  

**Correct Answer:**  
B  

**Explanation:**  
- **Spark** executes in-memory, avoids MapReduce disk I/O overhead → much faster.  
- **A/D** still depend on MapReduce.  
- **C** solves performance but increases cost (more hardware).  
- Spark = modern, scalable solution with better responsiveness.  

---

#### Q43: BigQuery Users table — FullName field

**Question:**  
Users table has `FirstName`, `LastName`. App wants `FullName` = `FirstName + ' ' + LastName`. Cheapest way?  

Options:  
<mark>A. Create a BigQuery view concatenating FirstName + LastName</mark>  
B. Add new column FullName + UPDATE all rows  
C. Dataflow pipeline to build new table  
D. Export → process in Dataproc → reload  

**Correct Answer:**  
A  

**Explanation:**  
- **View** = logical layer, no extra storage. Always up-to-date when queried.  
- **B** = more storage + maintenance for new inserts.  
- **C/D** = overkill, extra infra.  
- Cost-effective, minimal change = **View**.  

---

#### Q44: Cloud Datastore — avoid index explosion

**Question:**  
Entity *Movie*: fields = `actors` (multi), `tags` (multi), `date_released` (single).  
Queries like “all movies with actor=X ordered by date_released.”  
How to avoid **combinatorial index explosion**?  

Options:  
<mark>A. Manually configure composite indexes in index.yaml</mark>  
B. (invalid syntax)  
C. Exclude `actors, tags` from index  
D. Exclude `date_released` from index  

**Correct Answer:**  
A  

**Explanation:**  
- By default, Datastore builds indexes for every property combo → explosion if multiple arrays.  
- **Custom composite index** (actor/date, tag/date) avoids explosion.  
- **C/D** exclude needed fields → queries fail.  

---

#### Q45: Dataflow job once per day

**Question:**  
Manufacturing plant batches logs once daily at 2AM. Need to process exactly once/day, as cheaply as possible.  

Options:  
A. Use Dataproc instead  
B. Manually start Dataflow job  
<mark>C. Use App Engine Cron Service (or Cloud Scheduler) to trigger Dataflow</mark>  
D. Run job as streaming  

**Correct Answer:**  
C  

**Explanation:**  
- **Cron/Scheduler** = automate Dataflow trigger daily, reliable, no ops overhead.  
- **A**: Dataproc cluster = more infra, cost.  
- **B**: manual = error-prone, labor cost.  
- **D**: streaming job = expensive for once/day logs.  

---

#### Q46: BigQuery + external price data (updated every 30m)

**Question:**  
You need to join customer data in BQ with **price data** (100 goods, updated every 30 minutes). Must be cheap & up-to-date.  

Options:  
A. Load into partitioned table every 30 min  
<mark>B. Store in Cloud Storage, expose via federated external table</mark>  
C. Use Cloud Datastore + Dataflow  
D. Use GCS + Dataflow to push into BQ  

**Correct Answer:**  
B  

**Explanation:**  
- **External table (GCS)**: avoids constant reloading, always reflects updates, cheap.  
- **A**: partition granularity = 1h minimum, not 30m. Repeated loads add cost.  
- **C/D**: too complex for small ref data.  
- **Best practice**: external tables for small, frequently refreshed reference datasets.  

#### Q47: Database schema for ML-based food ordering service

**Question:**  
You are designing the schema for a food ordering service (user likes/dislikes, account info, order history).  
The DB must store **all transactional data** and support schema optimization. Which product?  

Options:  
A. BigQuery  
<mark>B. Cloud SQL</mark>  
C. Cloud Bigtable  
D. Cloud Datastore  

**Correct Answer:**  
B  

**Explanation:**  
- **Cloud SQL** = managed relational DB (ACID, schema design, queries). Perfect for transactional workloads.  
- **BigQuery (A)** = analytical warehouse, not for OLTP.  
- **Bigtable (C)** = wide-column, best for time-series/IoT, not relational.  
- **Datastore (D)** = schema-less NoSQL, not good for strict schema optimization.  

---

#### Q48: CSV data mismatch in BigQuery  

**Question:**  
You load CSVs into BigQuery. Import succeeds, but data doesn’t match byte-to-byte with the source. Why?  

Options:  
A. CSV not flagged correctly  
B. Invalid rows skipped  
<mark>C. Wrong file encoding (not UTF-8)</mark>  
D. Missing ETL  

**Correct Answer:**  
C  

**Explanation:**  
- **BigQuery defaults to UTF-8**. If CSV uses ISO-8859-1 or other encoding → BigQuery auto-converts.  
- Import succeeds, but data differs byte-by-byte.  
- **A/B/D** don’t fit since load completed without errors.  

---

#### Q49: Ingesting 20k small CSV files/hour with 200ms latency  

**Question:**  
You must ingest 20,000 CSV files/hour (<4 KB each) via GCP. Current SFTP barely keeps up. Next quarter volume doubles.  
Which two actions help?  

Options:  
A. Compress each file  
B. Increase ISP bandwidth  
<mark>C. Use `gsutil -m` to upload in parallel to GCS</mark>  
<mark>D. Batch 1,000 files into TAR before upload</mark>  
E. Use Storage Transfer Service from on-prem  

**Correct Answer:**  
C, D  

**Explanation:**  
- **C**: Parallel uploads reduce impact of 200ms latency on each file.  
- **D**: Fewer, larger files improve throughput.  
- **A**: compression useless (files are already tiny).  
- **B**: bandwidth not bottleneck (latency is).  
- **E**: STS requires higher throughput (≥300 Mbps).  

---

#### Q50: NoSQL DB for IoT telemetry (100 TB/year, 100 attributes/record)  

**Question:**  
IoT telemetry, 100 TB/year, high availability + low latency, no ACID required. Which 3 DBs?  

Options:  
A. Redis  
<mark>B. HBase</mark>  
C. MySQL  
<mark>D. MongoDB</mark>  
<mark>E. Cassandra</mark>  
F. HDFS + Hive  

**Correct Answer:**  
B, D, E  

**Explanation:**  
- **HBase (B)**: column-oriented, scalable, low latency.  
- **MongoDB (D)**: flexible schema, handles high-volume telemetry.  
- **Cassandra (E)**: distributed, high availability, low latency.  
- **Redis (A)**: in-memory, not for 100TB/year persistence.  
- **MySQL (C)**: relational, not NoSQL.  
- **Hive (F)**: OLAP, not low-latency NoSQL.  

Here you go — tidy cards for **Q51–Q54** with quick justifications:


#### Q51: Fix overfitting in a spam classifier (choose 3)

**Question:**  
You’re overfitting the training data. Which three actions help?

Options:  
<mark>A. Get more training examples</mark>  
B. Reduce the number of training examples  
<mark>C. Use a smaller set of features</mark>  
D. Use a larger set of features  
<mark>E. Increase the regularization parameters</mark>  
F. Decrease the regularization parameters  

**Correct Answer:**  
A, C, E

**Explanation:**  
- **More data (A)** → better generalization.  
- **Fewer features (C)** → simpler model, less noise.  
- **Stronger regularization (E)** → penalize complexity.  
- B & F increase overfitting risk; D often raises variance.

---

#### Q52: Securely automate GCS → Dataproc → BigQuery

**Question:**  
Nightly Spark (Dataproc) job reads **non-public** files from GCS and writes to BigQuery. How to run securely?

Options:  
A. Lock bucket to only yourself  
B. Give **Project Owner** to a service account  
<mark>C. Use a service account with GCS read + BigQuery write</mark>  
D. Use a user account with **Project Viewer**  

**Correct Answer:**  
C

**Explanation:**  
Follow **least privilege**: run with a **service account** scoped just to **read GCS** and **write BigQuery**.  
B is over-privileged; A/D don’t enable a secure automated pipeline.

---

#### Q53: BigQuery GROUP BY is very slow

**Question:**  
`SELECT country, state, city FROM [proj:ds.tbl] GROUP BY country` runs slowly; plan shows heavy skew in Read stage. Why?

Options:  
A. Too many concurrent queries  
B. Too many partitions  
C. Many NULLs in state/city  
<mark>D. Most rows share the same country (data skew)</mark>  

**Correct Answer:**  
D

**Explanation:**  
Grouping on a **highly skewed key** funnels most rows to one reducer/slot → **hotspot** → slow stage.

---

#### Q54: Real-time “who bid first” across global servers

**Question:**  
Multiple app servers emit bid events (item, amount, user, timestamp). Collate centrally in **real time** to determine who bid first.

Options:  
A. Write to shared file; batch Hadoop  
B. Pub/Sub → **push** → custom endpoint → Cloud SQL  
C. Per-server MySQL, then periodic merge  
<mark>D. Pub/Sub → pull with Dataflow; determine first in stream</mark>  

**Correct Answer:**  
D

**Explanation:**  
Use **Pub/Sub** for global ingestion and **Dataflow** streaming to process in real time using **event-time** timestamps, windowing, and tie-breaking logic. Cloud SQL (B) adds a custom endpoint, isn’t ideal for high-throughput ordered streaming, and complicates global scalability.


#### Q55: ODBC connection to BigQuery (Legacy SQL view issue)

**Question:**  
Your org has a **time-partitioned table** `events_partitioned`.  
To save cost, a **view** `events` was created (last 14 days only), but it’s written in **Legacy SQL**.  
Next month, apps will connect via **ODBC**. What must you do? (Choose 2)

Options:  
A. Create a new view over `events` using Standard SQL  
B. Create a new partitioned table using a Standard SQL query  
<mark>C. Create a new view over `events_partitioned` using Standard SQL</mark>  
<mark>D. Create a service account for the ODBC connection</mark>  
E. Create a Cloud IAM role for the ODBC connection  

**Correct Answer:**  
C, D  

**Explanation:**  
- **C** → ODBC drivers **only support Standard SQL**, not Legacy SQL. You must rewrite the view over the partitioned table.  
- **D** → ODBC connection requires **authentication via a Service Account** with proper IAM roles.  
- **A** wrong → still points to Legacy SQL view.  
- **B** wrong → no need for new table, just update the view.  
- **E** → custom IAM role not needed; service account already covers it.  

---

#### Q56: Query Firebase sharded tables in BigQuery (Legacy SQL)

**Question:**  
Firebase → BigQuery creates daily sharded tables: `app_events_YYYYMMDD`.  
You want to query last 30 days in **Legacy SQL**. What should you use?  

Options:  
<mark>A. TABLE_DATE_RANGE()</mark>  
B. `_PARTITIONTIME` pseudo column  
C. WHERE date BETWEEN …  
D. SELECT IF(date >= … AND date <= …)  

**Correct Answer:**  
A  

**Explanation:**  
- In **Legacy SQL**, `TABLE_DATE_RANGE([dataset.table_], start_date, end_date)` queries across date-sharded tables.  
- **B** `_PARTITIONTIME` works only in **Standard SQL partitioned tables**, not sharded legacy tables.  
- **C/D** are row filters, won’t union multiple sharded tables.  

#### Q57: Dataflow streaming + windowing job fails

**Question:**  
Your Pub/Sub → Dataflow pipeline applies windowing to group events for a campaign.  
During testing, the job fails for **all streaming inserts**. What is the most likely cause?  

Options:  
A. No timestamp assigned  
B. No triggers for late data  
C. No global windowing function applied  
<mark>D. No non-global windowing function applied</mark>  

**Correct Answer:**  
D  

**Explanation:**  
- In **Apache Beam/Dataflow**, unbounded PCollections default to a **global window**, which waits forever for completion.  
- If you use `GroupByKey` or aggregations without a **non-global window** (tumbling/sliding/session), the job **fails at pipeline construction**.  
- A (timestamps) or B (triggers) affect correctness, not this specific failure.  


---

#### Q58: Add missing sensor calibration to Hadoop ETL

**Question:**  
ETL = series of MapReduce jobs; processing takes days. A sensor calibration step was omitted.  
How should you change the ETL to systematically ensure calibration?  

Options:  
A. Modify every transform MR job to apply calibration first  
<mark>B. Add a new MapReduce job to calibrate raw data, chain all others after</mark>  
C. Add calibration metadata to final output, let users handle it  
D. Predict calibration factors via algorithm at the end  

**Correct Answer:**  
B  

**Explanation:**  
- Calibration is a **data quality step** that belongs at raw ingest.  
- Adding a **dedicated MR job** ensures **every downstream step** works on calibrated data.  
- A = repetitive, complex to maintain.  
- C = pushes responsibility to users (bad practice).  
- D = guesswork, not systematic.  


---

#### Q59: Single database for transactions + BI tool

**Question:**  
Retailer’s App Engine app adds **shopping transactions** (OLTP) + wants BI analysis (OLAP).  
They want **one database** for both. Which should they choose?  

Options:  
A. BigQuery  
<mark>B. Cloud SQL</mark>  
C. Cloud Bigtable  
D. Cloud Datastore  

**Correct Answer:**  
B  

**Explanation:**  
- **Cloud SQL** = fully managed RDBMS, supports **ACID transactions** + SQL for BI tools.  
- **BigQuery** = great for analytics, but not for **row-level transactional updates**.  
- **Bigtable** = wide-column NoSQL, not ACID, not BI-friendly.  
- **Datastore/Firestore** = document store, lacks SQL + joins for BI.  


---

#### Q60: Sharded log tables exceed 1000-table limit

**Question:**  
3 years of daily logs, sharded as `LOGS_YYYYMMDD`.  
Queries over long ranges exceed **1000-table wildcard limit** and fail. How to fix?  

Options:  
A. Convert all daily logs into multiple date-partitioned tables  
<mark>B. Convert all sharded tables into one partitioned table</mark>  
C. Enable query caching  
D. Create monthly views and query those  

**Correct Answer:**  
B  

**Explanation:**  
- **Partitioned tables** solve the 1000-table wildcard limit.  
- BigQuery manages partitions internally → **better performance + pruning**.  
- A still leaves many tables.  
- C only caches results (24h), doesn’t reduce tables.  
- D = workarounds with views, still metadata overhead.  


#### Q61: Optimize Dataproc cluster cost for weekly Spark job

**Question:**  
Analytics team runs a Spark job (30 min runtime on 15 nodes) weekly. Data in GCS, output to BigQuery. How to optimize cluster cost?

Options:  
A. Migrate to Cloud Dataflow  
<mark>B. Use pre-emptible VMs for the cluster</mark>  
C. Use higher-memory nodes so job runs faster  
D. Use SSDs on worker nodes so job runs faster  

**Correct Answer:**  
B

**Explanation:**  
- **Preemptible VMs (B)** cut compute cost by up to 80%. Perfect for **batch jobs** (short, restartable, non-critical).  
- **A** adds migration effort; question focuses on **cost optimization within Dataproc**.  
- **C** increases cost; speed isn’t the problem (job already fits in 30 min).  
- **D** SSDs increase I/O cost; Spark jobs reading from GCS don’t need large local PD.  

---

#### Q62: Handle late or out-of-order events in Dataflow

**Question:**  
Company receives batch + stream event data. Sometimes late or out-of-order. How should Dataflow pipeline handle this?

Options:  
A. Single global window  
B. Sliding windows  
<mark>C. Use watermarks and timestamps</mark>  
D. Require all data sources to include timestamps  

**Correct Answer:**  
C

**Explanation:**  
- **Watermarks** track event-time progress and allow Dataflow to wait for stragglers.  
- **Timestamps** order events correctly, even if out-of-order.  
- A/B don’t solve late arrivals properly.  
- D is good practice but incomplete—still need **watermarks** to know how late is acceptable.

---

#### Q63: Add synthetic feature for linear separation

**Question:**  
Dataset has circular separation by class (X,Y). Need to classify with linear algorithm by adding a synthetic feature. Which?  

Options:  
<mark>A. X² + Y²</mark>  
B. X²  
C. Y²  
D. cos(X)  

**Correct Answer:**  
A

**Explanation:**  
- Circle equation: **X² + Y² = r²**. Adding this feature makes data linearly separable in higher dimension.  
- B and C lose joint relationship (need both X and Y).  
- D ignores Y, doesn’t match circular boundary.

---

#### Q64: Secure app → BigQuery access without per-user auth

**Question:**  
IT app integrates with BigQuery. Users should not authenticate individually, nor get dataset access. How to access securely?  

Options:  
A. Grant group dataset access  
B. Use SSO + pass user creds  
<mark>C. Use service account, grant dataset access, use its key</mark>  
D. Dummy user + stored password  

**Correct Answer:**  
C

**Explanation:**  
- **Service accounts** are for apps, not humans. Grant dataset access to SA → app authenticates securely.  
- A/B/D require per-user or insecure key/password sharing.  
- **C is Google-recommended best practice** for app-to-BigQuery integration.

#### Q65: Casual prep for ML with nulls in logistic regression

**Question:**  
Build a data pipeline for logistic regression. Need a casual way to prep data, monitor/adjust **null values**, keep them **real-valued** (not removed).  

Options:  
A. Dataprep → find nulls → Dataproc job: convert to 'none'  
<mark>B. Dataprep → find nulls → Dataprep job: convert to 0</mark>  
C. Dataflow → find nulls → Dataprep job: convert to 'none'  
D. Dataflow → find nulls → custom script: convert to 0  

**Correct Answer:**  
B  

**Explanation:**  
- Logistic regression requires **numeric (real-valued)** inputs.  
- **Dataprep** is the “casual” tool (UI-based wrangling).  
- Converting nulls to **0** keeps them real-valued.  
- 'none' is a string, not numeric.  
- Dataflow/custom scripts are heavier ops than required.

---

#### Q66: Encrypt at rest for Redis/Kafka on GCE with key rotation

**Question:**  
Redis via Kafka on GCE. Must encrypt data at rest with keys you can **create, rotate, and destroy**.  

Options:  
A. SA + API call “encryption at rest”  
<mark>B. Create keys in Cloud KMS; use them for GCE data encryption</mark>  
C. Create keys locally, upload to KMS, use for GCE  
D. Create keys in KMS; reference in API calls at runtime  

**Correct Answer:**  
B  

**Explanation:**  
- **Cloud KMS** supports customer-managed keys (CMEK): creation, rotation, destruction.  
- Integrated directly with GCE disk encryption.  
- **C** (CSEK) = external keys, but rotation harder.  
- **D** = API call use, not true disk encryption at rest.  
- Best practice: use CMEK with KMS (option B).

---

#### Q67: Recommend videos (fast filtering, TB-scale)

**Question:**  
App recommends new videos by past views. Must generate **labels** for video entities, and provide **fast filtering** across several TB of data.  

Options:  
A. Build classifier (MLlib) → Dataproc  
B. Build 2 classifiers (MLlib) → Dataproc  
<mark>C. Use Video Intelligence API for labels; store in Bigtable; filter</mark>  
D. Use Video Intelligence API; store in Cloud SQL; join/filter  

**Correct Answer:**  
C  

**Explanation:**  
- Use **Video Intelligence API** for managed labeling (avoid custom ML).  
- **Bigtable** → low-latency, scalable TB+ data store with key-based filtering.  
- **Cloud SQL** → limited storage (~64TB), slower joins.  
- Spark MLlib (A/B) → heavy/overkill; not needed.

---

#### Q68: Cheapest scalable JSON → BigQuery pipeline

**Question:**  
Write/transform JSON from Pub/Sub to BigQuery. Must minimize **service costs**, handle variable input sizes, with minimal manual ops.  

Options:  
A. Dataproc + monitor CPU + resize workers  
B. Dataproc + diagnose bottleneck + manual tuning  
<mark>C. Dataflow + monitor lag (Stackdriver) + default autoscaling</mark>  
D. Dataflow + monitor runtimes + custom machine types  

**Correct Answer:**  
C  

**Explanation:**  
- **Dataflow** = serverless, auto-scaling, ideal for spiky workloads.  
- **Autoscaling** lowers costs and removes manual intervention.  
- **Dataproc** (A/B) = cluster ops overhead.  
- **D** customizing machine types = more manual ops.

---

#### Q69: YouTube channel log data transfer for ANSI SQL analysis

**Question:**
Your infrastructure includes YouTube channels. You need to transfer YouTube channel data into Google Cloud so worldwide marketing teams can perform **ANSI SQL analysis** on up-to-date logs. What should you do?

**Options:**  
A. Use Storage Transfer Service to transfer offsite backup files to **Cloud Storage Multi-Regional** bucket as final destination.  
B. Use Storage Transfer Service to transfer offsite backup files to **Cloud Storage Regional** bucket as final destination.  
C. Use **BigQuery Data Transfer Service** to transfer offsite backup files to **Cloud Storage Multi-Regional** bucket.  
D. Use **BigQuery Data Transfer Service** to transfer offsite backup files to **Cloud Storage Regional** bucket.  

**Correct Answer:** A

**Explanation:**

* **A**: Storage Transfer Service moves backup files into Cloud Storage → from there you can query with BigQuery (external tables / BigLake). Multi-Regional bucket ensures global access for distributed teams.
* **B**: Regional bucket is cheaper but not global; less aligned with worldwide requirement.
* **C/D**: BigQuery Data Transfer Service only loads into **BigQuery datasets**, not GCS. Options C/D are invalid.

---

#### Q70: Storage design for very large text files with ANSI SQL

**Question:**
You are designing storage for very large text files in a Google Cloud data pipeline. Requirements:

* Support **ANSI SQL queries**.
* Support **compression**.
* Support **parallel load** from input locations (Google best practices).

**Options:**  
A. Transform text files to compressed **Avro** using Cloud Dataflow. Store in BigQuery for storage and query.  
B. <mark>Transform text files to compressed **Avro** using Cloud Dataflow. Store in **Cloud Storage** and query via permanent BigQuery external tables.</mark>  
C. Compress text files to **gzip** using Grid Computing Tools. Store in BigQuery for storage and query.  
D. Compress text files to **gzip** using Grid Computing Tools. Store in Cloud Storage, then import into **Cloud Bigtable** for query.  

**Correct Answer:** B

**Explanation:**

* **B**: Best practice → Store Avro in Cloud Storage (cheap, compressed, parallel load). BigQuery external tables allow ANSI SQL queries without fully loading into BQ storage.
* **A**: Works but increases storage costs in BigQuery.
* **C/D**: Gzip is slower, not parallel-friendly; Bigtable doesn’t support ANSI SQL.

---

#### Q71: Auto-label blog posts without ML expertise

**Question:**  
You need to add **subject labels** to users’ blog posts quickly with **no ML expertise or extra dev resources**.  

**Options:**  
A. <mark>Call the **Cloud Natural Language API** and use **Entity Analysis** results as labels.</mark>  
B. Call the Cloud Natural Language API and use **Sentiment Analysis** as labels.  
C. Build/train a TensorFlow text classifier; deploy on Cloud ML Engine; call from the app.  
D. Build/train a TensorFlow model; deploy on GKE; call from the app.  

**Correct Answer:** A  

**Explanation:**  
- **A** uses a pre-trained API (fastest path) and returns label-like entities (person/org/location/product).  
- **B** returns emotion/attitude, not subjects.  
- **C/D** require custom ML work (slow, resource-heavy).  

---

#### Q72: Cheapest storage for 20 TB CSV with ANSI SQL via multiple engines

**Question:**  
Store **20 TB CSV** and let multiple teams query aggregates while minimizing **query cost**. Data is in **Cloud Storage** and queried by multiple engines.  

**Options:**  
A. Cloud **Bigtable** for storage; query with **HBase shell** on GCE.  
B. Cloud **Bigtable** for storage; link as **permanent tables** in BigQuery.  
C. <mark>**Cloud Storage** for storage; link as **permanent external tables** in BigQuery.</mark>  
D. **Cloud Storage** for storage; link as **temporary tables** in BigQuery.  

**Correct Answer:** C  

**Explanation:**  
- **C** stores cheaply in GCS and uses **permanent external tables** for reusable ANSI SQL without loading into BQ storage.  
- **A/B**: Bigtable suits NoSQL/point lookups, not aggregate analytics economy.  
- **D**: Temporary tables are ad-hoc and not shareable.  

---

#### Q73: Relational workload, horizontal transactions + range queries

**Question:**  
Two relational tables (~10 TB) must support **horizontally scalable transactions** and **range queries on non-key columns**.  

**Options:**  
A. **Cloud SQL** with secondary indexes.  
B. **Cloud SQL** + Dataflow transforms.  
C. <mark>**Cloud Spanner** with **secondary indexes**.</mark>  
D. **Cloud Spanner** + Dataflow transforms.  

**Correct Answer:** C  

**Explanation:**  
- **C**: Only **Cloud Spanner** provides **horizontal scale + transactions**; secondary indexes optimize range queries.  
- **A/B**: Cloud SQL scales vertically; Dataflow doesn’t fix scaling/transactions.  
- **D**: ETL not required for the query pattern.  

---

#### Q74: 50 TB financial time-series, frequent updates, Hadoop migration

**Question:**  
Store **50 TB time-series** data with **frequent updates/streaming** and migrate existing **Hadoop** jobs.  

**Options:**  
A. <mark>**Cloud Bigtable**</mark>  
B. **BigQuery**  
C. **Cloud Storage**  
D. **Cloud Datastore**  

**Correct Answer:** A  

**Explanation:**  
- **Bigtable** is ideal for **time-series** with high write/read throughput and HBase API compatibility (Dataproc/Hadoop).  
- **BigQuery** is for analytical queries, not frequent row updates.  
- **GCS/Datastore** don’t fit high-throughput time-series writes.  

---

#### Q75: Share aggregates securely across projects with cost isolation

**Question:**  
Expose only **aggregated** BigQuery results to other projects, **hide user-level data**, **minimize storage**, and **bill query cost to the consumer project**.  

**Options:**  
A. <mark>Create and share an **authorized view** that returns aggregates.</mark>  
B. Create/share a new dataset and a view with aggregates.  
C. Create/share a new dataset and a precomputed aggregate **table**.  
D. Grant **dataViewer** IAM on the dataset.  

**Correct Answer:** A  

**Explanation:**  
- **Authorized views** restrict raw data, avoid duplication, and billing goes to the querying project; storage isn’t duplicated.  
- **B/C** add management/storage overhead (and C duplicates data).  
- **D** exposes raw tables.  

---

#### Q76: Where to store data requiring auditable access records

**Question:**  
Regulations require an **auditable record of access** to certain data (assume expiring logs are archived correctly). Where to store the **regulated data**?  

**Options:**  
A. Encrypt in **Cloud Storage** with user-supplied keys; give separate decryption keys.  
B. <mark>Store in a **BigQuery** dataset restricted to authorized users; rely on **Data Access logs** for auditability.</mark>  
C. Store in **Cloud SQL** with separate DB users; use **Admin activity logs**.  
D. Use a **Cloud Storage** bucket only reachable via an App Engine service that logs access before sharing links.  

**Correct Answer:** B  

**Explanation:**  
- **B**: BigQuery’s **Data Access logs** + IAM provide native, fine-grained query/access auditing.  
- **A**: Encryption ≠ access audit trail.  
- **C**: Admin logs cover admin actions, not data read access granularity.  
- **D**: Custom logging adds complexity and is easier to bypass.  

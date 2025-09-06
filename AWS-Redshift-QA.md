# 🎯 Amazon Redshift Interview Q&A 

## 1. Basics
**Q1. What is Amazon Redshift? How is it different from traditional databases?**  
| English | 中文 |
| --- | --- |
| Amazon Redshift is a **PB-scale MPP (Massively Parallel Processing) data warehouse**. | Amazon Redshift 是一个 **PB 级大规模并行处理数据仓库**。 |
| Optimized for **OLAP (analytics)** not OLTP. | 优化于 **分析型查询（OLAP）**，而不是事务型处理（OLTP）。 |
| Uses **columnar storage** for fast scans/aggregations. | 使用 **列式存储**，加速扫描与聚合。 |
| Distributes data across multiple nodes for scalability. | 数据分布在多个节点以实现水平扩展。 |

**Q2. What are the components of a Redshift cluster?**  
| English | 中文 |
| --- | --- |
| **Leader Node**: Accepts queries, parses SQL, creates execution plan, coordinates workers. | **Leader 节点**：接收查询，解析 SQL，生成执行计划并协调执行。 |
| **Compute Nodes**: Store actual data and execute queries in parallel. | **计算节点**：存储实际数据并并行执行查询。 |
| **Node Types**: DC2 (SSD, smaller high-performance) vs RA3 (separated storage, scalable). | **节点类型**：DC2（SSD，小规模高性能） vs RA3（存储计算分离，可扩展）。 |

---

## 2. Storage & Distribution
**Q3. What is a Distribution Key? What distribution styles exist?**  
| English | 中文 |
| --- | --- |
| Defines how table data is distributed across compute nodes. | 定义表数据如何在计算节点间分布。 |
| **KEY**: Hash by a column (avoids data movement in joins). | **KEY**：按列哈希分布（减少 join 数据移动）。 |
| **EVEN**: Even distribution. | **EVEN**：均匀分布。 |
| **ALL**: Full copy on all nodes (small tables). | **ALL**：复制到所有节点（适合小表）。 |
| **AUTO**: Automatic choice (serverless default). | **AUTO**：自动选择（serverless 默认）。 |

**Q4. What is a Sort Key? Difference between Compound vs Interleaved?**  
| English | 中文 |
| --- | --- |
| Sort Key defines the physical storage order. | Sort Key 定义物理存储顺序。 |
| **Compound**: Sequential ordering, good for range filters. | **Compound**：按顺序排序，适合范围查询。 |
| **Interleaved**: Equal weighting of columns, good for multi-dimension filters. | **Interleaved**：多列平等排序，适合多维过滤。 |

**Q5. What is VACUUM in Redshift?**  
| English | 中文 |
| --- | --- |
| Redshift is append-only, deletes/updates leave empty space. | Redshift 是追加写模式，删除/更新会留下空洞。 |
| `VACUUM` reclaims space and re-sorts rows. | `VACUUM` 用于回收空间并重新排序数据。 |
| Improves query performance. | 提升查询性能。 |

---

## 3. Loading & Unloading
**Q6. How to load data from S3 into Redshift?**  
| English | 中文 |
| --- | --- |
| Use `COPY` command to load from S3. | 使用 `COPY` 命令从 S3 加载数据。 |
| Example: `COPY sales FROM 's3://bucket/sales/' IAM_ROLE 'arn:...' FORMAT AS PARQUET;` | 示例：`COPY sales FROM 's3://bucket/sales/' IAM_ROLE 'arn:...' FORMAT AS PARQUET;` |
| Optimizations: `COMPUPDATE OFF`, `STATUPDATE OFF`, `MAXERROR`. | 优化：`COMPUPDATE OFF`、`STATUPDATE OFF`、`MAXERROR`。 |

**Q7. How to unload data from Redshift to S3?**  
| English | 中文 |
| --- | --- |
| Use `UNLOAD` command. | 使用 `UNLOAD` 命令。 |
| Example: `UNLOAD ('SELECT * FROM sales') TO 's3://bucket/output/sales_' IAM_ROLE 'arn:...' FORMAT AS PARQUET;` | 示例：`UNLOAD ('SELECT * FROM sales') TO 's3://bucket/output/sales_' IAM_ROLE 'arn:...' FORMAT AS PARQUET;` |

**Q8. What does ELT mean in Redshift?**  
| English | 中文 |
| --- | --- |
| **Extract → Load → Transform**. | **提取 → 加载 → 转换**。 |
| Load raw data into Redshift, then transform with SQL. | 先加载到 Redshift，再用 SQL 转换数据。 |

---

## 4. Integration & Extensions
**Q9. What is Redshift Spectrum?**  
| English | 中文 |
| --- | --- |
| Query external tables stored in S3 without loading. | 直接查询存储在 S3 的外部表，无需加载。 |
| Supports Parquet/ORC/CSV. | 支持 Parquet/ORC/CSV。 |

**Q10. What is a Federated Query?**  
| English | 中文 |
| --- | --- |
| Allows Redshift to query external RDS/Aurora data. | 允许 Redshift 查询外部 RDS/Aurora 数据。 |

**Q11. Difference between Materialized View and View?**  
| English | 中文 |
| --- | --- |
| **View**: Logical SQL, no stored data, runs each time. | **View**：逻辑 SQL，不存储数据，每次运行实时计算。 |
| **Materialized View**: Stores results, refreshable, faster. | **Materialized View**：存储结果，可刷新，查询更快。 |

**Q12. What is Redshift Data Sharing?**  
| English | 中文 |
| --- | --- |
| Share data across clusters/accounts without duplication. | 跨集群或账户共享数据，无需重复存储。 |
| Read-only access for BI/analytics. | 提供只读访问，适合 BI 分析。 |

---

## 5. Performance & Optimization
**Q13. What is Workload Management (WLM)?**  
| English | 中文 |
| --- | --- |
| Manages query queues, memory, concurrency. | 管理查询队列、内存和并发。 |
| Prevents long queries from blocking short queries. | 避免长查询阻塞短查询。 |

**Q14. Difference between Concurrency Scaling and SQA?**  
| English | 中文 |
| --- | --- |
| **Concurrency Scaling**: Adds temporary clusters for high concurrency. | **并发扩展**：为高并发增加临时集群。 |
| **SQA**: Optimizes sub-second queries. | **SQA**：优化亚秒级查询。 |

**Q15. How to optimize Redshift performance?**  
| English | 中文 |
| --- | --- |
| Choose proper Distribution Key / Sort Key. | 选择合适的 Distribution Key / Sort Key。 |
| Avoid data skew. | 避免数据倾斜。 |
| Use compression (Encoding). | 使用列压缩。 |
| Run `VACUUM` and `ANALYZE`. | 定期运行 `VACUUM` 与 `ANALYZE`。 |
| Use Materialized Views / Spectrum. | 使用物化视图或 Spectrum。 |

---

## 6. Security & Access
**Q16. What are Redshift’s security features?**  
| English | 中文 |
| --- | --- |
| Network: VPC, Security Groups. | 网络：VPC、安全组。 |
| Authentication: IAM Role, DB users. | 认证：IAM 角色、数据库用户。 |
| Encryption: KMS, SSL/TLS. | 加密：KMS、SSL/TLS。 |
| Auditing: CloudTrail, logs. | 审计：CloudTrail、日志。 |

**Q17. How to implement fine-grained access control?**  
| English | 中文 |
| --- | --- |
| Row-Level / Column-Level Security. | 行级 / 列级安全。 |
| Lake Formation permissions. | 结合 Lake Formation 权限。 |

---

## 7. Advanced & Scenario Questions
**Q18. Design an e-commerce analytics warehouse in Redshift.**  
| English | 中文 |
| --- | --- |
| **Fact Table**: fact_sales (order_id, user_id, product_id, price, qty, date_id). | **事实表**：fact_sales (order_id, user_id, product_id, price, qty, date_id)。 |
| **Dimensions**: dim_user, dim_product, dim_date. | **维度表**：dim_user, dim_product, dim_date。 |
| Distribution: user_id or product_id. | 分布键：user_id 或 product_id。 |
| Sort Key: date_id. | 排序键：date_id。 |

**Q19. COPY command is slow, how to troubleshoot?**  
| English | 中文 |
| --- | --- |
| Check file sizes (~1GB chunks recommended). | 检查文件大小（推荐 ~1GB）。 |
| Parallel load matching node slices. | 并行加载，与节点数匹配。 |
| Disable auto compression/statistics. | 关闭自动压缩和统计更新。 |
| Use compressed formats (Parquet/ORC). | 使用压缩格式（Parquet/ORC）。 |

**Q20. Compare Redshift vs Snowflake vs BigQuery.**  
| English | 中文 |
| --- | --- |
| **Redshift**: AWS ecosystem, Spectrum, Serverless. | **Redshift**：AWS 生态，支持 Spectrum 和 Serverless。 |
| **Snowflake**: Cloud-native, separation of storage & compute. | **Snowflake**：云原生，存储与计算分离，多云支持。 |
| **BigQuery**: Fully serverless, pay-per-query, GCP ecosystem. | **BigQuery**：全托管，按查询计费，GCP 生态。 |

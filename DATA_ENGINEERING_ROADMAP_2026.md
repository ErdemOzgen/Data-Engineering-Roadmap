# Data Engineering Roadmap 2026

This roadmap assumes you are already a software engineer. It prioritizes production data platform work: reliable ingestion, lakehouse storage, orchestration, SQL transformation, data quality, observability, cloud security, and cost-aware operation.

## 1. Roadmap Modernization

### Priority Map

| Category | Must Know | Good to Know | Optional | Outdated / Lower Priority |
|---|---|---|---|---|
| Engineering fundamentals | Git, HTTP, APIs, auth basics, Docker, CI/CD, testing, semantic versioning, dependency management, logging, SOLID/KISS/YAGNI | Kubernetes basics, Scrum/Kanban, interface design, OOP tradeoffs | Deep algorithms for interviews | Framework-heavy OOP as default design style |
| Languages | Python, SQL | Java or Scala for JVM data engines, Go for tooling/services | R for analytics, JavaScript for dashboards | Learning all Python/Java/Scala/Go equally |
| Python ecosystem | `uv`, `pyproject.toml`, typing, pytest, ruff, mypy/pyright, pandas, Polars, PyArrow, Pydantic, SQLAlchemy, Click/Typer | multiprocessing, async IO, packaging, CLI design | Poetry if a company standard | unpinned `pip install`, notebooks as production jobs |
| SQL and databases | PostgreSQL, analytical SQL, query plans, indexes, transactions, partitions, materialized views | MySQL/MariaDB, SQL Server | Stored procedures by platform | Treating SQL as only beginner CRUD |
| Operational databases | PostgreSQL, Redis, MongoDB basics | Cassandra for wide-column scale, Neo4j for graph use cases | CouchDB | HBase unless supporting legacy Hadoop estates |
| Warehouses and OLAP | BigQuery, Snowflake, Redshift, Databricks SQL, ClickHouse | DuckDB for local analytics | Synapse/Fabric depending on Azure shop | On-prem MPP unless required |
| Storage and lakehouse | S3/GCS/Azure Blob, Parquet, Iceberg, Delta Lake, partitioning, compaction, schema evolution | Hudi for CDC-heavy lakehouses, table catalogs | Raw CSV/JSON archives only for landing | HDFS-first design, Hive-only lake |
| Transformation | dbt, SQL modeling, incremental models, snapshots, semantic layer awareness | Spark SQL, Dataform on GCP, stored transformations when justified | GUI ETL | Pig |
| Orchestration | Airflow, Dagster, Prefect concepts, retries, backfills, SLAs | Managed Airflow, sensors, asset-aware orchestration | Cron for tiny jobs | Jenkins as primary orchestrator |
| Batch processing | Spark DataFrames/SQL, DuckDB, Polars, DataFusion awareness | Beam for portable runners | Hadoop MapReduce internals | Handwritten MapReduce |
| Streaming | Kafka, Kafka Connect, schema registry, consumer groups, Flink, CDC with Debezium | Kafka Streams, Spark Structured Streaming, Kinesis/Pub/Sub/Event Hubs | ActiveMQ/RabbitMQ for app messaging | Lambda architecture by default |
| Data quality | Great Expectations, Soda, dbt tests, contracts, freshness, schema drift | Deequ, metadata-driven checks | Custom-only frameworks | Testing only row counts |
| Observability and governance | OpenLineage, DataHub/OpenMetadata, Prometheus, Grafana, OpenTelemetry, Datadog/Sentry, audit logs | Monte Carlo/Bigeye-style managed platforms | Full enterprise governance suites for solo projects | Logs with no metrics/lineage |
| Cloud and IaC | IAM, KMS, VPC/networking basics, Terraform, GitHub Actions OIDC, cost controls | Kubernetes, Helm, managed Spark, managed streaming | Multi-cloud deep expertise at once | Manual cloud console deployment |
| Visualization | BI table design, metrics layers, Looker/Power BI/Tableau basics | Streamlit/Superset/Metabase for portfolio | Jupyter for exploration | Dashboards without governed models |
| ML/MLOps add-on | Feature pipelines, MLflow basics, model data validation, vector/embedding pipelines | SageMaker/Kubeflow/TFX if ML platform role | TensorFlow/Keras/PyTorch depth | Treating ML frameworks as core DE |

### What Changed Since a 2022 Roadmap

| Shift | 2022 emphasis | 2026 emphasis |
|---|---|---|
| Hadoop | Hadoop, HDFS, Hive, MapReduce still common in roadmaps | Cloud object storage plus open table formats; know Hadoop mainly for legacy context |
| Pipelines | ETL tools and Airflow DAGs | ELT, asset-aware orchestration, contracts, lineage, backfills, quality gates |
| Lake | Data lake as files | Lakehouse tables with ACID, schema evolution, time travel, compaction, catalogs |
| Python | pandas and virtualenv | `uv`, `pyproject.toml`, typed packages, Polars, PyArrow, production CLIs |
| Batch | Spark everywhere | Spark for large distributed jobs; DuckDB/Polars for local and medium jobs |
| Streaming | Kafka plus micro-batch | Kafka/Flink/CDC/event-time semantics, schema registry, lag and replay design |
| Governance | Optional metadata | Catalog, ownership, lineage, PII classification, retention, access policies |
| Operations | Job success/failure | Freshness, volume, schema drift, null rates, cost, SLA, lineage, incident response |
| CI/CD | Jenkins | GitHub Actions/GitLab CI, container scanning, OIDC cloud deploys, Terraform |
| Cloud | Learn AWS/GCP/Azure services | Learn cloud-neutral primitives first, then map to managed services |

### Modern Topics To Add

Must know: lakehouse, Parquet, Iceberg or Delta, dbt, Airflow/Dagster/Prefect, DuckDB, Polars, PyArrow, Great Expectations/Soda, OpenLineage, DataHub/OpenMetadata, Terraform, GitHub Actions, OpenTelemetry, IAM, KMS, secrets management, data contracts, cost optimization.

Good to know: Hudi, Debezium, Kafka Connect, schema registry, Trino, DataFusion, Kubernetes operators, managed observability, FinOps tagging, feature stores, vector databases.

## 2. Core Skill Progression: 16 Weeks

| Week | Goal | Concepts | Hands-on tasks | Mini project | Tools | GitHub output | Interview skills |
|---|---|---|---|---|---|---|---|
| 1 | Production Python baseline | `pyproject.toml`, `uv`, typing, logging, config, CLI | Create package, lint/test/typecheck CI | CSV/API ingestor CLI | uv, ruff, pytest, Typer, Pydantic | `src/`, tests, Makefile, CI badge | Package and test a Python data tool |
| 2 | SQL foundations refresh | joins, CTEs, aggregation, window functions | Load sample data, answer analytics questions | Postgres analytics workbook | Postgres, DuckDB | SQL scripts plus answers | Explain joins/window functions under pressure |
| 3 | Database internals for DE | indexes, EXPLAIN, transactions, isolation | Compare plans, tune slow query | Query tuning lab | PostgreSQL | before/after plans | Diagnose slow analytical/OLTP queries |
| 4 | File formats and local OLAP | CSV vs JSON vs Parquet, partitioning, Arrow | Convert raw files, benchmark scans | Local lake with DuckDB/Polars | DuckDB, Polars, PyArrow | benchmark notebook/script | Choose file format and partition strategy |
| 5 | Batch ingestion | idempotency, watermarks, retries, schema validation | Pull API data incrementally | Raw-to-bronze ingestion | Python, S3-compatible MinIO | docker-compose, ingestion jobs | Design idempotent batch ingestion |
| 6 | Transformation modeling | ELT, dbt models, tests, snapshots, docs | Build staging/intermediate/marts | dbt sales mart | dbt, Postgres/DuckDB | dbt docs, tests, lineage | Model dimensions/facts incrementally |
| 7 | Orchestration | DAGs/assets, schedules, retries, backfills | Orchestrate ingestion + dbt + checks | Daily analytics pipeline | Airflow or Dagster | runnable orchestrator | Explain retries, catchup, backfills |
| 8 | Data quality | contracts, freshness, nulls, uniqueness, drift | Add quality gates and failure behavior | Quality-guarded mart | GX/Soda/dbt tests | check configs, failing examples | Define meaningful DQ checks |
| 9 | Lakehouse tables | Iceberg/Delta, catalogs, snapshots, compaction | Write partitioned Parquet/Iceberg tables | Bronze/silver/gold lakehouse | Spark, Iceberg or Delta | table maintenance scripts | Explain ACID on object storage |
| 10 | Spark | DataFrames, joins, shuffle, caching, partitioning | Optimize Spark job | Large batch transform | PySpark | Spark job, metrics notes | Debug skew/shuffles/resource use |
| 11 | Kafka fundamentals | topics, partitions, offsets, consumer groups | Produce/consume events, replay | Event ingestion service | Kafka, Redpanda, schema registry | docker-compose + consumers | Explain ordering, replay, delivery guarantees |
| 12 | Streaming processing | event time, windows, state, checkpoints | Aggregate events to serving table | Streaming metrics pipeline | Flink or Spark Structured Streaming | stream processor + tests | Discuss late data and exactly-once tradeoffs |
| 13 | CDC | binlog/WAL, Debezium, schema evolution | Replicate Postgres changes to lake/warehouse | CDC order pipeline | Debezium, Kafka Connect | connector configs | Design CDC with deletes and replays |
| 14 | Observability | SLIs, lineage, metrics, logs, traces | Add pipeline metrics and lineage | Observable pipeline | OpenLineage, Prometheus, Grafana | dashboards, alert rules | Define pipeline SLOs and incident signals |
| 15 | Cloud and IaC | IAM, object storage, warehouse, secrets, cost | Deploy one pipeline to cloud | Cloud lakehouse slice | Terraform, GitHub Actions | `infra/`, OIDC workflow | Explain least privilege and cost controls |
| 16 | Capstone hardening | runbooks, backfills, CI/CD, security, docs | Load test, break/fix, document operations | Portfolio-grade platform | Full stack | architecture docs, runbook, demo | System design for data platforms |

## 3. Modern Data Engineering Stack

### Recommended Practical Stack

| Layer | Default choice | Why |
|---|---|---|
| Local dev | Docker Compose, Make, direnv, pre-commit | Reproducible developer workflow |
| Python env | `uv`, `pyproject.toml`, ruff, pytest, mypy/pyright | Fast dependency management and production hygiene |
| SQL dev | PostgreSQL, DuckDB | OLTP realism plus fast local OLAP |
| Storage | MinIO locally; S3/GCS/Blob in cloud; Parquet | Mirrors cloud object storage cheaply |
| Table format | Iceberg or Delta Lake | ACID, schema evolution, snapshots, time travel |
| Batch | Spark for large data; DuckDB/Polars for local/medium data | Avoid distributed systems when one process is enough |
| Streaming | Kafka/Redpanda plus Flink for stateful processing | Replayable log plus event-time processing |
| Orchestration | Airflow for standard scheduled workflows; Dagster for asset-centric projects; Prefect for Python-first teams | Pick by team and workflow shape |
| Transformation | dbt | Versioned SQL models, tests, docs, lineage |
| Quality | dbt tests + GX or Soda | Lightweight model checks plus richer validation |
| Observability | OpenLineage, DataHub/OpenMetadata, Prometheus/Grafana, OpenTelemetry, Sentry/Datadog | Data and system observability together |
| CI/CD | GitHub Actions, Docker buildx, Trivy/Dependabot, Terraform | Test, scan, deploy, provision |
| Deployment | Cloud managed services first; Kubernetes only when needed | Lower operational burden |

### Language Comparison

| Language | Use it for | Avoid using it for |
|---|---|---|
| Python | Ingestion, orchestration, dbt tooling, Spark jobs, APIs, CLIs, quality checks | Ultra-low-latency services without careful design |
| Java | Kafka/Flink/Spark production internals, high-throughput services | Fast solo iteration if Python is enough |
| Scala | Spark-heavy platforms, functional JVM data pipelines | New greenfield teams without Scala experience |
| Go | Lightweight services, CLIs, exporters, infra tooling | Spark/Flink ecosystem work where JVM/Python wins |

### Orchestration

| Tool | Best for | Tradeoffs |
|---|---|---|
| Airflow | Scheduled batch workflows, broad integrations, managed cloud offerings | Not designed for continuous streaming; DAG authoring can get boilerplate-heavy |
| Dagster | Asset-aware pipelines, lineage, tests, partitioned assets, data platform teams | Smaller ecosystem than Airflow, requires asset-model thinking |
| Prefect | Python-native flows, flexible deployments, quick operationalization | Less warehouse/lakehouse convention than dbt + Airflow/Dagster stacks |

### Processing

| Tool | Best for | Notes |
|---|---|---|
| Spark | Large batch, SQL/DataFrames, lakehouse writes, mature ecosystem | Learn joins, shuffles, partitioning, file sizing, checkpoints |
| Flink | Stateful low-latency streaming, event time, exactly-once style processing | Higher learning curve; excellent for real-time products |
| Beam | Portable pipeline model across runners | Useful in GCP/Dataflow shops; less common for local portfolios |
| Kafka Streams | JVM microservices doing stream processing near Kafka | Great for app-owned streams; less general than Flink |

### Warehouses / OLAP

| Platform | Best fit |
|---|---|
| Snowflake | Cross-cloud warehouse, governance, semi-structured data, enterprise BI |
| BigQuery | Serverless analytics, GCP-native, event data, low-ops SQL analytics |
| Redshift | AWS-native warehouse, Redshift Serverless, S3/Athena/Glue integration |
| Databricks | Lakehouse, Spark, Delta, ML/AI workloads, notebooks plus jobs |
| ClickHouse | Real-time OLAP, logs/events, high-concurrency analytical APIs |

### Databases

| Database | Use when |
|---|---|
| PostgreSQL | Default relational source/serving DB, transactional consistency, rich SQL |
| MongoDB | Flexible document model and app-centric JSON workloads |
| Cassandra | Massive write scale, predictable key-based access, multi-region needs |
| Redis | Cache, rate limits, ephemeral state, stream-like lightweight queues |
| Neo4j | Graph traversals are first-class business logic |

### Storage and Table Formats

| Choice | Use when |
|---|---|
| S3/GCS/Azure Blob | Durable cloud object storage for raw and curated data |
| Iceberg | Open lakehouse standard, multi-engine access, schema/partition evolution, catalogs |
| Delta Lake | Databricks-centered lakehouse or Spark-first teams needing mature Delta features |
| Hudi | Upserts, CDC ingestion, incremental pulls into lake storage |

## 4. Six Portfolio-Grade Projects

### Project 1: Production Batch API to Warehouse

Description: ingest public API data, validate it, store raw files, transform to analytics tables, and expose BI-ready marts.

Architecture: API -> Python ingestion -> object storage raw -> dbt staging/marts -> Postgres/DuckDB/BigQuery -> dashboard.

Data sources: OpenWeather, GitHub, NYC taxi, OpenAQ, or SEC company facts.

Design: batch incremental with watermarks, idempotent writes, retryable API client, raw JSON archive.

Storage: MinIO/S3 raw JSON and Parquet; warehouse tables for marts.

Transformation: dbt staging, intermediate normalization, mart tables.

Orchestration: Airflow or Dagster daily schedule.

Quality: schema validation with Pydantic, dbt unique/not-null/relationships, GX freshness/volume checks.

Monitoring: job status, duration, row counts, freshness, API error rate, Slack/email alert.

Security: API keys in secrets, no secrets in logs, least-privilege bucket/database user.

Docker/local: Postgres, MinIO, orchestrator, app container.

Cloud: S3 + Glue/Athena or GCS + BigQuery or Blob + Fabric/Synapse.

Repo structure:

```text
api-warehouse-pipeline/
  src/ingestion/
  dags/ or defs/
  dbt/
  quality/
  infra/
  docker-compose.yml
  tests/
  docs/architecture.md
```

Proves: idempotent ingestion, SQL modeling, orchestration, quality, CI.

### Project 2: Lakehouse Medallion Pipeline

Description: build bronze/silver/gold tables over raw events using Iceberg or Delta.

Architecture: raw files -> Spark/Polars bronze -> cleaned silver -> aggregated gold -> Trino/DuckDB/Spark SQL.

Data sources: NYC taxi, e-commerce events, public crypto trades.

Design: batch partitions by event date, schema evolution, compaction job, backfill command.

Storage: MinIO/S3 with Parquet and Iceberg/Delta metadata.

Transformation: Spark SQL/DataFrames, optional dbt on Spark/Trino.

Orchestration: Dagster assets with partitions or Airflow DAG with backfill params.

Quality: bronze schema checks, silver dedupe, gold reconciliation totals.

Monitoring: partition freshness, file counts, small-file count, failed compaction.

Security: bucket prefixes by layer, KMS in cloud, IAM role per job.

Cloud: EMR/Glue + Iceberg, Dataproc/BigQuery external tables, Databricks + Delta.

Proves: lakehouse design, Spark optimization, partitioning, table maintenance.

### Project 3: CDC to Analytics

Description: replicate operational Postgres changes into Kafka, lakehouse, and analytics marts.

Architecture: Postgres WAL -> Debezium -> Kafka -> sink to Iceberg/warehouse -> dbt marts.

Data sources: synthetic orders/payments app.

Design: streaming CDC with tombstones, schema registry, replayable topics, daily reconciliation.

Storage: Kafka topics plus Iceberg/Hudi/Delta change tables.

Transformation: stream normalization, dbt incremental marts.

Orchestration: Kafka Connect configs plus Airflow/Dagster for reconciliation and dbt.

Quality: source-to-target counts, delete handling tests, late update tests.

Monitoring: connector status, lag, dead-letter records, schema compatibility failures.

Security: TLS/SASL for Kafka in cloud, DB replication user least privilege.

Cloud: MSK/Kinesis + Glue/Iceberg, Pub/Sub/Dataflow/BigQuery, Event Hubs/ADF/Fabric.

Proves: CDC, streaming ingestion, data consistency, operational debugging.

### Project 4: Real-Time Clickstream Analytics

Description: process clickstream events into near-real-time product metrics.

Architecture: event generator -> Kafka -> Flink -> ClickHouse/Postgres serving -> Grafana dashboard.

Design: event-time windows, late data, dedupe by event ID, checkpointed state.

Storage: Kafka retention plus ClickHouse rollups plus raw lake archive.

Quality: schema registry, event contract tests, null/duplicate/volume alerts.

Monitoring: Kafka lag, Flink checkpoints, throughput, failed events, dashboard freshness.

Security: producer auth, PII minimization, IP/user-agent hashing.

Cloud: Confluent/MSK + Managed Flink + ClickHouse Cloud/Redshift/BigQuery.

Proves: Kafka, Flink, event-time reasoning, real-time OLAP.

### Project 5: Data Observability and Governance Platform Slice

Description: instrument existing batch/lakehouse pipelines with lineage, catalog metadata, quality, and alerts.

Architecture: Airflow/Dagster -> OpenLineage -> Marquez/DataHub -> GX/Soda -> Grafana/Datadog.

Data sources: reuse Projects 1 and 2.

Design: metadata emission on every job, asset ownership, column docs, incidents and runbooks.

Storage: DataHub metadata store, Prometheus metrics, warehouse audit tables.

Quality: freshness, volume anomaly, schema drift, PII tag checks.

Monitoring: SLA dashboard, lineage graph, failed job traces, quality history.

Security: catalog auth, audit logs, redact samples, classify PII columns.

Cloud: DataHub on ECS/GKE/AKS or managed catalog equivalents.

Proves: production operation, governance, observability, incident maturity.

### Project 6: AI/ML Feature and Embedding Pipeline

Description: build reliable data pipelines for model features and vector search without pretending to be a full ML engineer.

Architecture: raw documents/events -> cleaning -> feature tables -> MLflow registry metadata -> vector DB -> retrieval API.

Data sources: product catalog, docs, support tickets, ecommerce behavior.

Design: batch feature generation plus incremental embedding updates.

Storage: lakehouse feature tables, Postgres/Redis/Feast optional online store, pgvector/Qdrant/Weaviate.

Transformation: Python, Spark/Polars, dbt for feature marts.

Orchestration: Dagster or Airflow with model/data version metadata.

Quality: embedding coverage, duplicate documents, feature nulls, training-serving skew checks.

Monitoring: feature freshness, vector index size, retrieval latency, cost per embedding batch.

Security: PII redaction before embeddings, model/API key secrets, access control to vectors.

Cloud: SageMaker/Vertex AI/Azure ML only as an add-on.

Proves: ML-adjacent DE, feature pipelines, vector data, production AI data hygiene.

## 5. Production Architecture Patterns

| Pattern | Practical meaning | Example |
|---|---|---|
| ETL | Transform before loading target | Clean PII and normalize vendor files before loading regulated warehouse |
| ELT | Load raw first, transform in warehouse/lakehouse | Land raw JSON to S3, transform with dbt in BigQuery |
| Batch pipeline | Finite scheduled processing | Daily orders snapshot -> revenue mart |
| Streaming pipeline | Continuous event processing | Click events -> Kafka -> Flink -> ClickHouse dashboard |
| CDC pipeline | Changes from DB logs | Postgres WAL -> Debezium -> Kafka -> Iceberg |
| Lakehouse | Object storage plus table format/catalog | S3 + Iceberg + Spark/Trino/dbt |
| Medallion | Bronze raw, silver cleaned, gold business-ready | `bronze.orders_raw`, `silver.orders`, `gold.daily_revenue` |
| Lambda | Batch truth plus speed layer | Large historical recomputation plus real-time dashboard correction |
| Kappa | Stream log as source of truth | Replay Kafka topics to rebuild derived tables |
| Event-driven | Services communicate via events | Payment succeeded event triggers fraud and analytics consumers |
| Data mesh | Domain-owned data products | Finance owns `revenue_events` contract and SLA |
| Data warehouse | Curated analytical store | Snowflake star schemas for BI |
| Data mart | Department-specific subset | Marketing campaign performance mart |
| Feature store | Reusable ML features online/offline | `customer_30d_spend` for training and serving |
| Reverse ETL | Warehouse data back to apps | Sync customer segments to CRM |

## 6. SQL and Database Mastery

### SQL Roadmap

| Level | Topics | Exercises |
|---|---|---|
| Beginner | SELECT, WHERE, GROUP BY, HAVING, JOINs, NULLs, dates, CTEs | Build 30 business queries on orders/customers/payments |
| Intermediate | window functions, subqueries, set ops, dedupe, slowly changing dimensions, pivoting, JSON fields | Create cohort retention, sessionization, top-N per group, late-arriving facts |
| Advanced | EXPLAIN, indexes, partitions, materialized views, transactions, locks, isolation, query rewrites, stored procedures | Tune five slow queries, design partitioning, prove isolation anomalies |
| Production | warehouse modeling, incremental loads, reconciliation, data contracts, cost-aware SQL | Build marts with tests, snapshots, backfills, and cost notes |

PostgreSQL exercises: design an order schema, load 10M synthetic rows, add B-tree/BRIN indexes, compare `EXPLAIN ANALYZE`, test `READ COMMITTED` vs `REPEATABLE READ`, create monthly partitions, refresh materialized views, implement upsert-based incremental loading.

Analytical SQL exercises: revenue fact table, customer dimension, SCD2 history, cohort retention, funnel conversion, rolling 7/30-day metrics, sessionization, anomaly query, duplicate detection, reconciliation between source and mart.

Production expectation: you should be able to design schemas, write complex analytical SQL, reason about query plans, debug wrong numbers, create incremental models, avoid fanout bugs, and explain transaction/locking behavior well enough to avoid corrupting pipelines.

## 7. Python for Data Engineering

### Learning Path

| Area | What to learn | Production proof |
|---|---|---|
| Files and APIs | streaming downloads, pagination, retries, rate limits, gzip, JSONL/CSV/Parquet | resilient ingestion client |
| Types and validation | typing, Pydantic, dataclasses, schemas | typed records and config validation |
| Packaging | `pyproject.toml`, `uv`, src layout, console scripts | installable package and CLI |
| DataFrames | pandas for common analytics, Polars for fast local transforms, PyArrow for columnar IO | benchmarked transform script |
| Databases | SQLAlchemy Core, psycopg, transactions, COPY | safe database loader |
| Concurrency | async IO for network-bound work, multiprocessing for CPU-bound tasks | parallel API/file ingestion |
| Logging | structured logs, correlation IDs, no secret leakage | machine-readable job logs |
| Testing | pytest, fixtures, testcontainers or Docker services, golden files | unit + integration tests in CI |
| CLI | Typer/Click, commands for ingest/backfill/validate | operator-friendly commands |

### Production Python Structure

```text
data-platform-project/
  pyproject.toml
  uv.lock
  src/data_platform/
    __init__.py
    config.py
    logging.py
    cli.py
    ingestion/
      api_client.py
      loaders.py
      schemas.py
    transforms/
      orders.py
    quality/
      checks.py
  tests/
    unit/
    integration/
  scripts/
  docker/
  .github/workflows/ci.yml
```

Example commands:

```bash
uv init --package
uv add pydantic sqlalchemy psycopg pyarrow polars typer structlog
uv add --dev pytest ruff mypy
uv run ruff check .
uv run pytest
uv run data-platform ingest --source orders --since 2026-01-01
```

## 8. Pipeline Implementation Guide

Design target: raw source to analytics-ready table.

1. Define contract: source owner, schema, expected volume, freshness SLA, PII classification.
2. Ingest raw: immutable landing path, idempotent filename, checksum, source timestamp.
3. Validate raw: parseability, required fields, schema version, duplicate file detection.
4. Normalize bronze: convert to Parquet, add load metadata, partition by ingestion date.
5. Transform silver: dedupe, type cast, conform keys, handle deletes/updates.
6. Build gold: business metrics, dimensional models, marts, aggregates.
7. Partition/storage: choose event date for query pruning; compact small files.
8. Orchestrate: explicit dependencies, retries with exponential backoff, catchup/backfill params.
9. Monitor: freshness, volume, schema drift, nulls, duplicates, job duration, cost.
10. Backfill: parameterized date ranges, isolated temp writes, reconciliation before publish.

Example structure:

```text
pipeline/
  src/
  dbt/
  quality/
  orchestration/
  data_contracts/orders.yml
  infra/
  docs/runbook.md
```

Example commands:

```bash
make up
uv run pipeline ingest orders --start 2026-01-01 --end 2026-01-31
uv run pipeline validate bronze/orders --date 2026-01-31
uv run dbt build --select tag:orders
uv run pipeline reconcile orders --date 2026-01-31
uv run pipeline backfill orders --start 2025-01-01 --end 2025-12-31 --dry-run
```

## 9. Security and Governance

Must know checklist:

- IAM: separate human and workload identities; deny-by-default; use cloud roles, not static keys.
- Least privilege: job role can read source path and write target path only.
- Encryption at rest: KMS-managed buckets, warehouse encryption, encrypted volumes.
- Encryption in transit: TLS for DB, Kafka, APIs, warehouse connections.
- Secrets: cloud secret manager or Vault; never `.env` in Git; rotate credentials.
- PII: classify, minimize, hash/tokenize, mask in non-prod, redact logs.
- GDPR awareness: lawful basis, right to delete, retention, data subject access workflows.
- Access control: RBAC/ABAC, row/column-level policies for sensitive marts.
- Audit logging: who accessed data, what job changed data, which deployment wrote it.
- Retention: lifecycle policies for raw data, legal holds, deletion workflows.
- Docker security: slim images, non-root users, pinned versions, vulnerability scanning.
- Dependency scanning: Dependabot, pip-audit/OSV, Trivy, SBOMs.
- Supply chain: signed images, GitHub Actions OIDC, protected branches, artifact attestations.

## 10. Observability and Reliability

Monitor four layers:

| Layer | Metrics |
|---|---|
| Job | success/failure, duration, retries, queue time, logs, exception class |
| Data | freshness, volume, null rate, duplicate rate, schema drift, distribution drift, reconciliation |
| Streaming | consumer lag, throughput, checkpoint health, late events, dead-letter rate |
| Platform/cost | CPU/memory, shuffle spill, warehouse credits/slots, object storage growth, small files |

Recommended tools:

| Need | Tools |
|---|---|
| Metrics/dashboards | Prometheus, Grafana, Datadog |
| App errors | Sentry, Datadog APM |
| Traces/logs | OpenTelemetry, cloud logging |
| Data quality | Great Expectations, Soda, dbt tests |
| Lineage | OpenLineage, Marquez, DataHub, OpenMetadata |
| Catalog/governance | DataHub, OpenMetadata, cloud catalogs |

Reliability practices: define SLAs and SLOs, create runbooks, page only on user-impacting failures, make backfills safe, store raw data immutably, design every job to be idempotent, and track cost as an operational metric.

## 11. Cloud Learning Path

Cloud-agnostic order: object storage -> IAM/KMS/secrets -> compute/jobs -> warehouse/query engine -> streaming -> orchestration -> catalog/governance -> monitoring -> IaC -> cost optimization.

| Capability | AWS | Google Cloud | Azure |
|---|---|---|---|
| Storage | S3 | Cloud Storage | Blob Storage / ADLS Gen2 |
| Warehouse | Redshift, Athena | BigQuery | Synapse, Fabric Warehouse |
| Spark/compute | EMR, Glue, EKS | Dataproc, Dataflow | Databricks, Synapse Spark, HDInsight legacy |
| Orchestration | MWAA, Step Functions, Glue Workflows | Cloud Composer, Workflows | Data Factory, Managed Airflow, Fabric pipelines |
| Streaming | MSK, Kinesis, Managed Flink | Pub/Sub, Dataflow | Event Hubs, Stream Analytics |
| Catalog/governance | Glue Catalog, Lake Formation, DataZone | Dataplex, Data Catalog | Purview |
| IAM/secrets | IAM, KMS, Secrets Manager | IAM, Cloud KMS, Secret Manager | Entra ID, Key Vault |
| Monitoring | CloudWatch, X-Ray | Cloud Monitoring/Logging/Trace | Azure Monitor, Application Insights |
| Deployment | Terraform, CDK, ECS/EKS/Lambda | Terraform, Cloud Run/GKE | Terraform, Container Apps/AKS/Functions |

## 12. MLOps and AI Add-On

Useful for data engineers: feature tables, offline/online consistency, training data snapshots, model input validation, vector/embedding pipelines, data lineage for models, MLflow tracking/registry basics, batch inference pipelines.

Machine learning engineering owns: model architecture, training loops, hyperparameter tuning, evaluation methodology, deployment strategies, GPU optimization, model monitoring beyond data health.

Optional tools unless your role touches ML platforms: SageMaker, Vertex AI, Azure ML, Kubeflow, TFX, Feast, MLflow, vector databases like pgvector/Qdrant/Weaviate/Pinecone.

High-value AI-era DE project: source documents -> PII redaction -> chunking -> embeddings -> vector index -> retrieval evaluation -> freshness and deletion pipeline.

## 13. Evaluation Rubric

| Level | Knowledge expected | Hands-on proof | GitHub proof | Interview proof | Production proof |
|---|---|---|---|---|---|
| Beginner | SQL joins, Python scripts, Docker basics, simple APIs | Load data into Postgres and query it | Scripts, README, basic tests | Explain ETL, joins, batch jobs | Can maintain a small scheduled job |
| Intermediate | dbt, orchestration, incremental loads, indexes, Parquet, quality checks | End-to-end batch pipeline | Docker Compose, CI, dbt docs, quality checks | Design batch pipeline with retries/backfill | Owns daily pipelines with alerts |
| Advanced | Spark, streaming, CDC, lakehouse, IAM, observability, query tuning | Lakehouse + streaming or CDC project | infra, runbooks, dashboards, tests | Data platform system design | Handles incidents, cost, schema changes |
| Production Ready | Multi-team platform design, governance, SLAs, cost/security tradeoffs | Capstone deployed to cloud with IaC | polished architecture docs, CI/CD, monitoring | Defends tradeoffs and failure modes | Designs and operates reliable governed platforms |

## 14. Milestones

By week 4: local Python/SQL/dataframe foundation with tests and benchmarks.

By week 8: production-style batch ELT project with orchestration, dbt, quality, and CI.

By week 12: lakehouse or streaming pipeline with real operational metrics.

By week 16: cloud-deployed capstone with IaC, security, observability, docs, runbooks, and demo data.

## Reference Commands

```bash
# local services
docker compose up -d postgres minio kafka

# Python quality gate
uv run ruff check .
uv run mypy src
uv run pytest

# dbt
uv run dbt deps
uv run dbt build --select state:modified+
uv run dbt docs generate

# Terraform
terraform fmt -recursive
terraform validate
terraform plan

# Spark local
uv run spark-submit jobs/orders_to_iceberg.py --date 2026-01-01
```

## Sources Checked

- Apache Airflow: https://airflow.apache.org/docs/apache-airflow/stable/index.html
- Dagster: https://docs.dagster.io/
- Prefect: https://docs.prefect.io/v3/get-started
- Apache Iceberg: https://iceberg.apache.org/docs/latest/
- Delta Lake: https://docs.delta.io/
- Apache Hudi: https://hudi.apache.org/docs/overview/
- dbt: https://docs.getdbt.com/docs/introduction
- Apache Spark: https://spark.apache.org/docs/latest/
- Apache Flink: https://nightlies.apache.org/flink/flink-docs-stable/
- Apache Beam: https://beam.apache.org/documentation/
- Kafka Streams: https://kafka.apache.org/documentation/streams/
- Great Expectations: https://docs.greatexpectations.io/docs/core/introduction/
- Soda: https://docs.soda.io/
- OpenLineage: https://openlineage.io/docs/
- DataHub: https://docs.datahub.com/docs/
- Terraform: https://developer.hashicorp.com/terraform/docs
- GitHub Actions: https://docs.github.com/en/actions
- uv: https://docs.astral.sh/uv/
- AWS Analytics overview: https://docs.aws.amazon.com/whitepapers/latest/aws-overview/analytics.html

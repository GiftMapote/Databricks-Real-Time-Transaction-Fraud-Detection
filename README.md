# Databricks-Real-Time-Transaction-Fraud-Detection
The project is about proactively stopping fraudulent banking transactions in real-time instead of reporting back on fraud cases that took place. The projects detects and reports the transaction in real time.

## Executive Summary
This is a production-grade, end-to-end data pipeline built on the **Databricks Lakehouse** to identify and quarantine fraudelent banking transactions in real-time. This project leverages behavioral fingerprinting and stateful streaming to reduce financial loss and improve system reliability.

## Busines Problem Statement
Legacy banking systems often rely on batch processing, leading to significant **detection latency (6+ hours)**. This system addresses that gap by implementing a **sub-second real-time architecture**, allowing the institution to block fraudulent transfers before funds are moved. 

## Architecture Design
This project follows the **Medallion Architecture** to ensure a governed and auditable data flow:

* **Bronze(Raw)**: Continous ingestion of synthetic API events via **Databricks Auto Loader** with schema evolution.
* **Silver(Enrinched)**: High Integrity data cleansing using **Delta Live Tables (DLT) Expectations** to quarantine malformed or suspicious records.
* **Gold(Behavioral)**: Business-level aggregates (e.g., transaction velocity, device dismatch )used for real-time alerting and historical reporting

## Tech Stack Decision

| Component | Choice | Rationable (The "why"|
|----------|----------|---------|
| **Ingestion**  | **Auto Loader**  | Chosen for efficient, incremental file discovery without manual schema management.  |
| **Processing**   | **PySpark**   |  Used for its horizontal scalability and robust support for stateful streaming.  |
| **Governance** | **Unity Catalog** | Implements fine-grained access control and end-to-end data lineage for audit compliance. |
| **DevOps** | **GitHub Actions** | Integrated for automated CI/CD, demonstrating production-read engineering practices. |

## Data Generation & API Simulation
To ensure the pipeline is end-to-end and reproducible, this project utilizes a **Synthetic Data Generation Framework** to simulate a high-velocity banking API.

**The Simulation Engine** 
We use the `dbldatageb` (Databricks Labs Data Generator) library to mock a real-time stream of financial transactions. This approach allows for:
* **Behavioral Injection**: Programmatically inject fradulent patterns, such as "Rapid-fire transfers" and "New device logins", which are difficult to find in public static datasets.
* **Volume Scaling**: The generator is configured to simulate peak traffic loads, testing the horizontal scalability of the **Spark** engine.
* **Cost Efficiency**: By generating data directly into the landing zone, we can utilize **Auto Loader** with `trigger(available=true)`, processing all "API" records and then automatically shutting down compute to save costs.



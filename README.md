# Databricks-Real-Time-Transaction-Fraud-Detection
The project is about proactively stopping fraudulent banking transactions in real-time instead of reporting back on fraud cases that took place. The projects detects and reports the transaction in real time.

## Executive Summary:
This is a production-grade, end-to-end data pipeline built on the **Databricks Lakehouse** to identify and quarantine fraudelent banking transactions in real-time. This project leverages behavioral fingerprinting and stateful streaming to reduce financial loss and improve system reliability.

## Busines Problem Statement
Legacy banking systems often rely on batch processing, leading to significant **detection latency (6+ hours)**. This system addresses that gap by implementing a **sub-second real-time architecture**, allowing the institution to block fraudulent transfers before funds are moved. 

## Architecture Design
This project follows the **Medallion Architecture** to ensure a governed and auditable data flow:

* **Bronze(Raw)**: Continous ingestion of synthetic API events via **Databricks Auto Loader** with schema evolution.
* **Silver(Enrinched)**: High Integrity data cleansing using **Delta Live Tables (DLT) Expectations** to quarantine malformed or suspicious records.
* **Gold(Behavioral)**: Business-level aggregates (e.g., transaction velocity, device dismatch )used for real-time alerting and historical reporting

## Tech Stack Decision:

| Column 1 | Column 2 | Column 3|
|----------|----------|---------|
| Row 1    | value    | Value   |
| Row 2    | Value    | Value   |

How will the data be generated


# subcompany-data-integration-pipeline
An end-to-end data integration pipeline using Databricks, PySpark, and AWS S3 to clean and merge an acquired sub-company's raw data into a centralized corporate Delta Lake Gold layer.

## Project Overview
This data engineering project implements an end-to-end ELT pipeline to solve a realistic corporate Mergers & Acquisitions (M&A) scenario. The objective is to ingest raw operational data from a newly acquired child company stored in cloud storage, process it through a structured Medallion Architecture, and seamlessly merge it into the existing Gold layer of the parent company's centralized data platform.

### Business Scenario
*   **Source A (Child Company):** Raw transactional data landing as CSV files in an isolated AWS S3 bucket.
*   **Source B (Parent Company):** Existing production Gold tables representing unified corporate history, managed within the Databricks Unity Catalog.
*   **The Challenge:** Clean and standardize the child company's data to match parent company schemas, handle duplicate records, and perform an incremental upsert (merge) into the target Gold layer without disrupting existing analytical workflows.

---

## Architecture Diagram

[AWS S3 Raw Bucket] ──► [Databricks Bronze Layer] (Raw Ingestion) ──► [Databricks Silver Layer] (Cleaning & Schema Enforcement) ──► [Databricks Gold Layer] (Match Business Logic with Parent Company) ──► [Delta Lake Merge to Parent Gold Layer (Upsert)] ──► [Final Consolidated Gold Catalog]

---

## Tech Stack
*   **Orchestration & Compute:** Databricks (Single-Node Cluster / Shared Compute)
*   **Language:** PySpark (Spark SQL & DataFrames)
*   **Storage Framework:** Delta Lake (for ACID compliance and Merge capabilities)
*   **Cloud Infrastructure:** AWS S3 (Raw Land Zone)
*   **Version Control:** Git & GitHub (Databricks Git Integration)

---

## Repository Structure

```text
├── Notebooks/
│   ├── 1_setup               		  # Setup date_table, catalogs and utilities.
│   └── 2_dimension_data_processing  # Process customers, products and pricing data.
├── sample data/
│   ├── child company data              # reference for incoming child company data
│   └── parent company data             # reference for existing target parent table
├── .gitignore                             # Ignores sensitive configuration and cluster state files
└── README.md                              # Project documentation

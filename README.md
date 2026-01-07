# The Sustainable Lakehouse: Green Data Engineering Proof of Concept

## 🌍 Project Overview

As cloud data volumes grow, so does the carbon footprint of data processing. This repository provides a reference implementation for a **"Sustainable Lakehouse"**—a data architecture designed to minimize Software Carbon Intensity (SCI) by optimizing Input/Output (I/O) efficiency.

This project demonstrates how **Apache Spark** and **Delta Lake** can be leveraged to reduce compute resource consumption (and consequently, electricity usage) through two distinct architectural patterns: **Read-Side Optimization** and **Write-Side Optimization**.

---

## 📂 Repository Structure

This repository contains two alternative notebook implementations, each focusing on a different vector of carbon reduction.

| Notebook File | Focus Area | Primary Technique | Carbon Impact |
| --- | --- | --- | --- |
| `01_Read_Optimization_ZOrder.ipynb` | **Read Efficiency** | Metadata Pruning & Z-Ordering | Reduces scan energy by ~40% for filtering queries. |
| `02_Write_Optimization_Dynamic.ipynb` | **Write Efficiency** | Dynamic Partition Overwrites | Reduces write I/O by >99% for historical updates. |

---

## 📘 Notebook 1: Read-Side Optimization

**File:** `01_Read_Optimization_ZOrder.ipynb`

This notebook simulates a scenario where data is ingested and then heavily queried by analysts. The focus is on minimizing the "Scan Intensity" of future SELECT queries.

### Key Features Implemented:

* **Metadata-Driven Pruning:** Demonstrates how Delta Lake's manifest files allow the engine to skip gigabytes of data files without physically reading them.
* **Carbon-Aware Scheduling:** A mock implementation of a "Green Scheduler" that checks the electrical grid's Carbon Intensity (gCO2/kWh) before running heavy maintenance jobs.
* **Z-Order Clustering:** Implements multi-dimensional clustering to physically co-locate related data (e.g., `Customer_ID`), drastically reducing the files scanned during filtration.

**Use Case:** Best for "Read-Heavy" analytical datasets (e.g., Customer 360, Fraud Detection History).

---

## 📗 Notebook 2: Write-Side Optimization

**File:** `02_Write_Optimization_Dynamic.ipynb`

This notebook targets the "Hidden Carbon Tax" of ETL pipelines: **Write Amplification**. It simulates a scenario where a small correction (late-arriving data) needs to be applied to a massive historical dataset.

### Key Features Implemented:

* **Dynamic Partition Overwrite:** Configures Spark to `spark.sql.sources.partitionOverwriteMode = "dynamic"`.
* **The "Smart Swap":** Demonstrates how to update a single day of data within a multi-year dataset without rewriting the entire table.
* **I/O Comparison:** Visualizes the difference between a "Legacy Overwrite" (High I/O) vs. a "Green Overwrite" (Low I/O).

**Use Case:** Best for "Write-Heavy" ETL pipelines, daily batch processing, and regulatory restatements.

---

## 🚀 Getting Started

### Prerequisites

* Databricks Runtime 10.4 LTS or higher (or Apache Spark 3.3+ with Delta Lake 2.0+).
* Python 3.8+.

### Installation

1. Clone this repository:
```bash
git clone https://github.com/your-username/sustainable-lakehouse.git

```


2. Import the `.ipynb` or `.py` files into your Databricks Workspace or Jupyter Lab environment.
3. Attach to a cluster and run all cells.

### Configuration

No external datasets are required. Both notebooks utilize `spark.range()` to generate synthetic financial data, making them self-contained and ready to run out of the box.

---

## 📉 The Science: Why This Matters

Software Carbon Intensity (SCI) in Big Data is largely a function of **Data Scanned** and **Data Written**.

* **Read Impact:** Every GB scanned requires disk spin-up (Storage Energy) and CPU cycles for decompression (Compute Energy).
* **Write Impact:** Rewriting unmodified data wastes energy on serialization and network transfer.

By adopting the patterns in this repo, you move from a "Brute Force" architecture to a "Precision" architecture, aligning engineering efficiency with environmental sustainability.

---

## 📜 License

Free to use

---

**Author:** Rudra Sinha
*Senior Manager, Data Engineering & Machine Learning*

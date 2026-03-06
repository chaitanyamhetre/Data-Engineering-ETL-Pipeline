# 🚕 NYC Taxi Data Engineering ETL Pipeline (PySpark)

## 📌 Project Overview

This project implements an **end-to-end ETL (Extract–Transform–Load) data engineering pipeline** using **Apache Spark (PySpark)** to process large-scale transportation data from the **NYC Yellow Taxi dataset**.

The pipeline demonstrates how large datasets can be ingested, transformed, and stored in an optimized format suitable for analytical workloads.

The goal of this project is to simulate a **real-world data engineering workflow**, including:

* Reading large-scale **Parquet datasets**
* Performing **data cleaning and transformation**
* Engineering new analytical features
* Writing optimized outputs using **columnar storage (Parquet)**
* Creating **Spark SQL tables** for querying and analytics

This project is designed to showcase **big data processing skills** using **Apache Spark**.

---

# 📊 Dataset Description

The dataset used in this project is the **NYC Yellow Taxi Trip Records dataset**, which contains information about taxi trips in New York City.

The dataset is publicly available from the **NYC Taxi & Limousine Commission (TLC)**.

Dataset source:
https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page

The dataset is stored in **Parquet format**, which is a **columnar storage format optimized for big data processing**.

---

## Dataset Contents

Each record represents a **single taxi trip** and contains information such as:

| Column                  | Description               |
| ----------------------- | ------------------------- |
| `VendorID`              | Taxi vendor identifier    |
| `tpep_pickup_datetime`  | Trip pickup timestamp     |
| `tpep_dropoff_datetime` | Trip dropoff timestamp    |
| `passenger_count`       | Number of passengers      |
| `trip_distance`         | Distance traveled (miles) |
| `RatecodeID`            | Rate code applied         |
| `PULocationID`          | Pickup location ID        |
| `DOLocationID`          | Dropoff location ID       |
| `payment_type`          | Payment method            |
| `fare_amount`           | Base fare amount          |
| `tip_amount`            | Tip paid                  |
| `total_amount`          | Total trip amount         |

---

## Dataset Characteristics

* Format: **Parquet**
* Size: ~200MB per monthly dataset
* Records: **Millions of taxi trips**
* Data type: **Structured tabular data**
* Domain: **Transportation analytics**

This makes it ideal for demonstrating **big data ETL pipelines**.

---

# ⚙️ ETL Pipeline Architecture

The pipeline follows the standard **ETL architecture**:

```
Online Dataset (Parquet)
        │
        ▼
EXTRACT
Read dataset using Spark
Load data into Spark DataFrame
        │
        ▼
TRANSFORM
• Remove missing values
• Filter invalid trips
• Feature engineering
• Data aggregation
        │
        ▼
LOAD
Create Spark SQL table
```

---

# 🔧 Technologies Used

| Technology       | Purpose                              |
| ---------------- | ------------------------------------ |
| **Apache Spark** | Distributed data processing          |
| **PySpark**      | Python API for Spark                 |
| **Google Colab** | Cloud-based development environment  |
| **Parquet**      | Efficient columnar storage format    |
| **Spark SQL**    | Analytical queries on processed data |

---

# 🧰 Prerequisites

Before running this project, make sure you have the following:

### 1️⃣ Basic Knowledge

* Python
* Data processing concepts
* Basic understanding of ETL pipelines

---

### 2️⃣ Software Requirements

The project runs in **Google Colab**, so no local installation is required.

However, the following components are installed during runtime:

* Java 8
* Apache Spark
* PySpark
* findspark

---

### 3️⃣ Python Libraries

The following Python packages are used:

```
pyspark
findspark
```

These are installed automatically in the notebook.

---

# 🚀 Project Setup

## Step 1: Clone Repository

```bash
git clone https://github.com/yourusername/spark-taxi-etl-pipeline.git
cd spark-taxi-etl-pipeline
```

---

## Step 2: Open in Google Colab

Upload the notebook to **Google Colab**.

or run locally if Spark is installed.

---

## Step 3: Install Spark

The notebook installs Spark automatically:

```python
!apt-get install openjdk-8-jdk-headless
!wget https://archive.apache.org/dist/spark/spark-3.5.0/spark-3.5.0-bin-hadoop3.tgz
!tar xf spark-3.5.0-bin-hadoop3.tgz
!pip install findspark
```

---

# 🔄 ETL Pipeline Steps

## 1️⃣ Extract

The pipeline begins by loading the **Parquet dataset** into Spark.

```python
df = spark.read.parquet("yellow_tripdata_2023-01.parquet")
```

Spark efficiently reads the dataset using **distributed processing**.

---

## 2️⃣ Load

The dataset is loaded into a **Spark DataFrame**, which allows scalable processing.

```python
df.show()
df.printSchema()
```

---

## 3️⃣ Transform

Several transformation steps are applied.

### Data Cleaning

Remove records with missing critical values.

```
passenger_count
trip_distance
fare_amount
```

---

### Filtering Invalid Trips

Trips with:

* Zero distance
* Negative fares

are removed.

---

### Feature Engineering

New features are created for analytics.

#### Trip Duration

```
trip_duration_minutes =
dropoff_time - pickup_time
```

---

#### Average Speed

```
avg_speed_kmh =
trip_distance / trip_duration
```

---

#### Pickup Hour

Extract the hour of the day from pickup timestamp.

This helps analyze **trip patterns across time**.

---

### Aggregation

Trips are grouped by **pickup hour** to analyze demand patterns.

Example metrics:

* Average fare
* Average trip distance
* Trip counts

---

# 💾 Load (Output)

After transformations, the processed dataset is stored in **Parquet format**.

```python
df.write.mode("overwrite").parquet("processed_taxi_data")
```

Benefits of Parquet:

* Columnar storage
* Faster queries
* Smaller storage size
* Optimized for big data analytics

---

# 🗄️ Spark SQL Table

A Spark SQL table is created for querying.

```python
df.write.saveAsTable("taxi_db.yellow_taxi_trips")
```

Example query:

```sql
SELECT pickup_hour,
       COUNT(*) AS trips,
       AVG(fare_amount) AS avg_fare
FROM taxi_db.yellow_taxi_trips
GROUP BY pickup_hour
ORDER BY pickup_hour;
```

---

# 📈 Example Insights

Using the processed data, we can analyze:

* Taxi demand by hour
* Average fare patterns
* Trip distance trends
* Passenger distribution

This demonstrates how **raw data can be transformed into analytical datasets**.

---

# 🎯 Key Learning Outcomes

This project demonstrates:

* Building a **scalable ETL pipeline**
* Processing **large datasets with Spark**
* Using **columnar storage formats**
* Performing **data transformations at scale**
* Creating **analytics-ready datasets**

---

# 🔮 Future Improvements

Possible extensions of this project include:

* Implementing **partitioned Parquet tables**
* Adding **data validation checks**
* Integrating **Airflow for orchestration**
* Creating **data warehouse layers (Bronze/Silver/Gold)**
* Deploying the pipeline using **Docker**

---



Please consider **starring the repository**.

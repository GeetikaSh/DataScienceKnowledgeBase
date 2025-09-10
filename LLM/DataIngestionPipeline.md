# Data Ingestion Pipeline
A **Data Ingestion Pipeline** is a process that collects raw data from multiple sources, transforms it into usable formats, and stores it for downstream tasks such as preprocessing, model training, and analytics.

- **Analogy**: Imagine a kitchen pipeline:
  - Farmers → deliver raw ingredients
  - Kitchen staff → clean, cut, prepare
  - Chefs → cook the final dish  
  Similarly, ingestion pipelines fetch raw data, clean it, and make it ready for ML pipelines.

---

## 🔹 Why is it Important in ML?
- Ensures **data consistency** across environments.
- Handles **large volumes of data** efficiently.
- Enables **real-time streaming** for applications like fraud detection, recommendation engines, etc.
- Provides **traceability & monitoring** to ensure data quality.

---

## 🔹 Types of Data Ingestion
1. **Batch Ingestion**  
   - Collect and load data at scheduled intervals.  
   - Example: Daily upload of customer transactions.  
   - Tools: Apache Nifi, Airflow, AWS Glue.

2. **Real-time / Streaming Ingestion**  
   - Ingests data continuously as it’s generated.  
   - Example: IoT sensor data, clickstream logs.  
   - Tools: Apache Kafka, Spark Streaming, AWS Kinesis.

3. **Lambda Architecture** (Hybrid)  
   - Combines batch + streaming for scalability + low latency.  

---

## 🔹 Architecture of a Data Ingestion Pipeline
1. **Source Layer**: Databases, APIs, files (CSV, JSON, Parquet), sensors, logs.  
2. **Ingestion Layer**: Kafka, Flume, Sqoop, Airbyte, custom scripts.  
3. **Processing Layer**: Spark, Beam, Flink, dbt for transformation & cleaning.  
4. **Storage Layer**: Data lake (S3, ADLS, GCS), Data warehouse (BigQuery, Snowflake, Redshift).  
5. **Serving Layer**: ML pipelines, dashboards, BI tools.

---

## 🔹 Example (Batch Pipeline in Python with Pandas)
```python
import pandas as pd

def ingest_csv(file_path):
    # Step 1: Read raw data
    df = pd.read_csv(file_path)

    # Step 2: Basic cleaning
    df = df.dropna()
    df.columns = [col.strip().lower() for col in df.columns]

    # Step 3: Save to processed layer
    df.to_parquet("processed/data.parquet", index=False)
    return df

data = ingest_csv("raw/customers.csv")
print("Ingested rows:", len(data))
```

---

## 🔹 Example (Streaming with Kafka in Python)
```python
from kafka import KafkaConsumer
import json

# Consume data from Kafka topic
consumer = KafkaConsumer(
    'transactions',
    bootstrap_servers=['localhost:9092'],
    auto_offset_reset='earliest',
    value_deserializer=lambda x: json.loads(x.decode('utf-8'))
)

for message in consumer:
    record = message.value
    print("Received:", record)
    # Process and store record (e.g., into database)
```

---

## 🔹 Best Practices
- Use **schema management** (e.g., Avro, Protobuf) for consistency.
- Monitor ingestion with logging & metrics (Prometheus, Grafana).
- Automate workflows with **Airflow, Prefect, Dagster**.
- Handle **idempotency** (avoid duplicate ingestion).
- Implement **error handling & retries**.

---

## 🔹 Common Tools
- **Batch**: Airflow, AWS Glue, Apache Nifi, Talend.  
- **Streaming**: Kafka, Spark Streaming, Flink, Pulsar.  
- **Cloud-native**: AWS Kinesis, GCP Dataflow, Azure Event Hub.  

---

## 🔹 Interview Questions
1. What is the difference between **batch** and **streaming ingestion**?  
2. How do you ensure **idempotency** in a data ingestion pipeline?  
3. What happens if your Kafka consumer crashes? How do you recover?  
4. Which ingestion strategy would you use for a **real-time fraud detection system**?  
5. How would you design ingestion for **petabyte-scale logs**?  

---

## ✅ Key Takeaways
- Data ingestion is the **first step** of any ML workflow.  
- Choose **batch vs streaming vs hybrid** depending on latency needs.  
- Ensure **scalability, monitoring, and fault tolerance** in design.  
- Strong pipelines = reliable ML models.  

---

# Kafka-Stream-Processing

## Overview

This repository demonstrates real-time anomaly detection on streaming data using Kafka, Python, and machine learning. The main workflow is illustrated in the Jupyter notebook `docs/tutorials/Kafka_Anomaly_Detection.ipynb` and involves generating synthetic transaction data, streaming it into Kafka topics, consuming the data, and applying anomaly detection in real time.

---

## How it Works

### 1. **Setup and Dependencies**
- Clones a related repository (`kafkaml-anomaly-detection`) for reference.
- Installs required Python packages: `kafka-python` for Kafka integration and `slackclient` (for notifications).
- Downloads and starts Apache Kafka and Zookeeper locally.

### 2. **Kafka Topics**
- Creates two Kafka topics:
  - `transactions`: Holds synthetic transaction data.
  - `anomalies`: Holds detected anomalies.

### 3. **Anomaly Detection Model Training**
- Generates synthetic 2D data for training.
- Uses the Isolation Forest algorithm (from scikit-learn) to fit an anomaly detection model.
- Saves the trained model for later use.

### 4. **Kafka Producer: Streaming Synthetic Data**
- Sends messages to the `transactions` topic.
- Each message contains an ID, a 2D data point, and a timestamp.
- Some messages are purposely made anomalous.
- Messages are serialized as JSON.

### 5. **Kafka Consumer: Real-Time Anomaly Detection**
- Reads messages from the `transactions` topic.
- For each message:
    - Deserializes the message.
    - Runs the data through the trained Isolation Forest model.
    - If an anomaly is detected, computes a score and sends it to the `anomalies` topic.

### 6. **Monitoring**
- Example code is included for consuming from Kafka topics to inspect messages.

---

## Technical Highlights

- **Kafka Workflow:** Classic producer-consumer pipeline with streaming data analyzed in real time.
- **Isolation Forest:** Unsupervised machine learning for anomaly detection.
- **Streaming ML Pipeline:** Model is trained once and used continuously as data streams through Kafka.
- **Synthetic Data:** Randomly generated, with some purposely anomalous for testing.

---

## High-Level Flow

1. **Generate Data** 
2. **Produce to Kafka (`transactions`)** 
3. **Consume Data** 
4. **Run ML Model** 
5. **If Anomaly, Produce to Kafka (`anomalies`)**

---

## Use Cases

- Real-time financial fraud detection
- Sensor anomaly monitoring
- Real-time alerting systems

---

For details, see the notebook:  
[`docs/tutorials/Kafka_Anomaly_Detection.ipynb`](docs/tutorials/Kafka_Anomaly_Detection.ipynb)


# 🚚 DeliveryBoy – Kafka Producer Service

This Spring Boot application acts as a Kafka **producer** that simulates real-time location updates for a delivery agent. It sends thousands of random coordinates to a Kafka topic.

---

## 📌 Purpose

This is part of a Kafka-based system to demonstrate how a microservice can produce location data that gets consumed by another service (like `enduser`).

---

## 🧱 Tech Stack

- Java
- Spring Boot
- Apache Kafka (tested with version 4.0.0 using KRaft mode)
- REST API

---

## 🚀 Kafka Setup Steps (KRaft Mode – No ZooKeeper)

### 1️⃣ Format Kafka Storage

```bash
bin/kafka-storage.sh format -t $(bin/kafka-storage.sh random-uuid) -c config/kraft/server.properties

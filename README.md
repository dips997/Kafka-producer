# Kafka Producer – DeliveryBoy Service

This is a Spring Boot-based **Kafka Producer service** that simulates sending real-time location updates for a delivery boy. It pushes the data into a Kafka topic which can then be consumed by another microservice (like a consumer).

---

## Purpose

This service demonstrates how a Kafka **Producer** works in a microservice setup using Spring Boot. It sends random location coordinates to a Kafka topic called `location-update-topic`.

The data can be consumed by a separate **Kafka Consumer** (like `enduser`) which listens to this topic.

---

## Tech Stack

- Java
- Spring Boot
- Apache Kafka (v4.0.0 using KRaft mode)
- Spring Kafka
- REST API

---

## Kafka Concept (Producer Side)

In Kafka terms:
> A **Producer** is an application that **writes (sends) messages to a Kafka topic**.  
> A **Consumer** listens to that topic and **reads those messages**.

This project is the **Producer**, sending simulated delivery-boy location updates to the topic `location-update-topic`.

---

## Kafka Setup Steps (KRaft – No ZooKeeper)

### 1.Generate a Cluster UUID

```bash
KAFKA_CLUSTER_ID="$(bin/kafka-storage.sh random-uuid)"
```

### 2. Format Kafka Storage

```bash
bin/kafka-storage.sh format -t $(bin/kafka-storage.sh random-uuid) -c config/kraft/server.properties
```

###  3. Start Kafka Server
```bash
bin/kafka-server-start.sh config/server.properties
```

---

## Test the Kafka Producer API using Postman

### 1. Open Postman
### 2. Click "New" > HTTP Request
### 3. Select POST method
### 4. 
```bash
    http://localhost:8080/location/update
```
### 5. Click "Send"
### 6. Response will look like:
```bash
{
  "message": "location updated"
}
```
---

## Kafka Producer Flow Summary

### 1. You call the REST endpoint `/location/update`  
### 2. It generates 200,000 random coordinates  
### 3. It sends each coordinate as a message to Kafka topic `location-update-topic`  
### 4. A consumer (e.g. `enduser`) receives and logs the messages

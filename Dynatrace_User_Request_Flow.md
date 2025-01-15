
# Understanding the Flow of a User Request in Dynatrace

## Overview

This document outlines the flow of a user request through various layers of a monitored system in Dynatrace. It identifies involved entities, data passed, and models used at each stage, providing enhanced clarity through monitoring and troubleshooting.

Each section specifies key layers and their associated models in this workflow:

---

## **Summary Table: Layers, Entities, and Associated Models**

| Layer                     | Entities Involved                         | Associated Models                                                   |
|---------------------------|-------------------------------------------|----------------------------------------------------------------------|
| **User Request**          | Application, User Session, User Action   | Behavioral, Business, Semantic                                      |
| **Service Request**       | Service, Queue, Load Balancer            | Logical, Integration, Behavioral                                    |
| **Backend Layer**         | Service, Process, Cloud Function, Custom Device | Physical, Behavioral, Configuration                                  |
| **Infrastructure Layer**  | Host, Container, Kubernetes Cluster      | Physical, Hybrid Cloud, Configuration                               |
| **Storage and Database Layer** | Database, Storage                  | Business, Behavioral, Configuration                                 |
| **Data Collection and Monitoring** | ActiveGate, OneAgent           | Observability, AI/ML, Integration                                   |
| **Dynatrace Internal Processing** | Problem, Synthetic Test         | Semantic, Observability, AI/ML                                      |
| **Query and Dashboards**  | Problem, Synthetic Test                  | Visualization, Observability, Business                              |

---

## Detailed Layer Breakdown

### 1. **User Request**
- **Entities Involved:**
  - Application (`dt.entity.application`)
  - User Session (`dt.entity.user_session`)
  - User Action (`dt.entity.user_action`)
  - Mobile App (`dt.entity.mobile_app`)
  
- **Data Passed:**
  - User Session: Entire user journey from entry to exit.
  - User Action: Button clicks, form submissions, etc.
  - Request Context: User agent, IP, page URL, geolocation, etc.

- **Associated Models:**
  1. Behavioral Model: Establishes baselines for normal user interaction behavior.
  2. Business Model: Correlates user actions with KPIs, such as conversion rates.
  3. Semantic Model: Maps dependencies between user sessions and application layers.

- **Example Entities:**
  - Application: `My-Web-App`
  - User Session: `1234567`
  - User Action: `Login Button Click`
  - Mobile App: `My-Mobile-App`

---

### 2. **Service Request**
- **Entities Involved:**
  - Service (`dt.entity.service`)
  - Queue (`dt.entity.queue`)
  - Load Balancer (`dt.entity.load_balancer`)

- **Data Passed:**
  - Request Metadata: Headers, payloads, and methods (POST, GET, etc.).
  - Queue Messages: Queued request payloads.
  - Span Data: Tracks request flow through the system.

- **Associated Models:**
  1. Logical Model: Groups services by environment or team ownership.
  2. Integration Model: Tracks how services integrate via queues and load balancers.
  3. Behavioral Model: Monitors baselines for queue processing times and service response rates.

- **Example Entities:**
  - Service: `Payment-Service`
  - Queue: `Payment-Processing-Queue`
  - Load Balancer: `AWS ALB`

---

### 3. **Backend Layer**
- **Entities Involved:**
  - Service (`dt.entity.service`)
  - Process (`dt.entity.process`)
  - Cloud Function (`dt.entity.cloud_function`)
  - Custom Device (`dt.entity.custom_device`)

- **Data Passed:**
  - Service Metrics: Request count, response time, throughput.
  - Logs: Errors, debug messages, etc.
  - Traces: Maps spans tracking the request through backend services.

- **Associated Models:**
  1. Physical Model: Represents underlying infrastructure hosting backend services.
  2. Behavioral Model: Identifies anomalies in response time or throughput baselines.
  3. Configuration Model: Ensures correct backend configurations (e.g., runtime versions).

- **Example Entities:**
  - Service: `Payment-Service`
  - Cloud Function: `AWS Lambda`
  - Custom Device: `IoT-Sensor-123`

---

### 4. **Infrastructure Layer**
- **Entities Involved:**
  - Host (`dt.entity.host`)
  - Container (`dt.entity.container`)
  - Kubernetes Cluster (`dt.entity.kubernetes_cluster`)

- **Data Passed:**
  - Metrics: CPU, memory, disk usage.
  - Container Data: Cluster health, node counts, etc.

- **Associated Models:**
  1. Physical Model: Represents hosts, containers, and Kubernetes clusters.
  2. Hybrid Cloud Model: Integrates monitoring for hybrid environments.
  3. Configuration Model: Captures details like enabled plugins and cluster setups.

- **Example Entities:**
  - Host: `EC2-Instance-567`
  - Container: `Payment-Service-Container`
  - Kubernetes Cluster: `Production-K8s-Cluster`

---

### 5. **Storage and Database Layer**
- **Entities Involved:**
  - Database (`dt.entity.database`)
  - Storage (`dt.entity.storage`)

- **Data Passed:**
  - Query Data: SQL queries sent to databases.
  - Data I/O: Read/Write interactions with storage systems.

- **Associated Models:**
  1. Business Model: Links database performance to transaction success rates.
  2. Behavioral Model: Detects anomalies in query response times.
  3. Configuration Model: Validates database and storage configurations.

- **Example Entities:**
  - Database: `Payment-DB`
  - Storage: `S3-Bucket-Transaction-Data`

---

### 6. **Data Collection and Monitoring**
- **Entities Involved:**
  - ActiveGate
  - OneAgent

- **Data Passed:**
  - Logs: Application and system logs.
  - Metrics: CPU, memory usage, response times, etc.
  - Traces: End-to-end request journeys.

- **Associated Models:**
  1. Observability Model: Centralizes metrics, logs, and traces for analysis.
  2. AI/ML Model: Automates root cause analysis and anomaly detection.
  3. Integration Model: Facilitates seamless data transfer to Dynatrace.

- **Example Tools:**
  - ActiveGate as a secure proxy.
  - OneAgent capturing entity data.

---

### 7. **Dynatrace Internal Processing**
- **Entities Involved:**
  - Problem (`dt.entity.problem`)
  - Synthetic Test (`dt.entity.synthetic_test`)

- **Data Passed:**
  - Logs, Metrics, and Traces: Used for anomaly detection.
  - Problem Notifications: Issues detected and raised for resolution.
  - Entity Relationships: Links between services, processes, and hosts.

- **Associated Models:**
  1. Semantic Model: Maps relationships between problems and affected entities.
  2. Observability Model: Provides a unified view of monitoring data.
  3. AI/ML Model: Detects anomalies, root causes, and automates problem detection.

---

### 8. **Query and Dashboards**
- **Entities Involved:**
  - Problem (`dt.entity.problem`)
  - Synthetic Test (`dt.entity.synthetic_test`)

- **Data Passed:**
  - Query Results: Filtered log/metric data from DQL queries.
  - Synthetic Test Data: Availability and performance metrics.

- **Associated Models:**
  1. Visualization Model: Powers interactive dashboards for data analysis.
  2. Observability Model: Unifies data for querying and visualizing trends.
  3. Business Model: Correlates operational insights with business KPIs.

- **Example DQL Query:**

```sql
fetch logs
| filter level == "ERROR"
| filter dt.entity.service == "SERVICE-123"
| fields timestamp, message, dt.entity.host
```

---

## **Conclusion**

By integrating these models with entities and workflows, Dynatrace simplifies monitoring, ensures seamless observability, and provides actionable insights across complex environments. This comprehensive approach enhances understanding, troubleshooting, and decision-making at every stage of the user request journey.

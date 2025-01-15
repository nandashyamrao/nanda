
# Understanding the Flow of a User Request in Dynatrace

## Overview
This document outlines the flow of a user request through various layers of a monitored system in Dynatrace. It identifies involved entities, data passed, models used at each stage, and descriptions to enhance clarity for monitoring and troubleshooting.

Each section specifies key layers, their associated models, and descriptions in this workflow:

---

## 1. User Request
**Entities Involved:**
- Application (`dt.entity.application`)
- User Session (`dt.entity.user_session`)
- User Action (`dt.entity.user_action`)
- Mobile App (`dt.entity.mobile_app`)

**Description:**  
A user makes a request through an Application or a Mobile App. The user's journey is tracked as a User Session, while specific interactions (like button clicks, taps, etc.) are recorded as User Actions.

**Data Passed:**
- User Session: Entire user journey from entry to exit.
- User Action: Button clicks, form submissions, etc.
- Request Context: User agent, IP, page URL, geolocation, etc.

**Associated Models:**
1. **Behavioral Model:** Establishes baselines for normal user interaction behavior.
2. **Business Model:** Correlates user actions with KPIs, such as conversion rates.
3. **Semantic Model:** Maps dependencies between user sessions and application layers.

**Example Entities:**
- Application: `My-Web-App`
- User Session: `1234567`
- User Action: `Login Button Click`
- Mobile App: `My-Mobile-App`

---

## 2. Service Request
**Entities Involved:**
- Service (`dt.entity.service`)
- Queue (`dt.entity.queue`)
- Load Balancer (`dt.entity.load_balancer`)

**Description:**  
The request enters a Load Balancer (like AWS ALB) that distributes it to the appropriate Service. The Service could also place tasks into a Queue (like AWS SQS or Kafka) for later processing.

**Data Passed:**
- Request Metadata: Headers, payloads, and methods (POST, GET, etc.).
- Queue Messages: Queued request payloads.
- Span Data: Tracks request flow through the system.

**Associated Models:**
1. **Logical Model:** Groups services by environment or team ownership.
2. **Integration Model:** Tracks how services integrate via queues and load balancers.
3. **Behavioral Model:** Monitors baselines for queue processing times and service response rates.

**Example Entities:**
- Service: `Payment-Service`
- Queue: `Payment-Processing-Queue`
- Load Balancer: `AWS ALB`

---

## 3. Backend Layer
**Entities Involved:**
- Service (`dt.entity.service`)
- Process (`dt.entity.process`)
- Cloud Function (`dt.entity.cloud_function`)
- Custom Device (`dt.entity.custom_device`)

**Description:**  
Backend services process user requests. These requests may run in a Cloud Function (like AWS Lambda) or on a Custom Device (like IoT devices or network equipment). The Process runs specific logic to execute business tasks.

**Data Passed:**
- Service Metrics: Request count, response time, throughput, etc.
- Logs: Errors, debug messages, etc.
- Traces: Maps spans tracking the request through backend services.

**Associated Models:**
1. **Physical Model:** Represents underlying infrastructure hosting backend services.
2. **Behavioral Model:** Identifies anomalies in response time or throughput baselines.
3. **Configuration Model:** Ensures correct backend configurations (e.g., runtime versions).

**Example Entities:**
- Service: `Payment-Service`
- Cloud Function: `AWS Lambda`
- Custom Device: `IoT-Sensor-123`

---

## 4. Infrastructure Layer
**Entities Involved:**
- Host (`dt.entity.host`)
- Container (`dt.entity.container`)
- Kubernetes Cluster (`dt.entity.kubernetes_cluster`)

**Description:**  
Requests that require containerized workloads or Kubernetes pods are handled here. Each Container is part of a Kubernetes Cluster. The Host is the underlying server, which could be an EC2 instance or an on-prem machine.

**Data Passed:**
- Metrics: CPU, memory, disk usage.
- Container Data: Cluster health, node counts, etc.

**Associated Models:**
1. **Physical Model:** Represents hosts, containers, and Kubernetes clusters.
2. **Hybrid Cloud Model:** Integrates monitoring for hybrid environments.
3. **Configuration Model:** Captures details like enabled plugins and cluster setups.

**Example Entities:**
- Host: `EC2-Instance-567`
- Container: `Payment-Service-Container`
- Kubernetes Cluster: `Production-K8s-Cluster`

---

## 5. Storage and Database Layer
**Entities Involved:**
- Database (`dt.entity.database`)
- Storage (`dt.entity.storage`)

**Description:**  
Requests often interact with databases (like PostgreSQL, MySQL, or Redis) or storage services (like AWS S3 or Azure Blob Storage) to fetch or store data.

**Data Passed:**
- Query Data: SQL queries sent to databases.
- Data I/O: Read/Write interactions with storage systems.

**Associated Models:**
1. **Business Model:** Links database performance to transaction success rates.
2. **Behavioral Model:** Detects anomalies in query response times.
3. **Configuration Model:** Validates database and storage configurations.

**Example Entities:**
- Database: `Payment-DB`
- Storage: `S3-Bucket-Transaction-Data`

---

## 6. Data Collection and Monitoring
**Entities Involved:**
- ActiveGate
- OneAgent

**Description:**  
Dynatrace Agents are installed on hosts, containers, and services to capture logs, metrics, traces, and events. ActiveGate acts as a secure proxy for sending data to Dynatrace.

**Data Passed:**
- Logs: Application and system logs.
- Metrics: CPU, memory usage, response times, etc.
- Traces: End-to-end request journeys.

**Associated Models:**
1. **Observability Model:** Centralizes metrics, logs, and traces for analysis.
2. **AI/ML Model:** Automates root cause analysis and anomaly detection.
3. **Integration Model:** Facilitates seamless data transfer to Dynatrace.

**Example Tools:**
- ActiveGate as a secure proxy.
- OneAgent capturing entity data.

---

## 7. Dynatrace Internal Processing
**Entities Involved:**
- Problem (`dt.entity.problem`)
- Synthetic Test (`dt.entity.synthetic_test`)

**Description:**  
Dynatrace processes collected data to detect anomalies, root causes, and raise problem notifications.

**Data Passed:**
- Logs, Metrics, and Traces: Used for anomaly detection.
- Problem Notifications: Issues detected and raised for resolution.
- Entity Relationships: Links between services, processes, and hosts.

**Associated Models:**
1. **Semantic Model:** Maps relationships between problems and affected entities.
2. **Observability Model:** Provides a unified view of monitoring data.
3. **AI/ML Model:** Detects anomalies, root causes, and automates problem detection.

---

## 8. Query and Dashboards
**Entities Involved:**
- Problem (`dt.entity.problem`)
- Synthetic Test (`dt.entity.synthetic_test`)

**Description:**  
Dashboards display visual summaries of logs, metrics, problems, and traces. Synthetic Tests simulate user activity to ensure site availability.

**Data Passed:**
- Query Results: Filtered log/metric data from DQL queries.
- Synthetic Test Data: Availability and performance metrics.

**Associated Models:**
1. **Visualization Model:** Powers interactive dashboards for data analysis.
2. **Observability Model:** Unifies data for querying and visualizing trends.
3. **Business Model:** Correlates operational insights with business KPIs.

**Example DQL Query:**
```sql
fetch logs
| filter level == "ERROR"
| filter dt.entity.service == "SERVICE-123"
| fields timestamp, message, dt.entity.host
```

---

## Summary Table

| **Entity Type**            | **DQL Reference**               | **Example Entity**               |
|----------------------------|----------------------------------|----------------------------------|
| Application                | `dt.entity.application`         | My-Web-App                      |
| User Session               | `dt.entity.user_session`        | User-Session-123                |
| User Action                | `dt.entity.user_action`         | Login Button Click              |
| Mobile App                 | `dt.entity.mobile_app`          | My-Mobile-App                   |
| Service                    | `dt.entity.service`             | Payment-Service                 |
| Queue                      | `dt.entity.queue`               | Payment-Processing-Queue        |
| Host                       | `dt.entity.host`                | EC2-Instance-567                |
| Container                  | `dt.entity.container`           | Payment-Service-Container       |
| Cloud Function             | `dt.entity.cloud_function`      | AWS Lambda                      |
| Database                   | `dt.entity.database`            | Payment-DB                      |
| Storage                    | `dt.entity.storage`             | S3-Bucket-Transaction-Data      |
| Problem                    | `dt.entity.problem`             | Payment-Problem                 |

By integrating these models with entities and workflows, Dynatrace simplifies monitoring, ensures seamless observability, and provides actionable insights across complex environments. This comprehensive approach enhances understanding, troubleshooting, and decision-making at every stage of the user request journey.

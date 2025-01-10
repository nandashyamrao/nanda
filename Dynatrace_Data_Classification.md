
# **Data Classification in Dynatrace During Data Collection**

In Dynatrace, the **Data Collection phase** is a foundational step where different types of data are gathered, processed, and categorized. These categories—**metadata**, **tags**, **attributes**, **metrics**, **logs**, **traces**, **events**, and **relationships**—help provide a comprehensive understanding of the monitored environment. This document explores each classification in depth.

---

## **1. Metadata**

### **Definition**:
Metadata consists of static or semi-static descriptive information about entities in your environment. It provides the foundational context necessary for monitoring and analyzing performance.

### **Examples**:
- **Host Metadata**:
  - Host name (e.g., `web-server-01`)
  - IP address (e.g., `192.168.1.10`)
  - OS type (e.g., Linux, Windows)
  - Cloud provider (e.g., AWS, Azure)
  - Instance type (e.g., `t2.medium`)
- **Service Metadata**:
  - Service name (e.g., `checkout-service`)
  - Framework (e.g., Spring Boot, .NET)
  - Deployment version (e.g., `v1.2.3`)
- **Process Metadata**:
  - Process group name
  - Executable path (e.g., `/usr/bin/nginx`)
  - Runtime version (e.g., JDK 11, Python 3.9)

### **Usage**:
Metadata acts as a **lookup reference** for deeper analysis, query building, and dependency mapping.

---

## **2. Tags**

### **Definition**:
Tags are custom labels assigned to entities to help with categorization, filtering, and grouping. They are flexible and can be either static or dynamically generated based on metadata or runtime conditions.

### **Examples**:
- **Static Tags**:
  - `environment: production`
  - `team: backend`
  - `region: us-east`
- **Dynamic Tags**:
  - Based on rules:
    - Automatically tag hosts with `cloud.provider: AWS` as `cloud: AWS`.
    - Tag services where `response time > 1s` as `performance: slow`.

### **Usage**:
Tags simplify **visualization**, **searching**, and **alerting** by providing context-based filters.

---

## **3. Attributes**

### **Definition**:
Attributes are runtime key-value pairs that describe the operational or contextual state of entities. They often reflect dynamic changes and current performance characteristics.

### **Examples**:
- **Host Attributes**:
  - CPU usage (e.g., `75%`)
  - Memory usage (e.g., `60%`)
  - Disk I/O (e.g., `200MB/s`)
- **Service Attributes**:
  - Average response time (e.g., `500ms`)
  - Error rate (e.g., `0.2%`)
  - Throughput (e.g., `100 requests/second`)
- **Log Attributes**:
  - Log severity (e.g., `INFO`, `WARN`, `ERROR`)
  - Source (e.g., `application`, `system`)

### **Usage**:
Attributes provide granular details that allow for **real-time monitoring** and **anomaly detection**.

---

## **4. Metrics**

### **Definition**:
Metrics are numeric time-series data representing resource utilization or performance measurements over time.

### **Examples**:
- CPU usage (`builtin:host.cpu.usage`)
- Memory utilization (`builtin:host.mem.usage`)
- Service response time (`builtin:service.response.time`)
- Custom metrics (e.g., `custom.metric.api.latency`)

### **Usage**:
Metrics are critical for **trend analysis**, **baseline creation**, and **capacity planning**.

---

## **5. Logs**

### **Definition**:
Logs are textual data that record system or application events. They are indexed and tied to the originating entity for streamlined analysis.

### **Examples**:
- **Application Logs**:
  - `Error: Connection timeout at db-service`
- **System Logs**:
  - `Kernel panic detected`
- **Cloud Logs**:
  - AWS CloudTrail events
  - Azure Activity Logs

### **Usage**:
Logs are indispensable for **debugging issues**, **forensic analysis**, and **auditing changes**.

---

## **6. Traces**

### **Definition**:
Traces are data that represent distributed transactions, mapping the end-to-end flow of requests across multiple services.

### **Examples**:
- **Span Metadata**:
  - Service name
  - Method called (e.g., `GET /orders`)
  - Error code (e.g., `500`)
- **Trace Metadata**:
  - Trace ID
  - Parent-child span relationships

### **Usage**:
Traces allow for **root cause analysis** in distributed systems and provide visibility into **inter-service dependencies**.

---

## **7. Events**

### **Definition**:
Events record state changes, anomalies, or user-defined triggers in the environment.

### **Examples**:
- **Deployment Events**:
  - `New version deployed: v1.2.3`
- **Scaling Events**:
  - `Autoscale increased instances from 2 to 4`
- **Anomalies**:
  - `Response time exceeded baseline by 200ms`
- **Health State Changes**:
  - `Host moved to CRITICAL state`

### **Usage**:
Events are essential for **alerting** and tracking **system state changes**.

---

## **8. Relationships**

### **Definition**:
Relationships represent the dependencies and interactions between entities.

### **Examples**:
- **Calls**:
  - `Service A calls Database B`
- **Contains**:
  - `Host contains Process X`
- **Depends On**:
  - `Service C depends on Queue D`

### **Usage**:
Relationships provide the context necessary for **dependency mapping** and **impact analysis**.

---

## **Summary Table: Classification of Collected Data**

| **Data Type**          | **Classification** | **Examples**                                                       |
|-------------------------|---------------------|---------------------------------------------------------------------|
| **Host Details**        | Metadata           | Host name, IP, OS type, cloud provider, instance type              |
| **Service Details**     | Metadata           | Service name, deployment version, runtime framework                |
| **Process Details**     | Metadata           | Process name, executable path, runtime version                     |
| **Environment Labels**  | Tags               | `environment: production`, `team: backend`, `region: us-east`      |
| **Performance Stats**   | Attributes         | CPU usage, response time, error rate                               |
| **Time-Series Data**    | Metrics            | `builtin:host.cpu.usage`, `builtin:service.response.time`          |
| **Application Logs**    | Logs               | `Error: Connection timeout`, `Kernel panic detected`               |
| **End-to-End Requests** | Traces             | Span IDs, trace ID, method called                                  |
| **State Changes**       | Events             | Deployment events, scaling events, health state changes            |
| **Dependencies**        | Relationships      | Calls, Contains, Depends On                                        |

---

## **Key Takeaways**
1. **Metadata** provides foundational context about entities.
2. **Tags** categorize entities for easy filtering and grouping.
3. **Attributes** describe real-time operational states.
4. **Metrics**, **logs**, and **traces** are critical for performance monitoring and debugging.
5. **Events** highlight significant system state changes.
6. **Relationships** enable powerful dependency mapping and root cause analysis.

---

Would you like additional examples or DQL queries tied to these classifications?

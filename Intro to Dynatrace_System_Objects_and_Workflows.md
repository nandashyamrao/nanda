
# System Objects and Workflows in Dynatrace

This document provides a comprehensive overview of **system objects** in Dynatrace and practical examples of workflows and queries to leverage these objects effectively.

---

## **System Objects in Dynatrace**

System objects are the foundational components used to organize, monitor, and interact with data in Dynatrace. These objects are critical for understanding how Dynatrace structures, analyzes, and visualizes the environment.

### **Categories of System Objects**

| **System Object**    | **Description**                                                                          | **Examples**                                       |
|-----------------------|------------------------------------------------------------------------------------------|---------------------------------------------------|
| **Entities**          | Monitored components in the environment, such as hosts, services, processes, and more.  | Host, Service, Process, Database, Application    |
| **Tags**              | Metadata used for categorization and grouping of entities.                              | `environment: production`, `team: backend`       |
| **Metadata**          | Descriptive information tied to entities, providing context and details.                | Hostname, IP address, OS, cloud provider         |
| **Metrics**           | Time-series data representing performance or resource utilization.                      | CPU usage, memory utilization, request latency   |
| **Logs**              | Textual data collected from applications, systems, and cloud platforms.                 | Application logs, system logs, AWS CloudTrail    |
| **Events**            | Notifications of state changes, anomalies, or significant activities.                   | Deployment events, scaling activities, anomalies |
| **Relationships**     | Connections between entities describing dependencies and interactions.                  | Calls, Contains, Depends On                      |
| **Dashboards**        | Visualizations of metrics, logs, and events for monitoring and analysis.                | Custom dashboards for services or environments   |
| **Views**             | Filtered or aggregated representations of data from tables and buckets.                 | Views for CPU usage or error rate trends         |
| **API Endpoints**     | Interfaces for programmatic interaction with Dynatrace data and settings.               | `/entities`, `/metrics`, `/logs` APIs            |

---

## **Key System Objects and Their Roles**

### **Entities**
- **Definition**: Core monitored components in Dynatrace.
- **Examples**:
  - `dt.entity.host`: Represents a physical or virtual machine.
  - `dt.entity.service`: Represents a backend or frontend service.
  - `dt.entity.database`: Represents a database instance.
- **Role**:
  - Central to Dynatrace’s observability model.
  - Organize and correlate data like metrics, logs, and events.

---

### **Tags**
- **Definition**: Key-value pairs applied to entities for filtering, categorization, and automation.
- **Examples**:
  - `environment=production`
  - `team=frontend`
- **Use Cases**:
  - Group entities for targeted monitoring.
  - Automate tagging through rules based on metadata or metrics.

---

### **Metadata**
- **Definition**: Static or semi-static descriptive information tied to entities.
- **Examples**:
  - Hostname: `web-server-01`
  - OS: `Linux`
  - Cloud provider: `AWS`
- **Role**:
  - Provides foundational context for monitored entities.
  - Used for filtering and querying in dashboards or API calls.

---

### **Metrics**
- **Definition**: Time-series data representing quantitative performance or resource utilization.
- **Examples**:
  - `builtin:host.cpu.usage`: CPU utilization for a host.
  - `builtin:service.response.time`: Response time for a service.
- **Role**:
  - Key to performance monitoring and baseline analysis.

---

### **Logs**
- **Definition**: Raw textual data from monitored systems, applications, and cloud platforms.
- **Examples**:
  - Application logs: `Error: Connection timeout`.
  - System logs: `Kernel panic detected`.
- **Role**:
  - Provide granular insights for debugging and anomaly detection.

---

### **Events**
- **Definition**: Discrete records of state changes, anomalies, or triggered activities.
- **Examples**:
  - Deployment event: `Version 1.2.3 deployed`.
  - Anomaly: `Response time exceeded baseline`.
- **Role**:
  - Used for real-time alerting and historical analysis.

---

### **Relationships**
- **Definition**: Connections between entities describing dependencies and interactions.
- **Examples**:
  - `calls`: Service A calls Database B.
  - `contains`: Host contains Process X.
  - `depends_on`: Service C depends on Queue D.
- **Role**:
  - Enable dependency mapping and root cause analysis.

---

### **Dashboards**
- **Definition**: Custom visualizations of metrics, logs, and events.
- **Examples**:
  - CPU and memory usage trends for production hosts.
  - Error rates and response times for critical services.
- **Role**:
  - Provide actionable insights through real-time and historical data.

---

### **Views**
- **Definition**: Filtered or aggregated representations of raw data from tables and buckets.
- **Examples**:
  - A view of all failed requests in the past hour.
  - Aggregated CPU usage for a specific service.
- **Role**:
  - Simplifies querying and visualization.

---

### **API Endpoints**
- **Definition**: Programmatic interfaces for interacting with Dynatrace data and settings.
- **Examples**:
  - `/entities`: Retrieve metadata and relationships for entities.
  - `/metrics`: Query time-series data for metrics.
  - `/logs`: Fetch indexed logs for debugging.
- **Role**:
  - Enable automation and integration with external systems.

---

## **Practical Workflows and Queries**

Here are practical examples of how to use system objects effectively:

### **Entities**

#### **Find High CPU Usage Hosts**
```sql
fetch metrics
| filter metric.key == "builtin:host.cpu.usage"
| filter datapoint.value > 80
| fields entity.name, datapoint.value
```

---

#### **Analyze Service Dependencies**
```sql
fetch dt.entity.service
| filter service.name == "order-service"
| join fetch dt.entity.database on service.calls == database
| fields service.name, database.name
```

---

### **Tags**

#### **Filter Services by Tag**
```sql
fetch dt.entity.service
| filter entity.tag.environment == "production"
| fields entity.name, entity.tag
```

---

### **Metadata**

#### **List Metadata for a Host**
```sql
fetch dt.entity.host
| filter entity.name == "web-server-01"
| fields entity.name, entity.ip, entity.metadata
```

---

### **Logs**

#### **Find Application Errors**
```sql
fetch logs
| filter entity.name == "order-service"
| filter log.severity == "ERROR"
| fields timestamp, message
```

---

### **Events**

#### **Track Deployment Events**
```sql
fetch events
| filter event.type == "DEPLOYMENT"
| filter timestamp >= now() - 7d
| fields timestamp, event.title, event.description
```

---

### **Relationships**

#### **Map Service-to-Database Calls**
```sql
fetch dt.entity.database
| filter entity.name == "customer-db"
| join fetch dt.entity.service on database.called_by == service
| fields database.name, service.name
```

---

## **Key Takeaways**
1. Entities: Core monitored objects tying together metrics, logs, traces, and events.
2. Tags: Enable grouping and filtering for specific use cases.
3. Relationships: Map dependencies for root cause analysis.
4. API Endpoints: Facilitate automation and external integrations.

## **System Objects: Hierarchical Representation**

```
System Objects
├── Entities
│   ├── Host
│   ├── Service
│   ├── Process
│   └── Database
├── Tags
│   ├── Static (e.g., environment=production)
│   └── Dynamic (e.g., based on metadata)
├── Metadata
│   ├── Hostname
│   ├── OS
│   └── Cloud Provider
├── Metrics
│   ├── CPU Usage
│   ├── Response Time
│   └── Error Rate
├── Logs
│   ├── Application Logs
│   ├── System Logs
│   └── Cloud Logs
├── Events
│   ├── Anomalies
│   ├── Deployments
│   └── Scaling Activities
├── Relationships
│   ├── Calls
│   ├── Contains
│   └── Depends On
├── Dashboards
│   └── Visualizations for Metrics, Logs, and Events
├── Views
│   └── Aggregated/Filtered Representations of Data
└── API Endpoints
    ├── /entities
    ├── /metrics
    └── /logs
```

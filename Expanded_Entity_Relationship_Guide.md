
# **Dynatrace Entity Relationship Guide**

---

## **Introduction**
In Dynatrace, entities are the core building blocks for monitoring and analyzing IT environments. Understanding how entities relate to one another, such as processes running on hosts or services communicating with applications, is key to troubleshooting, optimization, and performance tuning.

This guide explains the various entity types, their relationships, how Dynatrace tracks them, and detailed examples for better clarity.

---

## **Core Dynatrace Entities**

### **1. Process**
- **Definition**: A process is a running instance of a program on a host.
- **Examples**: 
  - `java.exe` running a Spring Boot application.
  - `mysqld` process managing a MySQL database.
  - `nginx` running as a web server.

**How Dynatrace Tracks Processes**:
Dynatrace tracks processes using its OneAgent, which monitors resource usage, connections, and dependencies in real-time.

**Attributes**:
- `process.name`: The name of the process.
- `process.groupName`: The group or category of the process.
- `process.cpuUsage`: CPU usage of the process.
- `process.memoryUsage`: Memory used by the process.

**Additional Examples**:
- **List all Java processes consuming high memory**:
  ```dql
  fetch dt.entity.process
  | fieldsAdd process.name, process.memoryUsage
  | filter process.name contains "java" and process.memoryUsage > 500
  ```
- **Identify processes connected to external services**:
  ```dql
  fetch dt.entity.process
  | fieldsAdd process.name, process.connectedServices
  | filter process.connectedServices contains "api.example.com"
  ```

---

### **2. Service**
- **Definition**: A service is a logical component of an application that handles specific functions or operations.
- **Examples**:
  - A payment processing service for an e-commerce app.
  - A REST API gateway service.
  - A recommendation engine service.

**How Dynatrace Tracks Services**:
Services are detected by monitoring incoming requests, outgoing calls, and their response times. Dynatrace groups requests based on endpoints, backend connections, and technologies.

**Attributes**:
- `service.name`: Name of the service.
- `service.technology`: The underlying technology (e.g., Java, Node.js).
- `service.responseTime`: Response time of the service.
- `service.failureRate`: Percentage of failed requests.

**Additional Examples**:
- **List services with high failure rates**:
  ```dql
  fetch dt.entity.service
  | fieldsAdd service.name, service.failureRate
  | filter service.failureRate > 10
  ```
- **Identify services calling external APIs**:
  ```dql
  fetch dt.entity.service
  | fieldsAdd service.name, service.externalCalls
  | filter service.externalCalls contains "stripe.com"
  ```

---

### **3. Host**
- **Definition**: A physical or virtual machine running monitored processes.
- **Examples**:
  - An AWS EC2 instance hosting a microservices architecture.
  - An on-premises Linux server running a legacy application.
  - A Kubernetes node hosting multiple pods.

**How Dynatrace Tracks Hosts**:
Dynatrace uses its OneAgent to gather host-specific data, including CPU, memory, disk usage, and network traffic. It also integrates with cloud platforms like AWS and Azure to enhance metadata.

**Attributes**:
- `host.name`: Name of the host.
- `host.osType`: Operating system (e.g., Linux, Windows).
- `aws.ec2.instanceId`: AWS-specific identifier for EC2 hosts.
- `host.networkTraffic`: Network traffic handled by the host.

**Additional Examples**:
- **List Linux hosts with high CPU usage**:
  ```dql
  fetch dt.entity.host
  | fieldsAdd host.name, host.cpuUsage
  | filter host.osType == "LINUX" and host.cpuUsage > 80
  ```
- **Identify hosts running out of disk space**:
  ```dql
  fetch dt.entity.host
  | fieldsAdd host.name, host.diskUsage
  | filter host.diskUsage > 90
  ```

---

### **4. Application**
- **Definition**: A collection of services providing functionality to end users.
- **Examples**:
  - An e-commerce application for online shopping.
  - A mobile banking app for managing transactions.
  - A customer support portal for tracking tickets.

**How Dynatrace Tracks Applications**:
Applications are tracked by monitoring user interactions, session data, and service dependencies. Dynatrace captures real-time telemetry through Real User Monitoring (RUM) and Synthetic Monitoring.

**Attributes**:
- `application.name`: Name of the application.
- `application.sessions`: Number of active user sessions.
- `application.errors`: Total errors encountered by users.

**Additional Examples**:
- **Identify applications with the highest user sessions**:
  ```dql
  fetch dt.entity.application
  | fieldsAdd application.name, application.sessions
  | sort application.sessions desc
  ```
- **List applications with significant error rates**:
  ```dql
  fetch dt.entity.application
  | fieldsAdd application.name, application.errors
  | filter application.errors > 50
  ```

---

### **5. Database**
- **Definition**: A relational or non-relational data storage system used by services or applications.
- **Examples**:
  - A MySQL database hosting user account data.
  - An Amazon RDS instance used for analytics.
  - A Redis cache for session management.

**How Dynatrace Tracks Databases**:
Dynatrace monitors database performance by analyzing queries, response times, and connection counts. It automatically identifies database types and usage patterns.

**Attributes**:
- `database.name`: Name of the database.
- `database.type`: Type of database (e.g., SQL, NoSQL).
- `database.queryTime`: Time taken to execute queries.

**Additional Examples**:
- **List databases with slow queries**:
  ```dql
  fetch dt.entity.database
  | fieldsAdd database.name, database.queryTime
  | filter database.queryTime > 100
  ```
- **Identify databases with high connection counts**:
  ```dql
  fetch dt.entity.database
  | fieldsAdd database.name, database.connections
  | filter database.connections > 50
  ```

---

## **Common Relationships in Dynatrace**
The following table summarizes relationships between entity types:

| **Relationship**    | **From Entity**     | **To Entity**        | **Description**                                   |
|---------------------|---------------------|----------------------|-------------------------------------------------|
| `runs_on`           | Process             | Host                 | Indicates which host a process is running on.   |
| `calls`             | Service             | Service              | Shows service-to-service communication.         |
| `connected_to`      | Host/Service        | Database/API         | Indicates a connection to external systems.     |
| `contained_in`      | Process/Service     | Host/Application     | Shows containment within larger entities.       |
| `interacts_with`    | Application         | Service/User         | Represents interaction with users or services.  |

---

## **Visualizing Relationships**
- **Smartscape View**: Displays real-time relationships between applications, services, hosts, and processes in a topology map.
- **Service Flow**: Shows how requests flow between services.
- **Problem Cards**: Highlights dependency issues in real-time.

---

## **Best Practices for Exploring Relationships**
1. **Start with Entity Type**: Always identify the entity type you want to query (e.g., `dt.entity.service`, `dt.entity.host`).
2. **Leverage Attributes**: Use attributes like `host.name` or `service.responseTime` to filter relevant data.
3. **Analyze Dependencies**: Focus on relationships such as `calls` or `runs_on` to understand data flow.
4. **Visualize Data**: Use Smartscape or dashboards to see relationships graphically.

---

This expanded guide provides detailed examples, additional clarity on how Dynatrace tracks entities, and their relationships. Let me know if you'd like further refinements!

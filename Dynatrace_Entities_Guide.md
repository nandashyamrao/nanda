
# **Understanding Entities and Entity Types in Dynatrace**

---

## **What Are Entities and Entity Types?**
In Dynatrace, an **entity** represents a monitored resource, such as a host, service, or application. **Entity types** categorize these resources based on their characteristics and functionality. Together, entities and entity types form the foundation of Dynatrace's monitoring and observability framework.

### **Key Definitions**
1. **Entity**: A single monitored instance, like a specific EC2 host, an S3 bucket, or a Kubernetes pod.
2. **Entity Type**: A classification or category of entities, such as all hosts, all services, or all Lambda functions.

---

## **Entity Types in Dynatrace**
Entity types in Dynatrace are defined using the `dt.entity.<entity_type>` naming convention. They group similar entities to simplify monitoring, querying, and visualization.

### **Examples of Common Entity Types**
| **Entity Type**                  | **Description**                              |
|----------------------------------|----------------------------------------------|
| `dt.entity.host`                 | Represents a host (e.g., EC2 instance).      |
| `dt.entity.service`              | Represents a service (e.g., web service).    |
| `dt.entity.process`              | Represents a process running on a host.      |
| `dt.entity.kubernetes_pod`       | Represents a Kubernetes pod.                 |
| `dt.entity.aws_lambda_function`  | Represents an AWS Lambda function.           |
| `dt.entity.aws_s3_bucket`        | Represents an AWS S3 bucket.                 |

---

## **How Entities Are Captured**
Entities are automatically detected by Dynatrace through various integrations and monitoring capabilities. The process of entity detection depends on the resource type:

### **1. Hosts**
- **Detection Method**: Dynatrace OneAgent or AWS integration.
- **Captured Attributes**:
  - `host.name`: Name of the host.
  - `host.osType`: Operating system type (e.g., LINUX, WINDOWS).
  - `aws.ec2.instanceId`: Instance ID for EC2 hosts.

**Example Query**:
```dql
fetch dt.entity.host
| fieldsAdd host.name, host.osType, aws.ec2.instanceId
| filter host.osType == "LINUX"
```

---

### **2. Services**
- **Detection Method**: Automatically detected by Dynatrace for applications and workloads.
- **Captured Attributes**:
  - `service.name`: Name of the service.
  - `service.technology`: Technology used (e.g., JAVA, NODEJS).
  - `service.responseTime`: Response time for the service.

**Example Query**:
```dql
fetch dt.entity.service
| fieldsAdd service.name, service.technology, service.responseTime
| filter service.technology == "JAVA"
```

---

### **3. Processes**
- **Detection Method**: Identified through Dynatrace OneAgent installed on hosts.
- **Captured Attributes**:
  - `process.name`: Name of the process.
  - `process.groupName`: Group name of the process.
  - `process.cpuUsage`: CPU usage of the process.

**Example Query**:
```dql
fetch dt.entity.process
| fieldsAdd process.name, process.groupName, process.cpuUsage
| filter process.cpuUsage > 50
```

---

### **4. Kubernetes Pods**
- **Detection Method**: Monitored through Kubernetes integration.
- **Captured Attributes**:
  - `kubernetes.namespace`: Namespace of the pod.
  - `kubernetes.podName`: Name of the Kubernetes pod.
  - `kubernetes.nodeName`: Name of the node running the pod.

**Example Query**:
```dql
fetch dt.entity.kubernetes_pod
| fieldsAdd kubernetes.namespace, kubernetes.podName, kubernetes.nodeName
| filter kubernetes.namespace == "production"
```

---

### **5. AWS Services**
Dynatrace captures AWS services through its AWS integration, which uses CloudWatch APIs to ingest metadata.

#### Examples of AWS Entity Types:
| **Entity Type**                  | **Description**                              |
|----------------------------------|----------------------------------------------|
| `dt.entity.aws_lambda_function`  | Represents AWS Lambda functions.             |
| `dt.entity.aws_s3_bucket`        | Represents AWS S3 buckets.                   |
| `dt.entity.aws_rds_instance`     | Represents AWS RDS database instances.       |

**Example Query for AWS Lambda Functions**:
```dql
fetch dt.entity.aws_lambda_function
| fieldsAdd aws.lambda.functionName, aws.lambda.memorySize
| filter aws.lambda.memorySize > 512
```

---

## **Entity Relationships**
Entities in Dynatrace are linked through relationships, enabling deeper insights into dependencies and data flow.

### **Common Relationships**
| **Relationship**   | **Description**                                               |
|---------------------|---------------------------------------------------------------|
| `calls`            | Service A calls Service B.                                    |
| `runs_on`          | A process runs on a specific host.                            |
| `contained_in`     | A Kubernetes pod is contained within a node or namespace.     |
| `connected_to`     | Host or service connected to another resource.                |

**Example Query for Relationships**:
```dql
fetch dt.entity.service
| fieldsAdd service.name, service.calls
| filter service.calls contains "database-service"
```

---

## **Best Practices for Working with Entities**
1. **Understand the Entity Type**  
   Identify the type of entity you are working with (`host`, `service`, `process`, etc.) to use appropriate attributes and filters.

2. **Leverage Relationships**  
   Use relationships (e.g., `calls`, `runs_on`) to explore dependencies and interactions.

3. **Use Filtering to Narrow Scope**  
   Use filters to focus on specific entities based on attributes like `host.name` or `service.responseTime`.

4. **Use the Data Explorer**  
   Dynatrace’s Data Explorer can help identify available entities and their attributes.

---

## **Examples of Entity Queries**

### **Example 1: Query All Hosts**
```dql
fetch dt.entity.host
| fieldsAdd host.name, host.osType, aws.ec2.instanceId
| filter aws.ec2.instanceId contains "i-"
```

### **Example 2: Query Kubernetes Pods in a Specific Namespace**
```dql
fetch dt.entity.kubernetes_pod
| fieldsAdd kubernetes.podName, kubernetes.namespace
| filter kubernetes.namespace == "production"
```

### **Example 3: Query Services with Slow Response Times**
```dql
fetch dt.entity.service
| fieldsAdd service.name, service.responseTime
| filter service.responseTime > 1000
```

---

This documentation explains the concept of entities and entity types, their attributes, relationships, and how to query them effectively in Dynatrace. Let me know if you want further refinements or additions!

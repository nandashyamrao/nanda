
# **Entity Properties in Dynatrace: Metadata, Attributes, Tags, and Labels. 

## **1. What Are Entity Properties?**

**Entity Properties** is a collective term used in Dynatrace to describe all the descriptive and operational data about monitored entities. These include:

1. **Metadata**: Contextual information automatically collected by Dynatrace.
2. **Attributes**: Specific operational characteristics or metrics of an entity.
3. **Tags**: Organizational identifiers used for grouping, filtering, and automation.
4. **Labels**: Descriptive metadata added to entities for additional business or operational context.

Together, these properties enable Dynatrace users to comprehensively describe, analyze, and manage monitored entities.

---

## **2. Differences Between Metadata, Attributes, Tags, and Labels**

| **Type**             | **Definition**                                                                                                                                   | **Source**                                                                                              | **Example**                                         |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|----------------------------------------------------|
| **Metadata**         | Contextual information automatically collected about an entity's environment or identity.                                                        | Automatically collected by Dynatrace (e.g., cloud provider, region, environment).                       | `kubernetes.namespace`, `host.cloudProvider`       |
| **Attributes**       | Operational characteristics or performance metrics associated with an entity.                                                                  | Collected via Dynatrace instrumentation (e.g., OneAgent) or user-defined.                              | `kubernetes.container.cpuUsage`, `host.cpuCores`   |
| **Tags**             | Key-value pairs or identifiers assigned to entities for organization and filtering.                                                              | Manually added, rule-based (dynamic), or automatically inherited from metadata.                        | `env:production`, `team:frontend`                 |
| **Labels**           | Descriptive metadata added to entities for additional business or operational context.                                                           | User-defined via Dynatrace API, integrations, or deployment pipelines.                                 | `application=frontend`, `namespace=backend`        |

---

## **3. Sources for Entity Properties**

### **Metadata**
- **Where It Appears**:
  - Entity Overview pages (e.g., Kubernetes Pods, Nodes).
  - Dynatrace UI under entity details (e.g., `kubernetes.cluster.name`, `pod.namespace`).
  - Available for filtering in **Management Zones** and **DQL queries**.

#### **Examples of Kubernetes Metadata Sources**
| **Entity Type**       | **Metadata Example**                 | **Source**                             |
|-----------------------|---------------------------------------|----------------------------------------|
| **Kubernetes Node**   | `kubernetes.node.name`, `region`     | Automatically collected from the Kubernetes cluster. |
| **Kubernetes Pod**    | `kubernetes.namespace`, `pod.name`   | Kubernetes API metadata.               |

---

### **Attributes**
- **Where They Appear**:
  - Performance metrics in Dynatrace UI (e.g., container CPU/memory usage).
  - Used for filtering in DQL queries.
  - Visualized in Dashboards (e.g., container utilization graphs).

#### **Examples of Kubernetes Attribute Sources**
| **Entity Type**       | **Attribute Example**                | **Source**                            |
|-----------------------|---------------------------------------|---------------------------------------|
| **Kubernetes Pod**    | `kubernetes.container.cpuUsage`      | Derived from Kubernetes API and container monitoring. |
| **Kubernetes Node**   | `kubernetes.node.memoryUsage`        | Instrumentation via OneAgent.         |

---

### **Tags**
- **Where They Appear**:
  - Entity Overview and lists in the Dynatrace UI.
  - Used for dynamic filtering in **Management Zones** and **DQL queries**.

#### **Examples of Kubernetes Tag Sources**
| **Source**            | **Tag Example**                     | **How They Are Added**                |
|-----------------------|--------------------------------------|---------------------------------------|
| **Manual**            | `namespace:backend`                | Manually assigned to pods or namespaces. |
| **Rule-Based**        | `cloud:aws`, `team:backend`         | Dynamically assigned based on metadata (e.g., `kubernetes.namespace`). |
| **API/CI/CD**         | `deployment:1.2.3`                 | Added during deployment pipelines via API. |

---

### **Labels**
- **Where They Appear**:
  - Entity details in the Dynatrace UI.
  - Used in API responses for enriched business context.

#### **Examples of Kubernetes Label Sources**
| **Source**            | **Label Example**                   | **How They Are Added**                |
|-----------------------|--------------------------------------|---------------------------------------|
| **User-Defined**      | `namespace=backend`                 | Manually or via API.                  |
| **CI/CD Pipelines**   | `application=frontend`              | Assigned during deployments.          |
| **Third-Party Systems**| `priority=critical`                | Added via integrations or metadata mapping. |

---

## **4. Using Kubernetes Entity Properties in Queries**

### Combined Query Example
Use metadata, attributes, and tags to refine Kubernetes-specific queries:
```dql
fetch dt.entity.kubernetes.pod
| filter pod.namespace == "backend" and kubernetes.container.cpuUsage > 0.5
| fields pod.name, pod.namespace, kubernetes.container.cpuUsage, tags
```

**Result**:
| **Pod Name**         | **Namespace** | **CPU Usage** | **Tags**       |
|----------------------|---------------|---------------|----------------|
| backend-pod-1        | backend       | 0.6 cores     | team:backend   |

---

## **5. Key Kubernetes Use Cases**

### **Using Metadata**
- **Scenario**: Find all pods in the "frontend" namespace.
```dql
fetch dt.entity.kubernetes.pod
| filter pod.namespace == "frontend"
| fields pod.name, pod.namespace
```

**Result**:
| **Pod Name**         | **Namespace** |
|----------------------|---------------|
| frontend-pod-1       | frontend      |

---

### **Using Attributes**
- **Scenario**: Identify pods with high memory usage (>1GB).
```dql
fetch dt.entity.kubernetes.pod
| filter kubernetes.container.memoryUsage > 1
| fields pod.name, kubernetes.container.memoryUsage
```

**Result**:
| **Pod Name**         | **Memory Usage** |
|----------------------|------------------|
| backend-pod-2        | 1.5 GB           |

---

### **Using Tags**
- **Scenario**: Filter all Kubernetes entities tagged with `team:backend`.
```dql
fetch dt.entity.kubernetes.pod
| filter tags contains "team:backend"
| fields pod.name, tags
```

**Result**:
| **Pod Name**         | **Tags**         |
|----------------------|------------------|
| backend-pod-1        | team:backend     |

---

### **Using Labels**
- **Scenario**: Query logs labeled as `priority=critical`.
```dql
fetch logs
| filter labels.priority == "critical"
| fields log.message, labels.priority
```

**Result**:
| **Log Message**               | **Priority** |
|-------------------------------|--------------|
| Pod memory spike              | critical     |

---
# Saving the markdown content for Dynatrace Entity Properties Examples

content = """
# **Entity Properties in Dynatrace: Expanded Examples**

---

## **1. Metadata**

**Metadata** provides contextual information automatically collected about an entity’s environment or identity.

### **Examples of Metadata**

| **Entity Type**       | **Metadata Example**               | **Description**                                 |
|-----------------------|------------------------------------|-----------------------------------------------|
| Host                  | `host.cloudProvider`              | Cloud provider (e.g., AWS, Azure, GCP).        |
| Host                  | `host.osType`                     | OS type (e.g., Linux, Windows).                |
| Host                  | `host.region`                     | Geographical region (e.g., `us-east-1`).       |
| Service               | `service.type`                    | Type of service (e.g., Web Service, Database). |
| Service               | `service.environment`             | Service environment (e.g., Production, Staging). |
| Kubernetes Pod        | `kubernetes.cluster.name`         | Kubernetes cluster name.                       |
| Kubernetes Pod        | `kubernetes.namespace`            | Namespace to which the pod belongs.            |
| Kubernetes Node       | `kubernetes.node.name`            | Kubernetes node name.                          |
| Kubernetes Pod        | `kubernetes.container.name`       | Container name inside the pod.                 |
| Cloud Instance        | `cloud.instanceId`                | Unique cloud instance ID.                      |
| Cloud Instance        | `cloud.region`                    | Cloud region (e.g., `ap-south-1`).             |
| Application           | `application.version`             | Version of the application.                    |
| Application           | `application.users`               | Number of active users.                        |
| Logs                  | `log.source.aws.s3.bucket.name`   | S3 bucket name where the logs originate.       |
| Logs                  | `log.source.aws.s3.key.name`      | Key name for the log object in S3.             |
| Process Group         | `processGroup.technology`         | Technology (e.g., Java, Python, Nginx).        |
| Process               | `process.commandLineArguments`    | Command line arguments used to start the process. |
| ActiveGate            | `activeGate.id`                   | ID of the ActiveGate.                          |
| Network Device        | `network.device.type`             | Type of network device (e.g., Router, Switch). |
| Database              | `database.vendor`                 | Vendor of the database (e.g., MySQL, Oracle).  |

---

## **2. Attributes**

**Attributes** describe operational characteristics or performance metrics associated with an entity.

### **Examples of Attributes**

| **Entity Type**       | **Attribute Example**              | **Description**                               |
|-----------------------|------------------------------------|---------------------------------------------|
| Host                  | `host.cpuCores`                   | Number of CPU cores available on the host.   |
| Host                  | `host.memory.total`               | Total memory of the host.                    |
| Host                  | `host.disk.space.available`       | Available disk space.                        |
| Service               | `service.responseTime`            | Response time of the service.                |
| Service               | `service.errorRate`               | Percentage of errors in the service.         |
| Kubernetes Pod        | `kubernetes.container.cpuUsage`   | CPU usage of the container in the pod.       |
| Kubernetes Pod        | `kubernetes.container.memoryUsage`| Memory usage of the container.               |
| Kubernetes Node       | `kubernetes.node.network.incomingTraffic` | Incoming network traffic to the node.  |
| Kubernetes Node       | `kubernetes.node.disk.io`         | Disk I/O on the Kubernetes node.             |
| Cloud Instance        | `cloud.cost.hourly`               | Hourly cost of the cloud instance.           |
| Application           | `application.activeSessions`      | Number of active user sessions.              |
| Process Group         | `processGroup.instanceCount`      | Number of process instances in the group.    |
| Process               | `process.cpuUsage`                | CPU usage of the process.                    |
| Process               | `process.memoryUsage`             | Memory usage of the process.                 |
| Logs                  | `log.timestamp`                   | Timestamp of the log entry.                  |
| Logs                  | `log.level`                       | Log level (e.g., INFO, ERROR, WARNING).      |
| ActiveGate            | `activeGate.connectedAgents`      | Number of agents connected to the ActiveGate.|
| Database              | `database.queryTime.avg`          | Average query time for the database.         |
| Network Device        | `network.device.utilization`      | Utilization percentage of the network device.|
| Network Device        | `network.device.latency`          | Latency of the network device.               |

---

## **3. Tags**

**Tags** are key-value pairs used to organize and filter entities.

### **Examples of Tags**

| **Source**            | **Tag Example**                  | **Description**                                     |
|-----------------------|----------------------------------|---------------------------------------------------|
| Manual                | `env:production`                | Tagging entities belonging to the production environment. |
| Manual                | `team:frontend`                 | Tagging entities managed by the frontend team.    |
| Manual                | `service:payment-gateway`       | Tagging a specific service for payment gateway.   |
| Rule-Based            | `cloud:aws`                     | Dynamically tagging all AWS entities.             |
| Rule-Based            | `cloud:azure`                   | Dynamically tagging all Azure entities.           |
| Rule-Based            | `namespace:backend`             | Tagging all entities in the backend namespace.    |
| Rule-Based            | `region:us-east-1`              | Tagging all entities in a specific region.        |
| CI/CD Pipeline        | `build-version:1.2.3`           | Tagging entities based on the build version.      |
| CI/CD Pipeline        | `deployment:blue-green`         | Tagging for blue-green deployments.               |
| CI/CD Pipeline        | `feature:beta`                  | Tagging beta feature releases.                    |
| API                   | `priority:high`                 | Tagging entities for high-priority resources.     |
| API                   | `application:shopping-cart`     | Tagging all resources related to the shopping cart app. |
| API                   | `database:mysql`                | Tagging all MySQL databases.                      |
| API                   | `environment:staging`           | Tagging entities in the staging environment.      |
| Integration           | `monitoring-tool:dynatrace`     | Tagging for integration with Dynatrace.           |
| Integration           | `cost-center:marketing`         | Tagging entities for cost tracking.               |
| Integration           | `region:ap-south-1`             | Tagging entities for APAC region.                 |
| Integration           | `team:backend`                  | Tagging backend resources.                        |
| Integration           | `deployment:rolling`            | Tagging rolling deployment resources.             |

---

## **4. Labels**

**Labels** are descriptive metadata added to entities for additional business or operational context.

### **Examples of Labels**

| **Source**            | **Label Example**                | **Description**                                   |
|-----------------------|----------------------------------|-------------------------------------------------|
| Manual                | `priority=high`                 | Labeling high-priority entities.                |
| Manual                | `namespace=frontend`            | Labeling entities in the frontend namespace.    |
| Manual                | `cost-center=finance`           | Labeling resources for finance cost tracking.   |
| API                   | `team=backend`                  | Adding backend team ownership.                  |
| API                   | `region=us-west-2`              | Labeling entities in the US West region.        |
| API                   | `deployment=blue-green`         | Labeling resources used in blue-green deployment. |
| CI/CD Pipeline        | `application=checkout-service`  | Labeling resources related to the checkout service. |
| CI/CD Pipeline        | `build=1.5.2`                   | Labeling resources with the specific build version. |
| CI/CD Pipeline        | `feature=beta`                  | Labeling resources under beta testing.          |
| CI/CD Pipeline        | `owner=devops-team`             | Adding ownership for DevOps.                    |
| Integration           | `environment=production`        | Labeling resources for production environment.  |
| Integration           | `project=ecommerce`             | Labeling resources under the ecommerce project. |
| Integration           | `module=authentication`         | Labeling resources in the authentication module.|
| Integration           | `tier=critical`                 | Adding criticality label to resources.          |
| Integration           | `vendor=aws`                    | Labeling resources belonging to AWS.            |
| Integration           | `database-type=nosql`           | Labeling NoSQL databases.                       |
| Integration           | `compliance=gdpr`               | Adding GDPR compliance metadata.                |
| Integration           | `security-level=high`           | Labeling high-security resources.               |
| Integration           | `department=marketing`          | Adding department-specific labels.              |
| Integration           | `purpose=analytics`             | Labeling resources used for analytics.          |

---

Let me know if you’d like to expand further on these examples or explore specific use cases!
"""

file_path = "/mnt/data/Dynatrace_Entity_Properties_Examples.md"
with open(file_path, "w") as file:
    file.write(content)

file_path
## **6. Best Practices for Kubernetes Properties**

| **Best Practices**                  | **Details**                                                                 |
|-------------------------------------|-----------------------------------------------------------------------------|
| **Standardize Tagging**             | Use consistent tags for namespaces (e.g., `namespace:<name>`).              |
| **Use Dynamic Tagging Rules**       | Automate tags for cloud providers or environments (e.g., `cloud:aws`).      |
| **Combine Metadata with Attributes**| Filter pods by namespace (`metadata`) and CPU/memory usage (`attributes`).  |
| **Incorporate Labels for Context**  | Use labels to track application owners, priorities, and deployment versions.|

with open(file_path, "w") as file:
    file.write(content)

file_path

# Rewriting the content to include earlier examples and additional use cases for a complete guide

content = """
# **Entity Properties in Dynatrace: Metadata, Attributes, Tags, and Labels**

---

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
| **Host**              | `host.region`, `host.osType`         | Derived from the environment (e.g., AWS, Azure).      |

---

### **Attributes**
- **Where They Appear**:
  - Performance metrics in Dynatrace UI (e.g., container CPU/memory usage, service response time).
  - Used for filtering in DQL queries.
  - Visualized in Dashboards (e.g., container utilization graphs, error rates).

#### **Examples of Attribute Sources**
| **Entity Type**       | **Attribute Example**                | **Source**                            |
|-----------------------|---------------------------------------|---------------------------------------|
| **Kubernetes Pod**    | `kubernetes.container.cpuUsage`      | Derived from Kubernetes API and container monitoring. |
| **Kubernetes Node**   | `kubernetes.node.memoryUsage`        | Instrumentation via OneAgent.         |
| **Service**           | `service.responseTime`, `service.errorRate` | Derived from transaction monitoring.  |

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

## **5. Expanded Use Cases**

### **Using Metadata**
- **Scenario**: Find all AWS hosts in a specific region.
```dql
fetch dt.entity.host
| filter host.cloudProvider == "AWS" and host.region == "us-east-1"
| fields host.name, host.cloudProvider, host.region
```

### **Using Attributes**
- **Scenario**: Identify services with high error rates (>5%).
```dql
fetch dt.entity.service
| filter service.errorRate > 5
| fields service.name, service.errorRate
```

### **Using Tags**
- **Scenario**: Filter all Kubernetes entities tagged with `team:frontend`.
```dql
fetch dt.entity.kubernetes.pod
| filter tags contains "team:frontend"
| fields pod.name, tags
```

### **Using Labels**
- **Scenario**: Query logs labeled as `priority=high`.
```dql
fetch logs
| filter labels.priority == "high"
| fields log.message, labels.priority
```

---

## **6. Best Practices for Kubernetes Properties**

| **Best Practices**                  | **Details**                                                                 |
|-------------------------------------|-----------------------------------------------------------------------------|
| **Standardize Tagging**             | Use consistent tags for namespaces (e.g., `namespace:<name>`).              |
| **Use Dynamic Tagging Rules**       | Automate tags for cloud providers or environments (e.g., `cloud:aws`).      |
| **Combine Metadata with Attributes**| Filter pods by namespace (`metadata`) and CPU/memory usage (`attributes`).  |
| **Incorporate Labels for Context**  | Use labels to track application owners, priorities, and deployment versions.|

---

This updated guide consolidates earlier examples, Kubernetes-specific use cases, and comprehensive best practices for **metadata**, **attributes**, **tags**, and **labels** in Dynatrace. Let me know if you need further additions!
"""

file_path = "/mnt/data/Dynatrace_Entity_Properties_Enhanced.md"
with open(file_path, "w") as file:
    file.write(content)

file_path

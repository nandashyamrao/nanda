
# Understanding and Using `fetch entity` in Dynatrace

The `fetch entity` command in Dynatrace is a powerful way to query **entities** that represent the objects or components being monitored in your environment. Entities include hosts, services, applications, processes, Kubernetes workloads, and cloud-native resources.

This document provides a detailed explanation, practical examples, and use cases for using `fetch entity` effectively.

---

## **1. Purpose of Querying Entities**

Querying entities is useful when you need to:
1. Explore metadata, such as tags, names, or IDs, about the objects in your environment.
2. Analyze relationships between entities, such as which services depend on each other.
3. Serve as a starting point for more complex queries involving logs, metrics, or events.
4. Build dashboards or alerts that group or filter entities based on their attributes.

---

## **2. What Is Retrieved with `fetch entity`?**

The `fetch entity` query retrieves metadata about entities, such as:
- **Name (`entity.name`)**: The human-readable name of the entity.
- **Type (`entity.type`)**: The type of the entity (e.g., HOST, SERVICE, APPLICATION).
- **ID (`entity.id`)**: A unique identifier for the entity.
- **Tags (`tags`)**: Tags associated with the entity (e.g., `env:prod`, `team:frontend`).
- **Relationships**: Connections to other entities (e.g., `called_by`, `sends_to`).
- **Attributes**: Additional metadata like cloud provider, OS type, or application version.

---

## **3. Practical Examples**

### **Example 1: Fetching All Hosts**
```dql
fetch dt.entity.host
| fields entity.name, entity.id, host.osType, tags
```

- **What This Does:** Retrieves all hosts in your environment, displaying their names, IDs, operating system types, and associated tags.
- **Use Case:** Identify which hosts are running Linux or Windows, and check their environment tags.

---

### **Example 2: Fetching Services with a Specific Name**
```dql
fetch dt.entity.service
| filter entity.name == "order-service"
| fields entity.name, entity.id, tags
```

- **What This Does:** Fetches metadata for the `order-service`, such as its unique ID and tags.
- **Use Case:** Quickly locate a specific service and verify its metadata.

---

### **Example 3: Fetching Applications and Their Associated Tags**
```dql
fetch dt.entity.application
| fields entity.name, entity.id, tags
```

- **What This Does:** Lists all applications, showing their names, IDs, and tags.
- **Use Case:** Identify which applications are tagged for a specific team or environment, such as `team:frontend`.

---

### **Example 4: Fetching Relationships Between Entities**
```dql
fetch dt.entity.service
| filter entity.name == "order-service"
| fields entity.name, called_by, sends_to
```

- **What This Does:** Displays which services call or are called by the `order-service`.
- **Use Case:** Analyze service dependencies for troubleshooting or architecture review.

---

## **4. Advanced Queries Combining Entities and Data Sources**

Entities can serve as the starting point for more complex queries. Here are examples that combine entities with logs, metrics, and events.

### **Combining Entities with Logs**
```dql
fetch dt.entity.service
| filter entity.name == "order-service"
| join (
    fetch logs
    | filter log.source.service.name == "order-service"
) on entity.id
| fields entity.name, log.content, log.timestamp
```

- **What This Does:** Fetches logs associated with the `order-service`, showing the service name, log content, and timestamps.
- **Use Case:** Troubleshoot application errors by combining metadata with logs.

---

### **Combining Entities with Metrics**
```dql
fetch dt.entity.host
| filter host.osType == "linux"
| join (
    fetch metrics
    | filter metric.name == "cpu.usage"
) on entity.id
| fields entity.name, metric.value, metric.timestamp
```

- **What This Does:** Fetches all Linux hosts and joins their CPU usage metrics.
- **Use Case:** Monitor resource utilization for Linux hosts.

---

### **Combining Entities with Events**
```dql
fetch dt.entity.application
| filter entity.name == "retail-app"
| join (
    fetch events
    | filter event.type == "DEPLOYMENT"
) on entity.id
| fields entity.name, event.name, event.timestamp
```

- **What This Does:** Lists deployment events for the `retail-app`.
- **Use Case:** Validate if recent deployments impacted application performance.

---

## **5. Common Attributes of Entities**

Here are key attributes that you can retrieve or filter on when querying entities:

| **Attribute**             | **Description**                                | **Example**                   |
|---------------------------|-----------------------------------------------|-------------------------------|
| `entity.name`             | Name of the entity.                          | `order-service`, `web-host`  |
| `entity.type`             | Type of the entity.                          | `HOST`, `SERVICE`, `APPLICATION` |
| `entity.id`               | Unique identifier for the entity.            | `HOST-12345`, `SERVICE-67890` |
| `tags`                    | Tags assigned to the entity.                 | `env:prod`, `team:frontend`  |
| `called_by`               | Services calling this service.               | `ui-service`                 |
| `sends_to`                | Services this service sends data to.         | `payment-service`            |
| `host.osType`             | Operating system type of the host.           | `linux`, `windows`           |
| `cloud.provider`          | Cloud provider associated with the entity.   | `AWS`, `Azure`, `GCP`        |

---

## **6. Benefits of Querying Entities**

1. **Metadata Exploration:** Quickly retrieve detailed metadata about monitored components.
2. **Dependency Analysis:** Understand how services, hosts, or applications interact.
3. **Targeted Data Fetching:** Use entities as a base for joining logs, metrics, or events for deeper insights.
4. **Dashboard Customization:** Build dashboards by grouping entities using tags or attributes.

---

## **7. Best Practices**

1. **Start with a Simple Entity Query:** Begin by fetching entities and their metadata to understand the data structure.
   ```dql
   fetch dt.entity.service
   | fields entity.name, tags
   ```

2. **Use Filters to Narrow Results:** Apply filters to focus on specific entities or attributes.
   ```dql
   fetch dt.entity.host
   | filter host.osType == "linux"
   ```

3. **Combine with Data Sources When Needed:** Use joins to enrich entity queries with logs, metrics, or events for deeper insights.

4. **Leverage Relationships:** Use attributes like `called_by` or `sends_to` to map dependencies and interactions.

5. **Test Queries Incrementally:** Start with basic queries and add filters or joins step by step to avoid complexity.

---

## **8. Example Use Cases**

### **Use Case 1: Building a Dependency Map**
Fetch all services and their dependencies:
```dql
fetch dt.entity.service
| fields entity.name, called_by, sends_to
```

### **Use Case 2: Tagging Strategy Validation**
Find entities with missing or incorrect tags:
```dql
fetch dt.entity.host
| filter tags does not contain "env:prod"
| fields entity.name, tags
```

### **Use Case 3: Root Cause Analysis**
Combine service metadata with error logs:
```dql
fetch dt.entity.service
| filter entity.name == "order-service"
| join (
    fetch logs
    | filter content contains "error"
) on entity.id
| fields entity.name, log.content, log.timestamp
```

---

## **Conclusion**
The `fetch entity` command is a powerful way to explore, filter, and analyze the components being monitored by Dynatrace. By combining entities with data sources like logs, metrics, and events, you can create targeted queries for troubleshooting, dependency analysis, and operational insights.

Let me know if you'd like to explore more examples or build specific queries!

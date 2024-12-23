


### Dynatrace organizes observability data into **data sources** and **entities**. Understanding the distinction between these two concepts is essential to querying and analyzing your environment effectively. This document explains their relationship, when to join data sources, and how to create effective queries.

---

## **Data Sources vs. Entities**

### **What Are Data Sources?**
Data sources represent **streams of data** collected by Dynatrace. These include:
- **Logs:** Captured from applications, services, and infrastructure, representing events, errors, and operational details.
- **Metrics:** Time-series data points measuring performance, such as CPU usage or response times.
- **Events:** State changes or occurrences in your environment, like deployments, alerts, and configuration changes.

### **What Are Entities?**
Entities are **monitored objects** within your environment, such as:
- Hosts
- Services
- Applications
- Processes
- Containers
- Cloud resources

Entities generate or are associated with data streams (logs, metrics, events) and are identified by attributes like `entity.id` or `entity.name`.

---

## **How Data Sources Relate to Entities**

While logs, metrics, and events are streams of data, they are **tied to entities**. For example:
- **Logs:** A service or host produces log data during its operation.
- **Metrics:** Metrics measure performance or usage for an entity.
- **Events:** Events describe changes or incidents affecting an entity.

### **Approach to Queries**
1. **Start with the Data Source:** Choose the type of data you want to analyze (e.g., logs, metrics, or events).
2. **Filter by Entities:** Use attributes (like `entity.name` or `entity.type`) to narrow your query to specific entities.
3. **Correlate Data Sources (Optional):** Join multiple data sources for deeper insights.

---

## **Practical Example: Logs, Metrics, and Events**

1. **Logs:** Capturing error details.
   ```dql
   fetch logs
   | filter log.source.service.name == "order-service"
   | fields log.content, timestamp
   ```

2. **Metrics:** Measuring performance.
   ```dql
   fetch metrics
   | filter entity.name == "web-server-1" and metric.name == "cpu.usage"
   | fields metric.value, timestamp
   ```

3. **Events:** Tracking changes.
   ```dql
   fetch events
   | filter event.type == "DEPLOYMENT"
   | fields event.name, entity.name, timestamp
   ```

---

## **When and Why to Combine Data Sources?**

Combining multiple data sources (e.g., logs, metrics, and events) in a single query can provide a richer understanding of your environment. This is particularly useful in scenarios such as:

### **1. Root Cause Analysis**
Correlate metrics, logs, and events to pinpoint the origin of an issue.

#### Example Query:
```dql
fetch logs
| filter log.source.service.name == "order-service"
| join (
    fetch metrics
    | filter entity.name == "order-service" and metric.name == "response.time"
) on entity.id
| join (
    fetch events
    | filter event.type == "DEPLOYMENT"
) on entity.id
| fields log.content, metric.value, event.name, timestamp
```

### **2. Change Impact Analysis**
Validate whether a deployment caused errors or resource issues.

#### Example Query:
```dql
fetch events
| filter event.type == "DEPLOYMENT"
| join (
    fetch metrics
    | filter metric.name == "cpu.usage"
) on entity.id
| join (
    fetch logs
    | filter content contains "error"
) on entity.id
| fields event.name, metric.value, log.content, timestamp
```

### **3. Service Dependency Monitoring**
Understand how downstream services impact upstream services.

#### Example Query:
```dql
fetch logs
| filter log.source.service.name == "frontend-service"
| join (
    fetch metrics
    | filter entity.name == "backend-service" and metric.name == "failure.rate"
) on entity.id
| fields log.content, metric.value, timestamp
```

---

## **How Joining Works in Dynatrace**

### **Steps to Join Data Sources**
1. **Start with the Base Query:** Choose a primary data source.
2. **Use `join` to Add Related Data:** Bring in data from other sources using a shared attribute (e.g., `entity.id`).
3. **Define the Output:** Use `fields` to select attributes for display.

### Syntax:
```dql
<base query>
| join (<additional query>) on <common field>
| fields <list of fields>
```

### Common Identifiers:
- `entity.id`
- `entity.name`
- `log.source.service.name`

---

## **Best Practices for Joining Data Sources**
1. **Start Small:** Begin with a single data source and add joins iteratively.
2. **Minimize Joins:** Only join data sources when necessary to reduce query complexity.
3. **Use Common Identifiers:** Ensure the data sources share attributes like `entity.id` or `entity.name`.
4. **Test Queries Independently:** Validate each data source query before joining.
5. **Focus Outputs:** Limit the number of fields in your result for clarity.

---

## **Conclusion**

- Data sources (logs, metrics, events) and entities are interconnected.
- Start with a **data source**, filter by **entities**, and combine sources only when necessary.
- Use joins to correlate data for advanced scenarios like root cause analysis, change validation, and dependency monitoring.
- Follow best practices to create efficient, readable, and actionable  Dynatrace's observability capabilities.


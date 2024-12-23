
# Combining Dynatrace Data Sources in Queries

Dynatrace allows you to query different data sources, such as logs, metrics, and events, and filter them by associated entities. However, there are scenarios where combining multiple data sources in a single query can provide a richer and more comprehensive understanding of your environment. This guide explains how to approach combining data sources, why it might be necessary, and practical use cases.

---

## **Starting with the Data Source and Picking an Entity**

In Dynatrace, you typically start your query with a **data source** (e.g., logs, metrics, or events) and then narrow it down to specific entities within that data source. Here's the general approach:

1. **Choose the Data Source:** Identify the type of data you want to query:
   - Logs for operational data.
   - Metrics for performance trends.
   - Events for changes and incidents.

2. **Filter or Select Entities:** Use attributes like `entity.name`, `entity.type`, or tags to filter the data by the entities generating it.

3. **Select Fields to Display:** Use the `fields` command to specify which attributes to include in the result.

### Example Queries:
#### Fetch Logs for a Specific Service
```dql
fetch logs
| filter log.source.service.name == "order-service"
| fields log.source.service.name, content, timestamp
```

#### Fetch Metrics for a Host
```dql
fetch metrics
| filter entity.name == "web-server-1" and metric.name == "cpu.usage"
| fields metric.name, value, timestamp
```

#### Fetch Events Related to Deployments
```dql
fetch events
| filter event.type == "DEPLOYMENT"
| fields event.name, entity.name, timestamp
```

---

## **When and Why to Combine Data Sources?**

Combining multiple data sources (e.g., logs, metrics, and events) in a single query is not always necessary. However, it becomes essential in specific scenarios such as:

1. **Root Cause Analysis:** Correlating metrics, logs, and events to pinpoint the origin of an issue.
2. **Change Impact Analysis:** Validating the effect of a deployment or configuration change by examining associated logs and metrics.
3. **Service Dependency Monitoring:** Understanding how a downstream service affects an upstream service.
4. **Alert Enrichment:** Adding context to alerts by combining metrics, logs, and events.

---

## **How Does Joining Work in Dynatrace?**

Dynatrace Query Language (DQL) supports combining multiple data sources using `join`. The process involves:

1. **Start with the Base Query:** Choose the primary data source to begin your query.
2. **Join Additional Data:** Use the `join` command to bring in related data from another data source.
3. **Define the Output:** Use `fields` to select attributes from each data source.

### Syntax:
```dql
<base query>
| join (<additional query>) on <common field>
| fields <list of fields>
```

### Common Identifiers for Joining:
- `entity.id`
- `entity.name`
- `log.source.service.name`

---

## **Use Cases for Joining Data Sources**

### **1. Root Cause Analysis**
Combine logs, metrics, and events to investigate an incident.
#### Query:
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
This query correlates:
- Logs from `order-service`.
- Response time metrics for performance degradation.
- Deployment events to identify changes causing the issue.

---

### **2. Change Impact Analysis**
Validate if a deployment increased resource usage or caused errors.
#### Query:
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
This query links:
- Deployment events.
- CPU usage metrics.
- Error logs.

---

### **3. Service Dependency Monitoring**
Understand how a backend service impacts a frontend service.
#### Query:
```dql
fetch logs
| filter log.source.service.name == "frontend-service"
| join (
    fetch metrics
    | filter entity.name == "backend-service" and metric.name == "failure.rate"
) on entity.id
| fields log.content, metric.value, timestamp
```
This query correlates:
- Logs from `frontend-service`.
- Failure rate metrics for `backend-service`.

---

### **4. Alert Context Enrichment**
Add logs and events to an alert's associated metrics for better context.
#### Query:
```dql
fetch metrics
| filter entity.name == "web-server-1" and metric.name == "disk.usage"
| join (
    fetch logs
    | filter log.source.host.name == "web-server-1" and content contains "disk error"
) on entity.id
| join (
    fetch events
    | filter event.type == "ALERT"
) on entity.id
| fields metric.name, metric.value, log.content, event.name, timestamp
```
This query helps you understand:
- Disk usage metrics.
- Disk error logs.
- Alert events.

---

## **Best Practices for Joining Data Sources**
1. **Start Small:** Begin with one data source and add joins iteratively.
2. **Minimize Joins:** Use joins only when necessary to avoid performance issues.
3. **Ensure Common Identifiers:** Verify that data sources share a common field like `entity.id`.
4. **Test Filters First:** Ensure each query returns valid results before joining.
5. **Use Relevant Fields:** Limit fields in the output to keep results concise.

---

## **Conclusion**

- Start with the **data source** (`logs`, `metrics`, `events`) and refine by entity.
- Use joins to correlate multiple data sources for advanced use cases like root cause analysis, change validation, and service dependency monitoring.
- Always test filters and refine outputs for clarity and performance.



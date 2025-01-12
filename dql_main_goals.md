
# Main Goals of Dynatrace Query Language (DQL)

This document elaborates on the main goals of Dynatrace Query Language (DQL), including practical examples and use cases to help users understand its purpose and capabilities.

## 1. Data Retrieval

**Goal**: Provide a flexible way to retrieve data across logs, metrics, traces, events, and entities.

- **Use Case**: Retrieve host CPU usage data for the past hour.
- **Example**:
    ```dql
    fetch metrics
    | filter metric.key == "builtin:host.cpu.usage"
    | filter timestamp >= now() - 1h
    | fields timestamp, entity.name, metric.value
    ```

- **Output**: 
  - Timestamps
  - Host names
  - CPU usage values for each host.

---

## 2. Filtering and Narrowing Data

**Goal**: Enable precise filtering to focus on relevant subsets of data.

- **Use Case**: Retrieve all error logs from a specific service.
- **Example**:
    ```dql
    fetch logs
    | filter log.severity == "ERROR"
    | filter dt.entity.service == "order-service"
    | fields timestamp, message
    ```

- **Output**: 
  - Error messages with timestamps from the `order-service`.

---

## 3. Correlation and Relationships

**Goal**: Map relationships between entities to understand dependencies.

- **Use Case**: Identify which databases are being called by a specific service.
- **Example**:
    ```dql
    fetch dt.entity.service
    | filter service.name == "checkout-service"
    | join fetch dt.entity.database on service.calls == database
    | fields service.name, database.name, database.response_time
    ```

- **Output**: 
  - Databases called by the `checkout-service` along with their response times.

---

## 4. Real-Time and Historical Analysis

**Goal**: Support both real-time monitoring and historical analysis.

- **Use Case**: Analyze response times of a service over the past week.
- **Example**:
    ```dql
    fetch metrics
    | filter metric.key == "builtin:service.response.time"
    | filter dt.entity.service == "payment-service"
    | filter timestamp >= now() - 7d
    | avg(metric.value)
    ```

- **Output**: 
  - Average response time for `payment-service` over the last 7 days.

---

## 5. Aggregation and Summarization

**Goal**: Summarize large datasets for easier interpretation.

- **Use Case**: Count the number of error logs in the last 24 hours.
- **Example**:
    ```dql
    fetch logs
    | filter log.severity == "ERROR"
    | filter timestamp >= now() - 1d
    | count()
    ```

- **Output**: 
  - Total number of error logs.

---

## 6. Visualization and Dashboards

**Goal**: Provide a foundation for creating visual dashboards and widgets.

- **Use Case**: Show the top 5 services with the highest error rates.
- **Example**:
    ```dql
    fetch metrics
    | filter metric.key == "builtin:service.errors"
    | group by entity.name
    | sum(metric.value)
    | sort sum desc
    | limit 5
    ```

- **Output**: 
  - A list of the top 5 services with their error counts.

---

## 7. Root Cause Analysis

**Goal**: Identify the root cause of performance issues or anomalies.

- **Use Case**: Pinpoint services contributing to high latency in a distributed trace.
- **Example**:
    ```dql
    fetch traces
    | filter trace.status == "ERROR"
    | filter dt.entity.service == "checkout-service"
    | fields timestamp, trace.id, span.duration, span.error.message
    ```

- **Output**: 
  - Trace IDs, span durations, and error messages for the `checkout-service`.

---

## 8. Custom Analysis

**Goal**: Perform tailored analyses specific to user needs.

- **Use Case**: Analyze the distribution of request latencies for a custom API.
- **Example**:
    ```dql
    fetch metrics
    | filter metric.key == "custom.api.latency"
    | group by latency.bucket
    | count()
    ```

- **Output**: 
  - Request count for each latency bucket.

---

## 9. Optimization and Cost Management

**Goal**: Help optimize resource usage and monitor costs.

- **Use Case**: Monitor AWS cost usage for a specific account.
- **Example**:
    ```dql
    fetch metrics
    | filter metric.key == "builtin:aws.billing.usage"
    | filter account.id == "123456789012"
    | fields timestamp, metric.value
    ```

- **Output**: 
  - AWS billing data over time for the specified account.

---

## 10. Automation and Integration

**Goal**: Enable seamless integration with automation pipelines and external tools.

- **Use Case**: Automate incident detection and notification for slow services.
- **Example**:
    ```dql
    fetch logs
    | filter log.severity == "ERROR"
    | sort timestamp desc
    | limit 10
    ```

- **Automation**: 
  - This query result can trigger an alert or feed into an incident management tool.

---

## Key Takeaways

1. **DQL is Flexible**: Adaptable to various monitoring and troubleshooting needs.
2. **Data Correlation**: Helps map relationships and dependencies.
3. **Real-Time and Historical Insights**: Enables immediate and retrospective analysis.
4. **Custom Analysis**: Supports tailored queries for unique challenges.
5. **Actionable Outputs**: Directly feeds dashboards, alerts, and automation pipelines.

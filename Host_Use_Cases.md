
# Host Use Cases in Dynatrace (DQL)

This document provides comprehensive **use cases for hosts** in Dynatrace, along with the **corresponding DQL queries**.

---

## 1. List All Hosts
**Use Case**: Retrieve basic information about all hosts in your environment.

```sql
fetch dt.entity.host
| fields host.name, host.ip, cloud.provider, availability_zone
```

**Explanation**: Lists all hosts with their name, IP address, cloud provider, and availability zone.

---

## 2. Identify Hosts with High CPU Usage
**Use Case**: Find the top 5 hosts with the highest CPU usage.

```sql
fetch dt.entity.host
| fields host.name, cpu.usage
| sort cpu.usage desc
| limit 5
```

**Explanation**: Retrieves and sorts hosts by CPU usage in descending order, showing the top 5.

---

## 3. Identify Underutilized Hosts
**Use Case**: Find hosts with less than 10% CPU usage.

```sql
fetch dt.entity.host
| filter cpu.usage < 10
| fields host.name, cpu.usage
```

**Explanation**: Filters hosts with CPU usage below 10% and displays their names and usage.

---

## 4. Hosts with High Memory Usage
**Use Case**: Retrieve the top 5 hosts with the highest memory usage.

```sql
fetch dt.entity.host
| fields host.name, memory.usage
| sort memory.usage desc
| limit 5
```

**Explanation**: Fetches hosts, sorts them by memory usage, and displays the top 5.

---

## 5. Disk Utilization Across Hosts
**Use Case**: List all hosts with their disk utilization.

```sql
fetch dt.entity.host
| fields host.name, disk.used, disk.total, disk.utilization
```

**Explanation**: Displays disk usage metrics for each host, including used space, total space, and utilization percentage.

---

## 6. Hosts by Cloud Provider
**Use Case**: Group hosts by their cloud provider and count them.

```sql
fetch dt.entity.host
| group by cloud.provider
| count()
| fields cloud.provider, count
```

**Explanation**: Groups hosts by cloud provider (e.g., AWS, Azure) and counts the number in each group.

---

## 7. Hosts in a Specific Availability Zone
**Use Case**: Find all hosts running in `us-east-1a`.

```sql
fetch dt.entity.host
| filter availability_zone == "us-east-1a"
| fields host.name, cloud.provider, availability_zone
```

**Explanation**: Filters hosts by availability zone and lists their names, cloud providers, and zones.

---

## 8. Hosts with Frequent Process Restarts
**Use Case**: Identify hosts where processes have restarted more than 3 times in the last day.

```sql
fetch dt.entity.host
| filter process.restart_count > 3
| filter timestamp > now()-1d
| fields host.name, process.restart_count
```

**Explanation**: Filters hosts with frequent process restarts in the last day.

---

## 9. Hosts Running Specific Applications
**Use Case**: Find hosts running a specific application (e.g., NGINX).

```sql
fetch dt.entity.host
| filter process.name contains "nginx"
| fields host.name, process.name
```

**Explanation**: Filters hosts running processes with "nginx" in the name and displays the host and process names.

---

## 10. Hosts with Anomalies
**Use Case**: Identify hosts with detected anomalies in the last 24 hours.

```sql
fetch events
| filter event.type == "ANOMALY"
| filter dt.entity.host exists
| filter timestamp > now()-24h
| fields dt.entity.host, event.title, timestamp
```

**Explanation**: Lists hosts with anomaly events, their titles, and timestamps in the last day.

---

## 11. Average CPU and Memory Usage per Cloud Provider
**Use Case**: Calculate the average CPU and memory usage for hosts grouped by cloud provider.

```sql
fetch dt.entity.host
| summarize avg_cpu = avg(cpu.usage), avg_memory = avg(memory.usage) by cloud.provider
```

**Explanation**: Groups hosts by cloud provider and calculates their average CPU and memory usage.

---

## 12. Compare CPU Usage Between Hosts
**Use Case**: Compare CPU usage for two specific hosts.

```sql
fetch dt.entity.host
| filter host.name in ["host-a", "host-b"]
| fields host.name, cpu.usage
```

**Explanation**: Filters for two specific hosts and compares their CPU usage.

---

## 13. Hosts with High Network Traffic
**Use Case**: Identify hosts with high network input and output traffic.

```sql
fetch dt.entity.host
| fields host.name, network.in, network.out
| sort network.in desc, network.out desc
| limit 5
```

**Explanation**: Lists the top 5 hosts with the highest network input and output traffic.

---

## 14. Hosts with Missing Tags
**Use Case**: Find hosts missing a specific tag (e.g., `environment=production`).

```sql
fetch dt.entity.host
| filter not tag.environment == "production"
| fields host.name, tag.environment
```

**Explanation**: Identifies hosts missing the `environment=production` tag.

---

## 15. Disk Space Alerts on Hosts
**Use Case**: Identify hosts with disk utilization above 90%.

```sql
fetch dt.entity.host
| filter disk.utilization > 90
| fields host.name, disk.utilization
```

**Explanation**: Filters hosts where disk utilization exceeds 90% and displays their names and utilization.

---

## 16. Count Hosts by Operating System
**Use Case**: Count the number of hosts running each operating system.

```sql
fetch dt.entity.host
| group by os.type
| count()
| fields os.type, count
```

**Explanation**: Groups hosts by operating system type and counts them.

---

## 17. Host Lifecycle Analysis
**Use Case**: Track hosts added or removed in the last week.

```sql
fetch dt.entity.host
| filter lifecycle.state in ["added", "removed"]
| filter timestamp > now()-7d
| fields host.name, lifecycle.state, timestamp
```

**Explanation**: Filters hosts added or removed in the last week, showing their names, states, and timestamps.

---

## 18. Historical Performance of Hosts
**Use Case**: Analyze historical CPU usage trends for the last 30 days.

```sql
fetch metrics
| filter metric.key == "builtin:host.cpu.usage"
| filter timestamp > now()-30d
| summarize avg_cpu = avg(datapoint.value) by day(timestamp)
```

**Explanation**: Summarizes daily average CPU usage over the past month.

---

## 19. Cross-Host Dependency Analysis
**Use Case**: Find relationships between hosts and the services they support.

```sql
fetch dt.entity.host
| join fetch dt.entity.service on host.calls == service
| fields host.name, service.name
```

**Explanation**: Joins host and service entities to analyze their dependencies.

---

## 20. Real-Time Monitoring of Host Metrics
**Use Case**: Monitor real-time CPU and memory usage of all hosts.

```sql
fetch dt.entity.host
| filter timestamp > now()-15m
| fields host.name, cpu.usage, memory.usage
```

**Explanation**: Retrieves recent CPU and memory usage data for all hosts within the last 15 minutes.

---

### End of Use Cases

---

## 21. Hosts with Multiple IP Addresses
**Use Case**: Identify hosts with more than one IP address.

```sql
fetch dt.entity.host
| filter array_length(host.ip) > 1
| fields host.name, host.ip
```

**Explanation**: Filters hosts that have multiple IP addresses and displays their names and IP lists.

---

## 22. Average CPU Usage by Availability Zone
**Use Case**: Calculate the average CPU usage of hosts grouped by availability zone.

```sql
fetch dt.entity.host
| summarize avg_cpu = avg(cpu.usage) by availability_zone
```

**Explanation**: Groups hosts by availability zone and calculates the average CPU usage for each zone.

---

## 23. Hosts with Frequent Health State Changes
**Use Case**: Find hosts with frequent health state changes in the last 7 days.

```sql
fetch events
| filter event.type == "HEALTH_STATE_CHANGE"
| filter timestamp > now()-7d
| summarize change_count = count() by dt.entity.host
| filter change_count > 5
| fields dt.entity.host, change_count
```

**Explanation**: Lists hosts with more than 5 health state changes in the past week.

---

## 24. Hosts Supporting Multiple Services
**Use Case**: Identify hosts that support more than 3 services.

```sql
fetch dt.entity.host
| join fetch dt.entity.service on host.calls == service
| summarize service_count = count() by dt.entity.host
| filter service_count > 3
| fields dt.entity.host, service_count
```

**Explanation**: Joins host and service data, counts the number of services per host, and filters hosts with more than 3 services.

---

## 25. Hosts with High Error Rates
**Use Case**: Retrieve hosts experiencing error rates above 5%.

```sql
fetch dt.entity.host
| filter error.rate > 5
| fields host.name, error.rate
```

**Explanation**: Filters hosts with error rates above 5% and lists their names and rates.

---

## 26. Hosts with Long Boot Times
**Use Case**: Identify hosts that take longer than 5 minutes to boot.

```sql
fetch dt.entity.host
| filter boot.time > 300
| fields host.name, boot.time
```

**Explanation**: Filters hosts with boot times longer than 300 seconds (5 minutes).

---

## 27. Hosts with Specific Tags
**Use Case**: Find all hosts tagged as "production" or "staging."

```sql
fetch dt.entity.host
| filter tag.environment in ["production", "staging"]
| fields host.name, tag.environment
```

**Explanation**: Filters hosts based on the `environment` tag.

---

## 28. Hosts with Low Network Traffic
**Use Case**: List hosts with network traffic below 1 MB/s.

```sql
fetch dt.entity.host
| filter network.in < 1 and network.out < 1
| fields host.name, network.in, network.out
```

**Explanation**: Filters hosts with low input and output network traffic.

---

## 29. Identify Hosts Running Deprecated Processes
**Use Case**: Find hosts running outdated or deprecated software (e.g., "Java 8").

```sql
fetch dt.entity.host
| filter process.runtime.version contains "Java 8"
| fields host.name, process.name, process.runtime.version
```

**Explanation**: Filters hosts with processes running deprecated software versions.

---

## 30. Hosts Running the Most Resource-Intensive Process
**Use Case**: Identify the most resource-intensive process on each host.

```sql
fetch dt.entity.process
| sort cpu.usage desc
| summarize top_cpu_usage = max(cpu.usage) by dt.entity.host
| fields dt.entity.host, top_cpu_usage
```

**Explanation**: Aggregates the highest CPU usage process per host.

---

## 31. Hosts with High Disk Latency
**Use Case**: Find hosts experiencing high disk latency (e.g., > 10 ms).

```sql
fetch dt.entity.host
| filter disk.latency > 10
| fields host.name, disk.latency
```

**Explanation**: Filters hosts with disk latency above 10 milliseconds.

---

## 32. Hosts with Frequent Service Failures
**Use Case**: Identify hosts where services failed more than 5 times in the last 7 days.

```sql
fetch events
| filter event.type == "SERVICE_FAILURE"
| filter timestamp > now()-7d
| summarize failure_count = count() by dt.entity.host
| filter failure_count > 5
| fields dt.entity.host, failure_count
```

**Explanation**: Lists hosts with more than 5 service failures in the past week.

---

## 33. Top Hosts by Process Count
**Use Case**: Find the top 5 hosts with the most running processes.

```sql
fetch dt.entity.host
| summarize process_count = count(process.id) by host.name
| sort process_count desc
| limit 5
```

**Explanation**: Counts running processes per host, sorts by the highest count, and limits to the top 5.

---

## 34. Historical Trends for Host Health
**Use Case**: Track health state changes for a specific host over the last month.

```sql
fetch events
| filter dt.entity.host == "host-a"
| filter event.type == "HEALTH_STATE_CHANGE"
| filter timestamp > now()-30d
| fields timestamp, event.title, new_state
```

**Explanation**: Lists health state changes for a specific host in the last month.

---

## 35. Hosts with Unstable Network Connections
**Use Case**: Identify hosts with frequent network disconnections.

```sql
fetch events
| filter event.type == "NETWORK_DISCONNECT"
| summarize disconnect_count = count() by dt.entity.host
| filter disconnect_count > 3
| fields dt.entity.host, disconnect_count
```

**Explanation**: Lists hosts with more than 3 network disconnections.

---

## 36. Hosts Running Services in Production
**Use Case**: Find all production hosts running active services.

```sql
fetch dt.entity.host
| filter tag.environment == "production"
| join fetch dt.entity.service on host.calls == service
| filter service.state == "active"
| fields host.name, service.name
```

**Explanation**: Joins hosts and services, filters for production hosts with active services.

---

## 37. Hosts with High File Descriptors
**Use Case**: Identify hosts with file descriptor usage exceeding 90%.

```sql
fetch dt.entity.host
| filter file_descriptor.usage > 90
| fields host.name, file_descriptor.usage
```

**Explanation**: Filters hosts with high file descriptor usage.

---

### End of Additional Use Cases

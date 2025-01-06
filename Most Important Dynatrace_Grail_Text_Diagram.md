
# **Dynatrace Grail: Library Analogy Hierarchy**

```plaintext
+---------------------------------------------+
|                 ENTITY                      |
|---------------------------------------------|
| Represents the contextual grouping:         |
| - Services, Hosts, Applications             |
| Examples:                                   |
| - Payment Service                           |
| - Checkout Service                          |
+---------------------------------------------+
               ↓
+---------------------------------------------+
|                 TABLE                       |
|---------------------------------------------|
| Logical organization of data by type:       |
| - Logs, Metrics, Events, Spans              |
| Examples:                                   |
| - Logs Table                                |
| - Metrics Table                             |
+---------------------------------------------+
               ↓
+---------------------------------------------+
|                 BUCKET                      |
|---------------------------------------------|
| Physical storage with retention policies:   |
| - Default Logs Bucket                       |
| - Payment Logs Bucket                       |
| - Audit Logs Bucket                         |
+---------------------------------------------+
               ↓
+---------------------------------------------+
|                 RECORD                      |
|---------------------------------------------|
| Smallest unit of data, like a book entry:   |
| - Log entry, Metric point, Event, Span      |
| Examples:                                   |
| - Log: ERROR: Payment Service Timeout       |
| - Metric: CPU Usage: 85%                    |
| - Event: Deployment Started                 |
+---------------------------------------------+
               ↓
+---------------------------------------------+
|                 VIEW                        |
|---------------------------------------------|
| Filtered or curated view of the data:       |
| - Logs for payment errors                   |
| - High CPU usage metrics                    |
| - Deployment events in production           |
+---------------------------------------------+
               ↓
+---------------------------------------------+
|                 METADATA                    |
|---------------------------------------------|
| System-level data organization:             |
| - Metadata tables for logs, metrics, spans  |
| Examples:                                   |
| - \`dt.system.data.objects\`                  |
| - \`dt.system.buckets\`                       |
+---------------------------------------------+
               ↓
+---------------------------------------------+
|                 POLICY                      |
|---------------------------------------------|
| Controls access to data:                    |
| - Who can view what                         |
| Examples:                                   |
| - Only security team sees audit logs        |
| - Only developers access application logs   |
+---------------------------------------------+
               ↓
+---------------------------------------------+
|                 PIPELINE                    |
|---------------------------------------------|
| Enrichment and processing of data:          |
| - Adds context like \`service=payment\`       |
| Examples:                                   |
| - Tagging logs with \`env=prod\`              |
| - Adding trace IDs to spans                 |
+---------------------------------------------+
               ↓
+---------------------------------------------+
|                 RETENTION                   |
|---------------------------------------------|
| Defines how long data is kept:              |
| Examples:                                   |
| - Logs: 35 days                             |
| - Metrics: 1 year                           |
| - Spans: 7 days                             |
+---------------------------------------------+
               ↓
+---------------------------------------------+
|                 MONITORING                  |
|---------------------------------------------|
| Alerts and insights based on queries:       |
| Examples:                                   |
| - Alert if errors > 100/hour                |
| - Alert if CPU > 80% for 10 mins            |
| - Alert if traces exceed 2 seconds          |
+---------------------------------------------+
```

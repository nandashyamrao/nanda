
# **Dynatrace Grail Hierarchy**

- **Entities** (Define context: e.g., services, hosts, applications)
  - Payment Service
  - Checkout Service
  - Inventory Service

- **Tables** (Organize data by type: logs, events, spans)
  - Logs Table
  - Events Table
  - Spans Table

- **Buckets** (Store data with retention policies)
  - Default Logs Bucket
  - Payment Logs Bucket
  - Audit Logs Bucket

- **Records** (The actual data points: log entries, events, spans)
  - Log Records
  - Event Records
  - Span Records

- **Policies** (Control data access)
  - Entity-Level Policies
  - Record-Level Policies
  - Bucket-Level Policies

- **Metadata** (Store system-level information)
  - `dt.system.data.objects` (List of tables)
  - `dt.system.buckets` (List of buckets)
  - `dt.system.events` (System event logs)

- **Pipelines** (Process and enrich incoming data)
  - Security Context Enrichment
  - Routing to Buckets
  - Retention Management

- **Monitoring and Alerts** (Insights and real-time actions)
  - Query-Based Alerts
  - Volume-Based Thresholds
  - Integration with Observability

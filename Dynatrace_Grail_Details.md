
# **Dynatrace Grail Hierarchy**

## **1. Grail Data Organization Overview**

Grail organizes data into tables, which contain records stored in buckets. Here’s the hierarchy:

```
Dynatrace Grail
├── Tables
│   ├── logs
│   ├── events
│   ├── spans (future support)
│   ├── system_events
│   ├── system_buckets
│   └── custom tables (if defined)
├── Buckets
│   ├── Default Buckets
│   │   ├── default_logs
│   │   ├── default_events
│   │   └── default_spans
│   ├── Custom Buckets
│   │   ├── custom_audit_logs
│   │   ├── custom_service_logs
│   │   └── other user-defined buckets
├── Records
│   ├── Log Records
│   │   ├── Fields (Columns)
│   │   │   ├── timestamp
│   │   │   ├── message
│   │   │   ├── dt.system.aws.accountId
│   │   │   ├── process.name
│   │   │   ├── log.level
│   │   │   ├── hostname
│   │   │   └── service.name
│   ├── Event Records
│   │   ├── event.name
│   │   ├── event.type
│   │   └── other metadata
│   └── Span Records (future)
│       ├── trace.id
│       ├── span.id
│       ├── duration
│       ├── attributes
│       └── other tracing metadata
```

---

## **2. Table and Bucket Relationship**

- **Tables**: Tables define the logical structure of data. Examples: logs, events, spans.
- **Buckets**: Buckets are storage containers where data is physically stored. Each table can query data from one or more buckets.
  - **Default Buckets**: Predefined for storing general logs/events/spans.
  - **Custom Buckets**: User-defined for organizing logs based on specific needs (e.g., retention policies, teams, services).

---

## **3. Columns (Fields) in a Table**

Tables are composed of fields (columns). The fields vary depending on the type of table (e.g., logs, events). Here’s a typical example for the logs table:

```
logs Table
├── timestamp            (Time the log was generated)
├── dt.system.aws.accountId (AWS Account ID)
├── dt.system.bucket     (Bucket name where the log resides)
├── dt.security.context  (Custom security context)
├── process.name         (Name of the process that generated the log)
├── log.level            (INFO, WARN, ERROR)
├── message              (Log content)
├── hostname             (Host where the log was generated)
├── service.name         (Service associated with the log)
├── trace.id             (Unique trace identifier for tracing)
├── span.id              (Unique span identifier for tracing)
└── other custom fields
```

---

## **4. Key System Metadata**

Grail provides system tables to help manage and query metadata about the stored data.

### **System Tables**
```
├── dt.system.data.objects
│   ├── Purpose: Lists all available queryable objects (tables and views).
│   ├── Columns:
│   │   ├── name (Name of the object)
│   │   ├── type (Type: table or view)
│   │   └── other metadata
├── dt.system.buckets
│   ├── Purpose: Lists all buckets and their details.
│   ├── Columns:
│   │   ├── bucket.name
│   │   ├── retention (Retention policy in days)
│   │   ├── storage.size (Storage size in MB/GB)
│   │   └── other bucket metadata
└── dt.system.events
    ├── Purpose: Tracks system-level events like queries, errors, etc.
```

---

## **5. Data Flow for Logs**

### **Steps**:
1. **Log Ingestion**  
   - Logs are ingested from various sources (e.g., AWS CloudTrail, Kubernetes, custom applications).
   - The pipeline enriches logs (e.g., adds `dt.security.context` or other metadata).
2. **Log Storage**  
   - Logs are stored in buckets (default or custom) based on routing rules.
3. **Log Querying**  
   - Use DQL (Dynatrace Query Language) to retrieve, filter, and analyze logs.

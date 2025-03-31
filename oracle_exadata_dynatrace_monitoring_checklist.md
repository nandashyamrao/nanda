
# Oracle Exadata Monitoring Setup with Dynatrace – Full Checklist (SQL + JMX)

---

## 1. ActiveGate Deployment (Mandatory)

| Step | What to Do | Why |
|------|------------|-----|
| 1.1 | Install an **Environment ActiveGate** in the same on-prem network as the Oracle DB (Exadata) | The extension runs on ActiveGate and must reach the DB via JDBC and/or JMX |
| 1.2 | Ensure outbound access to `*.live.dynatrace.com:443` | For pulling config and pushing data to Dynatrace SaaS |
| 1.3 | Open Oracle **listener port** (default: `1521`) from ActiveGate to DB | Required for **JDBC-based SQL metric collection** |
| 1.4 | Open JMX port (e.g., `9010`, `7071`, or custom) from ActiveGate to JVM | Required for **JMX-based monitoring** if enabled in Oracle or WebLogic |

---

## 2. Oracle Database User Setup (for SQL Metrics)

| Step | What to Do | Why |
|------|------------|-----|
| 2.1 | Create a **read-only monitoring user** in Oracle DB | Used by ActiveGate for executing metric queries |
| 2.2 | Grant SELECT access on required views | Typical: `v$session`, `v$sysstat`, `dba_tablespaces`, `v$pgastat`, etc. |
| 2.3 | (Optional) Monitor app-level tables (e.g., job statuses) | For business-related metric queries |

**Example:**
```sql
CREATE USER dynatrace_monitor IDENTIFIED BY "StrongPassword123!";
GRANT CONNECT TO dynatrace_monitor;
GRANT SELECT ON v$session TO dynatrace_monitor;
GRANT SELECT ON v$sysstat TO dynatrace_monitor;
GRANT SELECT ON dba_tablespaces TO dynatrace_monitor;
```

---

## 3. Enable and Configure JMX in Oracle (if needed)

| Step | What to Do | Why |
|------|------------|-----|
| 3.1 | Enable JMX remote access on Oracle JVM (or WebLogic) | Required if using JMX-based monitoring |
| 3.2 | Configure port, authentication, and SSL settings | Port like `9010`; can be secured or open for testing |
| 3.3 | Confirm JMX MBeans are exposed (e.g., memory, threads, GC, session info) | You can query using tools like `jconsole`, `jvisualvm`, or Dynatrace |

---

## 4. ActiveGate Extension Setup

| Step | What to Do | Why |
|------|------------|-----|
| 4.1 | Assign ActiveGate to an **Extension Execution Group** | So Dynatrace knows where to run the extension |
| 4.2 | Confirm that the **Extension Execution Controller** is enabled | It runs the logic that pulls data from SQL/JMX |
| 4.3 | (Optional) Create a group just for Oracle (e.g., `exadata-monitoring`) | Good for scalability and clarity |

---

## 5. Deploy Dynatrace Oracle DB Extension (SQL-based)

| Step | What to Do | Why |
|------|------------|-----|
| 5.1 | Go to Dynatrace Hub → Search **Oracle Database** → Install | This is Dynatrace's official SQL Extension for Oracle |
| 5.2 | Review documentation: [Oracle DB Monitoring Docs](https://docs.dynatrace.com/docs/extend-dynatrace/extensions20/data-sources/sql/oracle-exadata-monitoring) | Understand available feature sets and metrics |

---

## 6. Set Up Credential Vault

| Step | What to Do | Why |
|------|------------|-----|
| 6.1 | Navigate to **Settings → Integration → Credential vault** | Securely store DB login credentials |
| 6.2 | Add a new “Username and password” credential (e.g., `oracle-exadata-monitor`) | Will be referenced in the monitoring config |

---

## 7. Create Monitoring Configuration for Oracle DB (SQL Extension)

| Step | What to Do | Why |
|------|------------|-----|
| 7.1 | Go to **Oracle DB Extension** → Add monitoring configuration | This creates the endpoint definition |
| 7.2 | Enter hostname, port, and service name/SID | This forms the JDBC connection string |
| 7.3 | Select the stored credential from vault | Dynatrace uses this for DB authentication |
| 7.4 | Choose feature sets like: `system_metrics`, `tablespace_usage`, `session_data`, etc. | These control what metrics are collected |
| 7.5 | Set polling frequency (e.g., 5 minutes) | Balances data freshness and load |

---

## 8. (Optional) Set Up JMX Monitoring (if Oracle WebLogic is involved)

| Step | What to Do | Why |
|------|------------|-----|
| 8.1 | Install the **JMX/PMI Extension** from Dynatrace Hub | Used to collect JMX metrics |
| 8.2 | Create a JMX monitoring configuration | Specify host, port, object name, attributes |
| 8.3 | Use sample queries like `Catalina:type=ThreadPool` or `java.lang:type=Memory` | Collect JVM-level metrics like heap, threads, GC, sessions |

**Sample JMX Metric in YAML:**
```yaml
jmx:
  - group: oracle_jvm_stats
    featureSet: memory
    interval:
      minutes: 1
    query:
      objectName: "java.lang:type=Memory"
      attribute: "HeapMemoryUsage"
      key: "used"
    metrics:
      - key: custom.oracle.jvm.heap.used
        type: gauge
        unit: Byte
```

---

## 9. Testing and Validation

| Step | What to Do | Why |
|------|------------|-----|
| 9.1 | Check extension logs in Dynatrace UI | Ensure DB/JMX connections are successful |
| 9.2 | Use Data Explorer to search for metrics like `custom.oracle.session.count`, `oracle.tablespace.usage`, etc. | Validate ingestion of expected data |
| 9.3 | Use built-in dashboards or create custom ones | Visualize key DB and JVM metrics |
| 9.4 | Enable self-monitoring logs for extensions (optional) | For debugging and auditing extension behavior |

---

## 10. Maintenance Tips

| Task | Why |
|------|-----|
| Rotate DB passwords securely in Credential Vault | Keeps security compliant without editing config |
| Update extension schema/version when new features are released | Access improved queries, better dashboards, bug fixes |
| Use naming conventions (e.g., `exadata-prod-east`) for configs | Easier management of many monitored DBs |
| Export configs and dashboards as JSON | Useful for reuse, backup, and ServiceNow automation |

from pathlib import Path

# Recreate markdown content for retry
markdown_checklist = '''\
# Log Hygiene & Parsing Validation Checklist for Dynatrace OpenPipeline

This checklist helps developers, SREs, and platform engineers ensure their application logs are clean, parsable, and usable by Dynatrace’s AI and analytics systems.

---

## ✅ Log Formatting & Structure

- [ ] Logs follow a **consistent and predictable format** across all services.
- [ ] Log format is **structured** (preferably JSON) or follows a documented pattern.
- [ ] Each log line includes a **parseable timestamp** (`ISO8601`, RFC3339, or `yyyy-MM-dd HH:mm:ss.SSS`).
- [ ] Each log line includes a **log level** or can have one inferred (`INFO`, `ERROR`, etc.).
- [ ] Multi-line logs (e.g., exceptions) are properly handled (merged or delimited).
- [ ] Fields use consistent naming conventions (`request_id`, `trace_id`, `user_id`, etc.).
- [ ] All logs include a **clear message field** or summary of the event.
- [ ] Timestamps are **in UTC** to avoid time zone confusion.

---

## ✅ Severity Classification (logLevel)

- [ ] Known log levels are used: `TRACE`, `DEBUG`, `INFO`, `WARN`, `ERROR`, `FATAL`.
- [ ] No important logs are assigned `logLevel: NONE`.
- [ ] Custom log levels (e.g., `CRIT`, `MAJOR`) are **remapped** using Dynatrace rules.
- [ ] Log level is correctly extracted using parsing rules or `FIELDS_REMAP`.
- [ ] Severity text and number are properly set for OpenTelemetry logs.

---

## ✅ Enrichment & Context

- [ ] Logs contain **contextual identifiers**: environment, team, region, pod name, host, etc.
- [ ] Relevant metadata is added using `FIELDS_ADD`, `FIELDS_RENAME`, or `FIELDS_COPY`.
- [ ] Sensitive data (e.g., passwords, tokens, PII) is removed or masked using `FIELDS_MASK`.
- [ ] Trace and span IDs are included for correlation with distributed traces.

---

## ✅ Dynatrace Ingestion-Specific

- [ ] Parsing rules are applied in **Log Processing** (custom or built-in rules).
- [ ] `logLevel`, `timestamp`, `content`, and custom fields are extracted correctly.
- [ ] OpenPipeline steps (parse → enrich → transform → route) are validated.
- [ ] Routing rules are configured to associate logs with the right entities or services.

---

## ✅ Queryability with DQL

- [ ] Fields like `logLevel`, `service`, `status`, `env` are available in DQL.
- [ ] You can run:
  ```dql
  fetch logs | summarize count() by logLevel
  ```
  and get meaningful results.
- [ ] `logLevel == "ERROR"` returns actual error logs from key systems.
- [ ] Logs can be filtered or visualized in dashboards using custom fields.

---

## ✅ Monitoring & Problem Integration

- [ ] Davis AI can use logs to trigger or enrich problem cards.
- [ ] You can correlate logs with metrics and traces on the same dashboard.
- [ ] Important error logs are NOT missed due to missing or misparsed fields.

---

## ✅ Maintenance & Governance

- [ ] Log format changes are versioned and documented.
- [ ] Rules are reviewed quarterly for effectiveness and false positives.
- [ ] `logLevel: NONE` rate is tracked and addressed.
- [ ] No unused logs are being ingested (avoid cost and noise).

---

## Sample DQL for Unparsed Log Inspection

```dql
fetch logs
| filter logLevel == "NONE"
| summarize count(), earliest(timestamp), latest(timestamp) by log.source, content
```

---

## Final Tip

> Good logs aren't just for debugging. They're for **AI correlation**, **security insight**, **compliance tracking**, and **user journey analysis**. Treat them like telemetry assets.
'''

# Save the markdown file
file_path = Path("/mnt/data/dynatrace_log_hygiene_checklist.md")
file_path.write_text(markdown_checklist)

file_path.name

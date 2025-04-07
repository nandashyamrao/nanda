# Retry saving the markdown file after the previous error
from pathlib import Path

# Define the full markdown content again
markdown_content = '''\
# Dynatrace OpenPipeline Source Matrix by Data Type

## Logs

| Data Type | Source / Tool | Category | Ingestion Method | Description |
|-----------|----------------|----------|------------------|-------------|
| Logs | OneAgent | Built-in | Auto-discovery | Automatically collects log files from hosts, services, containers. |
| Logs | Classic Log API (v1) | Built-in | /api/v1/logs/ingest | Legacy direct log ingestion endpoint. |
| Logs | Log Ingest API (v2) | Custom | /api/v2/logs/ingest | Modern log ingestion API with OpenPipeline support. |
| Logs | Fluent Bit | Third-party | HTTP output → Log API | Collects logs from containers and systems. |
| Logs | Cribl Stream | Third-party | Pipeline → Log API | Pre-process logs before forwarding to Dynatrace. |
| Logs | OpenTelemetry Collector | Third-party | OTLP → Dynatrace OTEL endpoint | Can push structured logs via OTLP. |
| Logs | Syslog + Fluent Bit | File-Based | Forward → Log API | Forward syslogs using Fluent Bit to Dynatrace. |
| Logs | CSV/Flat File (via Cribl) | File-Based | Transformed → Log API | Converts tabular files into structured logs. |

## Metrics

| Data Type | Source / Tool | Category | Ingestion Method | Description |
|-----------|----------------|----------|------------------|-------------|
| Metrics | OneAgent | Built-in | Auto-discovery | Captures CPU, memory, disk, network, JVM, etc. |
| Metrics | Metrics Ingest API (v2) | Custom | /api/v2/metrics/ingest | Push custom metrics to Dynatrace. |
| Metrics | Extension Framework v2 | Built-in | SNMP/Script/Polling | Pulls metrics via CLI, APIs, SNMP, etc. |
| Metrics | Telegraf | Third-party | Plugin → Dynatrace endpoint | Collect system/app metrics and push to Dynatrace. |
| Metrics | StatsD | Third-party | UDP → Extension v2 or ActiveGate | Lightweight metrics emitter. |
| Metrics | OpenTelemetry Collector | Third-party | OTLP → Metrics endpoint | Push OTEL-compliant custom metrics. |
| Metrics | AWS/Azure/GCP Cloud Metrics | Cloud | Pull/Stream via ActiveGate | Cloud service metrics collected natively or via stream. |
| Metrics | SNMP Devices (via Ext. v2) | File-Based | SNMP Polling → OpenPipeline | Legacy network hardware metrics. |

## Traces

| Data Type | Source / Tool | Category | Ingestion Method | Description |
|-----------|----------------|----------|------------------|-------------|
| Traces | OneAgent | Built-in | Auto-instrumentation | Auto-collects PurePaths (traces) for services and transactions. |
| Traces | OpenTelemetry Collector | Third-party | OTLP Traces → Dynatrace | Push traces from custom-instrumented apps (vendor-neutral). |
| Traces | Custom Traces via API | Custom | (limited to OTEL SDK usage) | Manually instrument and forward trace spans. |

## Events

| Data Type | Source / Tool | Category | Ingestion Method | Description |
|-----------|----------------|----------|------------------|-------------|
| Events | Davis Extensions (v1) | Built-in | Events via built-in rules or Extension code | Push state-based or threshold-based events. |
| Events | Events Ingest API (v2) | Custom | /api/v2/events/ingest | Custom business or anomaly events. |
| Events | Cribl Stream | Third-party | Routed events via transformation | Can shape logs into events and send to Dynatrace. |
| Events | Business Event Scripts | Custom | Python/Shell → API v2 | Your custom logic detects business anomalies and pushes event payloads. |
| Events | AWS/Azure/GCP Event Triggers | Cloud | EventBridge, Cloud Functions → API | Triggered by cloud events, forwarded into Dynatrace. |
'''

# Save the content to a markdown file
file_path = Path("/mnt/data/dynatrace_openpipeline_source_matrix_by_type.md")
file_path.write_text(markdown_content)

file_path.name

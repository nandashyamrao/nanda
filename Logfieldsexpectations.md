# ✅ Log Data Expectations – Explained with Examples

This guide outlines best practices and expectations for logs to be ingested and processed efficiently in Dynatrace OpenPipeline.

---

## Log Field Expectations and Examples

| Expectation               | Description                                                                                                    | Examples |
|---------------------------|----------------------------------------------------------------------------------------------------------------|----------|
| **Structured Format Preferred** | Use **JSON**, **key=value**, or **delimited** format. Avoid plain text when possible.                        | ✅ `{ "timestamp": "...", "logLevel": "INFO", "message": "App started" }`<br>✅ `timestamp=... level=INFO message="App started"`<br>❌ `App started at 12:01` |
| **Parseable Timestamp**   | Timestamp must be present and parsable using known formats like **ISO 8601** or `yyyy-MM-dd HH:mm:ss`.         | ✅ `"timestamp": "2024-04-08T12:00:00Z"`<br>✅ `timestamp=2024-04-08 12:00:00`<br>❌ `Today at noon` |
| **Log Level**             | Logs should include a **logLevel** or `severity_text` / `severity_number` to enable filtering and scoring.     | ✅ `"logLevel": "ERROR"`<br>✅ `"severity_text": "WARN"`<br>✅ `"severity_number": 18`<br>❌ No level present |
| **Content Field**         | Clearly label the main message (e.g., `message`, `content`, `msg`).                                            | ✅ `"message": "User login failed"`<br>✅ `msg="Timeout occurred"` |
| **Entity Context**        | Include service, pod, host, or app information to enable mapping to Dynatrace topology.                        | ✅ `"service.name": "auth-api"`<br>✅ `"k8s.pod.name": "webapp-123"`<br>✅ `host="app-server-1"` |
| **Trace/Span IDs (optional)** | Helps with trace-log correlation for microservices. Include if available.                                  | ✅ `"trace_id": "abc123", "span_id": "def456"` |
| **Consistent Field Names** | Avoid dynamic keys like `user_123`. Use well-defined, documented fields.                                       | ✅ `user_id`, `response_time`<br>❌ `user_987_request_time` |
| **No Excessive Nesting**  | JSON logs should be shallow or flattened. Avoid deeply nested structures (6+ levels).                          | ✅ `{ "event": { "type": "login", "status": "success" } }`<br>❌ `{ "a": { "b": { "c": { "d": { "e": { "f": { "g": "too deep" }}}}}}` |
| **Avoid Encoding Artifacts** | Don't log base64 blobs, binaries, or encoded fields unless decoded upstream. Use UTF-8 strings.               | ✅ `"body": "GET /api/status"`<br>❌ `"data": "U29tZSBsb2cgc3RyaW5nIGVuY29kZWQ="` |

---

## ✅ Summary Best Practices

- Always use structured logging, preferably JSON.
- Include `timestamp`, `logLevel`, `message`, and `service.name`.
- Enrich logs with trace context and business metadata where possible.
- Validate parsing success rate in staging before promoting formats to production.

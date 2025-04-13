Here's a detailed explanation of each **log data expectation** that Dynatrace OpenPipeline (and any observability platform) benefits from — along with **realistic examples** for clarity:

---

## ✅ Log Data Expectations – Explained with Examples

| **Expectation**              | **Description**                                                                                                   | **Example** |
|-----------------------------|-------------------------------------------------------------------------------------------------------------------|-------------|
| **Structured Format Preferred** | Logs should be in **JSON** or a clean **key=value** or **delimited** format for easy parsing. Avoid plain text.  | ✅ Good: `{ "timestamp": "...", "logLevel": "INFO", "message": "App started" }`<br>✅ Good: `timestamp=... level=INFO message="App started"`<br>❌ Bad: `App started at 12:01` |
| **Parseable Timestamp**     | A timestamp field must be present and in a recognized format (e.g., ISO 8601) to allow proper time alignment.     | ✅ Good: `"timestamp": "2024-04-08T12:00:00Z"`<br>✅ Good: `timestamp=2024-04-08 12:00:00`<br>❌ Bad: `Today at noon` |
| **Log Level**               | Every log should include a **log level indicator** (e.g., `INFO`, `ERROR`) for filtering, severity scoring, etc.   | ✅ Good: `"logLevel": "ERROR"`<br>✅ Good: `"severity_text": "WARN"` or `"severity_number": 18`<br>❌ Bad: No log level at all |
| **Content Field**           | The **main message** should be clearly labeled, such as in a `message`, `content`, or `msg` field.                 | ✅ Good: `"message": "User login failed due to timeout"`<br>✅ Good: `msg="Payment declined"` |
| **Entity Context**          | Logs should include details that tie them to infrastructure — like `host.name`, `pod.name`, or `service.name`.     | ✅ Good: `"service.name": "auth-api"`<br>✅ Good: `"k8s.pod.name": "checkout-8472fd"`<br>✅ Good: `host="webserver-01"` |
| **Trace/Span IDs (optional)** | Helps correlate logs with traces for distributed systems. Include `trace_id` and `span_id` if available.          | ✅ Good: `"trace_id": "abc123", "span_id": "def456"`<br>Useful in microservice, serverless, or async apps |
| **Consistent Field Names**  | Use **fixed, documented field names** like `timestamp`, `logLevel`, `message`. Avoid dynamic or random field names.| ✅ Good: `user_id`, `response_time`<br>❌ Bad: `responseTime_usEast`, `user1234_action` |
| **No Excessive Nesting**    | Avoid deeply nested JSON structures — they’re hard to parse, flatten, and query.                                  | ✅ Good: `{ "event": { "type": "login", "status": "success" } }`<br>❌ Bad: 7+ levels like `{ "a": { "b": { "c": { "d": { "e": ... } } } } }` |
| **Avoid Encoding Artifacts**| Ensure log data is **UTF-8 text**. Avoid base64, binary blobs, or encrypted fields unless they are decoded upstream.| ✅ Good: `"body": "GET /api/status"`<br>❌ Bad: `"data": "U29tZSBsb2cgc3RyaW5nIGVuY29kZWQ="` (base64-encoded string) |

---

### ✅ Best Practices Summary:

- **Prefer JSON** — use flat and descriptive keys.
- Include `timestamp`, `logLevel`, and `message` **in every log**.
- Add context: `service.name`, `host.name`, `environment`, etc.
- Use `trace_id` and `span_id` if you're using distributed tracing.
- Avoid logs that require transformation after ingestion — do it before.

---

Would you like this converted into a markdown checklist or integrated into your log standards file?

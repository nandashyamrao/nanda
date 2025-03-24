
## 🧩 Core Facets (Requests) – Explained

Located under the **Requests** tab in the **Distributed Tracing App**, the **Core** section is your go-to for high-level filtering and scoping of traces. It includes the most frequently used dimensions to isolate problems.

Here’s what each facet under “Core” does:

---

### 1. **Response Time**
- **What it is**: A slider filter that lets you choose a range of durations (in milliseconds).
- **Why it matters**: Helps isolate **slow requests**.
- **Use case**: Focus on requests that took longer than 3,000 ms to identify long-tail latency issues or backend slowness.

---

### 2. **Service**
- **What it is**: Filters requests based on the service name.
- **Why it matters**: Services are logical units (like microservices or backends).
- **Use case**: Narrow down your trace view to just the `checkout-service`, `auth-service`, or any specific backend you're analyzing.

---

### 3. **Endpoint**
- **What it is**: Filters by the request endpoint (URL or route).
- **Why it matters**: Useful when you're debugging issues in a particular function, route, or controller.
- **Use case**: Troubleshoot failures only in `/login`, `/submitTransaction`, or similar endpoints.

---

### 4. **Request Status**
- **What it is**: Filters by outcome — **Success** or **Failure**.
- **Why it matters**: Immediately separates healthy requests from those that resulted in problems.
- **Use case**: Investigate all failed requests during a spike, or isolate healthy ones for baseline comparison.

---

### 5. **Span Status**
- **What it is**: Shows status of individual spans within each request — **OK** or **Error**.
- **Why it matters**: A request may succeed overall but still contain error-prone spans (e.g., retries or fallbacks).
- **Use case**: Spot **partial failures** inside successful requests, useful for silent failure debugging.

---

### 6. **Span Kind**
- **What it is**: Filters based on the **type of operation** each span represents:
  - `Client`: External API calls
  - `Server`: Entry point for service (e.g., HTTP request)
  - `Producer/Consumer`: Messaging systems (e.g., Kafka, SQS)
  - `Internal`: Within-service logic (like a function)
- **Why it matters**: Allows segmentation of where in the request path the issue is.
- **Use case**: Focus on `Client` spans to investigate third-party API slowness, or `Consumer` spans to debug queue bottlenecks.

---

## 🌐 HTTP Headers Facets – Explained

The **HTTP Headers** facet group in Dynatrace Distributed Tracing lets you filter requests based on **specific headers** sent with HTTP calls. These headers often contain valuable context such as user identity, trace IDs, custom attributes, and routing data.

Here’s a breakdown of key headers visible in your image:

---

### ▶️ Common HTTP Headers

| **Header**               | **Purpose**                                                                 |
|--------------------------|------------------------------------------------------------------------------|
| `Accept-Encoding`        | Indicates accepted compression types (e.g., gzip, deflate).                 |
| `Accept-Language`        | Specifies preferred language (e.g., `en-US`). Used for localization.        |
| `Cookie`                 | Holds session cookies or custom user state (e.g., `JSESSIONID`).            |
| `Referer`                | Refers to the page the request came from. Useful for navigation context.    |
| `User-Agent`             | Identifies the browser, OS, or client application.                          |
| `Host`                   | The domain or host header of the request.                                   |
| `Forwarded`, `X-Forwarded-For`, `X-Forwarded-Host` | Track originating IP or proxy info. Critical for client traceability in load-balanced environments. |

---

### ▶️ Dynatrace and Trace Context Headers

| **Header**                      | **Purpose**                                                                 |
|----------------------------------|------------------------------------------------------------------------------|
| `X-B3-TraceId`                  | Used in OpenTelemetry/Zipkin tracing for trace correlation.                  |
| `X-Dynatrace`                   | Contains Dynatrace-specific trace context.                                   |
| `X-Dynatrace-Tenant`, `X-Dynatrace-Test`, `X-Dynatrace-Visit` | Enriched by Dynatrace to provide session/tenant granularity.                |
| `X-Amz-Target`                  | Used in AWS API Gateway calls for targeting Lambda/API versions.             |

---

### ▶️ Custom or Application-Specific Headers

| **Header**                        | **Purpose**                                                                 |
|-----------------------------------|------------------------------------------------------------------------------|
| `X-sf-app-name`, `X-sf-channel`, `X-sf-flow-id`, `X-sf-referrer` | Likely custom headers defined by your org for routing, UI context, or user behavior tracking. |
| `X-Plauto-*`                      | Likely internal headers for screen tracking or UI testing in your app.      |

---

### ✅ Why These Headers Are Important

- **Correlate Requests Across Systems**  
  Trace headers (`X-B3-TraceId`, `X-Dynatrace`) enable cross-service trace stitching and log correlation.

- **Segment by Client or Region**  
  Headers like `User-Agent` or `Accept-Language` let you slice traffic by user type or locale.

- **Debug Proxy and Load Balancer Behavior**  
  `X-Forwarded-For` helps trace the real client IP even behind proxies.

- **Capture Business Context**  
  Custom headers (`X-sf-*`, `X-Plauto-*`) let you tag traffic based on business metadata (e.g., marketing campaign, customer cohort).

---

### Example Use Cases

- Filter traces where `User-Agent` contains “iPhone” to investigate mobile-only performance issues.
- Look for specific `X-B3-TraceId` to debug a trace across microservices.
- Identify where a specific `cookie` value caused inconsistent user sessions.

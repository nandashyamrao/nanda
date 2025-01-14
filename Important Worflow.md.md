
# Dynatrace Models and System Objects

## What are Models and Their Purpose?

Models in Dynatrace represent structured frameworks to organize, analyze, and monitor data, relationships, and processes within IT systems. They serve as the backbone for providing insights, defining dependencies, and enabling effective observability.

### Purpose of Models
- **Simplification**: Models abstract complex systems into manageable layers.
- **Organization**: They group data, entities, and relationships systematically.
- **Query Optimization**: Enable context-aware and dependency-driven querying through Dynatrace Query Language (DQL).

### Types of Models
1. **Physical Model**: Represents the actual infrastructure, including hosts, processes, and connected devices.
2. **Logical Model**: Groups data functionally or hierarchically (e.g., by environment, team, or service tiers).
3. **Semantic Model**: Highlights relationships and dependencies (e.g., "Service A calls Database B").

---

## System Objects in Dynatrace

### Core System Objects
1. **Entities**:
   - Represent real-world components like hosts, services, processes, and applications.
   - Example Types:
     - `dt.entity.host`
     - `dt.entity.service`
     - `dt.entity.process`

2. **Attributes**:
   - Key-value pairs describing the state or properties of entities.
   - Examples:
     - CPU usage, memory usage for hosts.
     - Response time, error rate for services.

3. **Tags**:
   - Custom labels for organizing and filtering entities.
   - Types:
     - Static Tags (e.g., `environment=production`).
     - Dynamic Tags (e.g., based on metadata).

4. **Relationships**:
   - Define dependencies and interactions between entities.
   - Examples:
     - `calls`, `contains`, `depends_on`.

5. **Metadata**:
   - Descriptive details about an entity, such as:
     - Hostname, OS, cloud provider.

6. **Metrics**:
   - Time-series data representing performance or resource utilization.
   - Examples:
     - CPU usage, response time.

7. **Logs**:
   - Textual data representing system or application events.
   - Examples:
     - Error logs, application logs.

8. **Traces**:
   - End-to-end representations of request flows in distributed systems.
   - Examples:
     - API request spans.

9. **Events**:
   - Notifications of state changes or anomalies.
   - Examples:
     - Deployment events, health state changes.

10. **Views**:
    - Filtered or aggregated representations of data for analysis and dashboards.

11. **Dashboards**:
    - Visualizations of collected data tailored to specific use cases.

---

## Integration of Pre-Querying Stages into DQL Workflows

### Understanding Pre-Querying Stages
The following stages set the foundation for querying in Dynatrace:
1. Setup and Instrumentation
2. Discovery
3. Data Collection
4. Semantics and Relationships
5. Real-Time Monitoring and Baseline Creation
6. Alerts and AI Insights
7. Visualization and Context Building

---

### Pre-Querying Stages with DQL Integration

#### 1. Setup and Instrumentation
- **Role in DQL**: Ensures all monitored components are registered as entities.
- **Example Query**:
  ```plaintext
  fetch metrics
  | filter entity.type == "dt.entity.host"
  | fields entity.name, metric.key, metric.value
  ```

#### 2. Discovery
- **Role in DQL**: Builds foundational structure for dependency-aware queries.
- **Example Query**:
  ```plaintext
  fetch logs
  | filter dt.entity.service == "Checkout Service"
  | join fetch dt.entity.database on service.calls == database
  | fields service.name, database.name, log.message
  ```

#### 3. Data Collection
- **Role in DQL**: Provides raw metrics, logs, traces, and events for analysis.
- **Example Query**:
  ```plaintext
  fetch metrics
  | filter metric.key == "builtin:service.response.time"
  | filter service.name == "Checkout Service"
  | fields timestamp, metric.value
  ```

#### 4. Semantics and Relationships
- **Role in DQL**: Enables context-aware queries using tags and dependencies.
- **Example Query**:
  ```plaintext
  fetch traces
  | filter service.tag == "tier:frontend"
  | fields trace.id, service.name, response.time
  ```

#### 5. Real-Time Monitoring and Baseline Creation
- **Role in DQL**: Baselines and real-time data enable anomaly detection.
- **Example Query**:
  ```plaintext
  fetch metrics
  | filter metric.key == "builtin:host.cpu.usage"
  | filter metric.value > baseline.value
  | fields entity.name, timestamp, metric.value
  ```

#### 6. Alerts and AI Insights
- **Role in DQL**: Focus queries on problems and AI-identified root causes.
- **Example Query**:
  ```plaintext
  fetch problems
  | filter problem.severity == "critical"
  | fields problem.id, problem.title, impacted.entity.name
  ```

#### 7. Visualization and Context Building
- **Role in DQL**: Powers dashboards and visual reports.
- **Example Query**:
  ```plaintext
  fetch metrics
  | filter dt.entity.service == "Checkout Service"
  | summarize avg(metric.value) by environment
  | fields environment, avg.metric.value
  ```

---

## Key Takeaways
- **Models**: Provide structure for monitoring and analysis.
- **Entities**: Act as the core components tied to all data.
- **DQL**: Seamlessly integrates with every stage of the monitoring workflow, making data actionable.

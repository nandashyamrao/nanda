
# Custom Devices in Dynatrace: Examples and Explanation

A **custom device** in Dynatrace is an entity that is not automatically discovered by the Dynatrace OneAgent or cloud integrations but is instead created manually or programmatically via Dynatrace APIs. Custom devices are used to monitor systems, applications, or devices that are outside the standard monitoring scope, such as legacy systems, IoT devices, or non-standard software.

---

## **Examples of Custom Devices**

### **1. Monitoring a Legacy Application**
- **Scenario**: You have a legacy application running on a server that does not support Dynatrace OneAgent installation.
- **What Makes It a Custom Device**:
  - The application cannot be automatically detected, so metrics are pushed to Dynatrace via the Custom Device API.
- **Data Collected**:
  - Metrics: Application-specific KPIs like transaction counts, response times, or error rates.
  - Events: Application start/stop events or state changes.
- **Example Use Case**:
  - A COBOL application running on a mainframe system.

---

### **2. Monitoring IoT Devices**
- **Scenario**: You want to monitor an IoT device fleet (e.g., temperature sensors, smart thermostats).
- **What Makes It a Custom Device**:
  - IoT devices do not run a OneAgent, so you use the Custom Device API to send metrics.
- **Data Collected**:
  - Metrics: Temperature, battery levels, device status.
  - Events: Device failures or firmware updates.
- **Example Use Case**:
  - Monitoring a network of smart thermostats in a building.

---

### **3. Network Switches or Routers**
- **Scenario**: Monitoring network devices for traffic and health.
- **What Makes It a Custom Device**:
  - Dynatrace cannot directly install an agent on these devices, so SNMP data or custom metrics are ingested.
- **Data Collected**:
  - Metrics: Network throughput, error rates, uptime.
  - Events: Device failures or configuration changes.
- **Example Use Case**:
  - Monitoring a Cisco router's network traffic.

---

### **4. External APIs or Third-Party Services**
- **Scenario**: You want to monitor the availability and performance of a third-party API that your application depends on.
- **What Makes It a Custom Device**:
  - The API is external, so it cannot be monitored directly. You push metrics about API response times and error rates.
- **Data Collected**:
  - Metrics: API latency, success/failure rates.
  - Events: Downtime or errors in API calls.
- **Example Use Case**:
  - Monitoring a payment gateway API like Stripe.

---

### **5. Custom Hardware Devices**
- **Scenario**: Monitoring non-standard hardware, like a custom-built industrial robot.
- **What Makes It a Custom Device**:
  - The robot runs proprietary software that cannot host a OneAgent.
- **Data Collected**:
  - Metrics: CPU usage, memory usage, task completion rates.
  - Events: Hardware failures or errors.
- **Example Use Case**:
  - Tracking the performance of an assembly line robot.

---

### **6. Monitoring a Non-Standard Database**
- **Scenario**: You have a database not supported by Dynatrace's standard integrations.
- **What Makes It a Custom Device**:
  - The database requires metrics to be pushed manually.
- **Data Collected**:
  - Metrics: Query execution time, connection counts.
  - Events: Database restarts or failures.
- **Example Use Case**:
  - Monitoring a legacy NoSQL database.

---

### **7. Tracking Batch Jobs**
- **Scenario**: You need to monitor batch jobs running on a server or scheduler.
- **What Makes It a Custom Device**:
  - Batch jobs do not generate real-time metrics unless configured to push data.
- **Data Collected**:
  - Metrics: Job execution time, success/failure rates.
  - Events: Job failures or delays.
- **Example Use Case**:
  - Monitoring nightly ETL processes in a data pipeline.

---

### **8. Monitoring a Custom Application in a Container**
- **Scenario**: You run a custom application in a Docker container not covered by OneAgent.
- **What Makes It a Custom Device**:
  - Custom metrics are pushed to Dynatrace via the API.
- **Data Collected**:
  - Metrics: Container CPU and memory usage, application response times.
  - Events: Container start/stop events.
- **Example Use Case**:
  - Monitoring a microservice with a proprietary runtime.

---

## **What Makes an Entity a Custom Device?**

1. **Non-Automatic Discovery**:
   - Custom devices are not automatically detected by OneAgent or native integrations.
2. **Manual or Programmatic Creation**:
   - Created using the **Custom Device API** to push metrics and events.
3. **Unique Identity**:
   - Custom devices are represented by unique identifiers (`custom_device.id`) within Dynatrace.
4. **Flexible Metrics and Events**:
   - You define the metrics and events to send, based on the monitoring needs.
5. **No Direct Agent Installation**:
   - Custom devices are for scenarios where installing an agent is not feasible or possible.

---

## **Querying Custom Devices in Dynatrace**

### **Fetching Metrics for a Custom Device**
```sql
fetch metrics
| filter dt.entity.custom_device == "CUSTOM-DEVICE-123"
| fields timestamp, datapoint.value, metric.key
```

### **Fetching Events for a Custom Device**
```sql
fetch events
| filter dt.entity.custom_device == "CUSTOM-DEVICE-123"
| fields timestamp, event.type, event.title
```

---

Would you like specific examples or guidance on setting up a custom device in Dynatrace?

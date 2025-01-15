
# Understanding the Flow of a User Request in Dynatrace

## Overview

This document outlines the flow of a user request through various layers of a monitored system in Dynatrace. It identifies involved entities, data passed, and models used at each stage, providing enhanced clarity through monitoring and troubleshooting.

Each section specifies key layers and their associated models in this workflow:

---

### 1. User Request

#### Entities Involved:
- **Application** (`dt.entity.application`)
- **User Session** (`dt.entity.user_session`)
- **User Action** (`dt.entity.user_action`)
- **Mobile App** (`dt.entity.mobile_app`)

#### Data Passed:
- **User Session**: Entire user journey from entry to exit.
- **User Action**: Button clicks, form submissions, etc.
- **Request Context**: User agent, IP, page URL, geolocation, etc.

#### Associated Models:
1. **Behavioral Model**: Establishes baselines for normal user interaction behavior.
2. **Business Model**: Correlates user actions with KPIs, such as conversion rates.
3. **Semantic Model**: Maps dependencies between user sessions and application layers.

#### Example Entities:
- Application: My-Web-App
- User Session: 1234567
- User Action: Login Button Click
- Mobile App: My-Mobile-App

---

### 2. Service Request

#### Entities Involved:
- **Service** (`dt.entity.service`)
- **Queue** (`dt.entity.queue`)
- **Load Balancer** (`dt.entity.load_balancer`)

#### Data Passed:
- **Request Metadata**: Headers, payloads, and methods (POST, GET, etc.).
- **Queue Messages**: Queued request payloads.
- **Span Data**: Tracks request flow through the system.

#### Associated Models:
1. **Logical Model**: Groups services by environment or team ownership.
2. **Integration Model**: Tracks how services integrate via queues and load balancers.
3. **Behavioral Model**: Monitors baselines for queue processing times and service response rates.

#### Example Entities:
- Service: Payment-Service
- Queue: Payment-Processing-Queue
- Load Balancer: AWS ALB

---

### Summary Table of High-Level Flow

| **Stage**            | **Input**                            | **Models Used**                     | **Enrichment Provided**                                         |
|-----------------------|--------------------------------------|--------------------------------------|-----------------------------------------------------------------|
| Data Collection       | Metrics, logs, traces from entities | Physical, Configuration             | Metadata, tags, context relationships                          |
| Data Processing       | Collected data                      | Behavioral, Semantic, Integration   | Baselines, dependency mappings                                 |
| Unified Observability | Processed data                      | Observability, AI/ML                | Anomaly detection, root cause insights                         |
| Business Context      | Observability data                  | Business, Service-Level Management  | Business impact, SLA compliance                                |
| Visualization         | Enriched data                       | Visualization, Lifecycle Management | Dashboards, historical trends, actionable insights             |

---

### Remarks:

This updated flow and summary table aim to enhance understanding by clearly outlining:
1. The **connection between models and entities** across monitoring workflows.
2. The **role of enrichment** at every stage, highlighting its value for actionable insights.
3. The inclusion of **summary-level visualization** for clarity.


# Dynatrace Entity Types (51-63)

| **#** | **Model Type**           | **Entity Category**     | **Entity Type**               | **Description**                               | **Examples**                              |
|-------|--------------------------|-------------------------|--------------------------------|-----------------------------------------------|------------------------------------------|
| 51    | Observability Models     | Observability Entities  | **EXTERNAL_SYNTHETIC_TEST**    | External synthetic monitoring tests.          | API tests, uptime checks                 |
| 52    | Observability Models     | Observability Entities  | **EXTERNAL_SYNTHETIC_TEST_STEP** | Steps within synthetic tests.                | User login workflows                     |
| 53    | Observability Models     | Observability Entities  | **SERVICE_METHOD**             | Individual methods within services.           | Specific API endpoints                   |
| 54    | Observability Models     | Observability Entities  | **SERVICE_METHOD_GROUP**       | Groups of related service methods.            | Grouped REST API methods                 |
| 55    | Observability Models     | Observability Entities  | **SOFTWARE_COMPONENT**         | Components of software for observability.     | Plugins, monitoring libraries            |
| 56    | Observability Models     | Observability Entities  | **RUNTIME_COMPONENT**          | Runtime systems under observation.            | JVM, Python interpreter                  |
| 57    | Observability Models     | Observability Entities  | **SYNTHETIC_TEST**             | Synthetic monitoring of application behavior. | Browser-based user simulations           |
| 58    | Observability Models     | Observability Entities  | **SYNTHETIC_TEST_STEP**        | Steps in synthetic tests.                     | Checkout steps in e-commerce apps        |
| 59    | Observability Models     | Observability Entities  | **HTTP_CHECK**                 | Monitoring HTTP endpoints.                    | Health checks for APIs                   |
| 60    | Observability Models     | Observability Entities  | **HTTP_CHECK_STEP**            | Specific steps in HTTP checks.                | User authentication workflows            |
| 61    | Observability Models     | Observability Entities  | **GEOLOCATION**                | Geographical location-based monitoring.       | User requests from specific zones        |
| 62    | Observability Models     | Observability Entities  | **GEOLOC_SITE**                | Sites monitored by geolocation.               | Data centers, regions                    |
| 63    | Observability Models     | Observability Entities  | **MONITORING_PLUGIN**          | Plugins for enhanced monitoring.              | Dynatrace extensions                     |

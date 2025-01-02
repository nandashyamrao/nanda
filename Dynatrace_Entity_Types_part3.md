
# Dynatrace Entity Types Grouped by Categories (Final Part)

## 7. Remaining Cloud-Native Entities (12)
Entities representing additional cloud and container infrastructure.

| **#** | **Entity Type**                  | **Description**                                | **Examples**                       |
|-------|----------------------------------|------------------------------------------------|-------------------------------------|
| 59    | **AWS_APPLICATION_LOAD_BALANCER** | AWS-specific application load balancers.       | ALB for web apps                   |
| 60    | **AWS_CREDENTIALS**              | AWS credential sets for accounts.              | AWS IAM keys, roles                |
| 61    | **GOOGLE_COMPUTE_ENGINE**        | Compute instances in Google Cloud Platform.    | Google Compute instances           |
| 62    | **GCP_ZONE**                     | Google Cloud Platform zones.                   | US-Central-1, Asia-South-1         |
| 63    | **DOCKER_CONTAINER_GROUP**       | Groups of Docker containers.                   | Docker Swarm setups                |
| 64    | **DOCKER_CONTAINER_GROUP_INSTANCE** | Instances of Docker container groups.          | Specific container setups          |
| 65    | **CF_FOUNDATION**                | Cloud Foundry application foundations.         | Application management setups      |
| 66    | **CLOUD_APPLICATION**            | Cloud-hosted applications.                     | SaaS services, web applications    |
| 67    | **CLOUD_APPLICATION_NAMESPACE**  | Namespaces within cloud applications.          | Kubernetes namespaces              |
| 68    | **MULTIPROTOCOL_MONITOR**        | Monitors for multiprotocol setups.             | Hybrid application communication   |
| 69    | **SOFTWARE_COMPONENT**           | Software components for application logic.     | Libraries, middleware              |
| 70    | **PROCESS_GROUP**                | Groups of running processes.                   | JVM clusters                       |

## 8. Observability Enhancements (7)
Entities related to monitoring and observability features.

| **#** | **Entity Type**                  | **Description**                                | **Examples**                       |
|-------|----------------------------------|------------------------------------------------|-------------------------------------|
| 71    | **RUNTIME_COMPONENT**            | Runtime-specific components for execution.     | JVMs, Python runtime setups        |
| 72    | **MONITORING_RULE**              | Rules defined for observability.               | API response time thresholds       |
| 73    | **HTTP_CHECK**                   | HTTP-based endpoint monitoring.                | Ping checks                        |
| 74    | **HTTP_CHECK_STEP**              | Workflow steps in HTTP monitoring checks.      | Endpoint path-by-path tracking     |
| 75    | **EXTERNAL_SYNTHETIC_TEST**      | External synthetic monitoring setups.          | Browser tests                      |
| 76    | **EXTERNAL_SYNTHETIC_TEST_STEP** | Steps in external synthetic monitoring tests.  | Login workflow tests               |
| 77    | **VIRTUALMACHINE**               | Virtualized machines for various services.     | Cloud VMs                          |

## 9. Miscellaneous Entities (9)
Entities that don’t fit neatly into other categories.

| **#** | **Entity Type**                  | **Description**                                | **Examples**                       |
|-------|----------------------------------|------------------------------------------------|-------------------------------------|
| 78    | **QUEUE**                        | Messaging queues for communication.            | Kafka topics, RabbitMQ queues      |
| 79    | **QUEUE_INSTANCE**               | Specific instances of message queues.          | SQS queues                         |
| 80    | **ELASTIC_LOAD_BALANCER**        | Load balancers with elastic properties.        | AWS ELB setups                     |
| 81    | **DATACENTER**                   | Physical or logical data centers.              | On-premise setups                  |
| 82    | **VCENTER**                      | VMware vCenter virtualized management.         | Management clusters                |
| 83    | **DISK**                         | Storage disk volumes.                          | SSDs for cloud instances           |
| 84    | **GEOLLOCATION**                 | Geographical mapping of hosted setups.         | Maps of regional servers           |
| 85    | **OPENSTACK_PROJECT**            | Tenant projects in OpenStack setups.           | Specific OpenStack applications    |
| 86    | **RELATIONAL_DATABASE_SERVICE**  | Relational database setups and services.       | MySQL, RDS                         |

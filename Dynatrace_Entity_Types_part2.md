
# Dynatrace Entity Types Grouped by Categories (Continued)

## 4. Database and Storage Entities (8)
Entities representing databases and storage volumes.

| **#** | **Entity Type**                | **Description**                               | **Examples**                       |
|-------|--------------------------------|-----------------------------------------------|-------------------------------------|
| 33    | **DATASTORE**                  | Datastore for monitoring.                     | MySQL, PostgreSQL                  |
| 34    | **DYNAMO_DB_TABLE**            | Tables in AWS DynamoDB.                       | User data table, Orders table       |
| 35    | **EBS_VOLUME**                 | AWS Elastic Block Store volumes.             | Persistent volume for AWS EC2      |
| 36    | **CINDER_VOLUME**              | OpenStack storage volumes.                   | Block storage in OpenStack          |
| 37    | **RELATIONAL_DATABASE_SERVICE** | Managed database services.                    | Amazon RDS, Google Cloud SQL       |
| 38    | **QUEUE_INSTANCE**             | Instances of messaging queues.               | AWS SQS, RabbitMQ                  |
| 39    | **S3BUCKET**                   | AWS S3 storage buckets.                      | Backup bucket, Logs bucket          |
| 40    | **SWIFT_CONTAINER**            | OpenStack Swift storage containers.          | Object storage in OpenStack         |

## 5. Networking Entities (9)
Entities related to networking components and infrastructure.

| **#** | **Entity Type**                | **Description**                               | **Examples**                       |
|-------|--------------------------------|-----------------------------------------------|-------------------------------------|
| 41    | **LOAD_BALANCER**              | Load balancers managing network traffic.     | AWS ELB, NGINX                     |
| 42    | **ELASTIC_LOAD_BALANCER**      | Elastic load balancers in cloud environments.| AWS ELB                            |
| 43    | **OPENSTACK_PROJECT**          | Projects in OpenStack environments.          | Tenant-specific OpenStack projects |
| 44    | **OPENSTACK_REGION**           | Regions in OpenStack infrastructure.         | Region-specific deployment         |
| 45    | **OPENSTACK_AVAILABILITY_ZONE**| Availability zones in OpenStack.             | Availability zones in OpenStack    |
| 46    | **OPENSTACK_COMPUTE_NODE**     | Compute nodes in OpenStack.                  | Compute resources in OpenStack     |
| 47    | **OPENSTACK_VM**               | Virtual machines in OpenStack.               | VM instances in OpenStack          |
| 48    | **NETWORK_INTERFACE**          | Network cards in virtual/physical hosts.     | Virtual NICs                       |
| 49    | **GEOLLOCATION**               | Geographical location data for entities.     | Data Center in California          |

## 6. Observability and Synthetic Entities (9)
Entities enabling observability and synthetic monitoring.

| **#** | **Entity Type**                | **Description**                               | **Examples**                       |
|-------|--------------------------------|-----------------------------------------------|-------------------------------------|
| 50    | **SYNTHETIC_TEST**             | Synthetic test monitors for apps.            | Browser test, API test             |
| 51    | **SYNTHETIC_TEST_STEP**        | Steps in synthetic test execution.           | Login page test step               |
| 52    | **SYNTHETIC_LOCATION**         | Locations where synthetic tests are executed.| Public locations, Private locations|
| 53    | **EXTERNAL_SYNTHETIC_TEST**    | External synthetic tests.                    | Third-party synthetic tests        |
| 54    | **EXTERNAL_SYNTHETIC_TEST_STEP**| Steps in external synthetic tests.           | Third-party test steps             |
| 55    | **MONITORING_RULE**            | Custom monitoring rules.                     | Rule to monitor API availability   |
| 56    | **HTTP_CHECK**                 | Monitors for HTTP endpoints.                 | Ping monitors                      |
| 57    | **HTTP_CHECK_STEP**            | Steps in HTTP check workflows.               | Step-by-step HTTP endpoint checks  |
| 58    | **RUNTIME_COMPONENT**          | Components at runtime (e.g., JVMs).          | JVM instance runtime components    |

...

# This file covers up to 58 entities; additional markdown file will continue the remaining.


# Dynatrace Entity Types: Improved Categorization
## 1. Infrastructure Entities (15)
Core infrastructure components like hosts, processes, and containers.
| **#** | **Entity Type**                  | **Description**                                | **Examples**                       |
|-------|----------------------------------|------------------------------------------------|-------------------------------------|
| 1     | **HOST**                         | Physical or virtual machines.                  | EC2 instance, on-prem server       |
| 2     | **PROCESS**                      | Running processes on a host.                   | nginx, java, python                |
| 3     | **PROCESS_GROUP**                | Group of identical processes.                  | Multiple nginx instances           |
| 4     | **CONTAINER_GROUP**              | Group of containers within orchestration.      | Docker container groups            |
| 5     | **CONTAINER_GROUP_INSTANCE**     | Specific instance of a container group.        | Pod running within EKS             |
| 6     | **OS**                           | Operating system on a host.                    | Linux, Windows Server              |
| 7     | **DISK**                         | Disks for data storage.                        | SSD, HDD                           |
| 8     | **DATACENTER**                   | Logical or physical data centers.              | AWS region, on-prem server rooms   |
| 9     | **NETWORK_INTERFACE**            | Interfaces used for communication.             | Ethernet, cloud NICs               |
| 10    | **VIRTUALMACHINE**               | Virtual machines hosted on hypervisors.        | VMs in VMware                      |
| 11    | **HYPERVISOR**                   | Virtualization platforms.                      | VMware ESXi, Hyper-V               |
| 12    | **HYPERVISOR_CLUSTER**           | Clusters of hypervisors.                       | VMware cluster setups              |
| 13    | **HYPERVISOR_DISK**              | Disks in virtualization platforms.             | VMware disk drives                 |
| 14    | **MULTIPROTOCOL_MONITOR**        | Monitoring hybrid communication systems.       | TCP, UDP, HTTP monitoring          |
| 15    | **VCENTER**                      | Management platforms for virtualized systems.  | VMware vSphere                     |
## 2. Cloud-Native Entities (15)
Entities designed for cloud orchestration and microservices.
| 16    | **KUBERNETES_CLUSTER**           | Orchestrated clusters in Kubernetes.           | EKS, GKE, AKS                      |
| 17    | **KUBERNETES_NODE**              | Nodes within a Kubernetes cluster.             | Worker nodes, control planes       |
| 18    | **KUBERNETES_SERVICE**           | Services running within Kubernetes.            | Frontend microservices             |
| 19    | **AWS_CREDENTIALS**              | Credentials for AWS integrations.              | IAM roles, secrets                 |
| 20    | **AWS_LAMBDA_FUNCTION**          | Functions in serverless architectures.         | AWS Lambda setups                  |
| 21    | **AWS_APPLICATION_LOAD_BALANCER** | Load balancers for cloud applications.         | AWS ALB setups                     |
| 22    | **CLOUD_APPLICATION**            | Cloud workloads within orchestration.          | Application workloads in GCP       |
| 23    | **CLOUD_APPLICATION_INSTANCE**   | Specific instances of cloud workloads.         | Individual cloud application pods  |
| 24    | **CLOUD_APPLICATION_NAMESPACE**  | Namespaces for cloud orchestration.            | Kubernetes namespaces              |
| 25    | **CLOUD_STORAGE_BUCKET**         | Storage buckets in cloud platforms.            | S3 buckets, GCP Cloud Storage      |
| 26    | **OPENSTACK_PROJECT**            | Projects within OpenStack.                     | OpenStack project setups           |
| 27    | **OPENSTACK_REGION**             | Regional zones in OpenStack.                   | US-East, EU-West                   |
| 28    | **OPENSTACK_VM**                 | Virtual machines in OpenStack environments.    | Virtualized OpenStack instances    |
| 29    | **ELASTIC_LOAD_BALANCER**        | Load balancers in elastic cloud setups.        | AWS ELB setups                     |
| 30    | **GCP_ZONE**                     | Geographical zones in GCP.                     | US-Central, EU-West                |
## 3. Application Entities (10)
Entities representing applications and services.
| 31    | **APPLICATION**                  | Web or mobile applications.                    | Retail app, customer portal        |
| 32    | **CUSTOM_APPLICATION**           | User-defined custom applications.              | IoT applications                   |
| 33    | **SERVICE**                      | Backend services providing business logic.     | Payment API, Order service         |
| 34    | **SERVICE_INSTANCE**             | Specific instances of services.                | Replica of a service in deployment |
| 35    | **SOFTWARE_COMPONENT**           | Software components for application logic.     | Libraries, middleware              |
| 36    | **RUNTIME_COMPONENT**            | Runtime-specific components for execution.     | JVMs, Python runtime setups        |
| 37    | **DEVICE_APPLICATION_METHOD**    | User actions monitored in applications.        | Mobile tap gestures                |
| 38    | **DEVICE_APPLICATION_METHOD_GROUP** | Groups of application methods or actions.      | Grouped user interactions          |
| 39    | **MOBILE_APPLICATION**           | Mobile applications hosted for end-users.      | Mobile banking app                 |
| 40    | **HTTP_CHECK**                   | HTTP-based endpoint monitoring.                | API health checks                  |
... (continuing for other entities and adjusting further as needed)
## 4. Database and Storage Entities (10)
Entities related to databases and storage systems.
| 41    | **RELATIONAL_DATABASE_SERVICE**  | Managed relational databases.                  | AWS RDS, Azure SQL Database        |
| 42    | **DYNAMO_DB_TABLE**              | Tables in DynamoDB for NoSQL databases.        | DynamoDB table                     |
| 43    | **EBS_VOLUME**                   | Storage volumes attached to EC2 instances.     | Amazon Elastic Block Storage       |
| 44    | **CINDER_VOLUME**                | Volumes in OpenStack storage systems.          | Cinder storage                     |
| 45    | **SWIFT_CONTAINER**              | Object storage containers in OpenStack Swift.  | OpenStack object storage buckets   |
| 46    | **S3BUCKET**                     | Object storage buckets in AWS.                 | Amazon S3 buckets                  |
| 47    | **DATASTORE**                    | General-purpose data storage systems.          | Elasticsearch, Redis               |
| 48    | **QUEUE**                        | Queues for messaging systems.                  | Kafka, RabbitMQ                    |
| 49    | **QUEUE_INSTANCE**               | Specific instances of message queues.          | SQS queues, Kafka topics           |
| 50    | **DISK**                         | Disks used in storage systems.                 | Physical or virtual disks          |
## 5. Observability Entities (13)
Entities supporting observability and monitoring.
| 51    | **EXTERNAL_SYNTHETIC_TEST**      | External synthetic monitoring tests.           | API tests, uptime checks           |
| 52    | **EXTERNAL_SYNTHETIC_TEST_STEP** | Steps within synthetic tests.                  | User login workflows               |
| 53    | **SERVICE_METHOD**               | Individual methods within services.            | Specific API endpoints             |
| 54    | **SERVICE_METHOD_GROUP**         | Groups of related service methods.             | Grouped REST API methods           |
| 55    | **SOFTWARE_COMPONENT**           | Components of software for observability.      | Plugins, monitoring libraries      |
| 56    | **RUNTIME_COMPONENT**            | Runtime systems under observation.             | JVM, Python interpreter            |
| 57    | **SYNTHETIC_TEST**               | Synthetic monitoring of application behavior.  | Browser-based user simulations     |
| 58    | **SYNTHETIC_TEST_STEP**          | Steps in synthetic tests.                      | Checkout steps in e-commerce apps  |
| 59    | **HTTP_CHECK**                   | Monitoring HTTP endpoints.                     | Health checks for APIs             |
| 60    | **HTTP_CHECK_STEP**              | Specific steps in HTTP checks.                 | User authentication workflows      |
| 61    | **GEOLLOCATION**                 | Geographical location-based monitoring.        | User requests from specific zones  |
| 62    | **GEOCLOC_SITE**                 | Sites monitored by geolocation.                | Data centers, regions              |
| 63    | **MONITORING_PLUGIN**            | Plugins for enhanced monitoring.               | Dynatrace extensions               |
## 6. Remaining Technology-Specific Entities (20)
Entities tied to specific technologies and tools.
| 64    | **APPMON_SERVER**                | AppMon server setups.                          | Dynatrace AppMon setups            |
| 65    | **APPMON_SYSTEM_PROFILE**        | System profiles in AppMon.                     | Application monitoring profiles    |
| 66    | **CF_FOUNDATION**                | Cloud Foundry foundations.                     | Pivotal Cloud Foundry              |
| 67    | **BOSH_DEPLOYMENT**              | BOSH-managed deployments.                      | VM deployments with BOSH           |
| 68    | **DEVICE_APPLICATION_METHOD**    | User actions tracked in device apps.           | Mobile app gestures                |
| 69    | **DEVICE_APPLICATION_METHOD_GROUP** | Groups of actions in device apps.              | Grouped mobile interactions        |
| 70    | **EXTERNAL_TOOL**                | External tools connected to Dynatrace.         | Prometheus, Grafana integrations   |
| 71    | **ELASTIC_LOAD_BALANCER**        | Cloud-based load balancing services.           | AWS ELB setups                     |
| 72    | **KUBERNETES_NAMESPACE**         | Namespaces for Kubernetes.                     | Namespace setups for isolation     |
| 73    | **OPENSTACK_COMPUTE_NODE**       | Compute nodes within OpenStack setups.         | OpenStack node clusters            |
| 74    | **OPENSTACK_PROJECT**            | Projects managed in OpenStack.                 | OpenStack resource pools           |
| 75    | **GOOGLE_COMPUTE_ENGINE**        | Compute instances in Google Cloud.             | GCP VMs                            |
| 76    | **RELATIONAL_DATABASE_SERVICE**  | Managed relational databases.                  | RDS, MySQL, PostgreSQL             |
| 77    | **VIRTUAL_MACHINE**              | VMs managed in cloud or on-prem.               | AWS, VMware, Azure instances       |
| 78    | **DATA_CENTER**                  | Physical or logical data centers.              | On-prem or cloud-based data hubs   |
| 79    | **SWIFT_CONTAINER**              | Object storage systems.                        | OpenStack Swift                    |
| 80    | **ENVIRONMENT**                  | Complete monitoring environments.              | Staging, production environments   |
| 81    | **SOFTWARE_COMPONENT**           | Components inside monitored applications.      | Plugins, agents                    |
| 82    | **USER_SESSION**                 | End-user sessions tracked by Dynatrace.        | RUM session monitoring             |
| 83    | **VCENTER**                      | VMware vCenter instances.                      | VMware management tools            |
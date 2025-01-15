|   # | Entity Type                     | Model Type           | Description                                           |
|----:|:--------------------------------|:---------------------|:------------------------------------------------------|
|   1 | HOST                            | Infrastructure       | Represents physical or virtual machines.              |
|   2 | PROCESS                         | Infrastructure       | Represents running processes on a host.               |
|   3 | PROCESS_GROUP                   | Infrastructure       | Groups identical processes together.                  |
|   4 | CONTAINER_GROUP                 | Infrastructure       | Groups of containers within orchestration.            |
|   5 | CONTAINER_GROUP_INSTANCE        | Infrastructure       | Represents instances of container groups.             |
|   6 | OS                              | Infrastructure       | Operating system information for a host.              |
|   7 | DISK                            | Infrastructure       | Represents physical or virtual disks on a host.       |
|   8 | DATACENTER                      | Infrastructure       | Represents logical or physical data centers.          |
|   9 | NETWORK_INTERFACE               | Infrastructure       | Represents network interfaces on a host.              |
|  10 | VIRTUALMACHINE                  | Infrastructure       | Represents virtual machines hosted on hypervisors.    |
|  11 | HYPERVISOR                      | Infrastructure       | Represents virtualization platforms like VMware ESXi. |
|  12 | HYPERVISOR_CLUSTER              | Infrastructure       | Clusters of virtualization platforms.                 |
|  13 | HYPERVISOR_DISK                 | Infrastructure       | Represents disks on hypervisors.                      |
|  14 | MULTIPROTOCOL_MONITOR           | Infrastructure       | Monitors hybrid communication systems.                |
|  15 | VCENTER                         | Infrastructure       | Represents VMware management platforms.               |
|  16 | KUBERNETES_CLUSTER              | Cloud-Native         | Represents orchestrated clusters in Kubernetes.       |
|  17 | KUBERNETES_NODE                 | Cloud-Native         | Represents nodes within a Kubernetes cluster.         |
|  18 | KUBERNETES_SERVICE              | Cloud-Native         | Represents services running within Kubernetes.        |
|  19 | AWS_CREDENTIALS                 | Cloud-Native         | Credentials for AWS integrations.                     |
|  20 | AWS_LAMBDA_FUNCTION             | Cloud-Native         | Functions in serverless architectures.                |
|  21 | AWS_APPLICATION_LOAD_BALANCER   | Cloud-Native         | Load balancers for cloud applications.                |
|  22 | CLOUD_APPLICATION               | Cloud-Native         | Represents cloud workloads within orchestration.      |
|  23 | CLOUD_APPLICATION_INSTANCE      | Cloud-Native         | Instances of cloud workloads.                         |
|  24 | CLOUD_APPLICATION_NAMESPACE     | Cloud-Native         | Namespaces for cloud orchestration.                   |
|  25 | CLOUD_STORAGE_BUCKET            | Cloud-Native         | Storage buckets in cloud platforms.                   |
|  26 | OPENSTACK_PROJECT               | Cloud-Native         | Projects within OpenStack environments.               |
|  27 | OPENSTACK_REGION                | Cloud-Native         | Represents regions in OpenStack.                      |
|  28 | OPENSTACK_VM                    | Cloud-Native         | Represents virtual machines in OpenStack.             |
|  29 | ELASTIC_LOAD_BALANCER           | Cloud-Native         | Load balancers in cloud environments.                 |
|  30 | GCP_ZONE                        | Cloud-Native         | Represents zones in Google Cloud Platform.            |
|  31 | APPLICATION                     | Application          | Represents web or mobile applications.                |
|  32 | CUSTOM_APPLICATION              | Application          | Represents user-defined custom applications.          |
|  33 | SERVICE                         | Application          | Backend services providing business logic.            |
|  34 | SERVICE_INSTANCE                | Application          | Represents specific instances of services.            |
|  35 | SOFTWARE_COMPONENT              | Application          | Software components for application logic.            |
|  36 | RUNTIME_COMPONENT               | Application          | Represents runtime-specific components.               |
|  37 | DEVICE_APPLICATION_METHOD       | Application          | Tracks user interactions in applications.             |
|  38 | DEVICE_APPLICATION_METHOD_GROUP | Application          | Groups user interactions in apps.                     |
|  39 | MOBILE_APPLICATION              | Application          | Represents mobile applications for users.             |
|  40 | HTTP_CHECK                      | Application          | Monitors HTTP endpoints for health checks.            |
|  41 | RELATIONAL_DATABASE_SERVICE     | Database and Storage | Managed relational database services.                 |
|  42 | DYNAMO_DB_TABLE                 | Database and Storage | Represents tables in DynamoDB.                        |
|  43 | EBS_VOLUME                      | Database and Storage | Represents storage volumes in AWS.                    |
|  44 | CINDER_VOLUME                   | Database and Storage | Represents OpenStack storage volumes.                 |
|  45 | SWIFT_CONTAINER                 | Database and Storage | OpenStack object storage containers.                  |
|  46 | S3BUCKET                        | Database and Storage | Represents object storage buckets in AWS.             |
|  47 | DATASTORE                       | Database and Storage | Represents general-purpose data storage systems.      |
|  48 | QUEUE                           | Database and Storage | Represents queues in messaging systems.               |
|  49 | QUEUE_INSTANCE                  | Database and Storage | Specific instances of messaging queues.               |
|  50 | DISK                            | Database and Storage | Represents disks used in storage systems.             |
|  51 | EXTERNAL_SYNTHETIC_TEST         | Observability        | External synthetic monitoring tests.                  |
|  52 | EXTERNAL_SYNTHETIC_TEST_STEP    | Observability        | Steps within synthetic monitoring tests.              |
|  53 | SERVICE_METHOD                  | Observability        | Individual methods within services.                   |
|  54 | SERVICE_METHOD_GROUP            | Observability        | Groups of related service methods.                    |
|  55 | SOFTWARE_COMPONENT              | Observability        | Components in monitored software.                     |
|  56 | RUNTIME_COMPONENT               | Observability        | Runtime systems under observation.                    |
|  57 | SYNTHETIC_TEST                  | Observability        | Monitors application behavior using simulations.      |
|  58 | SYNTHETIC_TEST_STEP             | Observability        | Steps in synthetic monitoring workflows.              |
|  59 | HTTP_CHECK                      | Observability        | Monitors HTTP-based endpoints.                        |
|  60 | HTTP_CHECK_STEP                 | Observability        | Specific steps within HTTP checks.                    |
|  61 | GEOLLOCATION                    | Observability        | Tracks geographical locations for monitoring.         |
|  62 | GEOCLOC_SITE                    | Observability        | Monitored sites by geolocation.                       |
|  63 | MONITORING_PLUGIN               | Observability        | Plugins for extended monitoring capabilities.         |
|  64 | APPMON_SERVER                   | Technology-Specific  | Represents AppMon server setups.                      |
|  65 | APPMON_SYSTEM_PROFILE           | Technology-Specific  | Profiles for AppMon systems.                          |
|  66 | CF_FOUNDATION                   | Technology-Specific  | Cloud Foundry foundations.                            |
|  67 | BOSH_DEPLOYMENT                 | Technology-Specific  | Represents BOSH-managed deployments.                  |
|  68 | DEVICE_APPLICATION_METHOD       | Technology-Specific  | Tracks device-specific user actions.                  |
|  69 | DEVICE_APPLICATION_METHOD_GROUP | Technology-Specific  | Groups actions in device apps.                        |
|  70 | EXTERNAL_TOOL                   | Technology-Specific  | External tools integrated with Dynatrace.             |
|  71 | ELASTIC_LOAD_BALANCER           | Technology-Specific  | Represents cloud-based load balancers.                |
|  72 | KUBERNETES_NAMESPACE            | Technology-Specific  | Represents namespaces in Kubernetes.                  |
|  73 | OPENSTACK_COMPUTE_NODE          | Technology-Specific  | Compute nodes in OpenStack setups.                    |
|  74 | OPENSTACK_PROJECT               | Technology-Specific  | Projects managed in OpenStack.                        |
|  75 | GOOGLE_COMPUTE_ENGINE           | Technology-Specific  | Compute instances in Google Cloud.                    |
|  76 | RELATIONAL_DATABASE_SERVICE     | Technology-Specific  | Managed relational database services.                 |
|  77 | VIRTUAL_MACHINE                 | Technology-Specific  | Represents virtual machines.                          |
|  78 | DATA_CENTER                     | Technology-Specific  | Represents physical/logical data centers.             |
|  79 | SWIFT_CONTAINER                 | Technology-Specific  | Object storage containers in OpenStack.               |
|  80 | ENVIRONMENT                     | Technology-Specific  | Represents entire monitoring environments.            |
|  81 | SOFTWARE_COMPONENT              | Technology-Specific  | Components inside monitored applications.             |
|  82 | USER_SESSION                    | Technology-Specific  | Tracks end-user sessions.                             |
|  83 | VCENTER                         | Technology-Specific  | Represents VMware vCenter management tools.           |
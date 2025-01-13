
# Dynatrace Entity Types: Model and Categorization (64-83)

| **#** | **Model Type**        | **Entity Category**             | **Entity Type**                    | **Description**                                   | **Examples**                        |
|-------|-----------------------|---------------------------------|------------------------------------|-------------------------------------------------|------------------------------------|
| 64    | Logical/Technology    | Technology-Specific Entities    | **APPMON_SERVER**                  | AppMon server setups.                            | Dynatrace AppMon setups             |
| 65    | Logical/Technology    | Technology-Specific Entities    | **APPMON_SYSTEM_PROFILE**          | System profiles in AppMon.                      | Application monitoring profiles     |
| 66    | Logical               | Cloud-Native Entities           | **CF_FOUNDATION**                  | Cloud Foundry foundations.                      | Pivotal Cloud Foundry               |
| 67    | Logical               | Infrastructure Entities         | **BOSH_DEPLOYMENT**                | BOSH-managed deployments.                       | VM deployments with BOSH            |
| 68    | Logical               | Application Entities            | **DEVICE_APPLICATION_METHOD**      | User actions tracked in device apps.           | Mobile app gestures                 |
| 69    | Logical               | Application Entities            | **DEVICE_APPLICATION_METHOD_GROUP**| Groups of actions in device apps.              | Grouped mobile interactions         |
| 70    | Logical               | Technology-Specific Entities    | **EXTERNAL_TOOL**                  | External tools connected to Dynatrace.          | Prometheus, Grafana integrations    |
| 71    | Physical              | Cloud-Native Entities           | **ELASTIC_LOAD_BALANCER**          | Cloud-based load balancing services.           | AWS ELB setups                      |
| 72    | Logical               | Cloud-Native Entities           | **KUBERNETES_NAMESPACE**           | Namespaces for Kubernetes.                     | Namespace setups for isolation      |
| 73    | Physical              | Cloud-Native Entities           | **OPENSTACK_COMPUTE_NODE**         | Compute nodes within OpenStack setups.         | OpenStack node clusters             |
| 74    | Logical               | Cloud-Native Entities           | **OPENSTACK_PROJECT**              | Projects managed in OpenStack.                 | OpenStack resource pools            |
| 75    | Physical              | Cloud-Native Entities           | **GOOGLE_COMPUTE_ENGINE**          | Compute instances in Google Cloud.             | GCP VMs                             |
| 76    | Logical               | Database Entities               | **RELATIONAL_DATABASE_SERVICE**    | Managed relational databases.                  | RDS, MySQL, PostgreSQL              |
| 77    | Physical              | Infrastructure Entities         | **VIRTUAL_MACHINE**                | VMs managed in cloud or on-prem.               | AWS, VMware, Azure instances        |
| 78    | Physical              | Infrastructure Entities         | **DATA_CENTER**                    | Physical or logical data centers.              | On-prem or cloud-based data hubs    |
| 79    | Logical               | Infrastructure Entities         | **SWIFT_CONTAINER**                | Object storage systems.                        | OpenStack Swift                     |
| 80    | Logical               | Infrastructure Entities         | **ENVIRONMENT**                    | Complete monitoring environments.              | Staging, production environments    |
| 81    | Logical               | Application Entities            | **SOFTWARE_COMPONENT**             | Components inside monitored applications.      | Plugins, agents                     |
| 82    | Logical               | Observability Entities          | **USER_SESSION**                   | End-user sessions tracked by Dynatrace.        | RUM session monitoring              |
| 83    | Logical/Technology    | Infrastructure Entities         | **VCENTER**                        | VMware vCenter instances.                      | VMware management tools             |

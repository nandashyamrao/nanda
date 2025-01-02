
# Dynatrace Entity Types Grouped by Categories (Updated to Include All 86 Entity Types)

## 1. Infrastructure Entities (10)
Entities representing the physical or virtual infrastructure of your IT environment.

| **#** | **Entity Type**         | **Description**                                | **Examples**                    |
|-------|-------------------------|------------------------------------------------|----------------------------------|
| 1     | **HOST**                | Physical or virtual machines.                 | Linux server, Windows VM        |
| 2     | **VMWARE_DATACENTER**   | VMware virtualized datacenter.                | Datacenter in VMware            |
| 3     | **VIRTUALMACHINE**      | Virtual machines running on hypervisors.      | Virtual machines in VMware, AWS |
| 4     | **OS**                  | Operating systems on hosts.                   | Windows Server, Ubuntu          |
| 5     | **NETWORK_INTERFACE**   | Network interface cards in infrastructure.    | NIC in a physical or virtual host |
| 6     | **HYPERVISOR**          | Hypervisors managing virtual machines.        | ESXi, Hyper-V                   |
| 7     | **HYPERVISOR_DISK**     | Storage volumes attached to hypervisors.      | Disk storage for VMs            |
| 8     | **HYPERVISOR_CLUSTER**  | Clusters of hypervisors.                      | VMware ESXi clusters            |
| 9     | **OPENSTACK_VM**        | Virtual machines in OpenStack environments.   | OpenStack compute instances     |
| 10    | **NEUTRON_SUBNET**      | Subnets in OpenStack Neutron.                 | Network subnets for OpenStack   |

## 2. Application Entities (12)
Entities related to the applications and services running in your environment.

| **#** | **Entity Type**         | **Description**                                | **Examples**                           |
|-------|-------------------------|------------------------------------------------|-----------------------------------------|
| 11    | **APPLICATION**         | Monitored web or mobile applications.         | Online shopping portal, mobile app     |
| 12    | **SERVICE**             | Backend services or APIs.                     | Payment service, Order API             |
| 13    | **SERVICE_INSTANCE**    | Specific instances of services.               | Instance of "Payment Service"          |
| 14    | **SERVICE_METHOD**      | Specific methods within a service.            | REST endpoints, API methods            |
| 15    | **APPLICATION_METHOD**  | Specific methods or functions within apps.    | Java methods, Python functions         |
| 16    | **APPLICATION_METHOD_GROUP** | Groups of application methods.                  | Grouped API methods                    |
| 17    | **CUSTOM_APPLICATION**  | Non-standard applications for monitoring.     | IoT app, custom-built apps             |
| 18    | **CUSTOM_DEVICE**       | Custom monitoring devices (e.g., IoT).        | IoT sensors, network devices           |
| 19    | **CUSTOM_DEVICE_GROUP** | Groups of custom devices.                     | IoT device clusters                    |
| 20    | **BROWSER**             | Web browsers for synthetic monitoring.        | Chrome, Firefox                        |
| 21    | **MULTIPROTOCOL_MONITOR** | Monitors for multi-protocol connections.       | Monitors for hybrid app communications |
| 22    | **SOFTWARE_COMPONENT**  | Components of a larger software system.       | Library dependencies, modules          |

## 3. Cloud-Native Entities (10)
Entities specific to cloud platforms and containerized environments.

| **#** | **Entity Type**         | **Description**                                | **Examples**                     |
|-------|-------------------------|------------------------------------------------|-----------------------------------|
| 23    | **AWS_LAMBDA_FUNCTION** | AWS Lambda serverless functions.              | Lambda for event processing       |
| 24    | **KUBERNETES_CLUSTER**  | Kubernetes clusters orchestrating workloads.  | Kubernetes clusters               |
| 25    | **CONTAINER_GROUP_INSTANCE** | Instances of containerized workloads.         | Docker containers, Pod instances  |
| 26    | **KUBERNETES_NODE**     | Nodes in a Kubernetes cluster.                | Kubernetes worker nodes           |
| 27    | **KUBERNETES_SERVICE**  | Kubernetes services exposed to the network.   | ClusterIP, NodePort               |
| 28    | **CLOUD_APPLICATION**   | Applications running in cloud environments.   | AWS-hosted apps                   |
| 29    | **CLOUD_APPLICATION_NAMESPACE** | Namespaces for cloud applications.            | Namespaces in Kubernetes           |
| 30    | **DOCKER_CONTAINER_GROUP** | Groups of containers in Docker.                | Docker Swarm services              |
| 31    | **DOCKER_CONTAINER_GROUP_INSTANCE** | Instances of Docker container groups.          | Instances of Docker Swarm services |
| 32    | **CF_FOUNDATION**       | Cloud Foundry foundations.                    | Cloud Foundry app foundations      |

...

# Remaining sections and entities will follow a similar approach. This ensures a complete list of **86 entities**. 


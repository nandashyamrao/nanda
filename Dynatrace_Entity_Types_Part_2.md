|   # | Model Type         | Entity Category       | Entity Type                   | Description                                 | Examples                          |
|----:|:-------------------|:----------------------|:------------------------------|:--------------------------------------------|:----------------------------------|
|  16 | Cloud-Native Model | Cloud-Native Entities | KUBERNETES_CLUSTER            | Orchestrated clusters in Kubernetes.        | EKS, GKE, AKS                     |
|  17 | Cloud-Native Model | Cloud-Native Entities | KUBERNETES_NODE               | Nodes within a Kubernetes cluster.          | Worker nodes, control planes      |
|  18 | Cloud-Native Model | Cloud-Native Entities | KUBERNETES_SERVICE            | Services running within Kubernetes.         | Frontend microservices            |
|  19 | Cloud-Native Model | Cloud-Native Entities | AWS_CREDENTIALS               | Credentials for AWS integrations.           | IAM roles, secrets                |
|  20 | Cloud-Native Model | Cloud-Native Entities | AWS_LAMBDA_FUNCTION           | Functions in serverless architectures.      | AWS Lambda setups                 |
|  21 | Cloud-Native Model | Cloud-Native Entities | AWS_APPLICATION_LOAD_BALANCER | Load balancers for cloud applications.      | AWS ALB setups                    |
|  22 | Cloud-Native Model | Cloud-Native Entities | CLOUD_APPLICATION             | Cloud workloads within orchestration.       | Application workloads in GCP      |
|  23 | Cloud-Native Model | Cloud-Native Entities | CLOUD_APPLICATION_INSTANCE    | Specific instances of cloud workloads.      | Individual cloud application pods |
|  24 | Cloud-Native Model | Cloud-Native Entities | CLOUD_APPLICATION_NAMESPACE   | Namespaces for cloud orchestration.         | Kubernetes namespaces             |
|  25 | Cloud-Native Model | Cloud-Native Entities | CLOUD_STORAGE_BUCKET          | Storage buckets in cloud platforms.         | S3 buckets, GCP Cloud Storage     |
|  26 | Cloud-Native Model | Cloud-Native Entities | OPENSTACK_PROJECT             | Projects within OpenStack.                  | OpenStack project setups          |
|  27 | Cloud-Native Model | Cloud-Native Entities | OPENSTACK_REGION              | Regional zones in OpenStack.                | US-East, EU-West                  |
|  28 | Cloud-Native Model | Cloud-Native Entities | OPENSTACK_VM                  | Virtual machines in OpenStack environments. | Virtualized OpenStack instances   |
|  29 | Cloud-Native Model | Cloud-Native Entities | ELASTIC_LOAD_BALANCER         | Load balancers in elastic cloud setups.     | AWS ELB setups                    |
|  30 | Cloud-Native Model | Cloud-Native Entities | GCP_ZONE                      | Geographical zones in GCP.                  | US-Central, EU-West               |
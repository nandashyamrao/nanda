|   # | Model Type           | Entity Category         | Entity Type              | Description                                   | Examples                         |
|----:|:---------------------|:------------------------|:-------------------------|:----------------------------------------------|:---------------------------------|
|   1 | Infrastructure Model | Infrastructure Entities | HOST                     | Physical or virtual machines.                 | EC2 instance, on-prem server     |
|   2 | Infrastructure Model | Infrastructure Entities | PROCESS                  | Running processes on a host.                  | nginx, java, python              |
|   3 | Infrastructure Model | Infrastructure Entities | PROCESS_GROUP            | Group of identical processes.                 | Multiple nginx instances         |
|   4 | Infrastructure Model | Infrastructure Entities | CONTAINER_GROUP          | Group of containers within orchestration.     | Docker container groups          |
|   5 | Infrastructure Model | Infrastructure Entities | CONTAINER_GROUP_INSTANCE | Specific instance of a container group.       | Pod running within EKS           |
|   6 | Infrastructure Model | Infrastructure Entities | OS                       | Operating system on a host.                   | Linux, Windows Server            |
|   7 | Infrastructure Model | Infrastructure Entities | DISK                     | Disks for data storage.                       | SSD, HDD                         |
|   8 | Infrastructure Model | Infrastructure Entities | DATACENTER               | Logical or physical data centers.             | AWS region, on-prem server rooms |
|   9 | Infrastructure Model | Infrastructure Entities | NETWORK_INTERFACE        | Interfaces used for communication.            | Ethernet, cloud NICs             |
|  10 | Infrastructure Model | Infrastructure Entities | VIRTUALMACHINE           | Virtual machines hosted on hypervisors.       | VMs in VMware                    |
|  11 | Infrastructure Model | Infrastructure Entities | HYPERVISOR               | Virtualization platforms.                     | VMware ESXi, Hyper-V             |
|  12 | Infrastructure Model | Infrastructure Entities | HYPERVISOR_CLUSTER       | Clusters of hypervisors.                      | VMware cluster setups            |
|  13 | Infrastructure Model | Infrastructure Entities | HYPERVISOR_DISK          | Disks in virtualization platforms.            | VMware disk drives               |
|  14 | Infrastructure Model | Infrastructure Entities | MULTIPROTOCOL_MONITOR    | Monitoring hybrid communication systems.      | TCP, UDP, HTTP monitoring        |
|  15 | Infrastructure Model | Infrastructure Entities | VCENTER                  | Management platforms for virtualized systems. | VMware vSphere                   |
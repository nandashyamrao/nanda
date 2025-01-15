
# Understanding the Flow of a User Request in Dynatrace

...

## Summary Table of Entities and Associated Models

| Entity Type        | DQL Reference               | Example Entity                  | Associated Models                                      |
|--------------------|-----------------------------|----------------------------------|-------------------------------------------------------|
| Application        | dt.entity.application      | My-Web-App                      | Behavioral Model, Business Model, Semantic Model     |
| User Session       | dt.entity.user_session     | User-Session-123                | Behavioral Model, Business Model                     |
| User Action        | dt.entity.user_action      | Login Button Click              | Behavioral Model, Business Model                     |
| Mobile App         | dt.entity.mobile_app       | My-Mobile-App                   | Behavioral Model, Business Model                     |
| Service            | dt.entity.service          | Payment-Service                 | Logical Model, Integration Model, Behavioral Model   |
| Queue              | dt.entity.queue            | Payment-Processing-Queue        | Logical Model, Integration Model, Behavioral Model   |
| Load Balancer      | dt.entity.load_balancer    | AWS ALB                         | Integration Model, Behavioral Model                  |
| Host               | dt.entity.host             | EC2-Instance-567                | Physical Model, Hybrid Cloud Model, Configuration Model |
| Container          | dt.entity.container        | Payment-Service-Container       | Physical Model, Hybrid Cloud Model                   |
| Kubernetes Cluster | dt.entity.kubernetes_cluster | Production-K8s-Cluster         | Hybrid Cloud Model, Physical Model                   |
| Database           | dt.entity.database         | Payment-DB                      | Business Model, Behavioral Model, Configuration Model|
| Storage            | dt.entity.storage          | S3-Bucket-Transaction-Data      | Business Model, Behavioral Model, Configuration Model|
| ActiveGate         | N/A                        | Secure Proxy                    | Observability Model, AI/ML Model, Integration Model  |
| OneAgent           | N/A                        | Installed Agent                 | Observability Model, AI/ML Model                     |
| Problem            | dt.entity.problem          | Payment-Problem                 | Semantic Model, Observability Model, AI/ML Model     |
| Synthetic Test     | dt.entity.synthetic_test   | Synthetic-Test-123              | Visualization Model, Observability Model, Business Model |

...


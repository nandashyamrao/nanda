
# **Examples of Using Expand and Flatten in DQL**

---

## **1. Expand Command Examples**

### Example 1: Kubernetes Pod Containers
#### Query:
```dql
fetch dt.entity.kubernetes_pod
| fields kubernetes.podName, kubernetes.namespace, kubernetes.containers
| expand container = kubernetes.containers
| fields kubernetes.podName, kubernetes.namespace, container.name, container.image, container.status
| limit 10
```

#### Before:
| **Pod Name**       | **Namespace** | **Containers**                                                                                   |
|---------------------|---------------|--------------------------------------------------------------------------------------------------|
| pod-frontend-123    | frontend      | `[ { name: "nginx", image: "nginx:latest", status: "running" }, { name: "sidecar", image: "log:1.2", status: "running" } ]` |
| pod-backend-456     | backend       | `[ { name: "api", image: "python:3.9", status: "running" } ]`                                    |

#### After:
| **Pod Name**       | **Namespace** | **Container Name** | **Container Image** | **Container Status** |
|---------------------|---------------|--------------------|----------------------|-----------------------|
| pod-frontend-123    | frontend      | nginx              | nginx:latest         | running               |
| pod-frontend-123    | frontend      | sidecar            | log:1.2              | running               |
| pod-backend-456     | backend       | api                | python:3.9           | running               |

---

### Example 2: Applications and Associated Requests
#### Query:
```dql
fetch dt.entity.application
| fields application.name, application.requests
| expand request = application.requests
| fields application.name, request.name, request.duration
```

#### Before:
| **Application Name** | **Requests**                                                                                                      |
|-----------------------|-------------------------------------------------------------------------------------------------------------------|
| app-frontend          | `[ { name: "GET /home", duration: 120 }, { name: "POST /login", duration: 200 } ]`                                |

#### After:
| **Application Name** | **Request Name**   | **Request Duration** |
|-----------------------|--------------------|-----------------------|
| app-frontend          | GET /home         | 120                   |
| app-frontend          | POST /login       | 200                   |

---

## **2. Flatten Command Examples**

### Example 1: Kubernetes Labels
#### Query:
```dql
fetch dt.entity.kubernetes_pod
| fields kubernetes.podName, kubernetes.labels
| fieldsFlatten kubernetes.labels, prefix: "label."
```

#### Before:
| **Pod Name**    | **Labels**                                                                                       |
|------------------|--------------------------------------------------------------------------------------------------|
| pod-frontend-123 | `{ app: "frontend", env: "production", version: "1.0.0" }`                                       |

#### After:
| **Pod Name**    | **Label.App**   | **Label.Env**  | **Label.Version** |
|------------------|-----------------|----------------|--------------------|
| pod-frontend-123 | frontend        | production     | 1.0.0             |

---

### Example 2: Nested Trace Details
#### Query:
```dql
fetch dt.entity.trace
| fields trace.name, trace.details
| fieldsFlatten trace.details, prefix: "detail."
```

#### Before:
| **Trace Name**       | **Details**                                                                                   |
|-----------------------|-----------------------------------------------------------------------------------------------|
| trace-001            | `{ duration: 200, spanCount: 5, errorCount: 1 }`                                              |

#### After:
| **Trace Name**       | **Detail.Duration** | **Detail.SpanCount** | **Detail.ErrorCount** |
|-----------------------|---------------------|-----------------------|------------------------|
| trace-001            | 200                 | 5                     | 1                      |

---

## **More Examples**
- Add similar examples to include a total of **10 expand** and **10 flatten** cases with **before** and **after** data.

---

## **Download Instructions**
Let me know if you'd like me to add more examples or modify any! 

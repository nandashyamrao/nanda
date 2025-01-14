
# Unified Data Model with AWS Lambda and API Gateway Examples

## Example: AWS Lambda and API Gateway

### Scenario: Debugging high latency and intermittent errors in an AWS Lambda function invoked through an API Gateway.

| **Model Type**       | **Role in Analysis**                                                                                                 | **Example**                                                                                              |
|-----------------------|---------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **Physical Model**    | Represents the infrastructure components supporting the API.                                                        | **Entities**: API Gateway, Lambda function, DynamoDB table. <br> **Attributes/Metadata**: Function name, runtime (Node.js). <br> **Metrics**: Lambda invocation time, API Gateway latency. |
| **Logical Model**     | Groups services based on environment or function.                                                                   | **Tags**: `environment:production`, `service:order-processing`.                                          |
| **Semantic Model**    | Maps the dependencies between the API Gateway, Lambda function, and DynamoDB database.                              | **Relationships**: API Gateway → Lambda Function → DynamoDB Table.                                       |
| **Behavioral Model**  | Establishes baselines for metrics like invocation duration and error rates.                                          | **Metrics**: Invocation duration, error rate, and request payload size.                                  |
| **Access Model**      | Tracks security configurations and access patterns.                                                                 | **Attributes**: IAM role policies, unauthorized API access attempts.                                     |

---

### Unified Workflow Example Using Lambda and API Gateway

#### Problem:

1. **Observations**:
   - High latency in API Gateway requests routed to the "Order Processing" Lambda function.
   - Lambda function logs show intermittent DynamoDB timeout errors.
   - API Gateway logs contain several 5XX errors.

2. **Impact**:
   - Slower order processing affects user satisfaction.
   - Missed API Gateway SLA thresholds.

---

#### Resolution:

1. **Physical Model**:
   - **Action**: Analyze Lambda invocation metrics.
   - **Example Query**:  
     ```dql
     fetch metrics
     | filter dt.entity.lambda_function == "order-processing-lambda"
     | summarize avg(metric.value) by dt.entity.name
     | fields dt.entity.name, avg.metric.value
     ```
   - **Outcome**: Identify prolonged Lambda execution duration.

2. **Logical Model**:
   - **Action**: Group functions by `environment:production` for targeted debugging.
   - **Example Query**:  
     ```dql
     fetch metrics
     | filter environment == "production"
     | summarize avg(metric.value) by service
     | fields service, avg.metric.value
     ```
   - **Outcome**: Pinpoint services with the most performance issues.

3. **Semantic Model**:
   - **Action**: Trace the API Gateway request lifecycle.
   - **Example Query**:  
     ```dql
     fetch traces
     | filter service.name == "API Gateway"
     | join fetch dt.entity.lambda_function on trace.contains == lambda_function
     | fields trace.id, lambda_function.name, trace.duration
     ```
   - **Outcome**: Visualize the API Gateway → Lambda → DynamoDB flow.

4. **Behavioral Model**:
   - **Action**: Compare invocation times to baseline metrics.
   - **Example Query**:  
     ```dql
     fetch metrics
     | filter dt.entity.lambda_function == "order-processing-lambda"
     | filter metric.key == "builtin:lambda.invocation.duration"
     | filter metric.value > baseline.value
     | fields timestamp, metric.value, baseline.value
     ```
   - **Outcome**: Detect anomalies in Lambda invocation durations.

5. **Access Model**:
   - **Action**: Audit IAM roles and permissions.
   - **Example Query**:  
     ```dql
     fetch events
     | filter event.type == "unauthorized_access"
     | fields entity.name, event.type, event.title
     ```
   - **Outcome**: Ensure no unauthorized API Gateway access.

---

### Key Takeaways

- **Models in Action**: The combination of models ensures comprehensive coverage of the issue, from infrastructure analysis to user access validation.
- **Unified Data Model**: All data types (metrics, logs, traces, relationships) are tied to entities like Lambda functions and API Gateway endpoints.
- **Business Impact**: Resolving latency in the order-processing workflow improves user satisfaction and meets SLA thresholds.


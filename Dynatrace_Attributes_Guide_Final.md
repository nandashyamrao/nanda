# **Understanding Attributes in Dynatrace**

---

## **What Are Attributes?**
In Dynatrace, **attributes** are the metadata and properties associated with monitored entities or ingested data. They provide detailed information about each entity or data type, allowing for precise filtering, querying, and analysis.

### **Key Points About Attributes:**
1. **Attributes Describe Entities**  
   Attributes give context to entities, such as a host's name, an application’s version, or a Lambda function’s memory size.

2. **Attributes Enable Filtering and Aggregation**  
   Attributes can be used in queries to filter or group data, making it easier to analyze specific subsets of your environment.

3. **Attributes Vary by Entity Type**  
   Different entity types (e.g., hosts, services, AWS resources) have unique attributes relevant to their context.

4. **Custom Attributes Extend Functionality**  
   Custom attributes (`dt.custom.*`) provide additional metadata that may not be part of Dynatrace’s default entity schema.

---

## **Types of Attributes**
Attributes in Dynatrace can be categorized into three main types:

### **1. Standard Attributes**
- **Definition**: Predefined attributes that come with Dynatrace entities or ingested data.
- **Examples**:
  - `host.name`: The name of a monitored host.
  - `aws.lambda.functionName`: The name of an AWS Lambda function.
  - `log.level`: The severity level of a log message (`INFO`, `ERROR`, etc.).

### **2. AWS-Specific Attributes**
- **Definition**: Attributes specific to AWS services and entities, such as EC2, S3, or Lambda.
- **Examples**:
  - `aws.ec2.instanceType`: The instance type of an EC2 instance (e.g., `t2.micro`).
  - `aws.s3.bucketName`: The name of an S3 bucket.
  - `aws.rds.engine`: The database engine type (e.g., MySQL, PostgreSQL).

### **3. Custom Attributes**
- **Definition**: User-defined or automatically collected metadata that extends Dynatrace’s default functionality. These attributes are typically prefixed with `dt.custom.*`.
- **Examples**:
  - `dt.custom.aws.lambda.invocations`: Represents the number of AWS Lambda invocations.
  - `dt.custom.aws.rds.backupRetentionPeriod`: Custom metadata for an RDS backup retention period.

---

## **Custom Attributes in Detail**
Custom attributes allow organizations to tailor Dynatrace’s monitoring capabilities to their specific needs. They are typically used to capture additional metadata about AWS services or custom applications.

### **Common Use Cases for Custom Attributes**
1. **Extending AWS Metadata**  
   Capture additional information not included in standard AWS attributes (e.g., Lambda timeout, RDS backup retention).

2. **Tracking Custom Metrics**  
   Use custom attributes to track business-relevant metrics like the number of API calls or application-specific tags.

3. **Filtering and Reporting**  
   Custom attributes can be used to filter or group entities based on extended metadata.

### **Example Table of Custom Attributes**
| **Custom Attribute**                     | **Description**                                 |
|------------------------------------------|------------------------------------------------|
| `dt.custom.aws.lambda.invocations`       | Number of invocations for an AWS Lambda function. |
| `dt.custom.aws.rds.backupRetentionPeriod`| Backup retention period for RDS instances.     |
| `dt.custom.aws.s3.storageClass`          | Storage class for an S3 bucket.                |
| `dt.custom.aws.ec2.tags`                 | Custom tags applied to EC2 instances.          |

---

## **How to Use Attributes in Queries**
Attributes are used in Dynatrace Query Language (DQL) to filter, group, or retrieve data. Here's how:

### **1. Filtering**
Attributes allow you to filter data for specific criteria.
```dql
fetch dt.entity.host
| fieldsAdd host.name, aws.ec2.instanceType
| filter aws.ec2.instanceType == "t2.micro"
```

### **2. Grouping**
You can group data by attributes to aggregate results.
```dql
fetch dt.entity.aws_s3_bucket
| fieldsAdd aws.s3.bucketName
| groupBy aws.s3.bucketName
```

### **3. Summarizing**
Attributes help calculate aggregates, such as counts or averages.
```dql
fetch dt.entity.aws_lambda_function
| fieldsAdd aws.lambda.functionName
| summarize count() by aws.lambda.functionName
```

---

## **How Attributes Are Structured**
Attributes in Dynatrace follow a hierarchical structure with **dot notation**, making it easy to identify and use them.  

### **Attribute Naming Examples:**
| **Attribute**                     | **Description**                                                  |
|------------------------------------|------------------------------------------------------------------|
| `host.name`                        | Name of the monitored host                                       |
| `aws.lambda.functionName`          | Name of the AWS Lambda function                                 |
| `kubernetes.namespace`             | Namespace of a Kubernetes resource                              |
| `log.message`                      | Message content in a log entry                                  |
| `dt.custom.aws.lambda.memorySize`  | Custom attribute for Lambda memory size                        |

---

## **Best Practices for Using Attributes**
1. **Understand the Entity Type**  
   Each entity type (e.g., `dt.entity.host`, `dt.entity.aws_lambda_function`) has unique attributes. Ensure you're familiar with the attributes available for your query.

2. **Leverage Filtering**  
   Use attributes to refine queries and focus only on the data you need. For example:
   ```dql
   fetch dt.entity.aws_lambda_function
   | fieldsAdd aws.lambda.functionName
   | filter aws.lambda.memorySize > 512
   ```

3. **Avoid Fetching Unnecessary Attributes**  
   Select only the attributes required for analysis to reduce query complexity and cost.

4. **Use Custom Attributes When Needed**  
   Extend default attributes with `dt.custom.*` for additional flexibility.

---

## **Examples of Attribute Usage in Queries**

### **Example 1: Query EC2 Instances**
List all EC2 instances and filter by instance type:
```dql
fetch dt.entity.host
| fieldsAdd host.name, aws.ec2.instanceId, aws.ec2.instanceType
| filter aws.ec2.instanceType == "t2.micro"
```

### **Example 2: Query S3 Buckets**
List S3 buckets with a specific storage class:
```dql
fetch dt.entity.aws_s3_bucket
| fieldsAdd aws.s3.bucketName, dt.custom.aws.s3.storageClass
| filter dt.custom.aws.s3.storageClass == "STANDARD"
```

### **Example 3: Query Logs by Log Level**
Filter logs with `ERROR` level:
```dql
fetch logs
| fieldsAdd log.level, log.message
| filter log.level == "ERROR"
```

---
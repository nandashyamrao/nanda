|   # | Model Type   | Entity Category               | Entity Type                 | Description                                   | Examples                         |
|----:|:-------------|:------------------------------|:----------------------------|:----------------------------------------------|:---------------------------------|
|  41 | Physical     | Database and Storage Entities | RELATIONAL_DATABASE_SERVICE | Managed relational databases.                 | AWS RDS, Azure SQL Database      |
|  42 | Physical     | Database and Storage Entities | DYNAMO_DB_TABLE             | Tables in DynamoDB for NoSQL databases.       | DynamoDB table                   |
|  43 | Physical     | Database and Storage Entities | EBS_VOLUME                  | Storage volumes attached to EC2 instances.    | Amazon Elastic Block Storage     |
|  44 | Physical     | Database and Storage Entities | CINDER_VOLUME               | Volumes in OpenStack storage systems.         | Cinder storage                   |
|  45 | Physical     | Database and Storage Entities | SWIFT_CONTAINER             | Object storage containers in OpenStack Swift. | OpenStack object storage buckets |
|  46 | Physical     | Database and Storage Entities | S3BUCKET                    | Object storage buckets in AWS.                | Amazon S3 buckets                |
|  47 | Physical     | Database and Storage Entities | DATASTORE                   | General-purpose data storage systems.         | Elasticsearch, Redis             |
|  48 | Physical     | Database and Storage Entities | QUEUE                       | Queues for messaging systems.                 | Kafka, RabbitMQ                  |
|  49 | Physical     | Database and Storage Entities | QUEUE_INSTANCE              | Specific instances of message queues.         | SQS queues, Kafka topics         |
|  50 | Physical     | Database and Storage Entities | DISK                        | Disks used in storage systems.                | Physical or virtual disks        |
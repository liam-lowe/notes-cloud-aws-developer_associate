# Kinesis

## Summary

AWS Kinesis is the AWS data streaming service, similar to Apache Kafka. Kinesis is a managed serivce which makes it easy to collect and analyze data and video streams in real time. It is considered a managed alternative to Apache Kafka.

- Kinesis maintains data streams.
- Streams are divided into shards (partitions)
- Data within a shard is ordered
- Multiple applications can consume the same stream
- Able to reprocess / replay data
- Data in Kinesis is immutable
- Data is automatically replicated to 3 AZs

### Summary - Shards

- A stream can contain one or more shards
- Write Capacity: 1MB/s or 1000 messages per secord per shard
- Read Capacity: 2MB/s per shard
- Billing is per shard
- Records are ordered per shard

### Summary - Components

- Kinesis Streams: Low latency streaming ingest at scale
- Kinesis Analytics: Real-time analytics on stream using SQL
- Kinesis Firehose: Load stream into S3, Redshift, Elastic, etc.

### Summary - Kinesis API

- PutRecord API: Requires a partition key which gets hashed
- Partition key should be highly distributed (otherwise a shard can become overwhelmed)
- PutRecord accepts batches - cost can be reduced
- PutRecord throw ProvisionedThroughputExceeded in case capacity is exceeded.
  - Exponential Backoff
  - More shards
  - Ensure partition key is highly distributed

### Summary - Kinesis Client Library (KCL)

- It is a Java library
- Each shard should be read by only one KCL instance
- Progress checkpoint is written to DynamoDB
- Records are read in order at the shard level

### Summary - Kinesis Data Analytics

- Read-time analytics on Kinesis Streams using SQL
- Pay for actual consumption - no need to pre-provision anything
- Can create stream from query results

### Summary - Kinesis Firehose

- Used for ETL, can load data into Redshift, S3, ElasticSearch
- Fully managed, automatic scaling
- Low Latency (60 seconds)
- Pay for the amount of data that goes through Firehose

## Security

- IAM policies
- Encryption at flight using HTTPS
- Encryption at rest using KMS
- Client side encryption / decryption (should be done manually)
- VPC endpoints available

## Use Case

- Great for application logs, metrics, IoT, clickstreams
- Real time big data
- Streaming processing neworks (Spark, Nifi, etc. )

## Cost

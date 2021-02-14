# RDS - Relational Database Service

## Summary

AWS Relational Database Service (RDS) is an AWS-managed SQL database service.

It allows for the creation of the following SQL databases:

- Postgres
- Oracle
- MySQL
- MariaDB
- Microsoft SQL Server
- Aurora

## Features

### Feature - RDS Read Replicas

#### RDS Read Replicas - Summary

- Up to 5 read replicas
- Can be within same AZ, cross AZ, cross region
- Replication is async
- Reads are eventually consistent
- Replicas can be promoted to their own DB
- Applications must update the connection string to leverage read replicas
- Read replicas can only be used for SELECT statements (not INSERT, UPDATE, DELETE)

#### RDS Read Replicas - Network Cost

- There's a network cost when data goes from one AZ to another

### Feature - RDS Multi AZ

#### RDS Multi AZ - Summary

- RDS Multi AZ is to be used for Distaster Recovery (DR)
- Sync Replication
- Shares one DNS name, automatic app failover
- Increases availability
- Failover in case of loss of AZ, loss of network, instance or storage failure
- Not to be used for scaling, only DR


### Feature - RDS Backups

#### RDS Backups - Summary

- Automated Backups
  - Automatic
  - Enabled by default
  - Daily full snapshot of the DB
  - Capture transaction logs in realtime
  - The ability to restore to any point in time
  - 7 day default retention (max 35 days)
- Snapshots
  - Manually triggered by the user
  - No limits on retention

### Feature - RDS Encryption

#### RDS Encryption - Summary

- Both encryption-at-rest and in-flight encryption
- Encryption-at-rest using AWS KMS - AES-256 encryption
- SSL certificates to encrypt data to RDS in-flight
- To enforce SSL is db specific
- To connect using SSL, provide SSL trust certificate and provide SSL connection options to the DB

#### RDS Encryption - Operations

- Encrypting RDS Backups
  - Snapshots of unencrypted RDS databases and also unencrypted
  - Snapshots of encrypted RDS databases are also encrypted
  - Can encrypt an unencrypted DB
- To encrypt and unencrypted RDS DB
  - Create a snapshot of unencrypted DB
  - Copy the snapshot and enable encryption for the snapshot
  - Restore the DB from encrypted snapshot
  - Migrate applications to the new DB, and delete the old database

### Feature - RDS Security

#### RDS Security - Summary

- RDS instances are typically deployed into a private subnet
- RDS security leverages Security Groups (SG), controlling who can access the RDS instance
- IAM policies control who can manage RDS
- Traditional DB login is used for logging into the DB
- IAM users can be used for logging into DB (MySQL, Aurora)
  
## Advantages

- AWS managed service
- Managed OS patching
- Continuous backups
- Point in time restore
- Monitoring dashboards
- Read replicas
- Multi AZ setup for DR
- Maintenance windows for upgrades
- Horizontal and vertical scaling

## Disadvantages

- Can't SSH into EC2 images
- Operating costs more expensive than self-managed

## Security

- Provides encryption-at-rest using KMS
- Provides in-flight encryption using SSL certificates

## Use Case

## Cost

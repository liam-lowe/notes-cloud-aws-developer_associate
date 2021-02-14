# Aurora

## Summary

Aurora is a managed database service provided by AWS, similar to RDS. Aurora is a closed-source proproetary database optimized for cloud distribution and workloads. Aurora Serverless in a an automated capacity-planned instance of Aurora.

## Features

### Feature - Driver Support

AWS Aurora has driver support for both Postgres and MySQL databases, enabling drivers to work as if Aurora was a postgres or MySQL database.

### Feature - Performance

Aurora is cloud-optimized, claiming 5x performance over MySQL on RDS and 3x performance of Postgres on RDS.
An Aurora cluster has a writer endpoing which points directly to the master, and a reader endpoint which does read replica load balancing.

### Feature - Storage

Aurora features automated storage resizing, adjusting in increments of 10GB, up to 64TB.

### Feature - Read Replicaas

Aurora can have 15 read replicas, compared to MySQL's 5.
Faster replication process than MySQL (sub 10ms replica lag).

### Feature - Global Aurora

Aurora has cross-region read-replicas:

- Useful in disaster recovery
- Easy to put into place

Aurora has a global database option (recommended):

- 1 Primary region (read / write)
- Up to 5 secondary read-only regions
- Cross-region replication lag is less than 1 second
- Up to 16 read replicas per region
- Helps to decrease latency
- Promoting another region (for disaster recorvery) has an RTO of under 1 minute

### Feature - Aurora Serverless

Aurora has a serverless offering allowing automated database instantiation and auto-scaling based on actual usage.
Good for infrequent, intermitent, or unpredictable workloads as no capacity planning is needed.

Cost is per-second, has the potential to be more cost-effective for the right workload.

### Feature - Disaster Recovery

Aurora failover is instantaneous
Aurora is HA native
Support for cross-region replication

## Security

Aurora has similar security to RDS as it uses the same engines.
Employs encryption-at-rest using KMS.
Automated backups, snapshots, and replicas are encrypted.
Encryption in-flight using SSL (same as MySQL or Postgres).
Possible to authenticate using an IAM token (same as RDS).
You are responsible for protecting the instance with security groups.
You can't SSH.

## Use Case

## Cost

- Costs 20% more than RDS, but is more cost-efficient

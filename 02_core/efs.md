# EFS - Elastic File Storage

## Summary

Elastic File Storage (EFS) is a managed Network File System (NFS) that can be mounted on many EC2 instances across many AZs.

- EFS is highly availbale, scalable, and expensive.
- Uses NFS v4.1 protocol
- Uses security groups to control access to EFS
- Compatible with Linux based AMIs
- Encryption at rest using KMS
- File system scales with use - no capacity planning

### Summary - EFS scale

- 1000s on concurrent NFS clients
- 10GB+/s throughput
- Grow to petabyte scale network file system, automatically

### Summary - Performance Mode

- Set at EFS creation time
- General Purpose: Default. Latency sensitive use cases
- Max I/O: Higher latency, throughput, parallel

### Summary - Storage Tiers

Standard: For frequently accessed files
Infrequently Accesses: IFA. Cost to rerieve files, lower price to store.

## Security

- Encryption at rest using KMS

## Use Case

- Content management
- Web Serving
- Data Sharing
- Wordpress

### Use Case - EBS vs EFS

EBS Volumes:

- can be attached to only one instance at a time
- are locked at the AZ level

EFS:

- mounts 100s of instances across AZs
- only available for linux
- more expensive

## Cost

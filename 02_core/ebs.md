# EBS - Elastic Block Storage

## Summary

Elastic Block Storage (EBS) are AWS netowrked attached storage drives.

EBS volumes are used for persistent data for EC2 machines. EC2 insances lose their root volume when it is terminated, and unexpected terminations can happen. An EBS Volume is a network drive that you can attach to your instances while they run. It allows for your instances to persist data.

An EBS volume:

- Is a network drive (not a physical drive)
  - It uses network latency to communicate to the instance, which means there might be a bit of latency.
  - It can be detached from an EC2 instance and attached to another one very quickly
- It is locked to an Availability Zone
  - An EBS Volume in ap-southeast-2a cannot be attached to an EC2 in ap-southeast-2b
  - To move a volume across, you need to snapshot it
- Has a provisioned capacity in GBs and in IOPs
  - You get billed for all provisioned capacity
  - You can increase the capacity of the drive over time
- Can only be attached to one instance at a time
- Root EBS volumes of instances get terminated by default if the EC2 instance gets disabled

### Summary - EBS Volume Types

EBS volumes come in 4 types:

- GP2 (SSD): *General Purpose* SSD volume that balances price and performance for a wide variety of workloads
- IO1 (SSD): *Input Output* optimized SSD. Highest performance SSD volume for mission-critical low-latency or high-throughput loads.
- ST1 (HDD): *Streaming* optimized HDD. Low cost HDD volume designed for frequently accessed, throughput intensive workloads
- SC1 (HDD): *Save Cost* optimized HDD. Lowest cost HDD volume designed for less frequently accessed workloads.

EBS volumes are characterized in size, throughput, and IOPS.

Only GP2 and IO1 can be used as boot volumes.

#### Summary - EBS Volume Types - GP2 - Use Cases

- Recommended for most workloads
- System boot volumes
- Virtual desktops
- Low-latency interactive apps
- Development and test environments

#### Summary - EBS Volume Types - IO1 - Use Cases

- Critical business applications that require sustained IOPS performance, or more than 16,000 IOPS per volume (gp2 limit)
- Large database workloads, such as: MongoDB, Cassandra, Oracle, Postgres

#### Summary - EBS Volume Types - ST1 - Use Cases

- Streaming workloads requiring consistent, fast throughput, at a low price
- Big data, data warehousing, log processing
- Apache Kafka
- Cannot be a boot volume

#### Summary - EBS Volume Types - SC1 - Use Cases

- Throughput-oriented storage for large volumes that is infrequently accessed
- Scenarios where lowest storage cost is important
- Cannot be a boot volume

### Summary - EBS Volume Resizing

You can resize your EBS volumes - after resizing, you need to repartition your drive.

### Summary - EBS Snapshots

EBS volumes can be backed up using snapshots. Snapshots only take the actual space of the blocks on the volume. Eg - if you snapshot 5gb of data on a 100gb volume, then your EBS Snapshit will only be 5GB.

Snapshots are used for:

- Backups: ensuring you can save data in case of an emergency
- Volume Migration:
  - Resizing a volume down
  - Changing the volume type
  - Encrypting a volume

EBS Snapshots use IO and shouldnt run while your application is handling a lot of traffic.

### Summary - EBS Snapshots - Encryption

When you create an encrypted EBS volume, you get the following

- Data at rest is encrypted inside the volume
- All the data in-flight between the instance and volume is encrypted
- All snapshots are encrypted
- All volumes created from the snapshot are encrypted

Encryption and decryption are handled transparently - there is nothing for you to do.

Encryption has a minimal impact on latency.

Encryption manages keys from KMS

Copying an unencrypted volume allows for encryption.

## Security

## Use Case

### Use Case - EBS vs Instance Store

Some instances do not come with a root EBS volume, instead they come with an instance store. Instance stores are physically attached to the machine.

Pros of Instance Store:

- Better I/O performance

Cons of Instance Store:

- On termination, the instance store is lost
- You can't resize the instance store
- Backups must be operated by the user

Overall, EBS-backed instances should fit most workloads

## Cost

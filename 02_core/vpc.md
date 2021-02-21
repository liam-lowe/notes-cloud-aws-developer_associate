# VPC - Virtual Private Cloud

## Summary

A VPC is a virtual private cloud.

Within a region, you're able to create VPCs. Each VPC contains subnets (networks). Each subnet is mapped to an AZ.

It is common to have a public IP and private IP subnet. It's common to have many subnets per AZ.

Public subnets usually contain:

- Load balancers
- Static websites
- Files
- Public Authentication Layers

Private Subnets usually contain:

- Web application servers
- Databases

Public and Private subnets can communicate if they're in the same VPC.

All new accounts come with a default VPC.

It's possible to use a VPN to connect to a VPC.

VPC flow logs allow you to monitor the traffic within, in, and out of your VPC. Usefulf for security, audit, performance.

VPC are per account per region. Subnets are per VPC per AZ.

Some AWS resources can be deployed in a VPC, while others can't.

You can peer VPC - within or across account - to make it look like they're part of the same network.

### Summary - Definitions

*VPC*: private network to deploy your resources

*Subnets*: Allow you to partition your network inside your VPC

*Public Subnet*: Is a subnet accessible from the internet

*Private Subnet*: Is a subnet not accessible from the internet

To define access to the internet and between subnets, we use *route tables*.

*Internet Gateways* help our VPC instances connect with the internet. Public Subnets have a route to the internet gateway.

*NAT gateways* (AWS Managed) and *NAT Instances* (self-managed) allow instances in your private instances in your private subnets to access the internet while remaining private.

### Summary - Network Access Control List / Network ACL / NACL

#### Network ACL

- A firewall which controls traffic to and from a subnet
- Can have ALLOW and DENY rules
- Are attached at the subnet level
- Rules only include IP addresses
- Operates at the subnet level
- Supports ALLOW and DENY rules
- Is stateless, return traffic must be explicitly allowed by rules
- We process rules in order when determining whether to allow traffic
- Automatically applies to all instances in the subnets it's associated with

#### Security Groups

- A firewall that controls traffic to and from an ENI / an EC2 instance
- Can only have allow rules
- Rules include IP addresses and other security groups
- Operates at the instance level
- Supports ALLOW rules only
- Is Stateful: Return traffic is automatically allowed regardless of any rules
- We evaluate all rules, before deciding whether to allow all traffic
- Applies to an instance only if someone specifies the security group when laucnhing the instance

### Summary - VPC Flow Logs

Capture information about traffic going into your interfaces

- VPC Flow Logs
- Subnet Flow Logs
- ENI Flow Logs

Helps to monitor and troubleshoot connectivity issues

- Subnets to Subnets
- Subnets to Internet
- Internet to Subnet

Captures information from AWS Managed Interfaces too:

- ELB
- ElastiCache
- RDS
- Aurora

VPC Flow Logs can go into S3 / CloudWatch

### Summary - VPC Peering

Connect any two VPCs privately, using AWS' internal network.

Make them behave as if they were using the same network

Must not have an overlapping CIDR (IP address range)

VPC Peering connection is not transitive. It must be established for each VPC that needs to communicate with eachother.

### Summary - VPC Endpoints

Endpoints allow you to connect to AAWS Services using a private network instead of the public www network

This gives you enhanced security, and lower latency to all AWS Services.

VPC Endpoint Gateway: S3 and DynamoDB

VPC Endpoint Interface: The rest

Only used within your VPC.

### Summary - Site to Site VPN and Direct Connect

#### Site To Site VPN

- Connect an on premise VPN to AWS
- The connection is automatically encrypted
- Goes over the public internet

#### Direct Connect (DX)

- Establishes a physical connection between on-premise and AWS.
- The connection is private, secure and fast
- Goes over a private network
- Takes at least a month to establish

Note: Site To Site and DX cannot access VPC endpoints

## Security

## Use Case

## Cost

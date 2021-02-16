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

## Security

## Use Case

## Cost

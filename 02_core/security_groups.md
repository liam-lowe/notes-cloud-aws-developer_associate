# Security Groups

## Summary

The fundamental of network security in AWS

- Can be attached to multiple instances
- Locked down to a region & VPC configuration
- Lives outside the EC2, if traffic is blocked, the EC2 instance won't see it
- It's good to maintain one separate security group for SSH access
- If your application is not accessible (timeout), then it's usually a security group issue
- If your application gives a "connection refused" error, then it's an application error or it's not launched
- All inbound traffic is blocked by default
- All outbound traffic in authorized by default

Security Groups act as a firewall on EC2 instances

They regulate:

- Access to ports
- Authorized IP ranges - IPv4 and IPv6
- Control of inbound network
- Control of outbound network

## Security

## Use Case

## Cost

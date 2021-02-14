# ASG - AutoScaling Group

## Summary

Auto-scaling groups are a series of rules for defining how our application's underlying servers should scale In real life, the load on websites an applications can change, ASGs allow for the scaling up and down of servers very quickly. The goal of an Auto Scaling Group (ASG) is to:

- Scale out (add EC2 instances) to match an increased load
- Scale in (remove EC2 instances) to match a decreased load
- Ensure we have a minimum and maximum number of machines running
- Automatically register new instances to a load balancer

ASGs have the following attributes:

- A launch configuration
  - AMI
  - Instance Type
  - EC2 User Data
  - EBS Volume
  - Security Group
  - SSH Key Pair
- Min Size / Max Size / Initial Capacity
- Network and Subnet information
- Load Balancer information
- Scaling policies

ASGs use launch configurations and you update an ASG by providing a new launch configuration.

IAM roles attached to an ASG will get assigned to new EC2 instances.

Having instances under an ASG means if they get terminated for whatever reason, the ASG will restart them.

ASG can terminate instances marked by the load balancer as unhealthy (and thus restart them).

### Summary - Scaling

ASGs use scaling policies to determine whether to scale the size of the EC2 cluster. They can be be based on CPU, Network, custom metrics, or a custom schedule.

#### Summary - Scaling Policies - Auto Scaling Alarms

It is possible to create an ASG based on CloudWatch alarms.

An alarm monitors a metric (such as average CPU). Metrics are computed as a total of all ASG instances.

Based on the alarm, we can scale out (increase EC2 instances), or scale in (decrease EC2 instances).

#### Summary - Scaling Policies - New Auto Scaling Rules

There are now more advanced auto scaling policies that are directly managed by EC2.

Examples:

- Target Average CPU Usage
- Number of requests on the ELB per instance
- Average network in
- Average network out

These rules are easier to set up, and can make more sense.

#### Summary - Scaling Policies - Auto Scaling Custom Metric

We can auto scale based on a custom published metric.

1. Send custom metric from an application on EC2 to cloudwatch (PutMetric API)
2. Create a Cloudwatch Alarm to react to low / high values
3. Use the Cloudwatch Alarm as the scaling policy for the ASG

## Security

## Use Case

## Cost

ASGs are free, you pay for the underlying EC2 instances.

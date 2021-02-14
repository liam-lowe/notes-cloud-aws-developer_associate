# EC2 - Elastic Compute Cloud

## Summary

EC2 or Elastic Compute Cloud is the AWS compute offering.

By default EC2s come with:

- A private IP for the internal AWS network
- A public IP for the WWW
  - To SSH into your EC2 machine, you must use the private IP, we can't use a private IP because we are not in the same network
  - If the machine is stopeed and restarted, the public IP will change

### Summary - Instance Types

There are multiple characterists for the different types of EC2 instance types:

- RAM (type / amount / generation)
- CPU (type / make / frequency / generation / cores)
- I/O (disk performance / EBS optimisations)
- Network (network bandwidth / network latency)
- GPU

There are over 50 instance types..

M - Balanced

T2 / T3 - Burtsable

#### Summary - Instance Types - Burst

AWS has a concept of burstable instances. Burst means that overall the instance has reasonable performance. When the machine needs to process something un expected, it can burst, and the CPU can be very good.

When the machine bursts it uses burst credits. If all the credits are gone, the EC2 CPU is not that great. When the machine stops bursting, burst credits are accumulated over time.

Burst instances are useful to handle unexpected traffic. If you are consistenly low on burst credits, you should probably upgrade instance size.

There is also an unlimited burst instance called T2 unlimited where you have unlimited burst balance - you pay more if you go over your credit balance, but you won't lose in performance.

### Summary - Instance Launch Types

There are many types of instance launch types:

#### Summary - Instance Launch Types - On Demand

- Instance is available when needed, charged by the second. Short workload, predictable pricing.
- Pay for what you use
- Has the highest cost, but no upfront payment
- No long term commitment
- Recommended for short-term and un-interrupted workloads where you can't predict how an application will behave

#### Summary - Instance Launch Types - Reserved Instances

- Long workloads >= 1 year
- Reservation periods of 1 or 3 years
- Up to 75% off compared to on-demand
- Pay upfront for what you use, with long term commitment
- Reserves a specific instance type
- Recommended for steady state usage applications (such as databases)

#### Summary - Instance Launch Types - Convertible Reserved Instances

- Long workloads with flexible instance sizes
- Reserved instances where you can change the instance type
- Up to 54% discount compared to On Demand instances

#### Summary - Instance Launch Types - Scheduled Reserved Instances

- Launches within a time window that you reserve
- Reserved instances available on a schedule
- Useful when you require consistent availability of a day / week / month

#### Summary - Instance Launch Types - Spot Instances

- Bid on instance pricing, super cheap, but can lose instances if your bid is less than the current spot price
- Up to 90% discount when compared to On-Demand
- You bid a price and get the instance as long as it's under that specified price
- Price varies based on offer and demand
- Spot instances are reclaimed with a 2 minutes notification warning when the spot price goes above your bid
- Used for batch jobs, big data analysis, or workloads resilient to failure
- Not great for critical jobs or databases

#### Summary - Instance Launch Types - Dedicated Instances

- No other customers will share your hardware
- Instances running on hardware that's dedicated to you
- May share hardware with other instances in the same account
- No control over instance placement (can move hardware after a start / stop)

#### Summary - Instance Launch Types - Dedicated Hosts

- Reserves and entire physical server, control instance placement
- Physical EC2 Server for your use
- Full control over EC2 instance placement
- Visibility into underlying sockets / physical cores of the hardware
- Allocated for your account for a 3 year reservation
- More expensive
- Useful for software that has a complicated licensing model
- Useful for companies with strong regulatory or compliance needs

### Summary - User Data

EC2 user data is the user data that is run on instance startup.

It is the bootstrapping of our instances using an EC2 user data script. Bootstrapping means running commands on instance startup - it is only run once at the instance first start, and not again upon successive restarts.

EC2 user data is used for automated boot tasks such as:

- Installing updates
- Installing software
- Downloading common files from the internet

The EC2 User Data script runs as the root user.

### Summary - Meta Data

EC2 Meta Data is information about your EC2 instance. It allows instances to learn about themselves without having to use an IAM role for that purpose.

You can retrieve IAM roles from EC2 MetaData but you cannot retrieve IAM policies.

The URL to hit EC2 Metadata is: `{EC2-IP-ADDRESS}/latest/meta-data`

### Summary - AMI - Amazon Machine Image

An AMI is a custom buit launch image.

By default AWS provides many base images:

- Ubuntu
- Fedora
- Amazon Linux
- RedHat
- Windows

These base images can be customized at launch time using user data. AMIs are base images with customised launch data ready to go.

Using an AMI provides the following advantages:

- Pre-installed packages
- Faster boot time (no need for EC2 user data)
- More monitoring control
- More security control
- Control over maintenance
- Install your app ahead of time (useful for auto scaling)
- Use someone else's AMI that's optimized for running a specific app

## Security

## Use Case

## Cost

EC2 instance price varies based on the following parameters:

- The region the instance is in
- Instance type being used
- Instance Launch Type (On Demand / Spot / Reserved)
- Instance OS (Linux / Windows / RHEL / Amazon Linux)

You are billed by the second.

There is a minimum billing time per instance of 60 seconds.

You also pay for other factors such as storage, data transfer, fixed IPs, load balancing

You do not pay for the instance while the instance is stopped.

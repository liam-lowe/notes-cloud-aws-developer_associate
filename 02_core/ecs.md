# ECS - Elastic Container Service

## Summary

ECS Clusters are a logical group of EC2 instances.

EC2 instances run the ECS agent (Docker container).

The ECS agent registers the instance to the ECS cluster.

The EC2 instances run a special AMI made for ECS.

ECS integrates with CloudWatch logs.

- You need to set up logging at the task definition level.
- Each container will have a different log stream.
- The EC2 instance profile needs to have the correct permissions.

### Summary - What is Docker

Docker is software to deploy containerised applications. Containers are packaged apps that can be run on any OS.

Apps run the same regardless of where they're run:

- Any machine
- No compatibility issues
- Predictable behavious
- Less Work
- Easier to maintain and deploy
- Works with any language, any OS, any technology

Docker images are stored in Docker repositories

- Public: DockerHub
- Private: Amazon ECR

### Summary - Docker vs Virtual Machine

Docker containers share resources with the host.

Virtual machines run on the hypervisor.

Docker containers run on a Docker daemon.

### Summary - Docker Container Management

To manage containers we need a container management platform.

- ECS - AWS own solution - Provision EC2 instances to run containers into
- Fargate - Serverless
- EKS - AWS managed kubernetes

### Summary - ECS Task Definitions

Tasks definitions are metadata in JSON form to tell ECS how to run a docker container.

It provides crucial information such as:

- Image now
- Port binding for container and host
- Memory and CPU requirements
- Environment variables
- Networking information
- IAM roles
- Logging information

### Summary - ECS Service

The ECS Service helps define how many tasks should run, and how they should be run

They ensure that the number of tasks desired is running across all of our EC2 instance.

They can be linked ELB if needed.

### Summary - ECS Service Auto Scaling

Not to be confused with EC2 auto scaling (instance level).

CPU and Ram is tracked in CloudWatch at the ECS service level.

- Target Tracking: target a specific average CloudWatch metric
- Step Scaling: Scaling based on CloudWatch alarms.
- Scheduled Scaling: Based on predictable changes

### Summary - Cluster Capacity Provider

A capacity provider is used in association with a cluster to determine the infrastructure that a task runs on.

For ECS Fargate users, the FARGATE and FARGATE_SPOT capacity providers are added automatically.

For ECS EC2 you need to manually associate tge capacity provider with the auto-scaling group.

When you run a task or a service, you need to define a capacity provider strategy to prioritze in which provider to run.

This allows the capacity provider to automatically provision infrastructure for you.

### Summary - ECS Classic

EC2 instances must be created.

We must configure the file `/etc/ecs/ecs.config` with the cluster name.

The EC2 instance must run an ECS agent.

EC2 instances can run multiple containers of the same type.

You must not specify a host port, only container port.

You should use an ALB with dynamic host mapping.

The EC2 instance security group must allow traffic from the ALB on all ports.

ECS tasks can have IAM roles to execute actions against AWS.

Security groups operate at the instance level, not the task level.

### Summary - Fargate

When launching an ECS cluster, we have to launch the underlying EC2 instances. If we need to scale, we add EC2 instances.

With Fargate, it's serverless.

We don't provision EC2 instances, we just create task defintions, and AWS will run our containers for us.

To scale, just modify the number of tasks.

### Summary - ECS Task Placement

When a task of type EC2 is launched, ECS must determine where to place it. Placement is affected by constraints of CPU, memory, and available port.

Similarly, when a service scales down, ECS needs to determins which task to terminate.

To assist with this, you can define a task placement strategy, and task placement constraints.

Note: This is only for ECS with EC2 - not with Fargate.

### Summary - ECS Task Placement Process

Task placement strategies are a best effort.

When AWS ECS places tasks, it uses the following process to select container instances.

1. Identify the instances that satisfy the CPU, memory, and port requirements in the task definition.
2. Identify the instances that satisfy the Task Placement Constraints
3. Identify the instances that satisfy the Taask Placement Strategies
4. Select the instances for task placement

### Summary - ECS Task Placement Strategies

The ECS Task Placement strategies can be mixed.

#### Summary - ECS Task Placement Strategies - Binpack

Places tasks based on least amount of available amount of CPU or memory. This minimizes the amount of instances in use (cost saving)

#### Summary - ECS Task Placement Strategies - Random

Places the tasks randomly.

#### Summary - ECS Task Placement Strategies - Spread

Spreads the tasks based on the specified value.

### Summary - ECS Task Placement Constraints

- distinctInstance: place each task on a different instance
- memberOf: places each task on instances that meet some expression

## Security

### Security - IAM Roles

Two types of IAM roles are used by ECS:

- EC2 Instance Profile: The IAM role used by the ECS agent, makes API calls to ECS service, pulls image from ECR, publishes logs to CloudWatch
- ECS Task Role: The IAM tole used by the specifc ECS task. Allows each task to have a specific role. Task role is defined in task definition.

## Use Case

## Cost

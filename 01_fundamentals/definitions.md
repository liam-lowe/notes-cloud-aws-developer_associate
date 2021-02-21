# Definitions

## Summary

Just some basic definitions related to all services.

### Scalability

Scalability means that an application can handle greater load by adapting.

There are two types of scalability:

#### Vertical Scalability

Vertical scalability means increasing the size of the instance. For example your application runs on a t2 micro - scaling that application means running it on a t2 large. Vertical scalability is very common for non distributed systems, such as a database. RDS and ElastiCache are services that can scale vertically. There's generally a limit to how much you can scale (hardware limit).

#### Horizontal Scalability

Horizontal scalability means increasing the number of instances / systems for your application. Horizontal scaling implies distributed systems. This is very common for web applications / modern applications. It's easy to scale horizontally thanks to cloud offerings such as Amazon EC2.

### High Availability

High availability goes hand-in-hand with horizontal scaling. High availability means running your application / system in at least 2 data centers / availability zones.  The goal of high availability is to ensure stability and availability during a data center loss. Horizontal scaling can be passive (like AWS RDS multi AZ) or active, like horizontal scaling.

#### High availability and Scalability for EC2

- Vertical Scaling increases instance size (scaling up or down)
- Horizontal scaling increases number of instances (scale in or out)
- High Availalbility: Run instances for the same application across multiple AZs

## Security

## Use Case

## Cost

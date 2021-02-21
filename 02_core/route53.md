# Route53

## Summary

Route53 is a managed DND (Domain Name System).

DNS is a collection of rules and records which inidcates to a client how to reach a specific server.

In AWS, the most common records are:

- A: URL to IPv4
- AAAA: URL to IPv6
- CNAME: URL to URL
- ALIAS: URL to AWS Resource

Aliases are preferred for AWS resources due to internal routing and performance improvements.
  
Route53 can use:

- Public domain names you own
- Private domain names that resolved by instances in your VPC

Route 53 has advanced features such as:

- Load balancing (through DNS - also called client load balancing)
- Health Checks
- Routing Policy

### Summary - Routing Policy

#### Summary Routing Policy - Simple

- Maps a hostname to another hostname.
- Use when you want to redirect to a single resource
- You can't attach health checks to a simple routing policy
- If multiple values are returned, one is chosen at random by the client

#### Summary Routing Policy - Failover

- Provides a failover server

#### Summary Routing Policy - Geolocation

- Routing policy based on user location
- Here we specify traffic from Region X should go to IP Y
- Should create a default policy

#### Summary Routing Policy - Geoproximity

- Maps to whichever AZ is physically closest to the user

#### Summary Routing Policy - Latency

- Redirect to the server with the least latency, with respect to the client
- Super heplful when latency of users is a priority
- Latency is evaluated in terms of user to designated AWS region.
- Germany may be routed to the US, if that's the lowest latency

#### Summary Routing Policy - Weighted

- Controls the % of the requests that go to a speficic endpoint
- Helpful to test 1% of traffic on a new app version for example
- Helpful to split traffic between two regions
- Can be associated with health checks

### Summary - Health Checks

- Have X health checks failed => unhealthy (default 3)
- Have X health checks passed => healthy (deefault 3)
- Default Health Check interval: 30 seconds (can be set to 10 seconds, higher cost)
- About 15 Health Checkers will check the endpoint, therefore one request every 2 seconds average
- Cab have HTTP, TCP, and HTTPS health checks (no SSL verification)
- Possibility of integrating health checks with CloudWatch
- Health Checks can be linked to Route53 DNS queries

### Summary - Route53 as a registrar

- A domain name registrar is an organization that manages the reservation of the Internet Domain Names
- Think GoDaddy, Google Domains, Etc
- Route53 is also a Domain Registrar.
- A Domain Registrar is not a DNS
- If you buy a domain from an external Domain Registrar, you can still use DNS - create a Hosted Zone in R53 and update NS records on 3rd party website to you Route53 Name Space.

## Security

## Use Case

## Cost

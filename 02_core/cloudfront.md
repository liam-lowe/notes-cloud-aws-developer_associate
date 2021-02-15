# CloudFront

## Summary

CloudFront is the AWS Content Delivery Network (CDN).

It improves read performance of data through caching it at edge locations. There are currently 216 edge locations.

CloudFront:

- Provides DDos Protection
- Has ntegration with Shield
- AWS Web Application Firewalls
- Can expose external HTTPS and can talk to internal HTTPS backends

At a high level, a user hits a CloudFront endpoint. If the requested object is available at the edge location, it is returned, otherwise it is fetched from the origin and cached at the edge location for future retrievals.

### Summary - Origin

CloudFront data can be originated from:

- S3 Buckets
- Custom Origin (HTTP)

#### Summary - Origin - S3 Bucket

Used for distributing files and caching them at the edge.

Provides enhanced security through CloudFront Origin Access Identity (OAI).

CloudFront can be used as an ingress to upload files to S3

#### Summary - Origin - Custom Origin (HTTP)

- Application Load Balancer
- EC2 Instance
- S3 Website
- Any HTTP backend that you want

### Summary - Restriction

#### Summary - Restriction - Geo Restriction

You can restrict who can access your deistribution with Geo restriction.

Geo restriction allows you to whitelist or blacklist content from users if their IP is from a specified list of countries.

*Whitelist:* Allow your users to access your content only if they're on the list of countries.

*Blacklist:* Disallow your users to access your content only if they're on the list of countries.

The country is determined using a third party GEO-IP database.

### Summary - Caching

CloudFront allows caching based on:

- Headers
- Session Cookies
- Query String Parameters

The cache lives at each CloudFront edge location.

You want to maximize the cache hit rate to minimize requests on the origin.

Control the TTL (up to 1 year), can be set by the origin using the Cache-Control Header or Expires header.

You can invalidate part of the cache using the CreateInvalidation API.

A good way to maximize hits is to separate static and dynamic distributions.

## Security

### Security - Protocols

CloudFront has 2 security protocols:

- Viewer Protocol Policy: The protocol between the Client and Edge Location
  - Redirect HTTP to HTTPS
  - Or use HTTPS only
- Origin Protocol Policy: Between Edge Location and Origin
  - HTTPS ony
  - Match Viewer (HTTP -> HTTP and HTTPS -> HTTPS)

Note: S3 bucket websites don't support HTTPS.

### Security Signed URL / Signed Cookies

To restrict viewer access, we can provide signed URLs and Signed cookies to our content.

These are timed, and make the content available for a certain period of time.

*Signed URL:* Access to individual fiels (one signed URL per file)

*Signed Cookies:* Access to multiple files.

## Use Case

### Use Case - CloudFront vs S3 Cross Region Replication

CloudFront:

- Global edge network
- Files are cached for a TTL
- Great for static content that must be available everywhere

S3 Cross Region Replication:

- Must be set up for each region where you want replication to happen
- Files are updated in near real time
- Read only
- Great for dynamic content that needs to be available at low-latency in a few regions

### Use Case CloudFront Signed URL vs S3 Signed URL

CloudFront Signed URL:

- Allows access to a path, no matter the origin
- Account wide key-pair, only the root can manage it
- Can leverage caching features

S3 Pre-Signed URL:

- Issue a request as the person with the presigned URL
- Uses the IAM key of the signed IAM principal
- Limited lifetime

## Cost

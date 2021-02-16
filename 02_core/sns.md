# SNS - Simple Notification Service

## Summary

Simple Notifcation System (SNS) is a fully managed messaging servide for both application-to-application (A2A) and application-to-person (A2P) communication.

The event producer sends the message to one SNS topic.

Many event receivers can listen to an SNS topic

Limits:

- 10,000,000 subscriptions per topic
- 100,000 topics

Subscriber types:

- SQS
- HTTP / HTTPS
- Lambda
- Emails
- Mobile Notifications
- SMS

SNS integrates with most AWS services:

- AWS services can send data directly to SNS for generating notifcations
  - CloudWatch (for alarms)
  - Auto Scaling Groups
  - S3 Buckets (for events)
  - CloudFormation (for state changes)

### Summary - How to publish a topic

- Simple
  - Create a topic
  - Create a subscription
  - Publish to the topic
- Publish directly from an application
  - Create an endpoint in your application
  - Publish to the platform endpoint
  - This works with:
    - Google GCM
    - Apple APNS
    - Amazon ADM

## Security

Encryption:

- In-flight encryption using HTTPS
- At-rest encryption using KMS keys
- Client-side encryption if the client wants to perform encryption / decryption themselves

Access Controls:

- IAM policies to regulate access to the SNS API

SNS Access Policies:

- Useful for multiple account access to SNS topics
- Useful for allowing other services to write to an SNS topic

## Use Case

### Use Case - SNS + SQS Fan Out

- Push once in SNS, receive in all SQS queues that are subscribers
- Fully decoupled, no data loss
- SQS allows for: data persistence, delayed processing and retries of work
- Ability to add more SQS subscribers over time
- Make sure your SQS queue access policy allows for SNS to write
- SNS cannot send SQS messages to FIFO queues (AWS limitation)

### Use Case - S3 Events To Multiple Queues

For the same combination of event type (eg. object create) and prefix (eg. /home/), you can only have one S3 event rule.

If you want to send the same S3 event to many queues, use fan. Send it to SNS then fan out to SQS.

## Cost

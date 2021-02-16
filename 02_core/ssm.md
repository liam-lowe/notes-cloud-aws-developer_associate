# SSM Parameter Store

## Summary

SSM Parameter Store is a secure storage for configuration and secrets. It provides optional encryption using KMS.

SSM is serverless, scalable, durable, and has an easy to use SDK.

SSM provides version tracking of configurations / secrets.

SSM has configuration management using path & IAM

Notifications with CloudWatch events

Integration with CloudFormation

### Summary - Parameters Policies

Allows you to assign a TTL to a parameter (expiration date) to force updating or deleting sensitive data, such as passwords.

Can assign multiple policies at a time.

- Expiration (to delete a parameter)
- Expiratipon Notification (CloudWatch event)
- No Change Notification (Cloudwatch event)

## Security

## Use Case

### Use Case - SSM Parameter Store vs Secrets Manager

Secrets Manager:

- Expensive
- Automatic rotation of secrets with AWS Lambda
- Integration with RDS, Redshiftm DocumentDB
- KMS encryption is mandatory
- Can integrate with CloudFormation

SSM Parameter Store:

- Cheaper
- Simple API
- No secret roation
- KMS encryption is optional
- Can integrate with CloudFormation
- Can pull a secrets managaer secret using the SSM Parameter Store API

## Cost

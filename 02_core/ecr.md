# ECR - Elastic Container Repository

## Summary

ECR is a private Docker image repository.

Access is controlled through IAM

AWS CLI v1 login: `$(aws ecr get-login --no-include-email --region eu-west-1)`

AWS CLI v2 login: `aws ecr get-login-password --region eu-west-1` or `docker login --username AWS --pasword-stdin 1234567890.dkr.eu-west-1.amazonaws.com`

Once logged in, use a docker push or pull to publish and retrieve images.

## Security

## Use Case

## Cost

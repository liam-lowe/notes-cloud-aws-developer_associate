# KMS - Key Management System

## Summary

AWS Key Management Service (KMS) is the AWS encryption / decryption service. KMS provides an easy way to control access to your data - AWS manages all the keys for us.

KMS is fully integrated into a lot of AWS offerings:

- EBS: to encrypt volumes
- S3: Server side encryption of objects
- Redshift: encryption of data
- RDS: encryption of data
- SSM: encrypts parameter store
- etc.

You can also use the CLI / SDK to encrypt required data.

Able to fully manage the keys & policies:

- Create
- Rotation Policies
- Disable
- Enable

Able to audit key usage (CloudTrail).

Three types of Customer Master Keys:

- AWS Managed Service Default CMK: free
- User keys created in KMS: $1/month
- User keys imported (must be 256-bit symmetric keys): $1/month

The value in KMS is that the CMK used to encrypt data can never be retrieved by the user, and the CMK can be rotated for extra security.

Neverstore your secrets in plaintext, especially in your code!

Encrypted secrets can be stored in the code / environment variables.

KMS can only help in encrypting up to 4KB of data per call, if >4KB use enveloping

### Summary - Customer Master Key (CMK) Types

- Symmetric (AES-256)
  - First offering of KMS, a single encryption key that is used to encrypt and decrypt
  - AWS services that are integrated with KMS use symmetric CMKs
  - Necessary for envelope encryption
  - You never get to access the key unencrypted (must call KMS API to use)
- Asymmetric (RSA & ECC key pairs)
  - Public (Encrypt) and Private (Decrypt) key pair
  - Used for Encrypt/Decrypt, or Sign/Unsign operations
  - The public key is downloadable, but you can't access the private key unencrypted
  - Use case: encryption for AWS by users who can't call the KMS API

### Summary - KMS Key Policies

Control access to KMS keys similar to S3 bucket policies
Difference: you cannot control access without them

Default KMS Key Policy:

- Created if you don't provide a specific KMS Key Policy
- Complete access to the key to the root user = entire AWS account
- Gives access to the IAM policies to the KMS key

Custom KMS Key Policy:

- Define users, roles, that can access the KMS key
- Define who can administer the key
- Useful for cross-account access of your KMS key

### Summary - Envelope Encryption

- KMS Encrypt API call has a limit of 4KB
- If you want to encrypt >4Kb you need to use Envelope Encryption
- The main API that will help us is the GenerateDataKey API

Anything over 4 KB of data that needs to be encrypted must use the envelope method.

Envelope method == GenerateDataKey API

GenerateDataKey API generates a data key which is used client side to encrypt the file.

The AWS Encryption SDK implemented Envelope Encryption for us. The Encryption SDK also exists as a CLI tool we can install

#### Summary - Envelope Encryption - Data Key Caching

- Re-use data keys instead of creating new ones for each encryption
- Helps us with reduce the number of call to AWS, but with a securtiy trade off
- Use LocalCryptoMaterialsCache (max age, max bytes max number of messages)

### Summary - API

- Encrypt: encrypt up to 4KB of data through KMS
- GenerateDataKey: generates a unique symmetric data key (DEK)
  - Returns a plaintext copy of the data key
  - AND a copy encrypted under the CMK that you specify
- GenerateDataKeyWithoutPlaintext
  - Generate a data key to use at some point (not immediately)
  - DEK that is encrypted under the CMK (must use Decrypt later)
- Decrypt: decrypt up to 4Kb of data
- GenerateRandom: returns a random byte string

### Summary - Request Quotas

When you exceed a request quota, you get a ThrottlingException

To respond, use an exponential backoff

For cryptographic operations, they share a quota

This includes requests made by AWS on your behalf

For GenerateDataKey, consider DEK caching from the Encryption SDK

You can request a Request Quotas increase through API or AWS support.

## Security

To give access to KMS to someone:

- Make sure the Key Policy allows the user
- Make sure the IAM Policy allows the API calls

## Use Case

Anytime you need to share sensitive information, use KMS.

- Database passwords
- Credentials to external services
- Private key of SSL certificate

## Cost

- AWS Managed Service Default CMK: free
- User keys created in KMS: $1/month
- User keys imported (must be 256-bit symmetric keys): $1/month

You must also pay for API calls to KMS ($0.03 / 10,000 calls)

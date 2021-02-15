# IAM - Identity Access Management

## Summary

When accessing AWS, the root account should never be used. Users must be created with the proper permissions. IAM is central to AWS.

- Users: a physical person
- Groups: Functions (admins, devops), Teams (engineering, design), which contain a group of users
- Roles: Internal usage within AWS resources
- Policies (JSON documents): Defines what each of the above can and cannot do.

Note: IAM has predefined managed policies

For big enterprises:

- IAM Federation: Integrate their own repository of users with IAM using SAML standard

Best Practice:

- One IAM User per person
- One IAM Role per application
- IAM credentials should never be shared
- Never write IAM credentials in your code
- Never use the ROOT account except for in initial setup
- It's best to give users the minimal permissions required to perform their job

### Summary - Policies

IAM policies define permission for an action regardless of the method you use to perform the action.

#### Summary - Policies - Policy Types

##### Summary - Policies - Policy Types - Identity-Based Policy

Attach managed and in-line policies to IAM identities (users, groups to which users belong, or roles). Identity based policies grant permissions to an identity.

##### Summary - Policies - Policy Types - Resource-Based Policy

Attach inline policies to resources. The most common examples of resource based policies are AWS S3 buckets and IAM role trust policies.

Resource based policies grant permissions to a principal entity that is specified in the policy. Principals can be in the same account, or in other accounts.

##### Summary - Policies - Policy Types - Permission Boundaries

Use a managed policy as the permissions boundary for an IAM entity (user or role). That policy defines the maximum permissions that the identity-based policies can grant to an entity, but does not grant permissions. Permissions boundaries do not define the maximum permissions that a resource based poluicy can grant to an entity.

##### Summary - Policies - Policy Types - Organization SCPs

Use an Organization Service Control Policy (SCP) to define the maximum permissions for account members of an organization or organizational unit (OU). SCPs limit permissions that identity-based policies or resource based policies grant to entities (users or roles) within the account, but do not grant permissions.

##### Summary - Policies - Policy Types - Access Control Lists

Use ACLs to control which principals in other accounts can access the resource to which the ACL is attached. ACLs are similar to resourced based policies, although they are the only policy type that doesnt use the JSON document structure. ACLs are cross account permission policies that grant permissions to the specified principal entity. ACLs cannot grant permissions to entities within the same account.

##### Summary - Policies - Policy Types - Session Policies

Pass advanced session policies when you use the AWS CLI or AWS API to assume a role or federated user. Session policies limit the permissions that the role or user's identity-based policies grant to the session. Session policies limit permissions for a created session, but do not grant permissions.

### Summary - AWS Policy Simulator

When creating new AWS policies, you can test them using the policy simulator.

You can also test them using the AWS CLI, using the `--dry-run` tag on most CLI commands.

- If the request would have succeeded you will get the response `Request would have succeeded but the DryRun flag is set`
- If the request would have failed you will get the response `An error occurred (UnauthorizedOperation) when calling the policy {policy_name} operation`

## Security

## Use Case

## Cost

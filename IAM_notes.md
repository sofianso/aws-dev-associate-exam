# IAM Notes

## IAM Access Keys

IAM Access Keys are combination of both Access Key ID and Secret Access Key

## AWS Managed Policies

- Cannot be modified.
- Use for common use cases.
- Created and administered by AWS.

## Identity-based Policies

Identity-based Policies are attached to IAM identity such as user, group of users, or role.

## Resource-based Policies

Resource-based Policies grant permissions to the principal specified as the principal.

## IAM Permission Boundaries

IAM Permission Boundaries are an advanced feature that sets the max permissions that an identity-based policy can grant to an IAM identity (user or role).

## AWS Organizations Service Control Policies (SCPs)

AWS Organizations Service Control Policies (SCPs) specify the maximum permissions for an organization or organizational unit (OU).

## Session Policies

Session Policies are advanced policies that you pass as parameters when you programmatically create a temporary session for a role or federated user.

## IAM Instance Profiles

An instance profile is a container for IAM role that you can use to pass role information to an EC2 instance when instance starts. It can only contain one role, although the role can be used in multiple instance profiles.

## Cross Account Access

Cross Account Access allows one account to access another account's resources. For example, account A wants to access account S3 bucket. Account B would need create a role, which account A will use for cross access.

To make a request to access the resource, you must have attach resource-based policy with the permission you need. Or, you must assume a role within that account with the permissions you need.

## IAM Best Practices

- Lock away your Root account.
- Create individual IAM users.
- Use Groups to assign permissions to IAM users.
- Grant least privilege.
- As a beginner, use AWS managed policies.
- Use Access Levels to review IAM Permissions.
- Configure a strong password policy for your users.
- Enable MFA.
- Use roles for applications that run on EC2 instances.
- Use Roles to delegate permissions.
- Do not share Access Keys.
- Rotate credentials
- Remove unnecessary credentials.
- Use Policy Conditions for extra security. (The Condition element lets you specify conditions for when a policy is in effect)
- Monitory activity in your AWS account.

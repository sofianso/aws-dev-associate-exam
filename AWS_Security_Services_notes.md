# AWS Security Services Notes

## AWS KMS

There are two types of AWS KMS Keys:

1. Customer Managed Keys
   - Customer have full control.
   - Can be rotated.
   - A CMK can encrypt data up to 4KB in size. For anything bigger a data encryption key must be generated from the CMK.
2. AWS Managed Keys
   - AWS have full control
   - Cannot be rotated

## Client-side Encryption

Client-side Encryption is used to encrypt data on-premises before uploading it to Amazon S3.

## Data Encryption Keys

You use Data Encryption Keys to encrypt data, including large amounts of data and other data encryption keys. For example, Data Encryption Key can be used for encrypting a 1 GB file with the AWS CLI

## Envelop Encryption

You use Envelop Encryption to encrypt the data key to protect it. A master key is required.
Benefits include:

- Protection of data keys
- Can re-encrypt data keys rather than the data.
- Combine strengths of multiple algorithms.

## AWS CloudHSM

AWS CloudHSM provides a dedicated single-tenant managed service for securely creating and managing encryption keys.

## AWS Secrets Manager VS AWS SSM Parameter Store

|        Features        |                  AWS Secrets Manager                   | AWS SSM Parameter Store |
| :--------------------: | :----------------------------------------------------: | :---------------------: |
| Automatic Key Rotation | Yes, built-in for some services, use Lambda for others | No native key rotation  |

| Key/Value Type | Encrypted only | String, StringList, SecureString(encrypted) |

| Change History | No | Yes |

| Price | Around $.40 per secret | Free for standard, changes for advanced |

Ideally, **Secrets Manager** is ideal for services such as Amazon RDS, Amazon Redshift, Amazon DocumentDB because it helps meet your security and compliance requirements by enabling you to **rotate secrets** safely without the need for code deployments.

## AWS Cognito

- Cognito works as an Identity Broker that handles interactions between applications and the Web ID provider.
- Provide authentication, authorization, and user management for your web and mobile apps.
- Allow users to sign in directly with a username and password or via third party such as Facebook, Amazon or Google.
- Federation allows users to authenticate with a Web Identity Provider.

### AWS Cognito - User Pools

- It manages sign-up and sign for mobile and web apps.
- Users sign into your web or mobile app with a User Pool.
- Handle interactions between applications and the Web ID provider.
- Issue JSON Web Tokens (JWT).
  **TIP**: Think of User Pools as being similar to IAM Users.

### AWS Cognito - Identity Pools

- Identity Pools can work with Use Pools together or separately.
- Enable you to create unique identities for your users and Identity Providers such as Facebook, Google, Apple, etc using **SAML OIDC**.
- Grant temporary access to other AWS services. For example, Cognito Identity pools provide temporary security credentials to access your app’s backend resources in AWS or any service behind Amazon API Gateway.
  **TIP**: Think of Identity Pools as being similar to an IAM Role.

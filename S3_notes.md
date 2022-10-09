# S3 Notes

## Facts About S3

- S3 is a global service but buckets are created within a region. Data is never replicated outside of that region unless you configure it (e.g. through CRR).
- A special type of user called an Origin Access Identity (OAI) can be used to restrict access to content in an Amazon S3 bucket. By using an OAI you can restrict users so they cannot access the content directly using the S3 URL, they must connect via CloudFront.

## 6 Types of S3 Storage Classes

- S3 Standard
- S3 Intelligent-Tiering (automatically moves data to save money)
- S3 Standard-Infrequent Access (durable, immediately available, infrequently accessed)
- S3 One Zone-Infrequent Access (lower cost for infrequently accessed data with less resilience)
- S3 Glacier (archived data, retrieval time in minutes or hours)
- S3 Glacier Deep Archive (lowest cost storage class for long term retention)

## S3 Gateway Endpoint

**S3 Gateway Endpoint** allows user to access the contents of S3 using via a Private Subnet that is in an EC2 instance instead of using public URL.

`Client --> EC2 (Public Subnet) --> EC2 (Private Subnet via S3 Gateway Endpoint) --> S3 bucket`

## EBS

- Volume is block-based and can either be in HDD or SSD.
- EC2 instance is used to store data in EBS.
- EBS is locked to an instance in that AZ.

## EFS

- EFS is ideal for logs.
- One or more instances in different AZs can store data to EFS.
- On-premise client can also be used to store data to EFS. (VPN is required)

### When To Use ACLs

- You use ACLs when you own the bucket but not the objects being uploaded to the bucket.
- You can also use ACLs to grant certain objects that start with certain prefix "logs".
- Bucket policies are limited to 20kb in size.
- When you only want to allow certain users to modify a certain file in a bucket.

### Multipart Upload Overview

When you upload a large file larger than 100MB, AWS will `Multipart Upload` the file into the bucket. The benefits are as followed:

- Upload file faster.
- Recover better if there's a network issue.
- Pause and resume upload.

### Query String Authentication

Query String Authentication basically generates a pre-assigned URL with an expiration date.

1. You must first SSH into the EC2 instance that has access to an S3 bucket and its objects.
2. Run the following command `aws s3 presign s3//NAME_OF_BUCKET/NAME_OF_FILE.jpg --expires-in 60`.

### S3 Transfer Acceleration

S3 Transfer Acceleration leverages CloudFront Edge location to upload your files faster which can be combined with **Multipart Upload**.

You must use a specific AWS endpoints and enable it.

### Versioning

Versioning saves the state of the file, you can modify a file with versioning and delete a deleted file. If you enable versioning, you can't undo and reset it back to the default state.

### Cross-Region Replication

Cross-Region Replication is an additional step to lower latency between users to an S3 bucket.

- Versioning must be enabled.
- Source and destination buckets must be in different regions.

### Lifecycle Management

Lifecycle Management allows objects in S3 buckets to be transitioned to different storage classes after a certain period of time.

### KMS Encryption

#### Server-side Encryption

- Server-side Encryption can be done with either S3 managed keys or KMS managed keys.
- It can also be done with client-provided keys.

#### Client side Encryption

Client encrypts the bucket and also the key.

### Event Notifications

You can set a notification for when an object is PUT/POST/COPY/DELETE or more in a bucket. First, you must set up a SNS Topic and configure a SNS configuration.

### Requester Pays

Bucket owner still pays for the bucket. However, requester pays for transfer charges.

### Server Access Logging

Server Access Logging allows logs to be generated for when a file is uploaded/downloaded from or to a bucket. It is recommended that the destination of the logs are sent to a different bucket.

### Object Lock

You can only use Object Lock during the **Create a New Bucket** process. This cannot be applied to an existing bucket and this cannot be undone.

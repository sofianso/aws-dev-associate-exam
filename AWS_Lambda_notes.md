# AWS Lambda Notes

## Dead Letter Queue

A dead-letter queue saves discarded events for further processing. A dead-letter queue acts the same as an on-failure destination in that it is used when an event fails all processing attempts or expires without being processed.

## Facts About Lambda

- You manage the code.
- Lambda automatically scales.
- Use for ETL, infrastructure, data validation, mobile backends.
- Limited to 900 execution time for single execution.
- Pay only for execution time based on memory allocation.

## Facts About Invoking Lambda

- You can invoke Lambda functions via Lambda console, Lambda API, AWS SDk, AWS CLI and AWS toolkits.
- You can use other AWS services to invoke Lambda.
- Invoking a Lambda function can either be synchronously (runs the function and waits for a response) or asynchronously (run the function, but it does not wait for a response). The parameter used for synchronous is `invoke` and for asynchronous is `Event`.

## Facts About Event Source Mappings

- Event Source Mappings allows to read from an event source and invokes a Lambda function.
- Permissions in the function's execution role must be able to read and manage items in the event source.

## Event Notifications

- Lambda can be used to process event notifications from Amazon S3. For example, when an object is created or deleted.
- You grant permission on an Amazon S3's bucket to invoke a function to use that resource by adding resource-based permission policy.

## Lambda Versioning

- Versioning enables multiple versions of a Lambda function. For example, a production Lambda function can still be in use while a Lambda function in beta testing can also be used.
- Each version contains unique ARN that contains all the dependencies, settings and environment variables.
- You use `MyFunction:$LATEST` to mark the Lambda function. This can be modified (mutable).
- With numbered versions, once created, it cannot be modified (immutable).

## Working With Dependencies

- Packages must be in the code when created to a zipped file.
- If it's less than 50MB, you upload it straight to Lambda but it's more you need to upload it to S3.

## Concurrency With Lambda

- Lambda functions can run in parallel.
- There is limit for concurrency and it varies region to region. Default being 1000 exec/sec.

## Lambda Monitoring And Logging

- Performance metrics are displayed in Amazon CloudWatch.
- Execution logs are stored in Amazon CloudWatch logs.
- The Lambda function must have permission to write to CloudWatch logs.

## Benefits of Tracing With X-Ray

- Identify bottlenecks.
- Troubleshoot requests that resulted in an error.
- X-Ray must have write permissions in the execution role.

## Setting Up Lambda In Your VPC

- Lambda can access private resources in your VPC during execution.
- Lambda must be allowed to connect to the private subnet.
- It requires Private Subnet ID and Security Group ID.
- Lambda automatically generates ENI using an available IP address from your private subnet.

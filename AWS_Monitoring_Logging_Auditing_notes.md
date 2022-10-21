# AWS Monitoring, Logging, & Auditing Notes

- Amazon CloudWatch is used to monitor AWS resources and application in real-time. To monitor memory usage of an Amazon EC2 instance, you must create a custom metric.
- CloudWatch Logs centralizes logs from systems, applications, and AWS services.
- CloudWatch Alarms monitor metrics and automatically initiate actions such as adding another instance with ALB.
- CloudWatch Logs centralizes logs from systems, applications, and AWS services.
- CloudWatch Events delivers a streams of events that describe changes in AWS resources. You can view the events in AWS CloudTrail.

## What Are Metrics?

A metric is time-ordered set of data points that published to CloudWatch.

### Some fun facts about Metrics:

1. Metrics exist within a region.
2. Metrics cannot be deleted but automatically expire after 15 months.
3. Metrics are defined by a name, a namespace, and zero or more dimensions.
   - Dimensions is name/value pair that is part of the identity of a metric.
   - Dimensions are categories for the characteristics of each metric.
4. Metrics can be in either standard resolution or high resolution. Standard means one-minute granularity, while high resolution means one-second granularity.

## Amazon CloudWatch Use API Actions

- `GetMetricData` retrieve 500 different metrics in a single request.
- `PutMetricData` publishes metric data points to CloudWatch. If metric doesn't exist, CloudWatch will create one.

## AWS CloudTrail

AWS CloudTrail records activity made on your account. It is mainly used for auditing purposes. Logs are stored in an S3 bucket.

There are two types of trails:

- A trail that applies to all regions.
- A trail that applies to a single region.

## AWS X-Ray

AWS X-Ray helps devs analyse and debug production, distributed apps, especially with a microservices architecture.

### AWS X-Ray Annotations

- User-defined annotations are metadata added to a segment by a developer.
- Annotations are used to record information on segments or subsegments that you want indexed for search.
- A segment can contain multiple annotations. These are key / value pairs used to index traces and use with filters.

### AWS X-Ray Metadata

- Key/value pairs, not indexed and not used for searching.

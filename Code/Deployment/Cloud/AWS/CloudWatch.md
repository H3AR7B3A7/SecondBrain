# CloudWatch

A monitoring service for the health and performance of your AWS resources, as well as the applications that you run on AWS, and in your own datacenter

Compute
- EC2 instances
- auto scaling groups
- Elastic Load Balancers
- Route53 health checks
- Lambda
Storage & content delivery
- EBS volumes
- Storage Gateway
- Cloudfront
Databases & analyhtics
- DynamoDB tables
- Elasticache nodes
- RDS instances
- Redshift
- Elastic Map Reduce
Other
- SNS topics
- SQS queues
- API Gateway
- Estimated AWS charges

## CloudWatch Agent
Define your own metrics

## CloudWatch Logs
allows you to monitor operating system and application logs
'CloudWatch Logs Insights' allows to query the logs

## EC2
Health and performance metrics indefinitely by default
- CPU
- network
- disk
- status check

You can retrieve data from EC2 or Elastic Load Balancer even after termination

Operating System-level metrics
- Not by default
- Install Agent on EC2 instance
- Memory usage, running processes, free disk space, cpu idle time

## CloudWatch Alarms

Alarms
- EC2 cpu utilization
- Elastic Load Balancer latency
- bill charges
- action - PutMetricAlarm
Threshholds
- alarms
- actions to be taken
Use Case
- Notifications
- Execute auto scaling policy

AWS Managed Policy - CloudWatchAgentServerPolicy

## CloudWatch Dashboard

- Single page for monitoring resources
- Custom view for meaningful metrics
- Mutli-region
- Remember to save

## Concepts

Metrics
- Sequence: Time ordered sequence of values
- Timestamp
- Defined by name, namespace, zero or more dimensions
Namespaces
- Container for metrics
- Isolated
- Not aggregated
Dimensions
- Filter
- name/value pair
- For example on InstanceId
- Aggregate

## CloudTrail

Differences
- Records user activity in your AWS account
- API activity record: Creation / modification/ deletion of resources
- By default last 90 days
- Stored in S3 bucket
- Can integrate with CloudWatch

## ClouWatch Actions

- PutMetricData
- PutMetricAlarm

## Common HTTP Error codes

### 4XX
Client-side errors

- 400: Access denied
- 403: Missing authentication token
- 404: Malformed query string

### 5XX
Server-side errors

- 500: Internal failure
- 503: Service unavailable

[List of http status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)

## Common SDK exceptions
A response to an error that has occurred when processing an SDK or API request.

BatchGetItem
- returns one or more items from DynamoDB
- Single Operation - limited to 16mb and 100 items
- Partial Result - with exception when DynamoDB can't return all items
	- More than 100 items
	- More than 16mb
	- Exceeded provisioned throughput

BatchGetItem exceptions
- ValidationException
	- Request fewer items
- UnprocessedKeys
	- Reduce the request size
- ProvisionedThroughputExceededException
	- Add capacity (e.g., add DAX to cache reads)

BatchWriteItem
- puts or deletes items in one or more DynamoDB tables
- Single operation - limited to 16mb or 25 put or read operations
- Failed operation- returns list of UnprocessedItems

BatchWriteItemExceptions
- UnprocessedItems
	- Retry
- ProvisionedThroughputExceededException
	- Increase write capacity units

## EventBridge
For event driven architectures

![[event-bridge.png]]

Event bridge rules can also run on a schedule (hourly / daily / ...)
Event bridge is the preferred way to manage your events.
CloudWatch events and EventBridge are the same underlying service and API, but EventBridge provides more features.
Changes you make to either will appear in each console.







---


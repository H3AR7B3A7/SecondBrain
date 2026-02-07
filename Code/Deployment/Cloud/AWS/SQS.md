# Simple Queue Service

A message queue service that enables web service applications to quickly and reliably queue messages that one component in the application generates for another component to consume.

A queue is a temporary repository for messages awaiting processing.

- Decouple application components
- Store messages (XML, JSON, unformatted text)
- Retrieve messages
- Acts as buffer / resolves scheduling issues
- Pull based
- Minimum 2min
- Maximum 14d
- Default 4d
- Max 256kb

## Types

- Standard: 
	- best effort ordering
	- unlimited transaction
	- at least once guarantee
- FIFO:
	- first-in-first-out
	- exactly once
	- 300 transactions per second


Visibility timeouts
- Default 30s
- Max 12h
- ChangeMessageVisibility

[SQS visibility timeout](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-visibility-timeout.html)

Short Polling
- Returns a response immediately even if the message queue being polled is empty.
- This can result in a lot of empty responses if nothing is in the queue.
- You will still pay for these responses.

Long Polling
- Periodically polls the queue
- Doesn't return a response until a message arrives in the message queue or the long poll times out.
- Can save money
- Long polling is generally preferable to short polling

Delay Queues
- Postpone delivery of new messages to a queue for a number of seconds
- Messages sent to the Delay Queue remain invisible to consumers for the duration of the delay period
- Default delay is 0s, maximum is 900s (15m)
- For standard queues, changing the setting doesn't affect the delay of messages already in the queue, only new messages
- For FIFO queues, this affects the delay of messages already in the queue

Large messages
- Use S3
- Use SQS Extended Client Library for Java to manage them
- Use AWS SDK for Java
- NOT cli / management console / sqs api


---

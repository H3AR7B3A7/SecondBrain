# Simple Notification Service

A web service that makes it easy to set up, operate, and send notifications from the Cloud.

Messages sent from an application can be immediately delivered to subscribers or other applications.


- Push notifications
	- Apple
	- Google
	- Fire OS
	- Windows
	- Android
- SMS and Email
	- SQS
	- Any http endpoint

Pub-/sub
Notifications are delivered using a push mechanism that eliminates the need to periodically check or poll for new information and updates.

Topic
It's an access point, allowing recipients to subscribe to, and receive identical copies of the same notification.
SNS delivers appropriately-formatted copies of the message to each subscriber (iOS, Android, SMS, ...)

Benefits
- Instantaneous
- Simple
- Flexible
- Inexpensive
- Easy to configure
- Managed service

## SES

- Scalable and Highly available Email
- Send and receive email
- Trigger Lambda and SNS

Use cases:
- Automated emails
- Online purchases
- Marketing emails

Differences
- SES
	- Email message service
	- Can trigger lambda function or SNS notifications
	- Can be used for both incoming and outgoing email
	- An email address is all that is required to start sending messages
- SNS
	- Pub/sub messaging service; formats include SMS, HTTP, SQS, email
	- Can trigger Lambda function
	- Can fanout messages to a large number of recipients (replicate and push messages to multiple endpoints and formats)
	- Consumer must subscribe to a topic to receive the notifications








---


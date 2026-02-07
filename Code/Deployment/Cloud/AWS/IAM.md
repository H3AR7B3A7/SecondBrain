# IAM

## Amazon Cognito
Provides web ID federation, including sign-up and sign-in functionality for your apps and access for guest users

- Identity broker
- Multiple devices
- Recommended for mobile

### Web Identity Federation
Simplifies authentication and authorization for web applications

- User access to AWS Resources: with web based identity provider like FB, Amazon or Google
- Authentication: code from the web ID provider
- Authorization: trade authentication for temporary AWS security credentials

### Benefits
- Temporary credentials
- Maps to IAM Role -> Resources
- Secure and seamless: no need for embeds or locally stored credentials

### Terminology
- User Pools: user directories - sign up/in for web/mobile
- Sign-in: to user pools - direct or with FB, Amazon, Google
- Identity Pools: provide temp AWS credentials -> services like S3, DynamoDB, ...

![[identity-federation.png]]

[User Pools](https://docs.aws.amazon.com/cognito/latest/developerguide/getting-started-with-cognito-user-pools.html)

### Push Synchronization
- Devices: tracks association between identity and different devices
- Seamless: push updates and synchronize data across different devices
- SNS Silent Notification: notifies all the devices associated with identity on cloud data changes

### Policies
- AWS Managed: IAM policy created and administered by AWS
	- Assign appropriate permissions to users without writing them yourself
	- Attach multiple users, groups or roles in same or across different accounts
	- Cannot change defined permissions
- Customer Managed
	- Created by you
	- Copy existing policy and customize
	- When your needs don't match managed policies
- Inline
	- Embedded within user, group or role (gone when these are deleted)
	- 1:1 relation between entity & policy
	- For when policy must not be assigned to any other user, group or role

Managed policies are recommended.

## STS
Security Token Service
- AssumeRoleWithWebIdentity:  API provided by STS
- Temporary credentials
- Web applications (for mobile use Cognito)

![[security-token-service.png]]

[AsumeRoleWithWebIdentity](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRoleWithWebIdentity.html)

## Cross-Account Access
[Cross-Account Access](https://aws.amazon.com/blogs/security/how-to-enable-cross-account-access-to-the-aws-management-console/)

IAM role for account







---

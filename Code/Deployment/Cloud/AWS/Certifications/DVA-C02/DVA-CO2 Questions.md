# AWS Certified Developer - Associate (DVA-C02) Practice Questions by Content Domain

## Content Domain 1: Development with AWS Services (32%)

### Task 1: Develop code for applications hosted on AWS

**Question 1** - A developer is creating a web application that must give users the ability to post comments and receive feedback in **near real time**.

Which solutions will meet these requirements? **(Select TWO.)**

- [x] **A) Create an AWS AppSync schema and corresponding APIs. Use an Amazon DynamoDB table as the data store.**
- [x] **B) Create a WebSocket API in Amazon API Gateway. Use an AWS Lambda function as the backend. Use an Amazon DynamoDB table as the data store.**
- [ ] C) Create an AWS Elastic Beanstalk application that is backed by an Amazon RDS database. Configure the application to allow long-lived TCP/IP sockets.
- [ ] D) Create a GraphQL endpoint in Amazon API Gateway. Use an Amazon DynamoDB table as the data store.
- [ ] E) Establish WebSocket connections to Amazon CloudFront. Use an AWS Lambda function as the CloudFront distribution's origin. Use an Amazon Aurora DB cluster as the data store.

---

**Question 2** - A developer is building a new application that transforms text files to .pdf files. A separate application writes the text files to a source Amazon S3 bucket. The new application must read the files as they arrive in Amazon S3 and must convert the files to .pdf files by using an **AWS Lambda function**. The developer has written an IAM policy to allow access to Amazon S3 and Amazon CloudWatch Logs.

What should the developer do to ensure that the **Lambda function has the correct permissions**?

- [x] **A) Create a Lambda execution role by using AWS Identity and Access Management (IAM). Attach the IAM policy to the role. Assign the Lambda execution role to the Lambda function.**
- [ ] B) Create a Lambda execution user by using AWS Identity and Access Management (IAM). Attach the IAM policy to the user. Assign the Lambda execution user to the Lambda function.
- [ ] C) Create a Lambda execution role by using AWS Identity and Access Management (IAM). Attach the IAM policy to the role. Store the IAM role as an environment variable in the Lambda function.
- [ ] D) Create a Lambda execution user by using AWS Identity and Access Management (IAM). Attach the IAM policy to the user. Store the IAM user credentials as environment variables in the Lambda function.

---

**Question 3** - A developer is building a web application that uses Amazon API Gateway. The developer wants to maintain **different environments** for development (dev) and production (prod) workloads. The API will be backed by an AWS Lambda function with two aliases: one for dev and one for prod.

How can the developer maintain these environments with the **LEAST amount of configuration**?

- [ ] A) Create a REST API for each environment. Integrate the APIs with the corresponding dev and prod aliases of the Lambda function. Deploy the APIs to their respective stages. Access the APIs by using the stage URLs.
- [x] **B) Create one REST API. Integrate the API with the Lambda function by using a stage variable in place of an alias. Deploy the API to two different stages: dev and prod. Create a stage variable in each stage with different aliases as the values. Access the API by using the different stage URLs.**
- [ ] C) Create one REST API. Integrate the API with the dev alias of the Lambda function. Deploy the API to the dev environment. Configure a canary release deployment for the prod environment where the canary will integrate with the Lambda prod alias.
- [ ] D) Create one REST API. Integrate the API with the prod alias of the Lambda function. Deploy the API to the prod environment. Configure a canary release deployment for the dev environment where the canary will integrate with the Lambda dev alias.

---

**Question 4** - A programmer is developing a **Node.js application** that will be run on a **Linux server** in their **on-premises data center**. The application will access various AWS services such as S3, DynamoDB, and ElastiCache using the **AWS SDK**.

Which of the following is the MOST suitable way to provide access for the developer to accomplish the specified task?

- [ ] A) Create an IAM role with the appropriate permissions to access the required AWS services. Assign the role to the on-premises Linux server.
- [x] **B) Go to the AWS Console and create a new IAM user with programmatic access. In the application server, create the credentials file at ~/.aws/credentials with the access keys of the IAM user.**
- [ ] C) Create an IAM role with the appropriate permissions to access the required AWS services and assign the role to the on-premises Linux server. Whenever the application needs to access any AWS services, request temporary security credentials from STS using the AssumeRole API.
- [ ] D) Go to the AWS Console and create a new IAM User with the appropriate permissions. In the application server, create the credentials file at ~/.aws/credentials with the username and the hashed password of the IAM User.

---

**Question 5** - A developer is working with an **AWS Serverless Application Model (AWS SAM)** application composed of several AWS Lambda functions. The developer runs the application **locally** on his laptop using **sam local commands**. While testing, one of the functions returns **Access denied errors**. Upon investigation, the developer discovered that the Lambda function is using the **AWS SDK** to make API calls within a **sandbox AWS account**.

Which combination of steps must the developer do to resolve the issue? **(Select TWO)**

- [x] **A) Use the aws configure command with the --profile parameter to add a named profile with the sandbox AWS account's credentials.**
- [ ] B) Create an AWS SAM CLI configuration file at the root of the SAM project folder. Add the AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY environment variables to it.
- [ ] C) Add the AWS credentials of the sandbox AWS account to the Globals section of the template.yml file and reference them in the AWS::Serverless::Function properties section of the Lambda function.
- [x] **D) Run the function using sam local invoke with the --profile parameter.**
- [ ] E) Run the function using sam local invoke with the --parameter-overrides parameter.

---

**Question 6** - A developer has deployed a Lambda function that runs in **DEV, UAT, and PROD environments**. The function uses **different parameters** that varies based on the environment it is running in. The parameters are currently **hardcoded** in the function.

Which action should the developer do to reference the appropriate parameters **without modifying the code** every time the environment changes?

- [ ] A) Create a stage variable called ENV and invoke the Lambda function by its alias name.
- [ ] B) Create individual Lambda Layers for each environment.
- [ ] C) Publish three versions of the Lambda function. Assign the aliases DEV, UAT, and PROD to each version.
- [x] **D) Use environment variables to set the parameters per environment.**

---

### Task 2: Develop code for AWS Lambda

**Question 7** - A developer is testing an application locally and has deployed the application to an AWS Lambda function. To avoid exceeding the **deployment package size quota**, the developer did not include the **dependencies** in the deployment file. When the developer tests the application remotely, the Lambda function does not run because of missing dependencies.

Which solution will resolve this issue?

- [ ] A) Use the Lambda console editor to update the code and include the missing dependencies.
- [ ] B) Create an additional .zip file that contains the missing dependencies. Include the .zip file in the original Lambda deployment package.
- [ ] C) Add references to the missing dependencies in the Lambda function's environment variables.
- [x] **D) Create a layer that contains the missing dependencies. Attach the layer to the Lambda function.**

---

### Task 3: Use data stores in application development

**Question 8** - A developer is adding Amazon ElastiCache for Memcached to a company's existing record storage application. The developer has decided to use **lazy loading** based on an analysis of common record handling patterns.

Which pseudocode example will correctly implement lazy loading?

- [ ] A) `record_value = db.query("UPDATE Records SET Details = {1} WHERE ID == {0}", record_key, record_value)` `cache.set (record_key, record_value)`
    
- [x] **B) `record_value = cache.get(record_key)` `if (record_value == NULL)` `record_value = db.query("SELECT Details FROM Records WHERE ID == {0}", record_key)` `cache.set (record_key, record_value)`**
    
- [ ] C) `record_value = cache.get (record_key)` `db.query("UPDATE Records SET Details = {1} WHERE ID == {0}", record_key, record_value)`
    
- [ ] D) `record_value = db.query("SELECT Details FROM Records WHERE ID == {0}", record_key)` `if (record_value != NULL)` `cache.set (record_key, record_value)`
    

---

**Question 9** - A developer is moving a legacy web application from their on-premises data center to AWS. The application is used simultaneously by thousands of users, and their **session states are stored in memory**. The on-premises server usually reaches 100% CPU Utilization every time there is a surge in the number of people accessing the application.

Which of the following is the best way to re-factor the **performance and availability** of the application's **session management** once it is migrated to AWS?

- [x] **A) Use an ElastiCache for Redis cluster to store the user session state of the application.**
- [ ] B) Store the user session state of the application using CloudFront.
- [ ] C) Use an ElastiCache for Memcached cluster to store the user session state of the application.
- [ ] D) Use Sticky Sessions with Local Session Caching.

---

**Question 10** - A web application is uploading **large files**, which are **over 4 GB in size**, to an Amazon S3 bucket called data.tutorialsdojo.com every 30 minutes.

To **minimize the time** required for each upload, which of the following actions should be taken?

- [x] **A) Use the Multipart upload API.**
- [ ] B) Enable Transfer Acceleration in the bucket.
- [ ] C) Use the BatchWriteItem API.
- [ ] D) Use the PutItem API.

---

**Question 11** - A web application is using an ElastiCache cluster that is suffering from **cache churn**. A developer needs to reconfigure the application so that data are retrieved from the database **only in the event that there is a cache miss**.

Which pseudocode illustrates the caching strategy that the developer needs to implement?

- [x] **Option 1:**

```
get_item(item_id):
    item_value = cache.get(item_id)
    if item_value is None:
        item_value = database.query("SELECT * FROM Items WHERE id = ?", item_id)
        cache.add(item_id, item_value)
    return item_value
```

- [ ] Option 2:

```
get_item(item_id):
    item_value = database.query("SELECT * FROM Items WHERE id = ?", item_id)
    if item_value is None:
        item_value = cache.set(item_id, item_value)
        cache.add(item_id, item_value)
    return item_value
```

- [ ] Option 3:

```
get_item(item_id):
    item_value = cache.get(item_id)
    if item_value is not None:
        item_value = database.query("SELECT * FROM Items WHERE id = ?", item_id)
        cache.add(item_id, item_value)
        return item_value
    else:
        return item_value
```

- [ ] Option 4:

```
get_item(item_id, item_value):
    item_value = database.query("UPDATE Items WHERE id = ?", item_id, item_value)
    cache.add(item_id, item_value)
    return 'ok'
```

---

**Question 12** - A Software Engineer is developing an application that will be hosted on an Amazon EC2 instance and read messages from a **standard Amazon SQS queue**. The **average time** that it takes for the producers to send a **new message** to the queue is **10 seconds**.

Which of the following is the MOST efficient way for the application to query the new messages from the queue?

- [x] **A) Configure the SQS queue to use Long Polling.**
- [ ] B) Configure each message in the SQS queue to have a custom visibility timeout of 10 seconds.
- [ ] C) Configure the SQS queue to use Short Polling.
- [ ] D) Configure an SQS Delay Queue with a value of 10 seconds.

---

## Content Domain 2: Security (26%)

### Task 1: Implement authentication and/or authorization for applications and AWS services

**Question 1** - A developer is adding **sign-up and sign-in functionality** to an application. The application must make an **API call to a custom analytics solution** to log user sign-in events.

Which combination of actions should the developer perform to meet these requirements? **(Select TWO.)**

- [x] **A) Use Amazon Cognito to provide the sign-up and sign-in functionality.**
- [ ] B) Use AWS Identity and Access Management (IAM) to provide the sign-up and sign-in functionality.
- [ ] C) Configure an AWS Config rule to make the API call when a user is authenticated.
- [ ] D) Invoke an Amazon API Gateway method to make the API call when a user is authenticated.
- [x] **E) Invoke an AWS Lambda function to make the API call when a user is authenticated.**

---

**Question 2** - A company is using Amazon API Gateway for its REST APIs in an AWS account. A developer wants to allow **only IAM users from another AWS account** to access the APIs.

Which combination of steps should the developer take to meet these requirements? **(Select TWO.)**

- [x] **A) Create an IAM permission policy. Attach the policy to each IAM user. Set the method authorization type for the APIs to AWS_IAM. Use Signature Version 4 to sign the API requests.**
- [ ] B) Create an Amazon Cognito user pool. Add each IAM user to the user pool. Set the method authorization type for the APIs to COGNITO_USER_POOLS. Authenticate by using the IAM credentials in Amazon Cognito. Add the ID token to the request headers.
- [ ] C) Create an Amazon Cognito identity pool. Add each IAM user to the identity pool. Set the method authorization type for the APIs to COGNITO_USER_POOLS. Authenticate by using the IAM credentials in Amazon Cognito. Add the access token to the request headers.
- [x] **D) Create a resource policy for the APIs to allow access for each IAM user only.**
- [ ] E) Create an Amazon Cognito authorizer for the APIs to allow access for each IAM user only. Set the method authorization type for the APIs to COGNITO_USER_POOLS.

---

### Task 2: Implement encryption by using AWS services

**Question 3** - A developer is working on an application that stores highly confidential data in a database. The developer must use AWS Key Management Service (AWS KMS) with **envelope encryption** to protect the data.

How should the developer configure the data encryption to meet these requirements?

- [ ] A) Encrypt the data by using a KMS key. Store the encrypted data in the database.
- [ ] B) Encrypt the data by using a generated data key. Store the encrypted data in the database.
- [ ] C) Encrypt the data by using a generated data key. Store the encrypted data and the data key ID in the database.
- [x] **D) Encrypt the data by using a generated data key. Store the encrypted data and the encrypted data key in the database.**

---

### Task 3: Manage sensitive data in application code

**Question 4** - A company is migrating a legacy application to Amazon EC2 instances. The application uses a user name and password that are stored in the source code to connect to a MySQL database. The company will migrate the database to an Amazon RDS for MySQL DB instance. As part of the migration, the company needs to implement a **secure way to store** and **automatically rotate** the database credentials.

Which solution will meet these requirements?

- [ ] A) Store the database credentials in environment variables in an Amazon Machine Image (AMI). Rotate the credentials by replacing the AMI.
- [ ] B) Store the database credentials in AWS Systems Manager Parameter Store. Configure Parameter Store to automatically rotate the credentials.
- [ ] C) Store the database credentials in environment variables on the EC2 instances. Rotate the credentials by relaunching the EC2 instances.
- [x] **D) Store the database credentials in AWS Secrets Manager. Configure Secrets Manager to automatically rotate the credentials.**

---

**Question 5** - A serverless application is composed of several Lambda functions which reads data from RDS. These functions must **share the same connection string** that should be **encrypted** to improve data security.

Which of the following is the MOST secure way to meet the above requirement?

- [x] **A) Create a Secure String Parameter using the AWS Systems Manager Parameter Store.**
- [ ] B) Use AWS Lambda environment variables encrypted with KMS which will be shared by the Lambda functions.
- [ ] C) Create an IAM Execution Role that has access to RDS and attach it to the Lambda functions.
- [ ] D) Use AWS Lambda environment variables encrypted with CloudHSM.

---

**Question 6** - To improve their information security management system (ISMS), a company recently released a new policy which requires all database credentials to be **encrypted** and be **automatically rotated** to avoid unauthorized access.

Which of the following is the MOST appropriate solution to secure the credentials?

- [ ] A) Create a parameter to the Systems Manager Parameter Store using the PutParameter API with a type of SecureString.
- [ ] B) Enable IAM DB authentication which rotates the credentials by default.
- [ ] C) Create an IAM Role which has full access to the database. Attach the role to the services which require access.
- [x] **D) Create a secret in AWS Secrets Manager and enable automatic rotation of the database credentials.**

---

## Content Domain 3: Deployment (24%)

### Task 4: Deploy code by using AWS CI/CD services

**Question 1** - A developer has recently completed a new version of a serverless application that is ready to be deployed using **AWS SAM**. There is a requirement that the traffic should shift from the previous Lambda function to the new version in the **shortest time possible**, but you still don't want to shift traffic **all-at-once** immediately.

Which deployment configuration is the MOST suitable one to use in this scenario?

- [ ] A) CodeDeployDefault.HalfAtATime
- [ ] B) CodeDeployDefault.LambdaLinear10PercentEvery1Minute
- [ ] C) CodeDeployDefault.LambdaLinear10PercentEvery2Minutes
- [x] **D) CodeDeployDefault.LambdaCanary10Percent5Minutes**

---

## Content Domain 4: Troubleshooting and Optimization (18%)

### Task 1: Assist in a root cause analysis

**Question 1** - A developer wants to track the performance of an application that runs on a fleet of Amazon EC2 instances. The developer wants to **view and track statistics**, such as the average request latency and the maximum request latency, across the fleet. The developer wants to receive **immediate notification** if the average response time exceeds a threshold.

Which solution will meet these requirements?

- [ ] A) Configure a cron job on each EC2 instance to measure the response time and update a log file stored in an Amazon S3 bucket every minute. Use an Amazon S3 event notification to invoke an AWS Lambda function that reads the log file and writes new entries to an Amazon OpenSearch Service cluster. Visualize the results in OpenSearch Dashboards. Configure OpenSearch Service to send an alert to an Amazon Simple Notification Service (Amazon SNS) topic when the response time exceeds the threshold.
- [ ] B) Configure the application to write the response times to the system log. Install and configure the Amazon Inspector agent on the EC2 instances to continually read the logs and send the response times to Amazon EventBridge (Amazon CloudWatch Events). View the metrics graphs in the EventBridge (CloudWatch Events) console. Configure an EventBridge (CloudWatch Events) custom rule to send an Amazon Simple Notification Service (Amazon SNS) notification when the average of the response time metric exceeds the threshold.
- [x] **C) Configure the application to write the response times to a log file. Install and configure the Amazon CloudWatch agent on the EC2 instances to stream the application log to CloudWatch Logs. Create a metric filter of the response time from the log. View the metrics graphs in the CloudWatch console. Create a CloudWatch alarm to send an Amazon Simple Notification Service (Amazon SNS) notification when the average of the response time metric exceeds the threshold.**
- [ ] D) Install and configure AWS Systems Manager Agent (SSM Agent) on the EC2 instances to monitor the response time and send the response time to Amazon CloudWatch as a custom metric. View the metrics graphs in Amazon QuickSight. Create a CloudWatch alarm to send an Amazon Simple Notification Service (Amazon SNS) notification when the average of the response time metric exceeds the threshold.

---
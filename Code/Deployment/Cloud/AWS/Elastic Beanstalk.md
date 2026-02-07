# Elastic beanstalk

Deploy and scale web applications

Supported languages
- Java
- .Net
- PHP
- Node.js
- Python
- Ruby
- Go

[Supported platforms](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts.platforms.html)
- Apache tomcat
- Docker

Benefits
- Focus on writing code
- don't worry about underlying infrastructure

- Infrastructure: Provisions infrastructure, load balancing, auto scaling and health monitoring
- Application platform: Installation and management of the application stack, including patching and updates to your operating system and application platform
- You are in control: You have complete administrative control of the AWS resources

Quickest and easiest way to deploy and scale your web applications, including the application server platform

Updating: Deployment options
- All at once
- Rolling
- Rolling with additional batch (keep full capacity)
- Immutable (no downtime rolling back)

Traffic splitting
Installs the new version on a new set of instances, like an immutable deployment.
Forwards a percentage of incoming client traffic to the new application version for evaluation
Enables canary testing

Customizing
- Pre-Linux 2 environments
	- Configuration file to define packages to install, create linux users/groups, run shell commands, enable services and configure loadbalancers
	- YAML/JSON
	- /.ebextensions/.config
- Linux 2
	- Buildfile: short running commands that exit upon task completion
	- Procfile: long runnings processes (start app)
	- platform hooks: custom scripts run at chosen stage
		- /.platform/hooks/prebuild
		- /.platform/hooks/predeploy
		- /.platform/hooks/postdeploy

## RDS & EB

RDS (relational db service)
- Inside EB env (also terminates db / not for prod)
- Outside EB env
	- Add additional security group to auto scaling group
	- Provide connection string and password to app servers using EB env props

## [Migrating Assistant Tool](https://github.com/awslabs/windows-web-app-migration-assistant)
- Powershell utility
- .Net apps
- Entire website

---

## Exercise instructions

### Deploying An Application With Elastic Beanstalk - Demo

https://learn.acloud.guru/course/aws-certified-developer-associate/learn/d36a1363-452a-8007-e874-54f19b10c0b7/baf22738-24ef-2c52-39e1-9576859a3e64/watch

### To create your example application, you'll use the 'Create application' console wizard. It creates an Elastic Beanstalk application and launches an environment within it. An environment is the collection of AWS resources required to run your application code.

### To create a service role for Elastic Beanstalk:

1. Open the Identity and Access Management (IAM) console.
2. Click 'Roles'.
3. Click 'Create role'.
4. Under 'Use cases for other AWS services', choose 'Elastic Beanstalk', select 'Elastic Beanstalk - Customizable', and click 'Next'.
5. Click 'Next'.
6. For 'Role name', type 'CustomServiceRoleForElasticBeanstalk'.
7. Click 'Create role'.

### To create an EC2 instance profile for Elastic Beanstalk:

1. Open the Identity and Access Management (IAM) console.
2. Click 'Roles'.
3. Click 'Create role'.
4. Under 'Common use cases', choose 'EC2'.
5. Click 'Next'.
6. Select the 'AWSElasticBeanstalkReadOnly' policy name.
7. Click 'Next'.
8. For 'Role name', type 'CustomEC2InstanceProfileForElasticBeanstalk'.
9. Click 'Create role'.

### To create an example application:

1. Open the Elastic Beanstalk console.
2. Click 'Create application'.
3. For Application name enter 'Hello Cloud Gurus'.
4. For Platform, choose 'PHP'.
5. Under 'Application code', select 'Upload your code', type 'v1' under 'Version label', select 'Local file' > 'Choose file' and upload the 'aws-cda-EBS_Demo_V1.zip' file available under the RESOURCES section of the lesson. Click 'Next'.
6. For 'Use an existing service role', choose 'CustomServiceRoleForElasticBeanstalk'.
7. For 'EC2 instance profile', choose CustomEC2InstanceProfileForElasticBeanstalk'.
8. Click 'Next'.
9. On the 'Set up networking, database, and tags - optional' page, click 'Next'.
10. On the 'Configure instance traffic and scaling - optional' page, click 'Next'.
11. On the 'Configure updates, monitoring, and logging - optional' page, under 'System' choose 'Basic', and under 'Managed platform updates' > 'Managed updates', uncheck the 'Activated' box. Click 'Next'.
12. The Review page displays a summary of all your choices. Choose 'Submit' at the bottom of the page.
13. Wait for the 'Successfully launched environment: HelloCloudGurus-env' event and check the URL available under 'Environment overview' > 'Domain'.

[Code](https://github.com/ACloudGuru-Resources/course-aws-certified-developer-associate/tree/main/Deploying_An_App_With_Elastic_Beanstalk_Demo)





---


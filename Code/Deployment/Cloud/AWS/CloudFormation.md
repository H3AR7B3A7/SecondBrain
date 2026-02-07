# CloudFormation

Manage, configure and provision your AWS infrastructure as code
- Uses template to make appropriate API calls to create resources
- YAML / JSON

Benefits
- Consistent
- Quick and efficient
- Version control
- Free to use
- Manage updates
- Rolling back

[CloudFormation Template](https://github.com/ACloudGuru-Resources/course-aws-certified-developer-associate/blob/main/Provisioning_Resources_Using_CloudFormation_Demo/aws-cda-2018-af53a522-cdf6-4fcd-b12d-e8948e84d58d.yml)
- Mappings section: values based on a region
- Parameters section
- Transform section: for referencing additional code stored in S3
- Resource section (mandatory)
- Outputs section

SAM
Serverless Application Model

- CloudFormation for Serverless
- Simplified syntax
	- APIs
	- Lambdas
	- DynamoDB tables
	- ...
- SAM CLI
	- sam package
	- sam deploy

Nested Stacks
- Stacks that create other stacks / template within a template
- Enable re-use of ClouFormation code for common use cases
- Type: AWS::ClouFormation::Stack (with mandatory TemplateURL)


CDK
Cloud Development Kit

Allows you to build applications, define and deploy AWS resources using a programming language of your choice

App > Stack > Constructs

Typescript:
- cdk init
- npm run build
- cdk synth
- cdk deploy

[Best Practices](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/best-practices.html)



---


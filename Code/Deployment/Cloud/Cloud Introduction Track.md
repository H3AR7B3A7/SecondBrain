# Cloud Introduction Track
## AWS Well Architected Framework
*The Well Architected tool can review the architecture of the application and is available for free in the AWS console.*

- Build and deploy faster
- Lower or mitigate risks
- Make informed decisions
- Learn AWS best practices

Five pillars - Architectural trade-offs:
- Operational excellence
- Security
- Reliability
- Performance efficiency
- Cost optimization

General Design Principles
- Stop guessing your capacity needs
- Test systems at production scale
- Automate to make architectural experimentation easier
- Allow for evolutionary architectures
- Drive architectures using data
- Improve through game days

### Operational Excellence
- Perform operation as code (IaC)
- Make frequent, small, reversible changes
- Refine operations procedures frequently
- Anticipate failure
- Learn from all operational failures

Helpful applications:
- Terraform (opensource)
- Cloudformation
- ...

Services:
- CloudFormation
- AWS Config
- Amazon CloudTrail
- Amazon CloudWatch

### Security
- Implement a strong identity foundation
- Enable traceability
- Apply security at all layers
- Automate security best practices
- Protect data in transit and at rest
- Keep people away from data
- Prepare for security events

### Reliability
- Automatically recover from failure
- Test recovery procedures
- Scale horizontally to increase aggregate workload availability
- Stop guessing capacity
- Manage change in automation

AWS Cloud infrastructure:
- AWS Region
	- Availability Zone

### Performance Efficiency
- Make advanced technology implementation easier
- Go global in minutes
- Use serverless architectures
- Experiment more often
- Use the technology approach that aligns best with your goals

Options:
- VM-based
	- EC2
- Container-based
	- ECS
	- EKS
	- ECS/EKS-Fargate (Serverless containers)
- Serverless-based
	- AWS Lambda

DB
- Relational
	- RDS
	- Aurora
- Non-remational
	- Amazon DynamoDB
	- Amazon DocumentDB
	- Amazon Neptune
	- Amazon ElastiCache
	- Amazon Timestream
- Data warehouse
	- Amazon Redshift
- Data indexing and searching solution
	- Amazon CloudSearch, ElasticSearch

Network
- AWS Global Accelerator
- N-series EC2 instances
- Hybrid cloud
	- AWS Direct Connect
	- AWS VPN
	- AWS Transit Gateway: central hub
- Elastic Load Balancing
- Choose appropriate region(s)

### Cost Optimization
- Avoiding unnecessary costs
- Understanding and controlling where money is being spent
- Selecting the most appropriate and right number of resource types
- Analyzing spend over time
- Scaling to meet business needs without overspending

## AWS EC2 By Example

## AWS Serverless By Example 1

## AWS Serverless By Example 2

## Azure Serverless By Example

## AWS Containers By Example

## AWS Devops By Example



---
#Cloud #AWS #Azure
## CLF-C02: AWS Certified Cloud Practitioner

![[Pasted image 20250628164414.png]]

### Key topics

- AWS well-architected framework
- AWS shared responsibility model
- How regions and zones keep your services running?
- How do AWS edge locations deliver faster services?

### Cloud Concepts
#### Types of Cloud Services and How They Work

| IaaS: Infrastructure as a Service    | Paas: Platform as a Service          | SaaS: Software as a Service          |
| ------------------------------------ | ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20250628164606.png]] | ![[Pasted image 20250628164646.png]] | ![[Pasted image 20250628164717.png]] |
#### On-Premise

![[Pasted image 20250628165518.png]]

#### In-Cloud
  
![[Pasted image 20250628165549.png]]

### Cloud Computing

#### Types
- Computing power
- Storage
- Networking
- Applications

#### Characteristics
- On-demand access
- Access from anywhere
- Shared resources
- Scalability
- Pay ad you go

### Shared responsibility

- Customer: Responsible for security IN the cloud
- AWS: Responsible for security OF the cloud

_There are some variations between services._

![[Pasted image 20250707084029.png]]


### Regions & Availability Zones

- Region: geographic region where AWS has different availability zones
- AZ: A data center or group of data centers within a region with independent power, cooling and networking

Example: Ireland (eu-west-1) has 3 AZ's: eu-west1a, eu-west1b, eu-west1c


### AWS Edge Locations

#### Cloudfront

- Distributes content through a network of edge locations worldwide
- Cashes static and dynamic content closer to end-users, reducing latency
- Works seamlessly with other AWS services to enhance scalability and security

#### Global Accelerator

- Routes user traffic through the AWS global network for low latency
- Provides static IP addresses and rapid failover for resilient application delivery
- Automatically directs users to the nearest and healthiest endpoints for faster response times

### AWS Well-architected Framework

- Applications need reliable systems to run soothly
- Ensures alignment with AWS best practices
- Facilitates continuous improvement

#### Key Principles

- Operational excellence
- Security
- Reliability
- Performance efficiency
- Cost optimization

#### Best practices

- Use managed services
- Employ infrastructure as code
- Automate your deployments with security checks
- Conduct regular security reviews

## AWS Compute Services

- Run applications without managing physical servers
- Choose different types of computing power
- AWS provides a way to scale up or down

Examples:
- Amazon EC2
	- Allows you to rent a computer on demand
	- Choose size and power that fits your needs
	- Pay only for what you use
	- Good for websites, business apps, and data processing
- Amazon ECS (Elastic container Service)
	- Allows you to run and manage containerized applications
	- Handles scaling and placement of containers automatically
	- Works with EC2 or Fargate for flexible deployment
	- Great for modular apps, growing apps, and batch tasks
- Amazon EKS (Elastic Kubernetes Service)
	- Allows you to run and manage Kubernetes applications
	- Automates scaling and deployments
	- Works with EC2 or Fargate for flexible deployment
	- Great for complex applications needing high availability and portability
- Lambda
	- Runs code only when an event happens
	- No need to manage servers or resources
	- Automatically scales to handle more users
	- Only pay for the time your code runs, which saves money


### EC2

#### Instance types

- General purpose
- Compute optimized
- Memory optimized
- Storage optimized
- Accelerated computing

#### Features

- Autoscaling
- Load balancing
- Pay as you go

#### Pricing models

- On-demand: Pay per hour/second with no commitment
- Reserved: Up to 75% discount for long term commitment
- Spot instance: Cost effective, but may be interrupted
- Savings plan: Flexible pricing with discounts















## AWS Certified Developer - Associate (DVA-C02)




---

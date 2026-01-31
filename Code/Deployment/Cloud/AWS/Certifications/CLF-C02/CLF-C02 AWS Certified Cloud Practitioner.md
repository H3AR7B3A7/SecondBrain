# CLF-C02: AWS Certified Cloud Practitioner - Complete Study Guide

## Exam Overview (CLF-C02)

- **Format**: 65 questions (50 scored + 15 unscored)
- **Duration**: 90 minutes
- **Passing Score**: 700/1000
- **Cost**: $100 USD
- **Validity**: 3 years
- **Question Types**: Multiple choice and multiple response

## Exam Domain Breakdown

1. **Cloud Concepts** - 24%
2. **Security and Compliance** - 30%
3. **Cloud Technology and Services** - 34%
4. **Billing, Pricing, and Support** - 12%

---

## Domain 1: Cloud Concepts (24%)

### Key Topics You Have

✓ AWS Well-Architected Framework ✓ AWS Shared Responsibility Model ✓ Regions and Availability Zones ✓ Edge Locations (CloudFront & Global Accelerator) ✓ Cloud Service Models (IaaS, PaaS, SaaS) ✓ Cloud Computing Characteristics

### **MISSING: Benefits of Cloud Computing**

#### Six Key Advantages of AWS Cloud

1. **Trade capital expense for variable expense**
    
    - No upfront infrastructure costs
    - Pay only for what you consume
2. **Benefit from massive economies of scale**
    
    - Lower pay-as-you-go prices due to AWS's scale
    - Hundreds of thousands of customers sharing infrastructure
3. **Stop guessing capacity**
    
    - Scale up or down based on actual demand
    - Avoid overprovisioning or underprovisioning
4. **Increase speed and agility**
    
    - Resources available in minutes
    - Reduce time from idea to implementation
5. **Stop spending money running and maintaining data centers**
    
    - Focus on projects that differentiate your business
    - Let AWS handle infrastructure management
6. **Go global in minutes**
    
    - Deploy applications in multiple regions worldwide
    - Provide lower latency and better experience to customers

### **MISSING: Cloud Migration Strategies (6 R's)**

1. **Rehost (Lift and Shift)** - Move applications without changes
2. **Replatform (Lift, Tinker, and Shift)** - Make minimal cloud optimizations
3. **Refactor/Re-architect** - Reimagine application using cloud-native features
4. **Repurchase** - Move to SaaS (e.g., from on-premise CRM to Salesforce)
5. **Retire** - Remove applications no longer needed
6. **Retain** - Keep certain applications on-premises

### **UPDATED: AWS Well-Architected Framework**

#### Six Pillars (You're Missing Sustainability!)

1. **Operational Excellence**
    
    - Run and monitor systems
    - Continually improve processes
    - Key services: AWS CloudFormation, AWS Config, CloudWatch
2. **Security**
    
    - Protect data, systems, and assets
    - Implement strong identity foundation
    - Key services: IAM, AWS Shield, Amazon GuardDuty, AWS WAF
3. **Reliability**
    
    - Recover from failures automatically
    - Scale horizontally
    - Key services: Auto Scaling, CloudWatch, Multi-AZ deployments
4. **Performance Efficiency**
    
    - Use computing resources efficiently
    - Maintain efficiency as demand changes
    - Key services: Lambda, Amazon EBS, Amazon S3
5. **Cost Optimization**
    
    - Avoid unnecessary costs
    - Use appropriate resources
    - Key services: Cost Explorer, AWS Budgets, Reserved Instances
6. **Sustainability** ⭐ NEW PILLAR (Added in 2021)
    
    - Minimize environmental impacts
    - Understand impact and maximize utilization
    - Key practices: Use managed services, reduce data movement

---

## Domain 2: Security and Compliance (30%)

### **MISSING: AWS Identity and Access Management (IAM)**

#### Core Concepts

- **Users**: Individual people or services
- **Groups**: Collection of users with shared permissions
- **Roles**: Temporary credentials for services/applications
- **Policies**: JSON documents that define permissions

#### Best Practices

- Enable MFA (Multi-Factor Authentication) for root account
- Use principle of least privilege
- Never share root account credentials
- Use IAM roles for EC2 instances
- Rotate credentials regularly
- Use policy conditions for extra security

### **MISSING: AWS Compliance Programs**

- **ISO 27001**: Information security management
- **SOC 1, 2, 3**: Service organization controls
- **PCI DSS**: Payment card industry standards
- **HIPAA**: Healthcare data protection
- **GDPR**: European data protection
- **FedRAMP**: US government cloud security

### **MISSING: AWS Security Services**

#### AWS Shield

- DDoS protection service
- **Standard**: Automatic, free protection
- **Advanced**: Enhanced protection for $3,000/month + data transfer fees

#### Amazon GuardDuty

- Threat detection service
- Monitors for malicious activity
- Uses machine learning
- Analyzes CloudTrail, VPC Flow Logs, DNS logs

#### AWS WAF (Web Application Firewall)

- Protects web applications
- Filters malicious web traffic
- Custom rules or managed rule groups
- Integrates with CloudFront, ALB, API Gateway

#### AWS Inspector

- Automated security assessment
- Identifies vulnerabilities
- Checks against best practices
- Network accessibility and application security

#### AWS Artifact

- On-demand access to compliance reports
- AWS security and compliance documents
- Download audit artifacts

#### Amazon Macie

- Data security and privacy service
- Discovers and protects sensitive data (PII)
- Uses machine learning
- Monitors S3 buckets

#### AWS Key Management Service (KMS)

- Create and manage encryption keys
- Control access to encrypted data
- Integrated with many AWS services
- FIPS 140-2 validated

#### AWS Secrets Manager

- Rotate, manage, and retrieve secrets
- API keys, passwords, certificates
- Automatic rotation
- Integrated with RDS, Redshift, DocumentDB

### **EXPANDED: Shared Responsibility Model**

#### AWS Responsibilities (Security OF the Cloud)

- Physical security of data centers
- Hardware infrastructure
- Network infrastructure
- Virtualization layer
- Managed service operations

#### Customer Responsibilities (Security IN the Cloud)

- Customer data
- Platform, applications, IAM
- Operating system, network, firewall configuration
- Client-side encryption
- Server-side encryption
- Network traffic protection

#### Shared Controls

- Patch management
- Configuration management
- Awareness and training

---

## Domain 3: Cloud Technology and Services (34%)

### Compute Services (EXPANDED)

#### **MISSING: AWS Elastic Beanstalk**

- Platform as a Service (PaaS)
- Deploy and scale web applications
- Supports multiple languages (Java, .NET, PHP, Node.js, Python, Ruby, Go)
- Handles capacity provisioning, load balancing, auto-scaling
- You retain full control over resources

#### **MISSING: AWS Lightsail**

- Simplified compute service
- Virtual private servers (VPS)
- Pre-configured applications (WordPress, Magento)
- Fixed monthly pricing
- Great for simple web applications

#### **MISSING: AWS Batch**

- Run batch computing jobs
- Automatically provisions resources
- Schedule and execute batch workloads
- No server management

#### **MISSING: AWS Outposts**

- Extend AWS infrastructure on-premises
- Hybrid cloud solution
- Run AWS services locally
- Low-latency access to on-premises systems

### **MISSING: Storage Services**

#### Amazon S3 (Simple Storage Service)

- Object storage service
- Store and retrieve any amount of data
- 99.999999999% (11 9's) durability
- **Storage Classes**:
    - **S3 Standard**: Frequent access, high availability
    - **S3 Intelligent-Tiering**: Automatic cost optimization
    - **S3 Standard-IA**: Infrequent access, lower cost
    - **S3 One Zone-IA**: Single AZ, even lower cost
    - **S3 Glacier Instant Retrieval**: Archive, millisecond access
    - **S3 Glacier Flexible Retrieval**: Archive, minutes to hours
    - **S3 Glacier Deep Archive**: Lowest cost, 12-hour retrieval

#### Amazon EBS (Elastic Block Store)

- Block storage for EC2 instances
- Persistent storage (survives instance termination)
- **Volume Types**:
    - **GP3/GP2**: General purpose SSD
    - **io2/io1**: Provisioned IOPS SSD (high performance)
    - **st1**: Throughput optimized HDD
    - **sc1**: Cold HDD (lowest cost)
- Snapshots stored in S3
- Can encrypt volumes

#### Amazon EFS (Elastic File System)

- Managed NFS file system
- Scales automatically
- Multiple EC2 instances can access
- Linux-based workloads
- Supports NFSv4 protocol

#### AWS Storage Gateway

- Hybrid cloud storage
- Connects on-premises to AWS cloud
- **Types**:
    - File Gateway (NFS/SMB)
    - Volume Gateway (iSCSI)
    - Tape Gateway (VTL)

#### Amazon FSx

- Fully managed third-party file systems
- **FSx for Windows File Server**: Windows-native
- **FSx for Lustre**: High-performance computing
- **FSx for NetApp ONTAP**: NetApp features
- **FSx for OpenZFS**: ZFS file system

### **MISSING: Database Services**

#### Amazon RDS (Relational Database Service)

- Managed relational databases
- Automated backups, patching, scaling
- **Supported Engines**:
    - MySQL, PostgreSQL, MariaDB
    - Oracle, Microsoft SQL Server
    - Amazon Aurora (AWS-optimized)
- Multi-AZ for high availability
- Read replicas for scalability

#### Amazon Aurora

- MySQL and PostgreSQL compatible
- 5x performance of MySQL, 3x PostgreSQL
- Automatically grows storage (up to 128 TB)
- Up to 15 read replicas
- Serverless option available

#### Amazon DynamoDB

- Fully managed NoSQL database
- Key-value and document database
- Millisecond latency at any scale
- Built-in security, backup, restore
- Global tables for multi-region
- Auto scaling
- DynamoDB Accelerator (DAX) for caching

#### Amazon ElastiCache

- In-memory caching service
- **Redis** or **Memcached**
- Microsecond latency
- Improves application performance
- Session stores, gaming leaderboards

#### Amazon Redshift

- Data warehouse service
- Petabyte-scale
- Fast query performance
- Columnar storage
- SQL-based
- Integrates with BI tools

#### Amazon Neptune

- Graph database service
- Social networks, recommendation engines
- Knowledge graphs
- Supports Apache TinkerPop Gremlin and SPARQL

#### Amazon DocumentDB

- MongoDB-compatible
- Document database
- Fully managed
- Scales storage automatically

#### Amazon Timestream

- Time series database
- IoT applications
- 1000x faster, 1/10th cost vs relational

#### Amazon QLDB (Quantum Ledger Database)

- Immutable ledger database
- Cryptographically verifiable
- Track all changes to data
- Centralized, trusted authority

### **MISSING: Networking and Content Delivery**

#### Amazon VPC (Virtual Private Cloud)

- Isolated virtual network
- Control IP address range
- Create subnets
- Configure route tables and gateways
- Security groups and NACLs
- VPN and Direct Connect integration

#### Elastic Load Balancing (ELB)

- Distributes traffic across targets
- **Types**:
    - **Application Load Balancer (ALB)**: HTTP/HTTPS, Layer 7
    - **Network Load Balancer (NLB)**: TCP/UDP, Layer 4, ultra-high performance
    - **Gateway Load Balancer**: Deploy third-party appliances
    - **Classic Load Balancer**: Legacy, Layer 4 & 7

#### Amazon Route 53

- Scalable DNS web service
- Domain name registration
- Health checks and monitoring
- **Routing Policies**:
    - Simple, Weighted, Latency
    - Failover, Geolocation, Geoproximity
    - Multi-value answer

#### AWS Direct Connect

- Dedicated network connection
- On-premises to AWS
- More consistent network performance
- Reduce bandwidth costs
- Private connectivity

#### AWS VPN

- Encrypted connections over internet
- **Site-to-Site VPN**: Connect on-premises to VPC
- **Client VPN**: Remote users to AWS/on-premises
- Cheaper than Direct Connect

#### Amazon API Gateway

- Create, publish, maintain APIs
- RESTful and WebSocket APIs
- Handle traffic management
- Authorization and access control
- Monitoring and API versioning

### **MISSING: Management and Governance**

#### AWS CloudFormation

- Infrastructure as Code (IaC)
- Define resources in JSON/YAML templates
- Automate and version infrastructure
- Create stacks
- Repeatable deployments

#### AWS CloudTrail

- Records AWS API calls
- Governance, compliance, audit
- Who did what, when, where
- Event history
- Integrates with CloudWatch Logs

#### Amazon CloudWatch

- Monitoring and observability
- **Metrics**: CPU, network, disk
- **Logs**: Collect and monitor log files
- **Alarms**: Trigger notifications or actions
- **Dashboards**: Visualize metrics
- **Events/EventBridge**: Respond to state changes

#### AWS Config

- Assess, audit, evaluate configurations
- Resource inventory
- Configuration history
- Change notifications
- Rules for compliance
- Remediation actions

#### AWS Systems Manager

- Operational insights
- Manage EC2 and on-premises systems
- Patch management
- Run commands at scale
- Parameter Store for secrets
- Session Manager for secure access

#### AWS Trusted Advisor

- Best practice recommendations
- **Five Categories**:
    - Cost optimization
    - Performance
    - Security
    - Fault tolerance
    - Service limits
- Real-time guidance
- **Free**: 7 core checks
- **Business/Enterprise Support**: All checks

#### AWS Organizations

- Centrally manage multiple AWS accounts
- Consolidated billing
- Service Control Policies (SCPs)
- Organize accounts in OUs
- Automate account creation

#### AWS Control Tower

- Set up and govern multi-account environment
- Blueprints (guardrails)
- Account Factory
- Dashboard for compliance

#### AWS Service Catalog

- Create and manage catalogs of IT services
- Centrally manage approved resources
- Enforce compliance
- Self-service portal for users

### **MISSING: Analytics Services**

#### Amazon Athena

- Query S3 data using SQL
- Serverless
- Pay per query
- Standard SQL (Presto)
- Integrate with QuickSight

#### Amazon EMR (Elastic MapReduce)

- Big data processing
- Apache Hadoop, Spark, HBase
- Process vast amounts of data
- Log analysis, data warehousing

#### AWS Glue

- ETL service (Extract, Transform, Load)
- Prepare data for analytics
- Serverless
- Data catalog
- Discovers and catalogs metadata

#### Amazon Kinesis

- Real-time data streaming
- **Kinesis Data Streams**: Collect and process
- **Kinesis Data Firehose**: Load into AWS services
- **Kinesis Data Analytics**: Analyze with SQL
- **Kinesis Video Streams**: Video streaming

#### Amazon QuickSight

- Business intelligence (BI) service
- Create visualizations and dashboards
- ML-powered insights
- Pay-per-session pricing

#### Amazon OpenSearch Service

- Search and analytics engine
- Log analytics
- Application monitoring
- Formerly Elasticsearch Service

### **MISSING: Application Integration**

#### Amazon SNS (Simple Notification Service)

- Pub/sub messaging
- Push notifications
- Multiple subscribers
- Email, SMS, HTTP, SQS, Lambda

#### Amazon SQS (Simple Queue Service)

- Message queue service
- Decouple components
- Pull-based
- **Standard**: At-least-once delivery
- **FIFO**: Exactly-once, ordered
- Unlimited throughput (Standard)

#### AWS Step Functions

- Orchestrate workflows
- Coordinate distributed applications
- Visual workflows
- Error handling and retry logic

#### Amazon EventBridge

- Serverless event bus
- Route events between AWS services
- SaaS applications
- Custom applications

### **MISSING: Migration and Transfer**

#### AWS Migration Hub

- Track migrations from single location
- Discover on-premises resources
- Group resources as applications

#### AWS Database Migration Service (DMS)

- Migrate databases to AWS
- Minimal downtime
- Source remains operational
- Supports homogeneous and heterogeneous migrations
- Continuous data replication

#### AWS Snow Family

- Physical devices to transfer data
- **Snowcone**: 8 TB, portable (2.1 kg)
- **Snowball Edge**: 80 TB, compute capabilities
- **Snowmobile**: 100 PB, shipping container
- Use when network transfer is too slow/expensive

#### AWS DataSync

- Automated data transfer
- On-premises to AWS
- NFS, SMB to S3, EFS, FSx
- Up to 10x faster than open-source tools

#### AWS Transfer Family

- Fully managed SFTP, FTPS, FTP
- Transfer files to/from S3 or EFS
- No infrastructure to manage

### **MISSING: Machine Learning and AI**

#### Amazon SageMaker

- Build, train, deploy ML models
- Fully managed
- Jupyter notebooks
- Built-in algorithms
- One-click deployment

#### Amazon Rekognition

- Image and video analysis
- Face detection and recognition
- Object and scene detection
- Content moderation

#### Amazon Comprehend

- Natural language processing (NLP)
- Sentiment analysis
- Entity recognition
- Language detection

#### Amazon Polly

- Text-to-speech
- Lifelike voices
- Multiple languages
- Neural and standard voices

#### Amazon Transcribe

- Speech-to-text
- Automatic speech recognition
- Real-time or batch
- Custom vocabularies

#### Amazon Translate

- Neural machine translation
- Real-time or batch
- 75+ languages
- Customizable

#### Amazon Lex

- Build conversational interfaces
- Chatbots and voice bots
- Same technology as Alexa
- Integrate with Lambda

#### Amazon Textract

- Extract text and data from documents
- OCR and beyond
- Forms and tables
- Handwriting recognition

### **MISSING: Developer Tools**

#### AWS CodeCommit

- Managed source control
- Git-based repositories
- No size limits

#### AWS CodeBuild

- Fully managed build service
- Compile code, run tests
- Continuous scaling
- Pay per minute

#### AWS CodeDeploy

- Automated deployments
- EC2, Lambda, on-premises
- Minimize downtime
- Rollback capabilities

#### AWS CodePipeline

- Continuous delivery service
- Automate release process
- Integrates with third-party tools
- Visual workflow

#### AWS Cloud9

- Cloud-based IDE
- Write, run, debug code
- Collaborate in real-time
- Direct terminal to AWS

#### AWS X-Ray

- Debug and analyze applications
- Distributed tracing
- Service map
- Identify performance bottlenecks

### **MISSING: IoT Services**

#### AWS IoT Core

- Connect IoT devices to cloud
- Billions of devices
- Trillions of messages
- Secure communication
- Rules engine

---

## Domain 4: Billing, Pricing, and Support (12%)

### **MISSING: AWS Pricing Models**

#### Free Tier

- **Always Free**: DynamoDB (25 GB), Lambda (1M requests/month)
- **12 Months Free**: EC2 (750 hours/month), S3 (5 GB)
- **Trials**: SageMaker (2 months), Lightsail (750 hours)

#### Pricing Factors

1. **Compute**: Instance type, duration
2. **Storage**: Amount of data, storage class
3. **Data Transfer**: Outbound data (inbound usually free)

#### EC2 Pricing Models (EXPANDED)

1. **On-Demand**
    
    - Pay per hour/second
    - No commitment
    - Best for: Short-term, unpredictable workloads
2. **Reserved Instances (RI)**
    
    - 1 or 3-year commitment
    - Up to 75% discount
    - **Types**:
        - Standard RI: Cannot change instance type
        - Convertible RI: Can change instance attributes
    - **Payment Options**:
        - All Upfront: Highest discount
        - Partial Upfront: Medium discount
        - No Upfront: Lowest discount
3. **Savings Plans**
    
    - Flexible pricing model
    - Commit to $/hour for 1 or 3 years
    - Up to 72% savings
    - **Types**:
        - Compute Savings Plans: Most flexible
        - EC2 Instance Savings Plans: Specific instance family
4. **Spot Instances**
    
    - Bid on spare capacity
    - Up to 90% discount
    - Can be interrupted with 2-minute warning
    - Best for: Fault-tolerant, flexible workloads
5. **Dedicated Hosts**
    
    - Physical server dedicated to you
    - Use existing licenses (BYOL)
    - Compliance requirements
    - Most expensive
6. **Dedicated Instances**
    
    - Instances run on dedicated hardware
    - May share hardware with other instances in your account
    - Less expensive than Dedicated Hosts

### **MISSING: AWS Cost Management Tools**

#### AWS Pricing Calculator

- Estimate costs before deployment
- Configure services and pricing models
- Share estimates with team
- Export to CSV

#### AWS Cost Explorer

- Visualize and analyze costs
- Historical data up to 12 months
- Forecast up to 12 months
- Filter by service, tag, region
- Identify cost drivers

#### AWS Budgets

- Set custom budgets
- Alerts when exceeding thresholds
- Track costs and usage
- Budget types: Cost, Usage, Reservation, Savings Plans

#### AWS Cost and Usage Report

- Most detailed billing data
- Hourly, daily, monthly reports
- S3 bucket delivery
- Integrate with Athena, Redshift, QuickSight

#### AWS Compute Optimizer

- ML-based recommendations
- Optimize EC2, EBS, Lambda, Auto Scaling
- Reduce costs up to 25%
- Improve performance

#### Cost Allocation Tags

- Track costs by project, department
- User-defined tags
- AWS-generated tags
- Enable in Billing console

### **MISSING: AWS Support Plans**

#### Basic Support (FREE)

- 24/7 customer service
- Documentation, whitepapers
- AWS Trusted Advisor (7 core checks)
- AWS Personal Health Dashboard

#### Developer Support ($29/month or 3% of Monthly AWS usage)

- All Basic features
- Business hours email access
- 1 primary contact
- Response times:
    - General guidance: < 24 hours
    - System impaired: < 12 hours

#### Business Support ($100/month or 10%/7%/5%/3% tiered)

- All Developer features
- 24/7 phone, email, chat
- Unlimited contacts
- Full Trusted Advisor checks
- Infrastructure Event Management (extra fee)
- Response times:
    - General guidance: < 24 hours
    - System impaired: < 12 hours
    - Production system impaired: < 4 hours
    - Production system down: < 1 hour

#### Enterprise On-Ramp ($5,500/month or 10% of Monthly AWS usage)

- All Business features
- Pool of Technical Account Managers (TAMs)
- Concierge Support Team
- Infrastructure Event Management (included)
- Response times:
    - Production system down: < 30 minutes
    - Business-critical system down: < 30 minutes
- Access to proactive programs

#### Enterprise Support ($15,000/month or 10%/7%/5%/3% tiered)

- All Enterprise On-Ramp features
- Designated Technical Account Manager (TAM)
- Operations reviews
- Training and game days
- Well-Architected reviews
- Response times:
    - Business-critical system down: < 15 minutes

### **MISSING: Other AWS Resources**

#### AWS Marketplace

- Digital catalog of software
- Third-party software
- AMIs, SaaS, professional services
- One-click deployment
- Consolidated billing

#### AWS Professional Services

- Global team of experts
- Help achieve business outcomes
- Prescriptive guidance
- Work alongside your team

#### AWS Partner Network (APN)

- Consulting Partners: Help design, build, migrate
- Technology Partners: Software and services on AWS
- Competency Programs
- Partner training and certification

#### AWS Training and Certification

- Free digital training
- Classroom training (paid)
- Certification exams
- Learning paths for different roles

#### AWS Documentation

- User guides, API references
- Tutorials and FAQs
- Best practices guides
- Free and comprehensive

#### AWS Forums

- Community discussions
- Ask questions
- Share knowledge
- AWS staff participation

#### AWS re:Post

- AWS-managed Q&A service
- Replaces forums
- Community-driven
- Expert-reviewed answers

---

## Study Tips for CLF-C02

### Focus Areas

1. **Understand core services**: EC2, S3, RDS, VPC, IAM, Lambda
2. **Security is crucial**: 30% of exam, know shared responsibility
3. **Pricing models**: Especially EC2, S3, and support plans
4. **Use cases**: Know when to use which service
5. **Well-Architected Framework**: All 6 pillars

### Common Pitfalls to Avoid

- Confusing services with similar names (CloudWatch vs CloudTrail)
- Not understanding pricing model differences
- Missing the "sustainability" pillar (newly added)
- Forgetting free tier details
- Overlooking support plan features

### Exam Strategy

- Read questions carefully (look for keywords like "MOST cost-effective", "LEAST operational overhead")
- Eliminate obviously wrong answers first
- Watch for scenarios requiring specific AWS services
- Don't overthink - this is a foundational exam
- Flag uncertain questions and review at end

### Recommended Hands-On Practice

1. Create a free tier AWS account
2. Launch an EC2 instance
3. Create an S3 bucket and upload files
4. Set up IAM users and policies
5. Create a simple VPC
6. Explore the AWS Console interface
7. Use AWS Pricing Calculator

---

## Quick Reference: Service Categories

### Compute

EC2, Lambda, ECS, EKS, Elastic Beanstalk, Lightsail, Batch, Fargate, Outposts

### Storage

S3, EBS, EFS, Storage Gateway, FSx, Backup

### Database

RDS, Aurora, DynamoDB, ElastiCache, Redshift, Neptune, DocumentDB, QLDB, Timestream

### Networking

VPC, CloudFront, Route 53, Direct Connect, VPN, API Gateway, Global Accelerator, ELB

### Security & Identity

IAM, Cognito, Shield, WAF, GuardDuty, Inspector, Macie, KMS, Secrets Manager, Certificate Manager

### Management & Governance

CloudWatch, CloudTrail, Config, Systems Manager, CloudFormation, Trusted Advisor, Organizations, Control Tower

### Analytics

Athena, EMR, Glue, Kinesis, QuickSight, OpenSearch, Data Pipeline

### Application Integration

SNS, SQS, Step Functions, EventBridge, AppFlow

### Migration & Transfer

Migration Hub, DMS, Snow Family, DataSync, Transfer Family

### Machine Learning

SageMaker, Rekognition, Comprehend, Polly, Transcribe, Translate, Lex, Textract

### Developer Tools

CodeCommit, CodeBuild, CodeDeploy, CodePipeline, Cloud9, X-Ray

---

## Additional Topics to Review

### AWS Global Infrastructure

- 33+ geographic regions (as of 2025)
- 105+ availability zones
- 600+ CloudFront edge locations
- Local Zones for ultra-low latency
- Wavelength Zones for 5G applications

### AWS Compliance

- AWS Artifact for compliance reports
- Shared responsibility model variations by service
- Data residency and sovereignty
- Encryption in transit and at rest

### Best Practices

- Design for failure
- Implement elasticity
- Decouple components
- Use appropriate storage solutions
- Secure every layer
- Automate everything
- Monitor and log

---

**Good luck with your AWS Certified Cloud Practitioner exam!** 🚀

# DVA-C02: AWS Certified Developer - Complete Study Notes

## Exam Overview

- **Duration**: 130 minutes
- **Questions**: 65 questions (including 15 unscored)
- **Passing Score**: 720/1000
- **Cost**: $150 USD
- **Question Format**: Multiple choice/multiple response
- **Question Style**: Scenario-based questions
- **Validity**: Valid for three years
- **Exam Code**: DVA-C02 (updated version)

## Exam Domains

1. **Development with AWS Services**: 32%
2. **Security**: 26%
3. **Deployment**: 24%
4. **Troubleshooting and Optimization**: 18%

---

## Domain 1: Development with AWS Services (32%)

### IAM (Identity and Access Management) 101

#### Key Features

- **Centralized Control**: Control of your AWS account
- **Shared Access**: Shared access to your AWS account
- **Granular Permissions**: Fine-grained access control
- **Identity Federation**: Supports well-known identity providers (Active Directory, Facebook, LinkedIn, SAML 2.0)
- **Multi-Factor Authentication (MFA)**: Increased security for accounts and resources
- **Temporary Access**: Temporary credentials for users/devices and services
- **Password Policies**: Custom password rotation and complexity policies
- **Integrated**: Works with many AWS services
- **Compliance**: Supports PCI DSS compliance
- **Free to Use**: No additional charge

#### Core Components

- **Users**: Individual end users (people)
- **Groups**: Collections of users with shared permissions
- **Roles**: Assignable to users, applications, and services for AWS resource access
- **Policies**: JSON documents defining permissions (identity-based and resource-based)

#### Important Concepts

- **IAM Policy Simulator**: Test policies before applying
- **Access Keys**: Programmatic access (Access Key ID + Secret Access Key)
- **Root User**: Complete access - should be secured and not used for daily tasks
- **Principle of Least Privilege**: Grant only necessary permissions
- **IAM Credentials Report**: Account-level report of all users and credential status
- **Access Advisor**: Shows service permissions granted and last accessed

### EC2 (Elastic Compute Cloud)

#### Overview

Secure, resizable compute capacity in the cloud. Virtual machines hosted in AWS instead of your own data center. Designed for web-scale cloud computing.

#### Key Benefits

- Pay only for what you use
- No wasted capacity
- Complete control of instances
- Quick scaling up or down

#### Pricing Options

1. **On-Demand**
    
    - Pay by the hour or second
    - No long-term commitments
    - Good for: short-term, spiky, unpredictable workloads
2. **Reserved Instances**
    
    - 1 or 3 year terms
    - Up to 72% discount
    - Types: Standard, Convertible, Scheduled
    - Good for: steady-state, predictable usage
3. **Spot Instances**
    
    - Purchase unused capacity at up to 90% discount
    - Can be terminated by AWS with 2-minute warning
    - Good for: flexible, fault-tolerant workloads
4. **Dedicated Hosts**
    
    - Physical EC2 server dedicated for your use
    - Good for: licensing requirements, compliance
5. **Savings Plans**
    
    - Commit to 1 or 3 years of usage
    - Up to 72% discount
    - Includes serverless (Lambda, Fargate)
    - Flexible across instance families, sizes, OS, and regions
6. **Pricing Calculator**
    
    - Estimate costs for AWS services
    - Plan your deployments

#### Instance Types

**Naming Convention**: `m5.2xlarge`

- `m` = instance family
- `5` = generation
- `2xlarge` = size

**Categories**:

1. **General Purpose** (T, M families)
    
    - Balanced compute, memory, networking
    - Good for: web servers, code repositories
2. **Compute Optimized** (C family)
    
    - High-performance processors
    - Good for: batch processing, gaming servers, HPC
3. **Memory Optimized** (R, X, Z families)
    
    - Fast performance for large datasets in memory
    - Good for: databases, caching, real-time big data
4. **Accelerated Computing** (P, G, F families)
    
    - Hardware accelerators (GPUs, FPGAs)
    - Good for: machine learning, graphics processing
5. **Storage Optimized** (I, D, H families)
    
    - High sequential read/write to large datasets
    - Good for: NoSQL databases, data warehousing

#### EC2 Key Concepts

- **User Data**: Bootstrap scripts run at instance launch
- **Metadata**: Data about your instance (`http://169.254.169.254/latest/meta-data/`)
- **Security Groups**: Virtual firewalls (stateful)
- **Key Pairs**: SSH access for Linux, password decryption for Windows
- **Placement Groups**: Control instance placement (Cluster, Partition, Spread)
- **EC2 Instance Connect**: Browser-based SSH connection

### EBS (Elastic Block Store)

#### Overview

Block-level storage volumes for EC2 instances. Network-attached storage that persists independently from instance lifecycle.

#### Volume Types

1. **General Purpose SSD (gp3, gp2)**
    
    - **gp3**: Latest generation, 3,000-16,000 IOPS
    - **gp2**: Previous generation, scales with volume size
    - Good for: boot volumes, dev/test environments
2. **Provisioned IOPS SSD (io2, io1)**
    
    - **io2**: 99.999% durability, up to 64,000 IOPS
    - **io1**: Up to 64,000 IOPS
    - **io2 Block Express**: Up to 256,000 IOPS
    - Good for: critical business applications, databases
3. **Throughput Optimized HDD (st1)**
    
    - Low-cost HDD for frequently accessed, throughput-intensive workloads
    - Good for: big data, data warehouses, log processing
4. **Cold HDD (sc1)**
    
    - Lowest cost HDD for less frequently accessed workloads
    - Good for: file servers, backups
5. **Magnetic (standard)** - Previous generation (deprecated)
    

#### Important EBS Features

- **Snapshots**: Point-in-time backups to S3
- **Encryption**: At rest and in transit
- **Multi-Attach**: io1/io2 can attach to multiple instances (same AZ)
- **Elastic Volumes**: Modify size, type, IOPS without downtime
- **EBS-Optimized Instances**: Dedicated throughput

### ELB (Elastic Load Balancing)

#### Load Balancer Types

1. **Application Load Balancer (ALB)**
    
    - **Layer**: 7 (Application layer)
    - **Protocols**: HTTP, HTTPS, WebSocket
    - **Features**:
        - Path-based routing
        - Host-based routing
        - Query string/header routing
        - Support for containers and microservices
        - Integration with ECS, EKS, Lambda
        - Support for HTTP/2 and gRPC
    - **Target Types**: Instances, IPs, Lambda functions
    - **Best for**: Modern web applications, microservices
2. **Network Load Balancer (NLB)**
    
    - **Layer**: 4 (Transport layer)
    - **Protocols**: TCP, UDP, TLS
    - **Features**:
        - Ultra-high performance (millions of requests/sec)
        - Static IP addresses
        - Elastic IP support
        - Preserve source IP
        - Low latency (~100 ms vs ~400 ms for ALB)
    - **Target Types**: Instances, IPs, ALB
    - **Best for**: Extreme performance, TCP/UDP traffic, static IPs
3. **Gateway Load Balancer (GLB)**
    
    - **Layer**: 3 (Network layer)
    - **Purpose**: Deploy, scale, and manage third-party virtual appliances
    - **Use cases**: Firewalls, IDS/IPS, deep packet inspection
    - **Protocol**: GENEVE on port 6081
4. **Classic Load Balancer (CLB)**
    
    - **Layer**: 4 & 7
    - **Protocols**: HTTP, HTTPS, TCP, SSL
    - **Status**: Previous generation (not recommended for new applications)

#### ELB Features

- **Health Checks**: Automatically detect unhealthy targets
- **SSL/TLS Termination**: Offload encryption/decryption
- **Sticky Sessions**: Route requests from same client to same target
- **Cross-Zone Load Balancing**: Distribute evenly across all AZs
- **Connection Draining**: Complete in-flight requests before deregistering
- **Access Logs**: Detailed request information

### Route 53

#### Overview

AWS's scalable DNS and domain registration service.

#### Routing Policies

1. **Simple Routing**
    
    - Single resource serving traffic
    - Multiple IP addresses = random selection
2. **Weighted Routing**
    
    - Route traffic based on assigned weights
    - Good for: A/B testing, gradual migrations
3. **Latency Routing**
    
    - Route to region with lowest latency
    - Good for: global applications
4. **Failover Routing**
    
    - Active-passive failover
    - Requires health checks
    - Good for: DR scenarios
5. **Geolocation Routing**
    
    - Route based on user location
    - Good for: content localization, compliance
6. **Geoproximity Routing**
    
    - Route based on geographic location with bias
    - Requires Route 53 Traffic Flow
7. **Multi-Value Answer Routing**
    
    - Return multiple values (up to 8 healthy records)
    - Not a substitute for ELB

#### Route 53 Features

- **Health Checks**: Monitor endpoint health
- **Traffic Flow**: Visual editor for complex routing
- **Private DNS**: DNS for VPC resources
- **DNSSEC**: Domain name system security extensions
- **Alias Records**: Map to AWS resources (no charge for queries)

### Lambda

#### Overview

Serverless compute service - run code without provisioning servers.

#### Key Concepts

- **Invocation Types**: Synchronous, Asynchronous, Event Source Mapping
- **Execution Time**: Up to 15 minutes
- **Memory**: 128 MB to 10,240 MB (CPU scales with memory)
- **Deployment Package**: Up to 50 MB (zipped), 250 MB (unzipped)
- **Concurrency**: 1,000 concurrent executions per region (can be increased)
- **Environment Variables**: Store configuration (can be encrypted)
- **Layers**: Share code and dependencies across functions
- **Versions**: Immutable versions of function code
- **Aliases**: Pointers to versions (e.g., PROD, DEV)

#### Lambda Triggers

- API Gateway
- S3
- DynamoDB Streams
- Kinesis
- SNS
- SQS
- CloudWatch Events/EventBridge
- ALB
- Cognito
- And many more...

#### Important Features

- **Dead Letter Queues (DLQ)**: Failed async invocations to SQS/SNS
- **Reserved Concurrency**: Guarantee execution capacity
- **Provisioned Concurrency**: Keep functions initialized (reduce cold starts)
- **Function URL**: HTTPS endpoint for Lambda (without API Gateway)
- **Lambda@Edge**: Run Lambda at CloudFront edge locations
- **VPC Access**: Connect to VPC resources
- **EFS Support**: Mount EFS for persistent storage

### API Gateway

#### Overview

Fully managed service to create, publish, maintain, monitor, and secure APIs.

#### API Types

1. **REST API**
    
    - Full-featured API
    - Regional, Edge-optimized, or Private endpoints
    - API keys, resource policies, request/response transformation
2. **HTTP API**
    
    - Simpler, lower cost than REST API
    - Better performance
    - Limited features (no API keys, resource policies)
3. **WebSocket API**
    
    - Two-way communication
    - Good for: chat apps, real-time dashboards

#### Key Features

- **Stages**: Different deployment environments (dev, test, prod)
- **Throttling**: Limit request rates (default: 10,000 rps)
- **Caching**: Cache API responses (TTL 300 seconds default)
- **CORS**: Cross-Origin Resource Sharing configuration
- **Authorization**: IAM, Cognito, Lambda authorizers, API keys
- **Request Validation**: Validate requests before Lambda execution
- **Mapping Templates**: Transform requests/responses
- **Mock Integrations**: Return responses without backend

### DynamoDB

#### Overview

Fully managed NoSQL database service. Provides fast, predictable performance with seamless scalability.

#### Core Concepts

- **Tables**: Collection of items
- **Items**: Collection of attributes (like a row)
- **Attributes**: Data elements (like a column)
- **Primary Key**: Required for each item
    - **Partition Key**: Single attribute
    - **Composite Key**: Partition key + Sort key
- **Secondary Indexes**:
    - **Global Secondary Index (GSI)**: Different partition and sort key
    - **Local Secondary Index (LSI)**: Same partition key, different sort key

#### Capacity Modes

1. **Provisioned**
    
    - Specify reads/writes per second
    - Auto Scaling available
    - More cost-effective for predictable traffic
2. **On-Demand**
    
    - Pay per request
    - Good for unpredictable traffic
    - No capacity planning needed

#### Important Features

- **DynamoDB Streams**: Capture table modifications (24-hour retention)
- **Point-in-Time Recovery**: Restore to any second in last 35 days
- **Global Tables**: Multi-region, multi-active replication
- **DynamoDB Accelerator (DAX)**: In-memory cache (microsecond latency)
- **Transactions**: ACID transactions across multiple items
- **TTL**: Automatic item deletion after expiration
- **Backup and Restore**: On-demand and continuous backups

#### Performance

- **Eventually Consistent Reads**: Default (lower latency)
- **Strongly Consistent Reads**: Most up-to-date data
- **Read/Write Capacity Units**:
    - 1 RCU = 1 strongly consistent read/sec (4 KB)
    - 1 RCU = 2 eventually consistent reads/sec (4 KB)
    - 1 WCU = 1 write/sec (1 KB)

### S3 (Simple Storage Service)

#### Overview

Object storage service with 11 9s (99.999999999%) durability.

#### Storage Classes

1. **S3 Standard**
    
    - Frequent access
    - 99.99% availability
    - ≥3 AZ redundancy
2. **S3 Intelligent-Tiering**
    
    - Automatic cost optimization
    - Moves objects between tiers based on access patterns
3. **S3 Standard-IA (Infrequent Access)**
    
    - Lower cost for infrequent access
    - 99.9% availability
    - Retrieval fee
4. **S3 One Zone-IA**
    
    - Lower cost, single AZ
    - 99.5% availability
    - Good for: recreatable data
5. **S3 Glacier Instant Retrieval**
    
    - Archive with millisecond retrieval
    - Minimum 90-day storage
6. **S3 Glacier Flexible Retrieval**
    
    - Archive with retrieval in minutes to hours
    - Minimum 90-day storage
7. **S3 Glacier Deep Archive**
    
    - Lowest cost
    - Retrieval in 12-48 hours
    - Minimum 180-day storage

#### Key Features

- **Versioning**: Keep multiple versions of objects
- **Object Lock**: WORM (Write Once Read Many) compliance
- **Lifecycle Policies**: Automate transitions and expirations
- **Replication**: Cross-Region Replication (CRR), Same-Region Replication (SRR)
- **Encryption**:
    - **SSE-S3**: S3-managed keys
    - **SSE-KMS**: KMS-managed keys
    - **SSE-C**: Customer-provided keys
    - **Client-Side Encryption**
- **Event Notifications**: Trigger Lambda, SQS, SNS on object operations
- **S3 Transfer Acceleration**: Fast uploads via CloudFront edge locations
- **Multipart Upload**: For objects >100 MB (required for >5 GB)
- **Presigned URLs**: Temporary access to objects
- **S3 Select**: Query data within objects using SQL

### SQS (Simple Queue Service)

#### Overview

Fully managed message queuing service for decoupling components.

#### Queue Types

1. **Standard Queue**
    
    - Unlimited throughput
    - At-least-once delivery
    - Best-effort ordering
    - Default queue type
2. **FIFO Queue**
    
    - Exactly-once processing
    - Strict ordering
    - Up to 3,000 messages/second (with batching: 30,000/sec)
    - Must have `.fifo` suffix

#### Key Concepts

- **Message Retention**: 1 minute to 14 days (default: 4 days)
- **Message Size**: Up to 256 KB (use S3 for larger)
- **Visibility Timeout**: Time message is invisible after being read (default: 30 sec, max: 12 hours)
- **Long Polling**: Reduce empty responses (1-20 seconds)
- **Short Polling**: Default, may return empty responses
- **Dead Letter Queue (DLQ)**: For messages that fail processing
- **Delay Queues**: Postpone message delivery (0-15 minutes)
- **Message Timers**: Per-message delay

#### Best Practices

- Use Long Polling to reduce cost
- Implement idempotency for Standard queues
- Set appropriate Visibility Timeout
- Use DLQ for failed messages
- Batch operations for better throughput

### SNS (Simple Notification Service)

#### Overview

Fully managed pub/sub messaging service for microservices and serverless applications.

#### Key Concepts

- **Topics**: Communication channel for messages
- **Publishers**: Send messages to topics
- **Subscribers**: Receive messages from topics
- **Message Filtering**: Subscribers receive only messages of interest
- **Message Attributes**: Metadata in key-value pairs

#### Subscriber Types

- HTTP/HTTPS
- Email/Email-JSON
- SQS
- Lambda
- SMS
- Mobile push notifications (APNS, FCM, etc.)
- Kinesis Data Firehose

#### Features

- **Fan-out Pattern**: SNS + SQS for parallel processing
- **Message Encryption**: At rest (KMS) and in transit
- **Delivery Retries**: Retry policies for HTTP endpoints
- **FIFO Topics**: Ordered messages with deduplication
- **Message Filtering**: Filter policies using JSON

### Step Functions

#### Overview

Serverless orchestration service for building distributed applications as workflows.

#### Key Concepts

- **State Machines**: Defined in Amazon States Language (JSON)
- **States**: Steps in workflow
    - **Task**: Do work (Lambda, ECS, etc.)
    - **Choice**: Conditional logic
    - **Parallel**: Execute branches in parallel
    - **Wait**: Delay for time period
    - **Succeed/Fail**: Terminal states
    - **Pass**: Pass input to output
    - **Map**: Iterate over array
- **Executions**: Instance of state machine running

#### Workflow Types

1. **Standard Workflows**
    
    - Exactly-once execution
    - Up to 1 year duration
    - Full execution history
2. **Express Workflows**
    
    - At-least-once execution
    - Up to 5 minutes duration
    - High-volume event processing

#### Integration

- Direct integrations with 200+ AWS services
- Optimized integrations: Lambda, ECS, Fargate, Batch, DynamoDB, SNS, SQS, Glue, SageMaker, EMR, Step Functions

### EventBridge (CloudWatch Events)

#### Overview

Serverless event bus service for building event-driven applications.

#### Key Concepts

- **Events**: State changes in AWS services or custom applications
- **Event Buses**: Receive events (default, custom, partner)
- **Rules**: Match events and route to targets
- **Targets**: Where events are sent (Lambda, SQS, SNS, Step Functions, etc.)
- **Schemas**: Define structure of events
- **Archive and Replay**: Store and replay events

#### Event Sources

- AWS services (100+)
- Custom applications
- SaaS applications (partner integrations)

#### Features

- **Event Filtering**: Content-based filtering using JSON patterns
- **Event Transformation**: Transform before sending to target
- **Scheduled Events**: Cron or rate expressions
- **Cross-Account Events**: Send events across accounts
- **Schema Registry**: Discover and manage event schemas

### Systems Manager (SSM)

#### Overview

Unified interface for operational tasks across AWS resources.

#### Key Services

1. **Parameter Store**
    
    - Store configuration and secrets
    - Standard and Advanced parameters
    - Integration with KMS for encryption
    - Versioning and TTL
    - Free for standard parameters
2. **Session Manager**
    
    - Browser-based shell access to instances
    - No SSH keys or bastion hosts needed
    - Logging and auditing
3. **Run Command**
    
    - Execute commands on multiple instances
    - No SSH needed
    - Logging to S3/CloudWatch
4. **Patch Manager**
    
    - Automate OS patching
    - Maintenance windows
5. **State Manager**
    
    - Maintain instance configuration

### Secrets Manager

#### Overview

Managed service to store, retrieve, and rotate secrets.

#### Features

- **Automatic Rotation**: Built-in for RDS, Redshift, DocumentDB
- **Fine-grained Access**: IAM policies
- **Encryption**: At rest using KMS
- **Cross-Region Replication**: Replicate secrets across regions
- **Versioning**: Track secret versions
- **Integration**: Lambda for custom rotation

#### Vs Parameter Store

- **Secrets Manager**: Automatic rotation, higher cost
- **Parameter Store**: Simpler, cheaper, manual rotation

### CloudFormation

#### Overview

Infrastructure as Code (IaC) service to provision AWS resources using templates.

#### Key Concepts

- **Templates**: JSON or YAML files describing resources
- **Stacks**: Collection of resources managed as single unit
- **ChangeSet**: Preview changes before stack update
- **Stack Sets**: Deploy stacks across multiple accounts/regions
- **Drift Detection**: Detect manual changes to resources

#### Template Sections

- **Parameters**: Input values
- **Mappings**: Static variables
- **Conditions**: Conditional resource creation
- **Resources**: AWS resources (required)
- **Outputs**: Values to export
- **Metadata**: Additional information

#### Intrinsic Functions

- `Ref`: Reference parameters or resources
- `Fn::GetAtt`: Get resource attributes
- `Fn::Join`: Join strings
- `Fn::Sub`: Substitute variables
- `Fn::If`: Conditional values
- `Fn::ImportValue`: Import exported values

### Elastic Beanstalk

#### Overview

PaaS for deploying and scaling web applications and services.

#### Supported Platforms

- Java, .NET, PHP, Node.js, Python, Ruby, Go
- Docker (single and multi-container)
- Custom platforms via Packer

#### Components

- **Application**: Container for environments
- **Environment**: Collection of resources
    - **Web Server Environment**: Handles HTTP requests
    - **Worker Environment**: Processes background tasks (SQS)
- **Environment Tier**: Web server or worker
- **Application Version**: Specific iteration of deployable code

#### Deployment Policies

1. **All at once**: Deploy to all instances simultaneously (downtime)
2. **Rolling**: Deploy in batches
3. **Rolling with additional batch**: Deploy to new instances first
4. **Immutable**: Deploy to new instances, then swap
5. **Blue/Green**: Deploy to separate environment, swap URLs
6. **Traffic Splitting**: Canary testing with portion of traffic

#### Configuration

- `.ebextensions/`: Customize resources and environment
- `Dockerrun.aws.json`: Docker configuration
- `Procfile`: Specify command to start application

### CodeCommit

#### Overview

Fully managed source control service using Git.

#### Features

- Standard Git functionality
- Encryption at rest and in transit
- IAM and resource policies for access control
- Integration with CodeBuild, CodePipeline
- Triggers for SNS, Lambda
- Pull requests and code reviews
- No repository size limits

### CodeBuild

#### Overview

Fully managed build service that compiles source code and runs tests.

#### Key Concepts

- **Build Projects**: Configuration for how to build
- **Build Environments**: Docker images with tools
- **buildspec.yml**: Build instructions file
- **Artifacts**: Build outputs stored in S3
- **Source**: CodeCommit, GitHub, Bitbucket, S3

#### buildspec.yml Phases

- **install**: Install dependencies
- **pre_build**: Commands before build
- **build**: Build commands
- **post_build**: Commands after build

#### Features

- Custom Docker images
- Local builds for testing
- Build caching
- Environment variables and Parameter Store integration
- VPC support
- Batch builds

### CodeDeploy

#### Overview

Automated deployment service for applications to EC2, Lambda, ECS, and on-premises servers.

#### Deployment Platforms

1. **EC2/On-Premises**
    
    - In-place or Blue/Green
    - Requires CodeDeploy agent
2. **Lambda**
    
    - Canary, Linear, All-at-once
    - Traffic shifting with aliases
3. **ECS**
    
    - Blue/Green deployments
    - Task set replacements

#### Key Concepts

- **Application**: Name for deployment
- **Deployment Group**: Set of instances or Lambda functions
- **Deployment Configuration**: Rules for deployment
    - CodeDeployDefault.AllAtOnce
    - CodeDeployDefault.HalfAtATime
    - CodeDeployDefault.OneAtATime
    - Custom configurations
- **AppSpec File**: Deployment instructions (appspec.yml)
    - **Hooks**: Lifecycle event scripts

#### AppSpec Hooks (EC2)

1. ApplicationStop
2. DownloadBundle
3. BeforeInstall
4. Install
5. AfterInstall
6. ApplicationStart
7. ValidateService

### CodePipeline

#### Overview

Continuous delivery service for fast and reliable application updates.

#### Components

- **Pipeline**: Workflow for release process
- **Stages**: Logical divisions (Source, Build, Test, Deploy)
- **Actions**: Tasks performed within stages
- **Transitions**: Connection between stages
- **Artifacts**: Files passed between stages

#### Integrations

- **Source**: CodeCommit, GitHub, S3, ECR
- **Build**: CodeBuild, Jenkins
- **Test**: CodeBuild, third-party tools
- **Deploy**: CodeDeploy, Elastic Beanstalk, CloudFormation, ECS, S3
- **Approval**: Manual approval actions

### CodeArtifact

#### Overview

Managed artifact repository service for software packages.

#### Features

- Support for npm, Maven, Gradle, pip, NuGet, generic
- Integrate with CodeBuild, CodePipeline
- Cache from public repositories
- Domain-based hierarchy
- Resource policies for access control
- Upstream repositories

### CodeStar

#### Overview

Unified interface for software development activities (deprecated in favor of separate services).

#### Features

- Quick project setup
- Integrated dashboard
- Templates for common application types
- Integration with Code services, Cloud9, Jira

### X-Ray

#### Overview

Distributed tracing service for analyzing and debugging production applications.

#### Key Concepts

- **Segments**: Work done by single component
- **Subsegments**: Granular detail within segment
- **Traces**: Collection of segments for single request
- **Sampling**: Control amount of data recorded
- **Annotations**: Indexed key-value pairs for filtering
- **Metadata**: Non-indexed key-value pairs

#### Components

- **X-Ray Daemon**: Listens for traffic and relays to X-Ray API
- **X-Ray SDK**: Instrument application code
- **X-Ray Service Map**: Visual representation of application

#### Integration

- Lambda (built-in support)
- API Gateway
- ELB
- EC2 (install daemon)
- ECS (daemon in container)
- Elastic Beanstalk (configure)

### CloudWatch

#### Overview

Monitoring and observability service for AWS resources and applications.

#### Components

1. **Metrics**
    
    - Time-ordered data points
    - Standard and Custom metrics
    - Resolution: 1 second (high-resolution) or 60 seconds
    - Retention: 15 months
2. **Alarms**
    
    - Watch metrics and trigger actions
    - States: OK, ALARM, INSUFFICIENT_DATA
    - Actions: SNS, Auto Scaling, EC2 actions, Systems Manager
3. **Logs**
    
    - Collect, monitor, and analyze log files
    - **Log Groups**: Collection of log streams
    - **Log Streams**: Sequence of log events
    - **Metric Filters**: Create metrics from logs
    - **Insights**: Query and analyze logs
    - **Retention**: Configurable (never expire to 10 years)
    - **Export**: To S3 or stream to Lambda, Kinesis
4. **Events / EventBridge**
    
    - See EventBridge section above

#### Common Metrics

- **EC2**: CPUUtilization, NetworkIn/Out, DiskReadOps/WriteOps
- **EBS**: VolumeReadBytes, VolumeWriteBytes
- **ELB**: RequestCount, TargetResponseTime, HTTPCode_Target_4XX
- **Lambda**: Invocations, Duration, Errors, Throttles
- **DynamoDB**: UserErrors, SystemErrors, ConsumedReadCapacityUnits

### CloudTrail

#### Overview

Service for governance, compliance, and auditing of AWS account activity.

#### Features

- Records API calls (console, SDK, CLI, AWS services)
- Delivers logs to S3
- Integration with CloudWatch Logs
- Event history: 90 days in console
- **Trails**: Long-term storage and analysis
    - Management events (default)
    - Data events (S3 object-level, Lambda invocations)
    - Insights events (unusual activity detection)

#### Use Cases

- Security analysis
- Compliance auditing
- Troubleshooting
- Change tracking

---

## Domain 2: Security (26%)

### KMS (Key Management Service)

#### Overview

Managed service to create and control encryption keys.

#### Key Types

1. **Customer Managed Keys (CMK)**
    
    - Full control
    - Rotation policy
    - Key policies
2. **AWS Managed Keys**
    
    - Created by AWS services
    - Automatic rotation every year
    - View but not manage
3. **AWS Owned Keys**
    
    - Used by AWS services
    - Not visible to customers

#### Key Concepts

- **Encryption**: Up to 4 KB data directly
- **Envelope Encryption**: Encrypt data keys for large data
- **Data Keys**: Used to encrypt large amounts of data
- **Key Policies**: Resource-based policies (required)
- **Grants**: Temporary permissions
- **Automatic Rotation**: Every year for CMKs
- **Manual Rotation**: Create new key, use alias

#### Integration

- S3, EBS, RDS, DynamoDB, Lambda, and many more
- CloudTrail logs all key usage

### IAM Best Practices (Security Focus)

#### Access Management

- Enable MFA for root and privileged users
- Use roles instead of access keys
- Rotate credentials regularly
- Apply least privilege principle
- Use groups to assign permissions
- Use IAM Access Analyzer to identify public resources

#### Policies

- **Identity-based**: Attached to users, groups, roles
- **Resource-based**: Attached to resources (S3 buckets, SQS queues, etc.)
- **Permission Boundaries**: Maximum permissions
- **Service Control Policies (SCPs)**: AWS Organizations policies

#### Policy Evaluation Logic

1. Explicit Deny (always wins)
2. Explicit Allow
3. Implicit Deny (default)

### Cognito

#### Overview

User authentication and authorization service for web and mobile apps.

#### Components

1. **User Pools**
    
    - User directory for authentication
    - Sign-up and sign-in functionality
    - MFA, password policies
    - Social identity providers (Facebook, Google, Amazon)
    - SAML identity providers
    - Lambda triggers for custom workflows
    - JWT tokens
2. **Identity Pools (Federated Identities)**
    
    - Grant temporary AWS credentials
    - Access AWS services directly
    - Supports authenticated and unauthenticated users
    - Integrate with User Pools, social providers, SAML

#### Token Types

- **ID Token**: User identity information
- **Access Token**: Access to resources
- **Refresh Token**: Get new tokens

#### Common Patterns

- User Pool for authentication → Get JWT
- Exchange JWT for temporary AWS credentials via Identity Pool
- Use credentials to access AWS services

### Secrets Rotation

#### Best Practices

- Use Secrets Manager for automatic rotation
- Rotate credentials regularly
- Use different secrets for different environments
- Version secrets
- Audit secret access with CloudTrail

### Encryption

#### Types

1. **Encryption at Rest**
    
    - S3: SSE-S3, SSE-KMS, SSE-C
    - EBS: KMS encryption
    - RDS: KMS encryption
    - DynamoDB: KMS encryption
2. **Encryption in Transit**
    
    - HTTPS/TLS
    - VPN
    - Direct Connect with MACsec

#### Certificate Management

- **AWS Certificate Manager (ACM)**
    - Free SSL/TLS certificates
    - Automatic renewal
    - Integration with ELB, CloudFront, API Gateway
    - Cannot export certificates (use ACM Private CA for that)

### VPC Security

#### Security Groups

- Stateful firewall
- Allow rules only
- Applied at instance level
- Default: Allow all outbound, deny all inbound

#### Network ACLs

- Stateless firewall
- Allow and deny rules
- Applied at subnet level
- Default: Allow all inbound and outbound
- Rules processed in order

#### VPC Flow Logs

- Capture IP traffic information
- Published to CloudWatch Logs or S3
- Useful for security analysis and troubleshooting

### Compliance

#### Services

- **AWS Artifact**: Access to compliance reports
- **AWS Config**: Assess, audit, evaluate resource configurations
- **GuardDuty**: Threat detection service
- **Inspector**: Automated security assessment
- **Macie**: Discover and protect sensitive data in S3
- **Security Hub**: Central security and compliance view

---

## Domain 3: Deployment (24%)

### CI/CD Concepts

#### Continuous Integration

- Frequent code merges to central repository
- Automated builds and tests
- Detect errors quickly

#### Continuous Delivery

- Automated deployment to staging/production
- Manual approval before production
- Always ready to deploy

#### Continuous Deployment

- Fully automated deployment to production
- No manual approval
- Every change goes through pipeline

### Docker and Containers

#### Docker Basics

- **Image**: Read-only template
- **Container**: Running instance of image
- **Dockerfile**: Instructions to build image
- **Registry**: Repository for images (ECR, Docker Hub)

#### Common Dockerfile Instructions

- `FROM`: Base image
- `RUN`: Execute commands
- `COPY/ADD`: Copy files
- `WORKDIR`: Set working directory
- `EXPOSE`: Document ports
- `CMD/ENTRYPOINT`: Default command

### ECS (Elastic Container Service)

#### Overview

Fully managed container orchestration service.

#### Launch Types

1. **EC2 Launch Type**
    
    - Run containers on EC2 instances you manage
    - More control over infrastructure
    - Use EC2 pricing
2. **Fargate Launch Type**
    
    - Serverless compute for containers
    - No infrastructure management
    - Pay per task

#### Key Concepts

- **Task Definition**: Blueprint for application (JSON)
    - Image, CPU, memory, environment variables, ports, volumes
- **Task**: Running instance of task definition
- **Service**: Maintains desired count of tasks
- **Cluster**: Logical grouping of tasks/services
- **Container Agent**: Runs on each EC2 instance (EC2 launch type)

#### Task Placement Strategies (EC2 Launch type)

- **binpack**: Minimize instances used
- **random**: Random placement
- **spread**: Spread across specified value (AZ, instance type)

#### Service Load Balancing

- ALB (recommended)
- NLB
- Classic Load Balancer

### ECR (Elastic Container Registry)

#### Overview

Fully managed Docker container registry.

#### Features

- Private registries
- Encryption at rest (S3) and in transit
- Integration with ECS, EKS
- Image scanning for vulnerabilities
- Lifecycle policies for image cleanup
- Cross-region and cross-account replication
- Pull through cache (proxy for public registries)

### EKS (Elastic Kubernetes Service)

#### Overview

Managed Kubernetes service.

#### Key Concepts

- **Control Plane**: Managed by AWS
- **Worker Nodes**: EC2 instances or Fargate
- **Node Groups**: Collection of EC2 instances
- **Pods**: Smallest deployable units
- **Services**: Expose applications

#### Features

- Highly available (multi-AZ control plane)
- Integration with AWS services (IAM, VPC, ELB, ECR)
- Managed node groups
- Fargate support
- Auto Scaling

### Blue/Green Deployments

#### Concept

- Two identical environments (Blue = current, Green = new)
- Test Green environment
- Switch traffic from Blue to Green
- Keep Blue for quick rollback

#### Implementation in AWS

- Route 53 weighted routing
- ELB target groups
- Elastic Beanstalk
- CodeDeploy
- CloudFormation with Lambda

### Canary Deployments

#### Concept

- Gradually shift traffic to new version
- Monitor metrics
- Roll back if issues detected
- Full rollout if successful

#### Implementation

- API Gateway canary settings
- Lambda versions and aliases with weighted routing
- CodeDeploy with Lambda or ECS

### Auto Scaling

#### Types

1. **EC2 Auto Scaling**
    
    - **Auto Scaling Groups (ASG)**
    - Launch Template/Configuration
    - Scaling Policies:
        - **Target Tracking**: Maintain metric target
        - **Step Scaling**: Scale based on CloudWatch alarms
        - **Simple Scaling**: Single scaling adjustment
        - **Scheduled Scaling**: Scale at specific times
    - **Lifecycle Hooks**: Custom actions during launch/termination
    - **Termination Policies**: Which instances to terminate
2. **Application Auto Scaling**
    
    - ECS services
    - DynamoDB tables
    - Aurora replicas
    - Lambda provisioned concurrency
    - And more...
3. **AWS Auto Scaling**
    
    - Unified scaling across services
    - Predictive scaling

#### Scaling Cooldowns

- Prevents thrashing
- Default: 300 seconds
- Simple scaling policy only

### CloudFormation Advanced

#### Nested Stacks

- Reuse common template patterns
- Max 5 levels deep

#### Stack Sets

- Deploy stacks across multiple accounts and regions
- Requires permissions in target accounts

#### Custom Resources

- Extend CloudFormation with Lambda
- Handle resources not natively supported
- Lifecycle events: Create, Update, Delete

#### Helper Scripts (cfn-init, cfn-signal)

- **cfn-init**: Retrieve and interpret metadata
- **cfn-signal**: Signal creation/update status
- **cfn-hup**: Detect metadata changes and run commands

### SAM (Serverless Application Model)

#### Overview

Framework for building serverless applications. Extension of CloudFormation.

#### Key Features

- Simplified syntax for serverless resources
- **sam cli**: Local testing and debugging
- **Transform**: AWS::Serverless-2016-10-31
- Supports Lambda, API Gateway, DynamoDB, Step Functions

#### Template Sections

```yaml
Transform: AWS::Serverless-2016-10-31
Globals:
  Function:
    Timeout: 3
    Runtime: python3.9
Resources:
  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: function/
      Handler: app.lambda_handler
      Events:
        MyApi:
          Type: Api
          Properties:
            Path: /hello
            Method: get
```

#### SAM CLI Commands

- `sam init`: Initialize project
- `sam build`: Build application
- `sam local start-api`: Run API locally
- `sam local invoke`: Invoke function locally
- `sam deploy`: Deploy to AWS
- `sam logs`: Fetch logs

### Deployment Strategies Summary

|Strategy|Downtime|Rollback Speed|Cost|Complexity|
|---|---|---|---|---|
|All at once|Yes|Slow|Low|Low|
|Rolling|No|Slow|Low|Medium|
|Blue/Green|No|Instant|High|High|
|Canary|No|Fast|Medium|High|
|Immutable|No|Fast|Medium|Medium|

---

## Domain 4: Troubleshooting and Optimization (18%)

### Lambda Optimization

#### Performance

- **Memory Allocation**: More memory = more CPU
- **Timeout**: Set appropriately (max 15 minutes)
- **Cold Starts**:
    - Keep functions warm with provisioned concurrency
    - Minimize package size
    - Use Lambda layers for dependencies
    - Initialize SDK clients outside handler
- **Environment Variables**: Use for configuration
- **VPC**: Adds latency (use only when needed)

#### Debugging

- **CloudWatch Logs**: All console output goes here
- **X-Ray**: Distributed tracing
- **Lambda Insights**: Enhanced monitoring
- **Environment Variables**: Add debug flags

#### Common Errors

- **Timeout**: Function exceeds configured timeout
- **Out of Memory**: Increase memory allocation
- **Throttling**: Concurrent execution limit reached
- **Permission Errors**: Check execution role

### DynamoDB Performance

#### Optimization

- **Partition Key Design**: Distribute data evenly
- **Use GSI/LSI**: For different query patterns
- **Batch Operations**: BatchGetItem, BatchWriteItem
- **DAX**: Microsecond latency for reads
- **Projection**: Return only needed attributes
- **Parallel Scans**: Split scan across multiple workers

#### Common Issues

- **Hot Partitions**: Uneven key distribution
- **Throttling**: Exceeding provisioned capacity
    - Solution: Enable Auto Scaling, use On-Demand mode
- **Large Items**: Items >400 KB (max)
- **GSI Throttling**: Independent of table throughput

### API Gateway Troubleshooting

#### Performance

- **Caching**: Enable response caching (TTL 300-3600 seconds)
- **Throttling**: Set account and per-stage limits
- **Integration Timeout**: Max 29 seconds
- **Payload Size**: Max 10 MB

#### Common Issues

- **429 Too Many Requests**: Throttling
- **502 Bad Gateway**: Backend errors
- **504 Gateway Timeout**: Integration timeout (29 seconds)
- **CORS Errors**: Configure CORS headers

#### Debugging

- **CloudWatch Logs**: Enable detailed logging
- **CloudWatch Metrics**: Monitor requests, latency, errors
- **X-Ray**: Trace requests through API and downstream services

### ELB Troubleshooting

#### Health Checks

- Ensure targets pass health checks
- Check health check configuration (path, timeout, interval)
- Review security groups

#### Common Issues

- **502 Bad Gateway**: Application error
- **503 Service Unavailable**: No healthy targets
- **504 Gateway Timeout**: Timeout waiting for response
- **Intermittent 502s**: Connection issues with targets

#### Monitoring

- **CloudWatch Metrics**: RequestCount, TargetResponseTime, HTTPCode_*
- **Access Logs**: Detailed request information (S3)
- **Connection Draining**: Allow in-flight requests to complete

### EC2 Troubleshooting

#### Instance Access

- **Cannot SSH**:
    - Check security group (port 22)
    - Check Network ACL
    - Verify key pair
    - Check instance status
- **Cannot RDP**: Check security group (port 3389)

#### Performance

- **High CPU**: Scale up or scale out
- **Status Checks**:
    - **System Status**: AWS infrastructure (restart to fix)
    - **Instance Status**: OS/application (troubleshoot inside instance)

#### Common Issues

- **Instance Store Lost**: Instance stopped/terminated
- **EBS Volume Not Available**: Check attachment, mount point
- **Burst Balance Depleted** (T instances): Upgrade to larger instance or unlimited mode

### CloudWatch Alarms

#### Best Practices

- Use multiple data points for evaluation
- Set appropriate threshold
- Use anomaly detection for dynamic thresholds
- Test alarms with SetAlarmState API

#### Common Metrics to Monitor

- **EC2**: CPUUtilization, StatusCheckFailed
- **ELB**: HealthyHostCount, UnHealthyHostCount
- **Lambda**: Errors, Throttles, Duration
- **DynamoDB**: UserErrors, SystemErrors, ConsumedCapacity
- **RDS**: CPUUtilization, DatabaseConnections, FreeStorageSpace

### Cost Optimization

#### Strategies

1. **Right-sizing**: Use appropriate instance/resource sizes
2. **Reserved Capacity**: RIs, Savings Plans for steady state
3. **Spot Instances**: For fault-tolerant workloads
4. **S3 Lifecycle Policies**: Move to cheaper storage classes
5. **Delete Unused Resources**: EBS volumes, snapshots, EIPs
6. **Use CloudWatch to Monitor**: Identify underutilized resources

#### Tools

- **Cost Explorer**: Visualize costs and usage
- **Budgets**: Set custom cost and usage budgets
- **Trusted Advisor**: Recommendations for cost optimization
- **Compute Optimizer**: Right-sizing recommendations

### Logging and Monitoring Best Practices

#### CloudWatch Logs

- Use log groups for organization
- Set retention periods
- Create metric filters for important patterns
- Use Logs Insights for querying

#### X-Ray

- Instrument critical paths
- Use annotations for filtering
- Sample appropriately
- Enable in all environments

#### CloudTrail

- Enable in all regions
- Configure S3 lifecycle for log retention
- Use CloudWatch Logs integration for alerting
- Enable log file validation

---

## Additional Topics

### RDS (Relational Database Service)

#### Overview

Managed relational database service supporting multiple database engines.

#### Supported Engines

- Amazon Aurora (MySQL/PostgreSQL compatible)
- MySQL
- PostgreSQL
- MariaDB
- Oracle
- SQL Server

#### Key Features

- **Automated Backups**: 1-35 day retention (enabled by default)
- **Manual Snapshots**: User-initiated (retained until deleted)
- **Multi-AZ**: High availability (synchronous replication)
- **Read Replicas**: Scalability (asynchronous replication)
    - Up to 5 replicas per source
    - Cross-region support
    - Can be promoted to standalone database
- **Encryption**: At rest (KMS) and in transit (SSL/TLS)
- **Enhanced Monitoring**: OS-level metrics
- **Performance Insights**: Database performance tuning

#### Aurora Specific

- **Aurora Serverless**: Auto-scaling, pay per second
- **Aurora Global Database**: Cross-region replication (<1 second lag)
- **Backtrack**: Rewind to previous point in time (MySQL)
- **Parallel Query**: Faster analytical queries

### ElastiCache

#### Overview

In-memory caching service supporting Redis and Memcached.

#### Redis Vs Memcached

|Feature|Redis|Memcached|
|---|---|---|
|Data Types|Advanced (lists, sets, sorted sets)|Simple (strings)|
|Persistence|Yes|No|
|Backup/Restore|Yes|No|
|Multi-AZ|Yes (automatic failover)|No|
|Read Replicas|Yes|No (multi-node)|
|Sorting/Ranking|Yes|No|
|Pub/Sub|Yes|No|
|Multi-threaded|No|Yes|

#### Use Cases

- **Database Caching**: Reduce database load
- **Session Store**: Stateless applications
- **Real-time Analytics**: Leaderboards, counting
- **Message Broker**: Pub/Sub patterns (Redis)

### Kinesis

#### Overview

Platform for streaming data on AWS.

#### Services

1. **Kinesis Data Streams**
    
    - Real-time data streaming
    - **Shards**: Unit of throughput (1 MB/sec in, 2 MB/sec out)
    - **Data Retention**: 24 hours default, up to 365 days
    - **Producers**: SDK, KPL, Kinesis Agent
    - **Consumers**: SDK, KCL, Lambda, Kinesis Data Firehose, Kinesis Data Analytics
2. **Kinesis Data Firehose**
    
    - Load streaming data into data stores
    - **Destinations**: S3, Redshift, Elasticsearch, Splunk, HTTP endpoints
    - **Near real-time**: Buffer interval 60-900 seconds
    - **Transformations**: Lambda functions
    - **No retention**: Data immediately delivered
3. **Kinesis Data Analytics**
    
    - Real-time analytics using SQL or Apache Flink
    - **Sources**: Kinesis Data Streams, Kinesis Data Firehose
    - **Destinations**: Kinesis Data Streams, Kinesis Data Firehose, Lambda
4. **Kinesis Video Streams**
    
    - Stream video from devices to AWS
    - **Use cases**: Security, computer vision, ML

### Athena

#### Overview

Serverless interactive query service for S3 data using SQL.

#### Features

- Pay per query (data scanned)
- Supports CSV, JSON, Parquet, ORC, Avro
- Integration with Glue Data Catalog
- JDBC/ODBC drivers
- Use partitions and columnar formats to reduce costs

### Glue

#### Overview

Serverless ETL (Extract, Transform, Load) service.

#### Components

- **Glue Data Catalog**: Metadata repository
- **Glue Crawlers**: Discover and catalog data
- **Glue ETL Jobs**: Transform data
    - Python or Scala
    - Serverless Apache Spark
- **Glue DataBrew**: Visual data preparation

#### Use Cases

- Prepare data for analytics
- Discover data schemas
- ETL workflows

### SES (Simple Email Service)

#### Overview

Email sending and receiving service.

#### Features

- Send transactional and marketing emails
- Receive emails and process with Lambda
- Template support
- Configuration sets for tracking
- Dedicated IP addresses
- Pay as you go

#### Sending Limits

- Sandbox: Limited sending (verification required)
- Production: Higher limits, no verification

### AppSync

#### Overview

Managed GraphQL service for application data queries.

#### Features

- Real-time subscriptions
- Offline data sync
- Multiple data sources (DynamoDB, Lambda, HTTP, RDS, OpenSearch)
- Fine-grained access control
- Caching
- Schema-driven development

---

## Exam Tips

### General Tips

1. **Read questions carefully**: Identify key requirements
2. **Eliminate wrong answers**: Narrow down choices
3. **Look for keywords**: "Highly available", "Cost-effective", "Least operational overhead"
4. **Time management**: ~2 minutes per question
5. **Flag and review**: Mark uncertain questions for review

### Common Scenarios

#### High Availability

- Multi-AZ deployments
- Auto Scaling
- ELB across multiple AZs
- Route 53 health checks and failover

#### Security

- Least privilege with IAM
- Encryption at rest and in transit
- Security groups and NACLs
- Secrets Manager for credentials
- VPC for network isolation

#### Cost Optimization

- Reserved Instances/Savings Plans for steady state
- Spot Instances for flexible workloads
- S3 Lifecycle policies
- Right-sizing resources
- Serverless where appropriate

#### Performance

- Caching (CloudFront, ElastiCache, DAX, API Gateway)
- Read replicas for read-heavy workloads
- DynamoDB with proper key design
- Lambda provisioned concurrency
- CDN for static content

#### Decoupling

- SQS for asynchronous processing
- SNS for pub/sub
- EventBridge for event routing
- Step Functions for workflows
- ELB for load distribution

### Service Selection

- **Compute**: Lambda (event-driven), EC2 (full control), ECS/EKS (containers), Fargate (serverless containers)
- **Storage**: S3 (objects), EBS (block), EFS (shared file system)
- **Database**: RDS (relational), DynamoDB (NoSQL), ElastiCache (in-memory)
- **Integration**: SQS (queue), SNS (notifications), EventBridge (event bus), Step Functions (orchestration)

---

## Study Resources

### Official AWS Resources

- AWS Developer Learning Path
- AWS Whitepapers (Well-Architected Framework)
- AWS Documentation
- AWS re:Post (Q&A community)
- AWS Skill Builder (free training)

### Practice

- AWS Free Tier (hands-on practice)
- Sample questions from AWS
- Practice exams
- AWS Workshops

### Review

- Service FAQs
- Service limits and quotas
- Pricing models
- Integration patterns

---

## Quick Reference Tables

### Compute Services Comparison

|Service|Use Case|Control Level|Pricing|
|---|---|---|---|
|EC2|Full control, any workload|High|Per hour/second|
|Lambda|Event-driven, serverless|Low|Per request + duration|
|Fargate|Containers, serverless|Medium|Per task|
|Elastic Beanstalk|Quick deployments, PaaS|Low|EC2 pricing|

### Storage Services Comparison

|Service|Type|Use Case|Durability|
|---|---|---|---|
|S3|Object|Files, backups, static websites|11 9s|
|EBS|Block|Database, boot volumes|99.8-99.9%|
|EFS|File|Shared file system|11 9s|
|Instance Store|Block|Temporary, high performance|Lost on stop/terminate|

### Database Services Comparison

|Service|Type|Scalability|Use Case|
|---|---|---|---|
|RDS|SQL|Vertical|OLTP, structured data|
|DynamoDB|NoSQL|Horizontal|High scale, low latency|
|Aurora|SQL|Auto-scaling|High performance, MySQL/PostgreSQL|
|ElastiCache|In-memory|Horizontal|Caching, session store|
|Redshift|SQL|Cluster|Data warehousing, OLAP|

### Integration Services Comparison

|Service|Pattern|Ordering|Retention|
|---|---|---|---|
|SQS Standard|Queue|Best effort|14 days|
|SQS FIFO|Queue|Strict|14 days|
|SNS|Pub/Sub|N/A|Immediate|
|EventBridge|Event bus|N/A|24 hours (archive)|
|Kinesis|Stream|Per shard|24 hours - 365 days|

---

## Key Takeaways for the Exam

1. **Serverless First**: Prefer serverless options when possible (Lambda, DynamoDB, S3)
2. **Security**: Always encrypt, use IAM roles, principle of least privilege
3. **High Availability**: Multi-AZ deployments, Auto Scaling, health checks
4. **Cost Optimization**: Use appropriate pricing models, right-size resources
5. **Monitoring**: CloudWatch for metrics/logs, X-Ray for tracing, CloudTrail for auditing
6. **Infrastructure as Code**: CloudFormation for reproducibility
7. **CI/CD**: Automate build, test, deploy with Code services
8. **Decoupling**: Use queues and event buses to decouple components

---

**Good luck with your AWS Certified Developer exam!** 🚀

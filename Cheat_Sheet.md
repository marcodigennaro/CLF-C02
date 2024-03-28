# AWS Cloud Practitioner Certification Cheat Sheet
# Notes for the CLF-C02 exam

### Intro
- 3 Deployment Methods Private, Public, Hybrid
- 5 Characteristics of CC 
- 4 Benefits of CC: Agility, Elasticity, Cost Savings, Deploy globally in minutes 
- 3 types of CC IaaS, PaaS, SaaS

### 6 Categories and colors
- Orange: Compute
- Purple: Network
- Pink: Governance and Monitoring
- Blue: Database
- Red: Security
- Green: Storage

### Pricing 
- Compute: by CPU time
- Storage: by MB stored
- Network: only data leaving the cloud

### Regions
- Clusters of data centers
- Compliance, Proximity, Latency
- Available services
- Edge Locations
- AWS Regional Services List

### Well Architected Framework - 6 pillars
- Operational Excellence
- Security
- Reliability
- Performance
- Cost Optimization
- Sustainability
  
### IAM (Identity and Access Management)
- Authorization vs Authentication
- Users mapped to a physical user, has a password for AWS Console
- Groups Contains Users only
- **Policies** = JSON document that outlines permissions for users or groups
  - Best practices:   
- **Roles** = For EC2 instants or AWS services
  - Best practices: 
- Security MFA + Password Policy
- **AWS CLI** Manage your AWS services using the Command Line Interface
- **AWS SDK** Manage your AWS services using a programming language Software Development Kit
- Access Keys Access AWS using the CLI or SDK
- Audit IAM Credential Reports & IAM Access Advisor

### EC2 (Elastic Compute Cloud)
- EC2 Instance
  - Boot strapping: lauch command when computer starts , aka automate boot tasks
  - AMI(OS) + Instance Size (CPU + RAM) + Storage + Security Group + EC2 User Data
- Security Groups — Firewall attached to the EC2 instance
- EC2 User Data — Script launched at the first start of an instance
- SSH — Start terminal into our EC2 Instances (port 22)
- EC2 Instance Role — Link to IAM roles
- Purchasing Options:
  - On-demand
  - Reserved (Standard + Convertible)
  - Serving Plans
  - Spot Instances
  - Dedicated Host
  - Dedicated Instance
  - Capacity Reservation

### Storage
- **S3** Simple Storage Service. Objects have key, data, metadata.
- **EFS** Elastic File System. No root storage, mounted to store data
  - **EFS IA** Infrequent Access
- **EBS** Elastic Block Store = Block based storage for EC2
- **AMI** Amazon Machine Image
- **EC2** Instance Store -> short term storage
- Access: standard, infrequent, archivial ( = glacier )

| Object | Block | File |
|--------|-------|------|
| S3     | EBS   | EFS, FxS |

### Amazon S3
- Can not be attached to EC2 instance
- accessed by REST API
- Buckets vs Objects — global unique name, tied to a region
- S3 Security — IAM policy, S3 Bucket Policy (public access), S3 Encryption
- S3 Websites — Host a static website on Amazon S3
- S3 Versioning — Multiple versions for files, prevent accidental deletes
- S3 Replication — Same-region or cross-region, must enable versioning
- S3 Storage Classes — Standard, IA, 1Z-IA, Intelligent, Glacier (Instant, Flexible, Deep)
- Snow Family
  — Import data onto S3 through a physical device, edge computing
  - Compute optimized vs Storage optimized
  - SnowCone & SnowCone SSD — Storage capacity → 8TB HDD, 14TB SSD, Storage capacity → 8TB size up to 24TB, online and offline
  - Snowball Edge & Storage Optimized — Storage capacity → 80TB usable, Storage capacity → up to Petabytes, offline
  - SnowMobile — Storage capacity → < 100PB, Storage capacity → up to Exabytes, offline
- OpsHub — Desktop application to manage Snow Family devices
- Storage Gateway — Hybrid solution to extend on-premises storage to S3 

### EC2 Instance Storage
- **EBS** = Elastic Block Store
  - Network drives attached to one EC2 instance at a time
  - Mapped to an Availability Zones
  - Can use EBS Snapshots for backups/transferring EBS volumes across AZ
- **AMI** — Create ready-to-use EC2 instance with our customisations
- **EC2 Image Builder** — Automatically build, test, and distribute AMIs
- **EC2 Instance Store**
  - High-performance hardware disk attached to our EC2 instance
  - Lost if our instance is stopped/terminated
- **EFS** — Network file system, can be attached to 100s of instances in a region
- **EFS-IA** — Cost-optimized storage class of Infrequent Access file
- FSx for Windows — Network File System for Windows servers
- FSx for Lustre — High-Performance Computing Linux file system

### ELB & ASG
- High Availability vs Scalability (vertical and horizontal) vs Elasticity vs Agility in the Cloud
- Elastic Load Balancers (ELB):
  - Distribute traffic across backend EC2 instances, can be Multi-AZ
  - Supports health checks
  - 4 types: Classic (old), Application (HTTP-L7), Network (TCP-L4), Gateway (L3)
- Auto Scaling Groups (ASG):
  - Most effective way of ensuring that a website is highly available
    - Define: minumum size, actual/desired size and maximum size  
  - Implement Elasticity for your application, across multiple AZ
  - Scale EC2 instances based on the demand on your system, and replace unhealthy
  - Integrated with the ELB

### Databases & Analytics
- Database vs Engine
- Non Relational Databases: Need for speed = key + value
  - **DynamoDB (serverless)
  - **DAX (cache for DynamoDB)
- RDS = Relational Database Service 
  - **RDS**: SQL, No OS access 
  - **Aurora**: SQL, cloud native engine, built-in security, continuous backup, serverless compute
  - **DMS**: Database Migration Service
  - **Redshift** (SQL) - Warehouse-OLAP
- Multi-AZ, Read Replicas, Multi-Region In-memory Database
- **Neptune**: graphs 
- **QuckSight** — Dashboard on your data (serverless)
- **ElasticCache**
- **Athena** — Query data on Amazon S3 (serverless & SQL)
- **DocumentDB** — “Aurora for MongoDB” (JSON- NoSQL database)
- **Amazon QLDB** — Financial Transactions Ledger (immutable journal, cryptographically verifiable)
- **Amazon Managed Blockchain** — managed Hyperledger Fabric & Ethereum blockchains
- **Glue** - Extract Transform Load
- **EMR** - Hadoop Cluster
- **ECS** = Elastic Container Server
  - Docker, containers to deploy apps
  - Fargate: no instance creation
  - ECRegisty
- **Time Stream**
- **Quick Sight**

### Serverless Compute: FaaS
- **Lamba** — Serverless, FaaS, seamless scaling, reactive 
  - **Lambda Billings**
    - By the time run x by the RAM Provisioned
    - By the number of invocations
  - Language Support — Many programming languages except (arbitrary) Docker
  - Invocation time — up to 15 minutes
- **Other Computes**
  - **ECS** Elastic Container Service — Run docker containers on EC2 instance
  - **Fargate**
    - Run Docker containers without provisioning the infrastructure
    - Serverless offering (no EC2 instances)
  - **ECR** Elastic Container Registr) — Private Docker Image Repository
  - **Batch** — Run batch jobs on AWS across managed EC2 instance
  - **Lightsail** — Predictable & low pricing for simple applications & DB

### Deployment
- **CloudFormation**
  - Cost
  - Productivity
  - IaaC: Infrastructure as a Code
  - Need to repeat architecture in different settings: environment, region or account
  - CFT: Cloud Formation Template
      
- **Beanstalk**
  - PaaS: Platform as a Service
  - Health Monitoring
      
- AWS CDK (Cloud Development Kit) — Defined your cloud infrastructure using a programming language
- CodeDeploy (Hybrid) — Deploy & upgrade any application onto servers
- CodeCommit — private git repository/version control
- CodeBuild — Build & Test code
- CodePipeline — Orchestration of pipeline (from code to build to deploy)
- CodeArtifact — Store software packages/dependencies on AWS
- CodeStar — Unified view for allowing developers to do CI/CD and code
- Cloud9 — Cloud IDE with collab
- Systems Manager (Hybrid) — Patch, configure, and run commands at scale
- OpsWorks (Hybrid) — Managed Chef and Puppet in AWS

### Leveraging the AWS Global Application
Latency, Disaster Recovery, Attack
- **Route 53**
  - Global, managed Domain Name System (DNS)  
  - It is great to route users to the closet deployment with the least latency
  - Great for disaster recovery strategies
  - Routing Policy: simple or weighted or latency or failover
- **CloudFront** Global Content Delivery Network (CDN):  
  - Securely deliver content with low latency and high transfer speeds
  - Replicate part of your application to AWS Edge Locations — decrease latency
  - Cache common requests — improved user experience and decreased latency
- **S3 Transfer Acceleration** Accelerate global uploads & download into Amazon S3 with private AWS network
- **AWS Global Accelerator** Improve global application availability and performance using the AWS global network
- **AWS Outposts**
  - Deploy Outposts Racks in your own Data Centers to extend AWS services
- **AWS WaveLenth**
  - Brings AWS services to the edge of the 5G networks
  - Ultra-low latency applications
- **AWS Local Zones**
  - Brings AWS resources (compute, database, storage, …) closer to your users
  - Good for latency-sensitive applications
- **WAF** Web application Firewall

### Cloud Integration
Decouple synchronous applications
- **SQS** (Simple Queue Service): produce messages in the queue
  - Queue service in AWS
  - Multiple Producers, messages are kept up to 14 days
  - Multiple Consumers share the read and delete message
  - Used to decouple applications in AWS
- **SNS** (Simple Notification Service): publish messages in the queue
  - Notification service in AWS
  - Publisher: Email, Lambda, SQS, HTTP, Mobile, …
  - Multiple Subscribers, send all messages to all of them
  - No message retention
- **Kinesis** — Real-time data streaming, persistence, and analysis (video)
- **Amazon MQ** — Managed message broker for ActiveMQ and RabbitMQ in the cloud (MQTT, AMQP… protocols)

### Cloud Monitoring
  - **CloudWatch** - Observe and monitor resources and applications on AWS, on premises, and on other clouds
  - **CloudWatch Log**:
    - Metrics — Monitor the performance of AWS services and billing metrics: CPU utilisation, Network
    - Alarms — Automate notification, perform EC2 action, notify to SNS based on metrics
    - Logs — Collect log files from EC2 instances, servers, Lambda functions...
    - Events (or **EventBridge**) — React to events in AWS, or trigger a rule on a schedule
  - **CloudTrail** — Track user activity and API usage on AWS and in hybrid and multicloud environments
  - **CloudTrail Insights** — Automated analysis of your CloudTrail Events
  - **AWS X-Ray**
    - Analyze and debug production and distributed applications
    - Trouble shooting peformance
    - Understand dependencies
    - review
    - identify impacted users
  - AWS Health Dashboard — Status of all AWS services across all regions
  - AWS Account Health Dashboard — AWS events that impact your infrastructure
  - **Amazon CodeGuru Security**
    - Detect, track, and fix code security vulnerabilities anywhere in the development cycle using ML and automated reasoning

  
### Security & Compliance
Shared Responsibility on AWS
DDoS = Distributed Denial of Service
7 layers **OSI** model (Open System Intercom):
  1. physical
  2. data
  3. network
  4. transport
  5. session
  6. presentation
  7. application
     
- Root user privileges
  - Change account setting
  - Close your AWS account
  - Change or cancel your AWS Support plan
  - Register as a seller in the Reserved Instance Marketplace

- **Sheild**
  — Standard: Automatic DDoS Protection
  - Advanced: 24/7 support (?)
- **WAF** — Web Application Firewall to filter incoming requests based on rules
  - Availability, Security, Eccessive Resources
- **KMS** Key Management System — Encryption keys managed by AWS
- **HSM** Hardware Security Models
- **ACM** AWS Certificate Manager: Provision and manage SSL/TLS certificates with AWS services and connected resources. In flight encryption
- **AWS Secrets Manager**: Rotation, Automation, Centrally manages the lifecycle of secrets
- **AWS Artifact** — Access AWS and ISV security and compliance reports.
- **GuardDuty** — Find malicious behavior with VPC, DNS & CloudTrail Logs
  - Logs (VPC, CloudTrail, DNS, Lambda, RDB, ...) -> GD -> EventBridge -> [SNS, Lambda, ...] 
- **Amazon Inspector** — Find software vulnerabilities in EC2, ECR images, and Lambda functions
- **Amazon Detective** — Find the root cause of security issues or suspicious activities
- **AWS Config** — Assess, audit, and evaluate configurations of your resources. Track config changes and compliance against rules
- **Macie** — Find sensitive data (e.g. PII data) in Amazon S3 buckets
- **AWS Abuse** — Report AWS resources used for abusive or illegal purposes
- **Security Hub** - Automate AWS security checks and centralize security alerts


## AWS Machine Learning
  - Rekognition — Face detection, labeling, celebrity recognition
  - Transcribe — Audio to Text (e.g. subtitles)
  - Polly — Text to Audio
  - Translate — Translations
  - Lex — Build conversation bots (e.g. chatbots), (like Alexa)
  - Connect — Cloud contact center
  - Comprehend — Natural Language Processing
  - SageMaker — Machine Learning for every developer and data scientist
  - Forecast — Build highly accurate forecasts
  - Kendra — ML-powered search engine
  - Personalize — Real-time personalized recommendations
  - Textact — Detect text and data in documents

## AWS VPC & Network
  - VPC — Virtual Private Cloud
  - Subnets — Tied to an AZ, network partition of the VPC
  - Internet Gateway — At the VPC level, provide Internet Access
  - NAT Gateway / Instances — Give internet access to private subnets
  - NACL — Stateless, subnet rules for inbound and outbound
  - Security Groups — Stateful, operate at the EC2 instance level or ENI
  - VPC Peering — Connect two VPC with non-overlapping IP ranges, nontransitive
  - Elastic IP — Fixed public IPv4, ongoing cost if not in-use
  - VPC Endpoints — Provide Private access to AWS Services within VPC
  - PrivateLink — Privately connect to a service in a 3rd party VPC
  - VPC Flow Logs — network traffic logs
  - Site to Site VPN — VPN over public internet between op-premises DC and AWS
  - Client VPN — OpenVPN connection from your computer into your VPC
  - Direct Connect — Direct private connection to AWS
  - Transit Gateway — Connect thousands of VPC and on-premises networks together

## Account Best Practices
  - Operate multiple accounts using Organizations
  - Use SCP (service control policies) to restrict account power
  - Easily setup multiple accounts with best-practices with AWS Control Tower
  - Use Tags & Cost Allocation Tags for easy management & billing
  - IAM guidelines — MFA, least-privilege, password policy, password rotation
  - Cofig To record all resources configurations & compliance over time
  - CloudFormation to deploy stack across accounts and regions
  - Trusted Advisor to get insights, Support Plan adapted to your needs
  - If your Account is compromised — change the root password, delete and rotate all passwords/keys, contact the AWS support
  - Allow users to create pre-defined stacks defined by admins using AWS Service Catalog

## Billing and Costing Tools
  - Compute Optimizer — Recommends resources’ configuration to reduce cost
  - Pricing Calculator — Cost of services on AWS
  - Billing Dashboard — High-level overview + free tier dashboard
  - Cost Allocation Tags — Tag resources to create detailed reports
  - Cost and Usage Reports — The most comprehensive billing dataset
  - Cost Explorer — View current usage (detailed) and forecast usage
  - Billing Alarms — in us-east-1 — track overall and per-service billing
  - Budges — More advanced — track usage, costs, RI, and get alerts
  - Saving Plans — Easy way to save based on long-term usage of AWS
  - Cost Anomaly Detection — Detect unusual spends using Machine Learning
  - Service Quotas — Notify you when you’re close to the service quota threshold

## Advanced Identity
- **IAM** Identity and Access Management inside your AWS account
- For users that you trust and belong to your company
Organizations — Manage multiple accounts
  - Security Token Service (STS) — temporary, limited-privileges credentials to access AWS resources
  - Cognito — Create a database of users for your mobile & web applications
  - Directory Services — Integrate Microsoft Active Directory in AWS
  - IAM Identify Center — One login for multiple AWS accounts & applications

## AWS Support Plan
There are four AWS support plans available:
- Basic — billing and account support only (access to forums only).
- Developer — business hours support via email.
- Business — 24×7 email, chat, and phone support.
- Enterprise — 24×7 email, chat, and phone support.



## AWS Well-Architected and the Six Pillars
The AWS Well-Architected Framework describes key concepts, design principles, and architectural best practices for designing and running workloads in the cloud.
By answering a few foundational questions, learn how well your architecture aligns with cloud best practices and gain guidance for making improvements.

- Operational Excellence Pillar — Includes the ability to run and monitor systems to deliver business value and to continually improve supporting processes and procedures
- Performance Efficiency Pillar — The performance efficiency pillar focuses on the structured and streamlined allocation of IT and computing resources. Key topics include selecting resource types and sizes optimized for workload requirements, monitoring performance, and maintaining efficiency as business needs evolve.
- Reliability Pillar — The reliability pillar focuses on workloads performing their intended functions and how to recover quickly from failure to meet demands. Key topics include distributed system design, recovery planning, and adapting to changing requirements.
- Security Pillar — The security pillar focuses on protecting information and systems. Key topics include confidentiality and integrity of data, managing user permissions, and establishing controls to detect security events.
- Cost Optimisation Pillar — The cost optimisation pillar focuses on avoiding unnecessary costs. Key topics include understanding spending over time and controlling fund allocation, selecting resources of the right type and quantity, and scaling to meet business needs without overspending.
- Sustainability Pillar — The sustainability pillar focuses on minimizing the environmental impacts of running cloud workloads. Key topics include a shared responsibility model for sustainability, understanding impact, and maximizing utilization to minimize required resources and reduce downstream impacts.

## AWS Cloud Adoption Framework (AWS CAF)

Other Services
 Amazon WorkSpace
Managed Desktop as a Service (DaaS) solution to easily provision Windows or Linux desktops
Great to eliminate management of on-premiseVDI (Virtual Desktop Infrastructure)
Fast and quickly scalable to thousands of users
Secured data – integrates with KMS
Pay-as-you-go service with monthly or hourly rates
 Amazon AppSteam 2.0
Desktop Application Streaming Service
Deliver to any computer, without acquiring, provisioning infrastructure
The application is delivered from within a web browser  AWS IoT Core
AWS IoT Core allows you to easily connect IoT devices to the AWS Cloud
Serverless, secure & scalable to billions of devices and trillions of messages ○ Your applications can communicate with your devices even when they aren’t connected
 Amazon Elastic Transcoder ○ ElasticTranscoder is used to convert media files stored in S3 into media files in the formats required by consumer playback devices (phones etc..)  AWS AppSync
○ Store and sync data across mobile and web apps in real-time
Makes use of GraphQL (mobile technology from Facebook)
 AWS Amplify — A set of tools and services that helps you develop and deploy scalable full-stack web and mobile applications
 AWS Device Farm — Fully-managed service that tests your web and mobile apps against desktop browsers, real mobile devices, and tablets
 AWS Backup — Fully-managed service to centrally manage and automate backups across AWS services
 Disaster Strategy
Backup and Restore
Pilot Light
Warm Standby
Multi-site/Hot-site
Amazon Elastic Disaster Recovery (DRS) — Quickly and easily recover your physical, virtual, and cloud-based servers into AWS
 AWS DataSync
Move large amounts of data from on-premises to AWS
Replication tasks can be scheduled hourly, daily, weekly
The replication tasks are incremental after the first full load

## AWS Application Discovery Service
- Plan migration projects by gathering information about on-premises data centers
- Server utilization data and dependency mapping are important for migrations 
- Agentless Discovery (AWS Agentless Discovery Connector) → VM inventory, configuration, and performance history such as CPU, memory, and disk usage 
- Agent-based Discovery (AWS Application Discovery Agent) → System configuration, system performance, running processes, and details of the network connections between systems
- Resulting data can be viewed within AWS Migration Hub
- AWS Application Migration Service (MNG)
- AWS Migration Evaluator
- AWS Migration Hub
- Central location to collect servers and applications inventory data for the assessment, planning, and tracking of migrations to AWS
- Helps accelerate your migration to AWS, automate lift-and-shift
- AWS Migration Hub Orchestrator — provides pre-built templates to save time and effort migrating enterprise apps (e.g., SAP, Microsoft SQL Server…)
- Supports migrations status updates from Application Migration Service

## (MGN) and Database Migration Service (DMS)  AWS Fault Injection Simulator (FIS)
- A fully managed service for running fault injection experiments on AWS workloads
- Based on Chaos Engineering — stressing an application by creating disruptive events (e.g., a sudden increase in CPU or memory), observing how the system responds, and implementing improvements
AWS Step Functions
Build a serverless visual workflow to orchestrate your Lambda functions
Use cases: order fulfillment, data processing, web applications, any workflow
 AWS Ground Station
Fully managed service that lets you control satellite communications, process data, and scale your satellite operations
Use cases: weather forecasting, surface imaging, communications, video broadcasts
 Amazon Pinpoint
Scalable 2-ways (inbound/outbound) marketing communication service
Supports email, SMS, push, voice, and in-app messaging
Use cases: run campaigns by sending marketing, bulk, and transactional SMS messages

# AWS Cloud Practitioner Certification Cheat Sheet
## Notes for the CLF-C02 exam

### Intro
- 3 Deployment Methods: Private, Public, Hybrid
- 3 types of CC: Infrastructure as a Service (IaaS), Platforms as a Service (PaaS), and Software as a Service (SaaS)
- 6 advantages of CC:
  - Trade fixed expense for variable expense
  - Benefit from massive economies of scale
  - Stop guessing capacity
  - Increase speed and agility
  - Stop spending money running and maintaining data centers
  - Go global in minutes 
- Elasticity: The ability to acquire resources as you need them and release resources when you no longer need them
- Agility: quickly developing, deploying, and launching software applications in the cloud
- Vertical Scalability: more computing and processing power is added to a machine to increase its performance
- Horizontal Scalability: one that can increase capacity by adding more computers to the system.
- High Availability: data protection for all the legacy file data that businesses want to move to AWS, as well as reliable performance with minimal downtime and costs. 


### 6 Categories and colors
|Category | Color |
|---------| ------|
|Compute  | Orange|
|Network  | Purple|
|Governance and Monitoring  |Pink|
|Database  |Blue|
|Security  |Red|
|Storate   |Green|


### Pricing 
- Compute: by CPU time
- Storage: by MB stored
- Network: only data leaving the cloud
- **TCO** Total Cost of Ownership - estimates costs wrt on premises


### Resources
| Resource          | Description                                           |
|-------------------|-------------------------------------------------------|
| **Region**            | - Global location<br>- separate geographic area <br>- Has multiple, isolated AZs                   |
| **Availability Zone** | - Isolated data centers<br>- Within a region <br>- Multiple AZs protect against failure§          |
| **Edge Location**     | - CDN sites<br>- Cache content to reduce latency<br>- Not used to deploy infrastructures (EC2 instances, EBS storage)|
| **Local Zone**        | - Extension of a Region close to users<br>- Low-latency access              |
| **Data Center**       | - House computer systems<br>- Associated components   |
| **Wavelength Zone**   | - Edge of 5G networks<br>- Ultra-low latency          |
- Compliance, Proximity, Latency
- Available services
- AWS Regional Services List

  
### Well Architected Framework - 6 pillars
- Operational Excellence
- Security
- Reliability
- Performance
- Cost Optimization
- Sustainability


### IAM (Identity and Access Management)
| IAM Identity | Can belong to | Description                      | Key Characteristics                                          |
|--------------|------------|----------------------------------   |--------------------------------------------------------------|
| **User**     | Groups     | An individual person or service  | - Permanent long-term credentials <br> - Can be a member of multiple groups <br> - Directly assigned policies |
| **Group**	   | N/A	      | A collection of users under a set of permissions | - Cannot be nested (no groups within groups)<br> - Simplifies permission management<br> - Does not have  credentials |
| **Role**	   | - AWS services <br>- Users<br>- Applications	| - A set of permissions <br>- Similar to a User, but not uniquely associated to a person <br>- a IAM identity with specific permissions <br> - For EC2 instants or AWS services | - Assumed temporarily<br>- Used for granting permissions to accounts/services<br>- No long-term credentials |
| **Policy**	 | - Users <br>- Groups <br>- Roles	| Documents that define permissions |	- JSON document detailing permissions<br>- Can be managed (AWS predefined) or inline (user-defined)<br>- Specifies what actions are allowed or denied |
| **Organizations** | N/A	| A service for managing multiple AWS accounts  | - Centralized management<br>- Apply policies across accounts<br>- Simplifies billing and access control<br>- Offers SCP to resctrict available permissions |

- Authorization vs Authentication
- Security MFA + Password Policy
- Programmatic Access: ID Key + Secret Access Key
- Encryption: Public/Private Keys
- Manage AWS services:
  - **AWS CLI** Command Line Interface
  - **AWS SDK** Software Development Kit using a programming language 
- Audit IAM Credential Reports & IAM Access Advisor
- **STS** Security Token Service — temporary, limited-privileges credentials to access AWS resources
- **Cognito** — Create a database of users for your mobile & web applications
- **Directory Services** — Integrate Microsoft Active Directory in AWS
- **IAM Identify Center** — One login for multiple AWS accounts & applications


### EC2 (Elastic Compute Cloud)
- EC2 Instance
  - Boot strapping: lauch command when computer starts , aka automate boot tasks
  - AMI(OS) + Instance Size (CPU + RAM) + Storage + Security Group + EC2 User Data
- Security Groups — Firewall attached to the EC2 instance
- EC2 User Data — Script launched at the first start of an instance
- SSH — Start terminal into our EC2 Instances (port 22)
- EC2 Instance Role — Link to IAM roles
- Instances Purchasing Options:
  - On-demand: no discount
  - Standard Reserved: up to 72% discount, 1 to 3 years contracts, required for right sized servers
  - Convertible Reserved: more flexibility: change OS type or family
  - Serving Plans
  - Spot Instances: up to 90% discount, can be terminated when needed
  - Dedicated Host
  - Dedicated Instance
  - Capacity Reservation
- **AutoScaling** application availability:
  - dynamic scaling
  - predictive scaling  


### Storage
- **S3** Simple Storage Service
  - Objects have key, data, metadata.
  - Can host static website or media hosting
- **EFS** Elastic File System
  - file-level storage - shared elastic file system with virtually unlimited scalability support
  - No root storage, mounted to store data
  - **EFS IA** Infrequent Access
- **EBS** Elastic Block Store
  - Block based storage for separate EC2
  - no two instances can have the same EBS volume attached to them
  - high-performance option, for various databases
  - not accessible via the internet
- **AMI** Amazon Machine Image
- **EC2** Instance Store -> short term storage
- Access: standard, infrequent, archivial ( = glacier )
- **Object Lock**: Write Once Read Many
- Database vs Storage: Database needs engine

|Type | Storage | 
|--------|-------|
|Object | S3 |
|Block | EBS |
|File | EFS |


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
- **Storage Gateway**
  — Hybrid solution to extend on-premises storage to S3
  - connects on-premises environments with cloud storage through cached volumes, stored volumes and tape-based backup.


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
- Low Latency != high availability
- **ELB** Elastic Load Balancers:
  - Load Balancing: Connections distributed across multiple instances
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
- **Quick Sight** - Scalable, Serverless, Embeddable ML powered BI service.


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
- **CloudFormation**: Content Delivery Network (CDN)
  - Cost
  - Productivity
  - IaaC: Infrastructure as a Code
  - Need to repeat architecture in different settings: environment, region or account
  - CFT: Cloud Formation Template
- **Elastic Beanstalk**
  - PaaS: Platform as a Service
  - Health Monitoring (?)
  - an orchestration service for deploying applications which orchestrates various services, including EC2, S3, SNS, CloudWatch, autoscaling, and Elastic Load Balancers.
- **AWS CDK** (Cloud Development Kit) — Defined your cloud infrastructure using a programming language
- **CodeDeploy** (Hybrid) — Deploy & upgrade any application onto servers
- **CodeCommit** — private git repository/version control
- **CodeBuild** — Build & Test code
- **CodePipeline** — Orchestration of pipeline (from code to build to deploy)
- **CodeArtifact** — Store software packages/dependencies on AWS
- **CodeStar** — Unified view for allowing developers to do CI/CD and code
- **Cloud9** — Cloud IDE with collab
- Systems Manager (Hybrid) — Patch, configure, and run commands at scale
- **OpsWorks** (Hybrid) — Automate Operations with Chef and Puppet

| Feature/Service     | Primary Focus                         | Use Case                                          | Key Features                                                   | Ideal For                                     | Integration                                        |
|---------------------|---------------------------------------|---------------------------------------------------|----------------------------------------------------------------|-----------------------------------------------|----------------------------------------------------|
| **AWS Config**      | Configuration management & compliance | Track configuration changes; audit compliance     | Configuration history; Compliance auditing                     | Compliance auditing; Tracking changes          | AWS services for monitoring                        |
| **AWS OpsWorks**    | Config management with Chef/Puppet    | Manage servers with Chef/Puppet                   | Application model management; Chef/Puppet integration          | Complex apps with specific config needs        | EC2 instances; Chef/Puppet                         |
| **AWS CloudFormation** | Infrastructure as Code               | Automate resource provisioning                    | Template-driven provisioning; Rollbacks                        | Automating AWS resource setup                   | Broad AWS integration                              |
| **AWS Systems Manager** | Operational management              | Manage/automate operational tasks                  | Instance/application management; Automation                    | Operational tasks automation                   | EC2; AWS services for operations                   |


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
- **CloudTrail** — Track user activity and API usage and in hybrid and multicloud environments
- **CloudTrail Insights** — Automated analysis of your CloudTrail Events
- **AWS X-Ray**
  - Analyze and debug production and distributed applications
  - Trouble shooting peformance
  - Understand dependencies
  - review
  - identify impacted users
- **AWS Health**
  - **Dashboard** — Status of all AWS services across all regions
  - **Account Dashboard** — AWS events that impact User's infrastructure
- **Amazon CodeGuru Security**
  - Detect, track, and fix code security vulnerabilities anywhere in the development cycle using ML and automated reasoning
- **Trusted Advisor** to get insights, Support Plan adapted to your needs
  - Identify under utilised EC2 instances to reduce costs
    - Cost option
    - Security
    - Fault tolerance
    - Performance
    - Service limits
  - reccomendation for improvement
  - Checks security groups for rules that allow unrestricted access (0.0.0.0/0) to specific ports


### Security & Compliance
Shared Responsibility on AWS
DDoS = Distributed Denial of Service
7 layers **OSI** model (Open System Intercom):
  | 1. physical  | 2. data |  3. network |
  | -------------|---------| ----------- |
  | 4. transport | 5. session | 6. presentation |
  | -------------|---------| ----------- |
  | 7. application | |
  | -------------|---------| ----------- |
- Root user privileges
  - Change account setting
  - Close your AWS account
  - Change or cancel your AWS Support plan
  - Register as a seller in the Reserved Instance Marketplace
- **Sheild**
  — Standard: Automatic DDoS Protection
  - Advanced: 24/7 support
- **WAF** — Web Application Firewall to filter incoming requests based on rules
  - Availability, Security, Eccessive Resources
- **KMS** Key Management System — Encryption keys managed by AWS
- **HSM** Hardware Security Models
- **ACM** AWS Certificate Manager: Provision and manage SSL/TLS certificates with AWS services and connected resources. In flight encryption
- **AWS Secrets Manager**: Rotation, Automation, Centrally manages the lifecycle of secrets
- **AWS Artifact** — Access AWS and ISV security and compliance reports.
- **GuardDuty**
  — Intelligent threat detection
  — Find malicious behavior with VPC, DNS & CloudTrail Logs
  - Logs (VPC, CloudTrail, DNS, Lambda, RDB, ...) -> GD -> EventBridge -> [SNS, Lambda, ...] 
- **Inspector**
  — Find software vulnerabilities in EC2, ECR images, and Lambda functions,
  - Improve security
- **Detective** — Find the root cause of security issues or suspicious activities
- **AWS Config** — Assess, audit, and evaluate configurations of your resources. Track config changes and compliance against rules
- **Macie** — Find sensitive data (e.g. PII data) in Amazon S3 buckets
- **AWS Abuse** — Report AWS resources used for abusive or illegal purposes
- **Security Hub** - Automate AWS security checks and centralize security alerts


### AWS Machine Learning
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


### AWS VPC & Network
- VPC — Virtual Private Cloud
- Subnets — Tied to an AZ, network partition of the VPC
- Internet Gateway — At the VPC level, provide Internet Access
- NAT Gateway / Instances — Give internet access to private subnets
- **Network ACL**
  — Stateless, subnet rules for inbound and outbound
  - is a firewall at the subnet level
- **Security Group**
  — Stateful, operate at the EC2 instance level or ENI
  - controls the traffic that is allowed to reach and leave the resources that it is associated with (eg inbound and outbound traffic to EC2 instance).
  - is a firewall at the instance level
- VPC Peering — Connect two VPC with non-overlapping IP ranges, nontransitive
- Elastic IP — Fixed public IPv4, ongoing cost if not in-use
- VPC Endpoints — Provide Private access to AWS Services within VPC
- PrivateLink — Privately connect to a service in a 3rd party VPC
- VPC Flow Logs — network traffic logs
- Site to Site VPN — VPN over public internet between op-premises DC and AWS
- Client VPN — OpenVPN connection from your computer into your VPC
- Direct Connect — Direct private connection to AWS
- Transit Gateway — Connect thousands of VPC and on-premises networks together


### Account Best Practices
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


### Billing and Costing Tools
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


### AWS Support Plan
There are four AWS support plans available:
- Basic — billing and account support only (access to forums only).
- Developer — business hours support via email.
- Business — 24×7 email, chat, and phone support.
- Enterprise — 24×7 email, chat, and phone support.


### Management 
- **AWS Managed Services**
  - manages the daily operations of your AWS infrastructure
  - Alignement with ITIL: Information Technology Infrastructure Library
  - Baseline integration with ITSM: Information Technology System Management
  - Supoorts 20+ services for Enterprises
- **AWS Systems Manager**
  - Manage your resources on AWS and in multicloud and hybrid environments
- **AWS Management Consolle**

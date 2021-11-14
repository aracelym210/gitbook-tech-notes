# AWS Cloud Practitioner Essentials

- AWS Cloud Concepts 
- AWS Services 
- Security in AWS
- AWS Architecture 
- AWS Pricing 
- AWS Support
- AWS Certified Cloud Practitoner Exam

## Module 1 - Overview of Cloud Concepts 
- **Benefits of AWS**
  - Flexibility of using resources as needed, and returning when no longer needed.
    - Makes it easier to develop and deploy applications  
  - Undifferentiated heavy lifting of IT (routine, repetive tasks) 
  - Trade upfront expense for variable expense 
    - Upfront expense = data centers, physical servers, etc. which requires payment before use
    - Variable expense = pay only for what you need
  - Focus less on managing infrastructure and servers and focus more on applications and customers 
  - Economies of scale allows AWS to provide lower pay-as-you-go prices
  - Applications can be deployed across the world quickly, providing customers around the world with low-latency 
- **Differences between on-demand delivery and cloud deployments**
  - "On-demand delivery" indicates that resources are available as you need them, when you need them. Additionally, resources can be returned when not needed.
  
    | Cloud-based Deployment | On-Premises Deployment | Hybrid Deployment | 
    | --------------------- | --------------------- | ------------------- | 
    | Run all parts of application in the cloud | Deploy resourcs by using virtualization and resource management tools | Connect cloud-based resources to on-premises infrastructure | 
    | Migrate existing applications to the cloud | Increase resource utilization by using app mgmt and virtualization technologies | Integrate cloud-based resources with legacy IT applications | 
    | Design and build new applications in the cloud | Aka "private cloud." | | 

## Module 2 - Elastic Compute Cloud (EC2)
- EC2 is enabled by multi-tenancy: sharing underlying hardware between virtual machines (via hypervisor that manages)
### Benefits of Elastic Compute Cloud (EC2) 
- Highly flexible
- Cost-effective
- Quick 

### Identify different EC2 instance types 
- Each is grouped under an instance family
- Each instance family offers various combinations of CPU, storage, memory, and networking capacity

| Instance Family Type | Notes | 
| -------------------- | ------ | 
| General purpose | Balanced resources; <br>Diverse workloads; <br>Web servers; <br> Code repos | 
| Compute optimized | Compute intesive tasks; <br>Gaming servers; <br>High Performance Computing (HPC); <br>Scientific modeling; <br>Also useful for batch processing workloads that require processing many transactions in a single group | 
| Memory optimized | Designed to deliver fast performance for workloads that process large datasets in memory. <br>High performance database; <br>Workload that involves performing real-time processing of a large amount of unstructured data. | 
| Accelearated computing | Floating point number calculations; <br>Graphics processing; <br>Data pattern matching; <br>Utilize hardware accelerators (coprocessors) | 
| Storage optimized | Workloads that require high sequential read and write access to large datasets on local storage; <br>Distributed file systems; <br>Data warehousing applications; <br>High frequency online transaction processing systems; <br>Applications with high IOPS (I/O) requirements. | 
  
### Differentiate between various billing options for EC2
| Name of Billing Option | Description | Use cases | Other notes | 
| ---------------------- | ------------ | --------- | ----------- | 
| On-demand purchase | only pay for duration that instance is run (per hour or per second, depending on OS and build) | | Developing, testing, running apps w/ predictable usage patters. <br>| Ideal for short-term, irregular workloads. <br>Not recommended for workloads that last a year or longer because there are greater cost savings options available. | 
| Savings plan | Up to 72% savings over on-demand instance in exchange for commitment to consistent compute usage for 1 or 3 year term. | | Offered for several compute services, including EC2. <br>Usage up to the commitment is charged at the savings plan rate, and anything beyond is charged at regular on-demand rates. |
| Reserved instances | Discount applied to use of on-demand instances in account. Requires 1 or 3 year commitment, *plus* payment in one of three ways. (1) All up front. (2) Partial upfront. (3) No upfront. | | | 
| Spot instances | Can save up to 90%, with the catch/ caveat that AWS can reclaim resources whenever needed, with only a 2 minute warning. | Ideal for workloads with flexible start and end times. <br>Batch processing data for a customer survey| | 
| Dedicated hosts | No shared-tenancy of the host. | Usually used for compliance reasons | | 

- AWS cost explorer is a tool that can analyze your EC2 usage over a period of time and provide recommendations. 

###  Summarize benefits of Amazon EC2 Auto Scaling 
Use the AWS Service, `Amazon EC2 Auto scaling` when you want the scaling process to happen automatically 
- Scalability & Elasticity; how capacity can grow and shrink based on data needs 
- High availability 
- No single point of failure 
- Able to support increase in demand

| Auto-scaling approach | Description | 
| --------------------- | ----------- | 
| Dynamic scaling | Responds to changing demand | 
| Predictive scaling | automatically schedules the right number of EC2 instances based on predicted demand. | 

**Scale up:** Add more power 
**Scale out:** Add more instances to handle increased requests 
- Auto scaling configuration has various capacity settings: 
  - Min capacity
  - Desired capacity 
  - Max capacity 
  - ![image](https://user-images.githubusercontent.com/2760319/139175169-527700af-13b2-470a-87e5-7fd4b8a1a9f8.png)


### Summarize benefits of Elastic Load Balancing
- Elastic load balancing helps to automatically redirect/ redistribute/ re-route traffic as resources (including EC2 instances) are auto-scaled
- Load balancer is an application that takes in requests and routes to instances to be processed. 
- Elastic Load Balancing (ELB) is an Amazon managed service and is a *regional* contruct, so the service it provides is highly available, by default

### Example uses for Elastic Load Balancing
- Application hosted on an EC2 instance goes through high demand and low demand periods over time. With auto-scaling configured for this application (auto-scaling is complimentary to ELB, but not the same), ELB acts as the host/ hostess/ director of traffic as resources are scaled up or down. 

### Differences between Amazon Simple Notification Service (SNS) and Simple Queue Service (SOS)
- SQS enables you to send, store, and receive messages between software components at any volume, without losing messages or requiring other services to be available. Each message has a *payload* that is protected until delivery. Like mostly all AWS services, AWS manages the underlying infrastructure of SNS so that the service is scaled automatically and is reliable and easy to configure and use. 
  - SQS can be thought of as a queue or buffer that is a critical component of a loosely coupled system architecture. 
- SNS can also be used for sending messages to services, but **additionally**, it can send notifications to subscribers, which can be an end user, an endpoint such as an SQS queue, AWS Lamda functions, HTTPS or HTTP web hooks, email addresses, etc. 

### Additional AWS compute options 
- "Serverless" means that you cannot see or access the underlying infrastructure or instances that are hosting your application. 
- Although managing infrastructure on EC2 instance(s) requires significantly less management of resources compared to hosting services on-prem, management processes will still be required (i.e. patching, ensuring high availability, etc.). AWS offers numerous other 'compute services' that abstract the traditional management processes of infrastucture even more. This concept is where the term "serverless" comes from. 

| AWS Service Name | Description | Use Case | 
| ---------------- | ----------- | -------- | 
| AWS Lamda | Service to host code that gets triggered upon configurable conditions being met. <br>Designed to complete in 15 minutes or less <br>charges only apply when code is running| Batch processing; <br>not designed for deep learning or extensive code functions | 
| Amazon Elastic Container Services (ECS) | Not quite serverless, but provides efficiency and flexibility; <br>Container orchestration tool (Docker). <br>Designed to help run containerized applications at scale <br>Can be hosted on EC2| | 
| Amazon Elastic Kubernetes Service | Not quite serverless, but provides efficiency and flexibility; <br>Container orchestration tool (Docker) | | 
| AWS Fartgate | Serverless compute service for ECS or EKS, if you don't want your ECS or EKS to sit on top of EC2 | | 

### Deciding which Amazon service to use
| Needs / Wants | Service | 
| ------------- | -------- | 
| Host traditional applications <br>Need full OS access (Linux/Windows) | EC2 | 
| Host short running functions <br>Service-oriented apps <br>Event driven apps <br>No desire/ need to manage underlying environment | AWS Lambda (serverless) | 

### Decision flow for containerized apps
If your usecase is running Docker container-based workloads on AWS, first you need to choose an orchestration tool - *Amazon ECS* or *Amazon EKS*, **THEN** you must choose platform - EC2, which is requires traditional mangement processes or AWS Fartgate, which is a serverless compute service that is managed for you. 


### Definitions
- **Cloud computing:** The on-demand delivery of IT resources over the internet with pay as you go pricing 

# Module 3
- Summarize benefits of AWS Global Infrastructure
- Describe basic concept of Availability Zones
- Describe benefits of Amazon cloudFront & edge locatoins 
- Compare different methods of provisioning AWS services

## AWS global Infrastructure 
- AWS broken up into regions
- Traffic does not leave designated AWS region without explicit permission and "delegration," meaning (unless you say so)
- Four (4) business factors that go into choosing a region
  -  Compliance 
  -  Proximity to customers 
  -  Feature availability/ Available services within a region 
  -  Pricing: each region has it's own price sheet

## Availability Zones 
- Each availibilty zone is one or more data centers with redundant power, networking and connectivity
- Located 10s of miles apart from each other, which allows for low latency (single ms)
- Regional services, are by default, highly available  

## Edge Locations
- Content Delivery Network - CDN = Amazon Cloudfront 
- An **edge location** is a site that Amazon Cloudfront uses to store cached copies of content closer to customers for faster delivery
- Helps to deliver data to edge locations to accelerate communication and content delivery
- AWS outposts are used to extend AWS infrastructure and services to on-prem data center

## How to provision AWS resources
- All AWS interaction is API calls
- AWS Mgmt console - browser based; manage resources visually; point and click 
- AWS CLI - make API calls using terminal on local machine; more scriptable
- AWS Software Development Kits (SDKs) - interact with AWS resources using various programming languages 
- AWS Elastic Beanstalk - provide code and config settings, and EBS deploys resources
- AWS Cloud Formation - Create automated, repeatable deployments; Infrastructure as Code; JSON or YAML cloud formation, declarative formats. Manages API calls.
  - EC2
  - Storage
  - Databases
  - Machine learning 


# Module 4 (AWS Networking)
- Objectives 
  -  Describe basic concepts of networking
  -  Describe difference between public and private networking resources
  -  Explain virtual private gateway 
  -  Explain a virtual private network (VPN)
  -  Describe benefit of AWS Direct Connect
  -  Describe benefit of hybrid deployments
  -  Describe the layers of security used in an IT strategy
  -  Describe the services customers use to interact with the AWS global network 

## Connectivity to AWS
- A **Virtual Private Cloud (VPC)** is an AWS networking service that can be used to establish boundaries around AWS resources. It is essentially your own private network within AWS. EC2 instances and other instances are placed into VPCs with various subnets.
- Public facing resources 
  -  Internet gateway is used to allow traffic from internet to internet facing services 
-  Private resources 
  -  A Virtual Private Gateway allows only traffic from certain internet addresses to access your VPC. For example, only traffic from your on-premises data center 
  -  AWS direct connect allows the creation of a completely private, fiber connection, from data center to AWS. Work with data provider in area   

## Subnets and network access control lists
- Subnets are used to separate areas within a Virtual Private Cloud (VPC) to group resources together.
- ![image](https://user-images.githubusercontent.com/2760319/140250205-9795509d-3c7e-47db-9808-e77f1140efcb.png)
- ![image](https://user-images.githubusercontent.com/2760319/140250999-a9615b7b-ebdc-4475-985f-4b03524eabdc.png)


### Network hardening
- **Network ACLs (NACL)** check packets crossing in and out of subnets, which can be used to separate resources that are allowed to access the internet and those that are not allowed.
  - Controls inbound/ outbound traffic at the subnet level
  - Default network ACL allows all inbound and outbound traffic; all custom nacl's deny all inbound/ outbound traffic unless explicitly allowed
  - Stateless packet filtering 
- **Security groups** provide instance level network security (i.e. two EC2 instances within the same subnet)
  - Default SG denies all inbound traffic and allows all outbound traffic
  - Stateful packet filtering 

## Global networking
### Route 53
- AWS DNS service 
  - Highly available and scalable 
- Route 53 policies
  - Latency-based routing
  - Geolocation DNS
  - Geoproximity routing
  - Weighted round robin
### Amazon CloudFront
- Amazon CDN
  - A **content delivery network (CDN)** is a network that delivers edge content to users based on their geographic location 

# Module 5 (Storage and Databases)
- Summarize the basic concept of storage and databases
- Describe the benefits of Amazon Elastic Block Store (Amazon EBS)
- Describe the benefits of Amazon Simple Storage Service (Amazon S3)
- Describe the benefits of Amazon Elastic File System (Amazon EFS)
- Summarize various storage solutions 
- Describe the benefits of Amazon Relational Database Service (Amazon RDS)
- Describe the benefits of Amazon DynamoDB
- Summarize various database services 

## Amazon Elastic Block Store (EBS)
- *Block level storage* is a place to store files (bytes stored to blocks on disk)
- An *instance store* provides temporarly block level storage for Amazon EC2 instance. 
  - EC2 instance storage is ephemeral, and when the instance is spun down, whatever is stored to disk may be lost. 
  - AWS recommends instance stores for use cases that involve temporary data that is not needed in the long term
- *EBS volumes* are separate drives from separate instance store volumes that can be attached and used with an EC2 instance.
  - Data stored on EBS volumes will persist if the EC2 instance is stopped and restarted
  - Backups are extremely important, and incremental backups can be taken via *Amazon EBS snapshots*

## Amazon Simple Storage Service (S3)
- S3 is a service that provides *object level storage* (contrast with instance/ block level)
- Data is stored as *objects*, and objects are stored in buckets 
  - `Object = data + metadata + key`
  - Example: `Object = image file + img metadata + unique id`
- Max upload 5TB
- Version control
- Static website hosting on S3
- Set permissions to control visibility and access to S3 files and buckets 

### Amazon S3 storage classes 
| Class Name | Use Case | Notes | 
| ---------- | --------- | -------- |
| S3 Standard | Desined for frequently accessed data <br>Stores data in min. 3 AZs <br>Websites, content distribution, data analytics | High avail. Higher cost than other storage classes intended for infrequently accessed data and archival storage | 
| S3 Standard-Infrequent access (S3 Standard IA) | Infrequently accessed data | Lower storage price, higher retrieval price from S3 standard. <br>Stores in min. 3 AZs | 
| S3 One Zone-Infrequent Access (S3 One Zone-IA) | Only stores in one AZ. <br>Lower storage price than S3 std IA. | Use this when you want to save costs on storage, or you can easily reproduce your data in the event of an AZ failure | 
| S3 Intelligent-Tiering | Ideal for data with unknown or changing access patterns <br>Requires small monthly monitoring and autoation fee per object | S3 monitors objects' access patterns and moves objects based on observations | 
| S3 Glacier | Low-cost storage designed for archiving. <br>Objects can be retrieved within a few minutes to hours | Example usecases include archived customer records or older photos and video files | 
| S3 Glacier Deep Archive | Lowest-cost storage designed for archiving. <br>Objects can be retrieved within 12 hours | Example usecases include archived customer records or older photos and video files | 

## Amazon EBS and S3 Comparison
| Elastic Block Storage | Simple Storage Service | 
| --------------------- | ---------------------- | 
| Up to 16 TiB | Unlimited storage| 
| Survives termination of EC2 instance | Max object size of 5TB | 
| SSD by default | Write once/ read many (WORM) | 
| HDD options | "11 9s" durrability.  (Highly available) | 
| | Web enabled with access rights controlled | 
| | Serverless | 

| Object Storage | Block Level Storage | 
| -------------- | ------------------- |
| S3 | EBS | 
| Treats a file as a complete, discrete object | | 
| If a file is editted, the entire file needs to be re-uploaded | Only bits that are editted are modified | 

## Amazon Elastic File System (EFS) 
- *File storage* is a storage system in which multiple clients (users, apps, servers, etc.) can access data that is stored in shared file folders.
  - This is achieved with a storage server using block storae with a local file system
- Ideal for use cases which a large number of services and resources need to access the same data at the same time
- *EFS* is a scalable file system used with AWS cloud services and on-prem resources. 

| EBS | EFS | 
| ----- | ------ | 
| Stores data in a single AZ | Regional service <br>Data is stored across multiple AZs |
| Attaches to EC2 instance, which must reside in the same AZ as the EBS volume | Can access data from all AZs in the region where a file system is located. | 

## Amazon Relational Database Service 
- Amazon RDS is a an AWS service that enables you to run relational databases in the AWS Cloud
- Automates tasks such as:
  - Hardware provisioning 
  - Database setup
  - Patching 
  - Backups 
- Security options include
  - Encryption at rest 
  - Encryption in transit 

### RDS database engines 
1. Amazon Aurora 
  - Compatible w/ MySQL and PostgreSQL. Faster than standard MySQL and PostgreSQL 
  - Reduce DB cost by reducing unnecessary I/O operations 
  - Should be considered if workloads require HA, as it replicates sixe copies of data across three AZs, and continuously backs up data to S3
2. PostgreSQL
3. MySQL
4. MariaDB
5. Oracle Database
6. Micrsoft SQL Server 

## Amazon DynamoDB
- Serverless database 
  - `Serverless = -harware provisioning - patching - server management`
- Non-relational/ NoSQL DB
  - Structures other than rows and columns to organize data 
  - Key-value pair
- Millisecond response time 
- Fully managed
- Highly scalable 

## Comparing RDS with DynamoDB

| Amazon RDS | Amazon DynamoDB | 
| ------------ | ---------------- | 
| Automatic HA recovery | NoSQL | 
| Customer ownership of data | Key-value pair | 
| Customer ownership of schema | Massive throughput capabilities | 
| Customer controls network | Petabyte (PB) size potential | 
| | Granular API access | 
| Built for business analytics | Can be used for anything else | 

## Amazon Redshift 
- *Data warehouses* historical analytics 
- Data warehouse as a service 
- Redshift is a data warehousing service that can be used for big data analytics. It can collect data from many sources to help understand relationships and trends across data 

## AWS Database Migration Service (DMS)
- Helps customers migrate databases to AWS in a safe, secure way
- Source DB remains fully operational during migrations
- Other use-cases 
  - Development and test DB migration
  - DB consolidation
  - Continuous db replication

| Migration Type | | 
| -------------- | ------------ | 
| Homogenous | Src and target DB are the same type | 
| Heterogeneous | Src and Dst DB are different types of DB. <br>2 step process | 

## Additional AWS DB
- Amazon DocumentDB: Good for content management, catalogs
- Amazon Neptune: Graph database for social networking, reocmmendation engines, fraud detection 
- Amazon Managed Blockchain
- Amazon Quantum Ledger Database: Immutable 

### DB accelerator 
- Amazon Elasticache
- Amazon DynamoDB Accelerator 

# Module 6 (Security)
- Explain the benefits of the shared responsibility model
- Describe multi-factor authentication (MFA)
- Differentiate between AWS Identity and Access Management (IAM) security levels 
- Explain the main benefits of AWS Organization
- Describe security policies at a basic level
- Summarize the benefits of compliance with AWS
- Explain additional AWS security services at a basic level

## Shared Responsibility Model
![image](https://user-images.githubusercontent.com/2760319/141129640-51f1520f-04db-4e12-95ad-778f6b755e1e.png)
- AWS responsible for the security "of" the cloud
  - Physical
  - Network
  - Hypervisor
- Customer responsible for security "in" the cloud 
  - Operating System
  - Application
  - Data 

## User permissions and access
### AWS account root user 
- Owner of the AWS account and has permissions to do whatever they want/ interact with any resouces 
  -  It is recommended to not use the root account for every day tasks
  -  MFA *highly* recommended for root user access
### AWS Identity and Access Management (IAM) Service
- AWS service to control access to resources in a granular way
### IAM User 
- Identity that can be created in AWS
- Accounts can be created and explicity grant permissions to users 
  - All permissions are denied by default, and must be explicitly granted
  - Least privilege model
- IAM policies are associated to users
  - JSON document that states permissions 
  ```
  {
    "version": "2021-11-09",
    "Statement": {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:::coffee_shop_reports"
    }
  }
  ```
### IAM Groups
- Collection of users 
- Eases the burden of managing permissions for individual IAM users 
### IAM Roles 
- Identities in IAM which can be assumed for temporary amounts of time
  - No username and password
  - Temp permissions 
  - *It is best practice to use roles for **temporary** access to services or resources, and not to be used long term*.

## AWS Organizations 
- **root** is the parent container for all accouns in an org
- AWS service that is a central organization to manage multiple AWS accounts 
- Billing, access, compliance, and resource sharing can be managed here
- Centralized managment of AWS accounts 
- Consolidated billing for all member accounts 
- Hierarchal grouping of accounts (similar to Organizational Units (OUs)
  - Good for managing accounts with similar business or security reqs
- AWS services and API actions access control 
- Service control policies 
  - Policies that restrict services, resources, and individual API actions that can be accessed in each member account   
  - Can be applied to an individual member **account** or an **organizational unit**
  - Although this is *similiar* to an IAM policies, there is a difference because IAM policies are applied to IAM users, groups or roles.
![image](https://user-images.githubusercontent.com/2760319/141137885-1b9ad07f-1169-4887-8ef8-26317a1911bb.png)
![image](https://user-images.githubusercontent.com/2760319/141137929-e3b52bd2-0493-48a8-9123-eadc84dce2d4.png)
![image](https://user-images.githubusercontent.com/2760319/141137996-c9af38ac-4aa4-4f26-a70f-b49802f59882.png)

## Compliance 
- AWS Artifact is a service that provides on-demand access to AWS Security and compliance reports
  - AWS Artifact agreements: review, accept, and manage agreements for an individual account and for all accounts in AWS organizations. Agreements are offers to address customers who are subject to specific regulations such as HIPPA
  - AWS Artifact reports provide compliance reports from 3rd party auditors 
- **Customer compliance center** contains AWS compliance resources 
- 

## DDOS
- Objective is to shutdown application's ability to function by overwhelming the capacity to the point where it can no longer operate 
- **UDP Flood** - Attacker gives a false return address (victim) address to a legitimate service request (i.e. weather)
  - AWS solution - Security groups which only allow in proper request traffic. SG's are AWS network level protection, not EC2 where application sits 
- **HTTP Level Attacks** 
- **SLOWORIS Attack** - Attacker pretends to have an extremely slow connection, creating a large queue and preventing other customers from accessing the application 
  - AWS solution - Elastic Load Balancing 

### AWS Shield with AWS WAF (Web Application Firewall) 
- Machine learning and signatures 
- WAF uses web access control lists to protect AWS resources 
- **AWS Shield Std** protects all AWS customers at no extra cost. AWS shield uses a variety of analysis techniques to detect malicious traffic in real time and automatically mitigate it 
- **AWS Shield Advanced** paid AWS service that provides detailed attack diagnostics and integrates with other services such as CloudFront, Route53, ELB. 

## Additional security services 
- Encryption at rest 
- Encryption in transit 
### Amazon Key Management Service (KMS)
- Enables user to perform encryption operations through cryptographic keys. Create, manage, and use keys, and control the use of the keys across a wide range of services 

### AWS Inspector
- Runs automated assessments to monitor to detect deviations from security best practices. A prioritized report is returned with a detailed list of security findings and recommendations to fix.
- Requires 3 things: 
  - Network configuration reachability piece
  - Amazon agent (can be installed on EC2 instances) 
  - Security assessment service 
 ### Amazon Guard duty 
 - Analyzes metadata (cloudTrail events, VPC flow logs, and Route53 logs) 
 - Runs independently from other services so as to not affect others 
 - Amazon guard duty can be interated with AWS Lambda to take remediation steps in response to GuardDuty's findings 

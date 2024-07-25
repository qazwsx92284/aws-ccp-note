# EC2
- EC2: virtual machine
- ELB: distribuing load
- ASG: scaling the service

# EC2 volume (storage) space:
## Network-attached
- EBS: storing data in a **Single AZ**
- EFS: stroing data **across multiple AZ**
## Hardware
- EC2 Instancee store

# EC2 config options
- Firewall rules: security group
- Bootstrap script to configure at first launch: EC2 User Data

# EC2 Instance Types
1. General purpose:
   - diversity of workloads
   - ex. web servers or code repositories
2. Compute optimized: compute intensive tasks, high performance processors. ex. batch, media transcoding, scientific modeling, machinee learning, dedicated gaming servers

3. Memory optimized: fast performance for workloads that process large data sets in memory. ex. high performance DB, distributed web scale cache stroes, in-momery db optimized for BI(business intelligence)
4. Storage optimized: high, sequential read and write access to large data sets on local storage. ex. high frequency online transaction processing(OLTP) systems, DB, cache for in memory, data warehousing app, distributed file systems.

 **Memory optimized is more focus on high performance process for large data sets, while storage optimized literally focus on DB, storing large data**

# Security Groups
- control how traffic is allowed into/out of EC2
- only contain **allow** rules
- like firewall
- regulate ports, ip ranges: ipv4 and ipv6, inbound/outbound network

# EC2 Pricing
- On demand: highest cost, predictable pricing, pay by second, no upfront payment, short term, un-interrupted workloads(can't predict how the app will behave)
- Reserved instance: 1 year, 3 years. No/partial/all upfront. steady-state usage (ex. DB). buy/sell in Reserved Instance Marketplace
- Convertiable reseervced instance
- EC2 Savings plan
- EC2 spot instances: most cost efficient, may lose at any point of time if your max price is less than the current spot price(like bid/auction), useful for workloads resilient to failure ex. batch jobs, data analysis, image processing, distributed workload, flexieble start and end time
- Dedicated hosts
- Dedicated instances
- EC2 Capacity Reservations

# EC2 Storage
- EBS (Elastic Block Store) : persist data, one instance at a time, single AZ, can move with snapshot
     - EBS snapshots: backup, copy cross AZ/region
       - EBS snapshot archive
       - Recycle bin for EBS snapshots
- EFS (Elastic File System) : NFS(network file system), multiple EC2, mLinux EC2 multi AZ
   - EFS-IA (EFS Infrequent Access): automaticaaly move your files to EFS-IA, enable with a Lifecycle policy
- EC2 Instance Store: physical drives, high-performance hardware disk, lose their storage if EC2 stopped (ephemeral)


# AMI (amazon machine image)
- customization of ec2
- built for specific region, can be copied across regions
- public(aws provided) / your own / AWS marketplace ami

# EC2 image builder
- automate the creation, maintain, validate and test EC2 AMIs
- can schedule 
- free, pay for underlying resources

# Scalability & High Availability
- Scalability: system can handle greater loads by adapting
   - vertical scalability: upgrade size. ex. micro -> large. scale up/down
   - horizontal scalability(=elasticity): increase num of system. ex. 2 -> 4. scale out/in
- high availability: to survive a data center loss. run app in at least 2 AZ

# ELB
- managed load balancer: aws do upgrade, maintainance, gurantee system working, few configs
- types:
   1. Application Load Balancer: HTTP/HTTPS, static DNS(URL), layer 7
   2. Network load balancer: ultra high performance, Static IP thru Elastic IP, TCP/UDP, layer 4
   3. Gateway load balancer: Firewalls, intrusion dectection, layer 3

# ASG
- scale in/out, automatically register new instance to LB, replace unhealthy instances, cost savings(run at optimal capacity)
- Types:
   1. manual scaling
   2. dynamic scaling
      - simple/step scaling
      - target tracking scaling
      - scheduled scaling: anticipate based on **known usage pattern** pattern.
      - predictive scaling: use machine lerning to predict future traffic
```
diagram
WEB Traffic -> LB -> (EC2 x 10 ) ASG
LB gets traffic, it handle the traffic route it to specific instance. ASG increase/decrese num of instances depending on traffic amount
```

# S3 
- Infinitely scaling storage
- use case
   1. Backup and **storage**
   2. disaster recovery
   3. archive
   4. hybrid cloud storage
   5. app **hosting**
   6. media hosting
   7. **data lakes & big data analytics
   8. software delivery
   9. **static website**

## S3 buckets
- store objects(files) in buckets(directories)
- must have globally unique name across all regions and all accounts
- defined at region level

## S3 objects
- files
- have a key which is the full path
- key = prefix + object name

## S3 security
1. user based: IAM policies
2. resource based:
   - bucket policies
   - object/bucket access control list(ACL)
3. encryption
   - server side encryption: default, server encrypts the file after receiving it
   - client side encryption: encrypts the file(user) before uploading it

## S3 versioning
- enabled at the bucket level
- same key overwrite whill change the version: 1,2,3...
- best practice to version your bucekts
- before enabling versioning will have version null
- suspending versioning does not delete the previous versions

## S3 Replication 
- must enable versioning in source and destination buckets
- Cross Region Replication (CRR)
  - compliance, lower lanency access, replication across accounts
- Same Region Replication (SRR)
  - log aggregation, live replication between production and test accounts
- buckets can be in different aws accounts
- copying in async
- must give proper IAM permissions to S3

## S3 storage classes
- Standard
- standard Infrequent Access (IA)
- One zone IA
- Glacier instant retrieval
- Glacier flexible retrieval
- Glacier deep archive
- Intelligent tiering
- **can momve between classes manually or using S3 lifecycle configurations**

## IAM Access Analyzer for S3
- ensures that only intended people have access to S3
- evaluate se bucket policies, ACLs, access point policies

## Snow family
- protable devices
- for edge location
- purpose:
  1. data migration
    - snowcone, snowball edge, snowmobile
  2. edge computing
    - snowcone, snowball edge
- **snowcone provides both online and offline data migration methods and DataSync agent is pre-installed**
- AWS OpsHub: to manage Snow Family Device, alternative way of previous CLI

## AWS Storage Gateway
- in hybrid cloud architecture(on-premises + cloud infrastructure), to allow on-premises to seamlessly use AWS Cloud
- bridge between on-premise data and cloud data in S3

# Databases
- stroing data on disk(EFS, EBS, EC2 Instance Store, S3) can have its limits
- many DB technologies could be run on EC2, but you must handle resiliency, backup, patching, high availability, fault tolerance, scaling... those could be done by AWS with its DB

## AWS RDS 
- Relational Database Service
- managed DB for SQL
- create below DBs in the cloud managed by AWS
  1. postgres
  2. MySql
  3. MariaDB
  4. Oracle
  5. Microsoft sql server
  6. Aurora(AWS proprietary database)

### Aurora 
- support PostgreSQL and MySql
- more expensive than RDS, but more efficient

### Aurora serverless
- automated DB instantiation and auto-scaling based on actual usage

## Athena
- serverless query service to analyze data stored in **S3**
- SQL

### RDS Deployments
1. Read Replicas: create read replica of main DB, data is only written in main DB
2. Multi AZ: failover in case of AZ outage(high availability), data is only read/written to main DB
3. Multi Region(Read replicas): create read replicas in other regions. read/writed only to the main DB. disater recovery, increase local performance for global read, replication cost

### ElastiCache
- fully managed in memory data store and cache service
- get managed Redis or Memcached 

## Dynamo DB
- fully managed high available with replication across 3 AZ
- NoSql DB
- serverless

### DynamoBD Accelerator (DAX)
- fully manged in memory cache for DynamoDB
- **DAX only for DynamoDB, while ElastiCache can be used for other DBs**

### DynamoDB Global Tables
- low latency in multi regions
- Active-Active replication = read/write to any AWS Region

## DocumentDB
- same for MongoDB (NoSQL DB)
- fully manged

## Redshift
- postgreSql
- not for OLTP(online transaction processing), RDS is goot for OLTP
- good for OLAP(online **analytical** processing), analytics and data warehousing
- load data once every hour not every second
- Columnar storage
- Massively Parallel Query Execution (MPP), highly available
- has SQL interface for performing quries
- BI tools; Quicksight, Tableau

### Redshift serverless
- automatically provisions and scales data warehouse underlying capacity
- use cases: reporting, dashboarding apps, real-time analytics

## EMR
- Elastic MapReduce
- Hadoop (big data)
- use case: data processing, machine learning

## Neptune
- fully managed graph DB
- ex. social media

## QuickSight
- serverless macine learning powered BI (business intelligence) service to create interactive dashboards
- integrated with RDS, Aurora, Athena, Redshift, S3

## Amazon Timestream
- fully managed, fast, scalable, serverless time series DB

## Amazon QLDB
- Quantum Ledger DB
- recording financial transactions
- fully managed, serverless, high available, replication across 3 AZ
- review history of all changes made to app data over time
- Immutable system: no entry can be removed or modified, cryptographically verifiable
- no decentralization component

## Amazon Managed Blockchain
- decentralization: multiple parties can execute transactions without the need for a trusted, central authority.
- Ethereum, Hyperleger Fabric

## AWS Glue
- Managed extract, transform and load service (ETL)
- fully serverless

# Docker
- software development plaform to deploy apps
- Apps run the same, regardless of where they're run

## Amazon ECR (Elastic Container Registry)
- private Docker registry = where Docker images are stored in private
- This is wheere you store your Docker images so that they can be run by ECS or Fargate
- Docker hub is where Docker images are soterd in public

## ECS
- Elastic Container Service
- launch Docker containers on AWS
- you must provision and maintain the infra(=EC2)
- AWS do starting/stopping containers
- integration with load balancer

## Fargate
- launch Docker containers on AWS
- you do **not provision** the infra
- serverless offering

## AWS Lambda
- virtual functions - no servers to manage
- limited by time - short executions
- run on-demand, **Event-Driven**
- serverless = managed service
- scaling is automated
- easy pricing, payper requeat and compute time
- use cases: serverless thumbnail creation, serverless CRON job

## Lambda container image
- must implement the Lambda Runtime API
- ECS/Fargate is preferred for running arbutary Docker images

# Amazon API Gateway
- fully managed
- serverless and scalable
- supports RESTful APIs, WebSocket APIs

# AWS batch
- fully managed
- at any scale
- batch = job with a start and an end (opposed to continuous)
- batch will dynamically launch EC2 or Spot Instances
- batch jobs are defined as Docker images and run on ECS

# Amazon Lightsail
- vitual servers, storage, DBs and networking
- low and predictable pricing
- great for people **with little cloud experience**
- simpler alternative to using EC2,RDS,ELB...., can setup notification and monitoring
- use cases: simple web apps, websites, dev/test environment
- high availability but no auto scaling, limited AWS integrations

# CloudFormation
- a declarative way of outlining your AWS, infra, for any resources 
- ex. within a CloudFormation template, you say, you want a security group, EC2, S3, ELB... then CloudFormation creates them for you in the **right order** with the **exact config** that you specify in the template.
- most of services are supported, you can use "custom resoources" for unsupported ones
- Infrasture as code
- can estimate the costs using CloudFormation template
- automated generation of diagram for your template
- ability to destory and re-create an infrasture on the cloud on the fly, ex. in dev, you could automation deletion of templates at 5pm and recreate at 8am safely
- can leverage exisiting templates on the web or documentation

## CloudFormation Stack Designer
- can see all resources and relations between the components

# AWS cloud development Kit (CDK)
- Define your cloud infrastructure using familir coding language; js,ts,python,java and .net
- the code is "compiled" into **CloudFormation template**(json/yaml)
- so you can deploy infratructure and app runtime code together
- great for Lambda functions and Docker containers in ECS/EKS

# Elastic Beanstalk
- service for deploying and scaling web apps and services.
- developer simply upload code and Elastic Beanstalk automatically handles the deployment including capacity provisioning, load balancing, auto scaling and health monitoring.
- uses all components, if not supported, you can write your custom platform (advanced)
- Platform as a Service (PaaS)
- free but you have to pay for the undelying instances

## Elastic beanstalk - Health Monitoring
- Health agent pushes metric to **CloudWatch**

# AWS CodeDeploy
- deploy app automatically
- work with EC2, On-premises servers, hybrid service
- servers/instances must be provisioned and configured ahead of time with the CodeDeploy Agent
- umm like Jenkins Deploy action?

# AWS CodeCommit
- git based code repository like GitHub

# AWS CodeBuild
- compiles source code, run tests, and produces packages that are ready to be deployed(by CodeDeploy for example)
- umm like Jenkins promotion action?

# AWS CodePipeline
- orchestrate the different steps to have the code automatically pushed to production
- code > build > test > provision > deploy
- basis for CICD = continuous Integration & Continuous Delivery
- fully managed, compatible with CodeCommit, CodeBuild, CodeDeploy, Elastic Beanstalk, CloudFormation, GitHub, 3rd party services....
- fast delivery and rapid updates
- diagram

```
CodePipeline : orchestration layer
codeCommit > codeBuild > CodeDeploy > Elastic Beanstalk
```

# AWS CodeArtifact
- storeing and retreving dependencies = artifact management
- developers and CodeBuild can retrieve dependencies from CodeArtifact
- umm like JFrog.. Nexus repository

# AWS CodeStar
- Unitied UI to easily manage software development activities in one place

# Cloud 9
- online cloud IDE

# AWS System Manager (SSM)
- helps you manage EC2 and On-premises: patching automation, run commands, configure servers
- hybrid AWS service

## SSM Session Manager
- allow you to start a secure shell on your EC2 and on-premises servers
- No SSH access, bastion hosts, or SSH keys needed (A bastion host is a server used to manage access to an internal or private network from an external network - sometimes called a jump box or jump server. Because bastion hosts often sit on the Internet, they typically run a minimum amount of services in order to reduce their attack surface.)
- No port 22 needed(better security)
- send session log data to S3 or CloudWatch Logs

## Systems Manager Parameter Store
- secure storage for configs and secrets
- serverless, scalable, durable, easy SDK
- control access with IAM
- version tracking and ecryption are optional
- umm.. like hashi corp vault?

# Global Applications in AWS
1. Global DNS: Route 53
2. Global Content Delivery Network(CDN): CloudFront
3. S3 Transfer Acceleration
4. AWS Global Accelerator

## Route 53
- mangaged DNS (Doman Name System)
- great to route users to the closest deployment with least latency
- great for disaster recovery strategies

### Route 53 routing policies
1. Simple routing policy
   - No health checks
2. Weighted routing policy
3. Latency routing policy
4. Failover routing policy
   - Disaster recovery
   - Health cehck on primary
**except for simple routing policy, everything else has health checks**

## AWS CloudFront
- Content Delivery Netwok (CDN)
- Improves read performance, content is cached at the edge
- DDoS protection because worldwide
- integration with Shield, AWS Web Application Firewall

## S3 Transfer Acceleration
- increase transfer speed by transferring file to AWS Edge Location which will forward the data to the S3 bucket in the target region

## AWS Global Accelerator
- improve global app availability and performance using AWS global network
- leverage AWS internal (private ) network
- 2 anycast IP are created and traffic is sent thru edge locations

# Amazon SQS (Simple Queue Service)
- fully managed service, serverless
- used to decouple app
- default retention of messages: 4days, max 14 days
- messages are deleted after they're read by consumers
- consumers share the work to read messages and scale horizontally
- FIFO Queue: messages are processed in order by the consumer

# Amazon SNS
- event publishers only sends message to one SNS topic
- event subscribers listen to the SNS topic notifications
- each subscriber to the topic will get all the messages

---

## AWS SNS vs SQS key feature differences
There are some key distinctions between SNS and SQS:

SNS supports A2A and A2P communication, while SQS supports only A2A communication.

SNS is a pub/sub system, while SQS is a queueing system. You'd typically use **SNS** to send the same message **to multiple consumers via topics**. In comparison, in most scenarios, each message in an **SQS** queue is processed **by only one consumer**.

With **SQS**, messages are delivered through **a long polling (pull) mechanism**, while **SNS** uses a **push mechanism** to immediately deliver messages to subscribed endpoints.

**SNS** is typically used for applications that need realtime **notifications**, while **SQS** is more suited for **message processing use cases**.

**SNS does not persist messages** - it delivers them to subscribers that are present, and then deletes them. In comparison, **SQS can persist messages (from 1 minute to 14 days).**

---

# Amazon Kinesis
- real time big data streaming
- managed service to collect, process, and analyze real-time streaming data at any scale

## Kinesis Types (Not CCP scopes but good to know)
1. kinesis data streams
2. kinesis data firehose
3. kinesis data anlytics
4. kinesis video streams

# Amazon MQ
- managed message broker service for RabbitMQ and AciveMQ in the cloud (MQTT, AMQP.. protocols)
- doesn't scale as much as SQS/SNS
- runs on servers, can run in multi AZ with failover
- has both queue feature (SQS) and topic features (SNS)

# Amazon CloudWatch Metrics
- CloudWatch provides metrics for **every** services in AWS

## Amazon CloudWatch Alarms
- trigger notifications for any metric
- alarms actions: auto scaling, EC2 actions, SNS notifications
- ex. create a billing alarm on CloudWatch Billing metric

## Amazon CloudWatch Logs
- can collect log from Elastic Beanstalk, ECS, Lambda, CloudTrail, CloudWatch log agents, Route53

### CloudWatch Logs for EC2
- by default, no logs from EC2 goes to CloudWatch
- need to run CloudWatch agent on EC2 to push log files
- CloudWatch log agent can be setup on-premises too

## Amazon EventBridge (=CloudWatch Events) : serverless event bus that ingests data from your own apps, SaaS apps, and AWS services and routes that data to targets.
- schedule: cron job
- event pattern
- trigger lambda functions, send SQS/SNS messages

# AWS CloudTrail
- provides governance, compliance and audit for you AWS account
- enabled by default
- get an **history of events/API calls** **made within account** by console SDK, SLI, AWS Services
- trail can be appliced to All regions (default), or a single region
- can put logs from CloudTrail into CloudWatch Logs or S3
- **if resouces is deleted in AWS, investigate CloudTrail first...**

## CloudTrail Insights
- automated analysis of your CloudTrail Events

# AWS X-Ray
- AWS X-Ray helps you **debug and analyze your microservices** applications with request tracing so you can find the root cause of issues and performance

# AWS CodeGuru
- **ML-powered** service
- automated code reviews and app performance recommendations
- provides two functionailities
  1. CodeGuru Reviewer: **automated code reviews** for static code analysis (development)
  2. CodeGuru Profiler: visibility/recommendations about app **performance** during **runtime**(production)
- coding: CodeGuru Reviewer. supports java, python. identify critical issue, vulnerabilities, bugs. umm like sonarqube
- Build&Test, Deploy, Measure: CodeGuru Profiler

# AWS Health Dashboard
- Service Health Dashboard
- Account health dashboard

# VPC
- virtual private cloud
- private network to deploy your resources(regional resource)

# Subnets
- to partition your netwok inside your VPC (AZ resource)
- public subnet: accessible from the internet
- private subnet: not accesible from the ineternet
- to define access to the internet and between subnets, use Route Tables

## VPN vs VPC
- A VPN (virtual private network) creates a secure connection over the internet to protect data exchanges between a user and the network. A VPC (virtual private cloud), however, is a segment of a public cloud infrastructure that offers a private cloud environment.

# Internet gateways
- help VPC instances connect with internet
- public subnets

# NAT Gateways(aws-managed) & NAT instances(self managed)
- allow instances in Private subets to access internet while remaining private

# NACL (Network ACL)
- firewall: control traffic from/to subnet
- ALLOW and DENY rules
- attached at subnet level
- rule: only IP address
- stateless: return traffic must be explicitly allowed by rules

# Security Groups
- freiwall: control traffic to/from an ENI/EC2 instance (what's ENI? Elastic Network Interface (ENI) is a virtual network interface that provides networking capabilities to Amazon EC2 instances)
- only ALLOW rules
- instance level
- rules: IP address and other security groups
- stateful: return traffic is automatically allowed, regardless of any rules

# VPC Flow logs
- Capture information about IP traffic oing into your interfaces

# VPC Peering
- Connect 2 VPC, privately using AWS's network
- must not have overlapping CIDR (IP address range, Classless Inter-Domain Routing (CIDR) is an IP address allocation method that improves data routing efficiency on the internet.)
- VPC Peering connection is not transitive(must be established for eash VPC that need to communicate with one another)

# VPC Endpoint
- to connect to AWS Service using a private network
- enhanced security, lower latency to access AWS services

## AWS PrivateLink (VPC endpoint services)
- most secure and scalable way to expose a service to thousands of VPCs.
- not require VPC peering, internet gateway, NAT, route tables...
- require a network load balancer and ENI

---

# Site to Site VPN
- connect an on-premises VPN to AWS
- connection is automatically encrypted
- goes over **public** internet
- On-premises must use a **Customer Gatewawy (CGW)**
- AWS must use a **Virtual Private Gateway (VGW)**

# Direct Connect (DX) 
- establish a **physical** connection between on-premises and AWS
- connection is private, secure and fast
- goes over a **private** network
- takes at least a month to eastablish

# AWS Client VPN
- connect from your computure using **OpenVPN** to your private network(VPC) in **AWS** and **on-premises**
- AWS Client VPN is a fully-managed remote access VPN solution used by your remote workforce to securely access resources within both AWS and your on-premises network. Fully elastic, it automatically scales up, or down, based on demand.
- allow you to connect to your EC2 over private IP (just as if you were in the private VPC network)
- goes over **public internet**

---

# Transit Gateway
- connect thousand of VPC and on-premises networks together
- hub-and-spoke (star) connection
- works with Direct Connect Gateway, VPN connections























































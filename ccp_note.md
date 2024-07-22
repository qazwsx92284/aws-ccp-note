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
- ex. SNS

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








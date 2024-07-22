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




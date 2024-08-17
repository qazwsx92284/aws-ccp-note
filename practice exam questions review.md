## block-level storage?
- Instance store
- EBS(Elastic Block store)
> EFS is designed to provide massively parallel shared access to thousands of Amazon EC2 instances, enabling your applications to achieve high levels of aggregate throughput and IOPS with consistent low latencies.
> S3 is object stroage. customers of all sizes and industries can use it to store and protect any amount of data for a range of use cases, such as websites, mobile applications, backup and restore, archive, enterprise applications, IoT devices, and big data analytics.

## simplify access management to multiple AWS accounts and facilitate AWS SSO(Single sign-on) access to AWS acounts.
- AWS IAM Identity Center

## Run a log backup process every Tues at 3 am. Usual runtime is 5 minutes. what services to build a serverless solution?
- Amazon Eventbridge
- AWS Lambda
> The lambda has a maximum execution time of 15 minutes, so it can be used to run this log backup process.
### Amazon Eventbridge 
- Amazon EventBridge is a service that provides real-time access to changes in data in AWS services, your own applications, and software as a service (SaaS) applications without writing code.
-  Amazon EventBridge Scheduler is a serverless task scheduler that simplifies creating, executing, and managing millions of schedules across AWS services without provisioning or managing underlying infrastructure.

## quickly deploy popular technology on AWS.
- Aws Partner Solutions (foremerly Quick Starts)
> AWS Partner Solutions are automated reference deployments built by Amazon Web Services (AWS) solutions architects and AWS Partners. Partner Solutions help you deploy popular technologies to AWS according to AWS best practices. You can reduce hundreds of manual procedures to a few steps and start using your environment within minutes.

AWS Partner Solutions are automated reference deployments for key workloads on the AWS Cloud. Each Partner Solution launches, configures, and runs the AWS compute, network, storage, and other services required to deploy a specific workload on AWS, using AWS best practices for security and availability.

## AWS services that are free to use
- AWS Identity and Access Management (IAM)
- AWS Auto Scaling

## Below are not free
- Amazon Simple Storage Service (S3)
- Amazon Elastic Compute Cloud (EC2)
- Amazon DynamoDB

## data encryption automatically enabled?
- S3
- AWS Storage Geteway

## Below data encryption is NOT auto enabled.
- EFS
- Redshift
- EBS

## An AWS user is trying to launch an Amazon Elastic Compute Cloud (Amazon EC2) instance in a given region. What is the region-specific constraint that the Amazon Machine Image (AMI) must meet so that it can be used for this Amazon Elastic Compute Cloud (Amazon EC2) instance?
- You must use an Amazon Machine Image (AMI) from the **same region** as that of the Amazon EC2 instance. The region of the Amazon Machine Image (AMI) has no bearing on the performance of the Amazon EC2 instance
> An Amazon Machine Image (AMI) provides the information required to launch an instance. You must specify an Amazon Machine Image (AMI) when you launch an instance. You can launch multiple instances from a single AMI when you need multiple instances with the same configuration.

The Amazon Machine Image (AMI) must be in the same region as that of the Amazon EC2 instance to be launched. If the Amazon Machine Image (AMI) exists in a different region, you can copy that Amazon Machine Image (AMI) to the region where you want to launch the EC2 instance. The region of Amazon Machine Image (AMI) has no bearing on the performance of the Amazon EC2 instance.

## To **provide secure shell access** to Amazon Elastic Compute Cloud **(Amazon EC2)** instances without opening new ports or using public IP addresses. Which tool/service will help you achieve this requirement?
- AWS Systems manager session manager
> AWS Systems Manager Session Manager is a fully-managed service that provides you with an interactive browser-based shell and CLI experience. It helps provide secure and auditable instance management without the need to open inbound ports, maintain bastion hosts, and manage SSH keys. AWS Systems Manager Session Manager helps to enable compliance with corporate policies that require controlled access to instances, increase security and auditability of access to the instances while providing simplicity and cross-platform instance access to end-users.

## automate operations on his on-premises environment using Chef and Puppet. 
- AWS OpsWorks

## What is the primary benefit of deploying an Amazon RDS Multi-AZ database with one standby?
- Amazon RDS Multi-AZ enhances database availability
> Amazon RDS Multi-AZ protects the database from a regional failure can't be answer. For this, you should use RDS in multi-region deployment config

## compare the cost of running their IT infrastructure on-premises vs AWS Cloud?
- AWS Pricing Calculator
> AWS Pricing Calculator lets you explore AWS services and create an estimate for the cost of your use cases on AWS. You can model your solutions before building them, explore the price points and calculations behind your estimate, and find the available instance types and contract terms that meet your needs.

## to use a storage service which would be accessed by hundreds of EC2 instances simultaneously to append data to existing files. 
- EFS
> Amazon Simple Storage Service (Amazon S3) - Amazon Simple Storage Service (Amazon S3) is an object storage service that offers industry-leading scalability, data availability, security, and performance. S3 is object storage and it does not support file append operations, so this option is incorrect.

## AWS Organizations provides which of the following benefits?
- Volume discounts for Amazon EC2 and Amazon S3 aggregated across the member AWS accounts
- Share the reserved Amazon EC2 instances amongst the member AWS accounts
- Centrally manage policies across multiple aws accounts
- automate aws account creation and management
- consolidate billing across multiple aws accoutns
- govrn access to aws services, resources, and regions
- configure aws services across multiple accounts

## AWS Marketplace facilitates
- AWS customer can buy software that has been bundled into customized Amazon Machine Image (AMIs) by the AWS Marketplace sellers
- Sell Software as a Service (SaaS) solutions to AWS customers
> Amazon EC2 Standard Reserved Instances (RI) can be bought from the Amazon EC2 console
> AWS Direct Connect connection can be raised from the AWS management consol






































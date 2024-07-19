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


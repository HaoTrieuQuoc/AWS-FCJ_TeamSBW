---
title : "Week 8 Worklog"

weight : 1 
chapter : false
pre : " <b> 1.8. </b> "
---
## Week 8 Objectives:
- Continue development of the **Batch-based Clickstream Analytics Platform** project.  
- Finalize and publish the **project proposal** on GitHub Pages for team-wide collaboration.  
- Plan next steps and begin research for integrating **Amazon Cognito** and **Amazon S3** into the e-commerce web application.  
- Review key AWS concepts and architectural principles for the **Midterm Exam**.  

---

## Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 1-2 | - **Team Meeting & Project Setup**:<br>&nbsp;&nbsp;• Meet the full team in person (first full meeting after one month of online collaboration).<br>&nbsp;&nbsp;• Leader pushes the project to GitHub and adds all members to the repository.<br>&nbsp;&nbsp;• Review and finalize the project proposal, check for errors, and publish it via **GitHub Pages**.<br>&nbsp;&nbsp;• Plan upcoming tasks:<br>&nbsp;&nbsp;&nbsp;&nbsp;- Research **Amazon Cognito** and **Amazon S3** for e-commerce web application integration.<br>&nbsp;&nbsp;&nbsp;&nbsp;- Explore additional AWS services for project implementation.<br>&nbsp;&nbsp;&nbsp;&nbsp;- Set target to complete the project before **Week 12**.<br>&nbsp;&nbsp;• Explore and test various **e-commerce web templates** to find the most suitable and responsive one. | 10/27/2025 | 10/28/2025 | [GitHub Repository](https://github.com/HaoTrieuQuoc/AWS-FCJ_TeamSBW) |
| 3-4 | - **Midterm Exam Preparation**:<br>&nbsp;&nbsp;• Review AWS topics: Secure, Resilient, High-Performing, and Cost-Optimized Architectures.<br>&nbsp;&nbsp;• Revisit key AWS services: EC2, S3, RDS, IAM, Lambda, CloudWatch, CloudFront, and EventBridge.<br>&nbsp;&nbsp;• Practice with mock questions and scenario-based case studies. | 10/29/2025 | 10/30/2025 |  |
| 5 | - **Midterm Exam** | 10/31/2025 | 10/31/2025 |  |

---

## Week 8 Achievements

### 1. Team Collaboration and Project Setup
- The full team successfully held the **first in-person meeting** after over a month of online collaboration.  
- The **team leader** created the GitHub repository, added all members, and pushed the finalized proposal to the repository.  
- The **proposal content** was thoroughly reviewed, corrected for formatting and logic errors, and deployed via **GitHub Pages** for public access.  

---

### 2. Project Planning and Research
- The team defined clear **short-term goals** and aligned on completing the project before **Week 12**.  
- Main focus areas for the next stage include:
  - Researching **Amazon Cognito** for user authentication and identity management.  
  - Exploring **Amazon S3** for data storage, static web hosting, and log management.  
  - Studying other relevant AWS services that can enhance the platform’s scalability and performance.  
- The team also explored several **e-commerce website templates**, testing features such as responsiveness, UI flow, and integration potential with AWS backend services.

---

### 3. Midterm Exam Preparation
### AWS Services Categorization for Exam Review

#### 1. Secure Architectures

| Service | Concept | How it works | Example |
|----------|----------|--------------|----------|
| **AWS Organizations** | Manage multiple AWS accounts under one organization. | Root account manages member accounts and applies Service Control Policies (SCPs). | Like a parent company managing its subsidiaries. |
| **Service Control Policy (SCP)** | Organization-wide policies that restrict permissions for accounts. | SCPs define allowed/denied actions across all accounts. | Like company laws that override department rules. |
| **AWS IAM** | Manage users, groups, roles, and permissions in AWS. | Users are authenticated and authorized using IAM Policies (JSON). | Like a card access system in a building. |
| **IAM Roles** | Grant temporary access permissions to users or services. | Services assume a role to gain temporary credentials. | EC2 assumes a role to access S3. |
| **IAM User Groups** | Group users with the same permissions. | Assign policies at the group level for easier management. | Like giving all HR employees the same access rights. |
| **AWS KMS** | Manage encryption keys to secure data. | Create CMKs to encrypt data in S3, EBS, and RDS. | Like a central bank vault with authorized keys. |
| **AWS Cognito** | User authentication and management for web/mobile apps. | Creates User Pools for login via email or social providers and issues tokens. | Like a reception desk that verifies visitor identity. |
| **AWS Config** | Track and audit AWS resource configurations over time. | Records configuration changes and evaluates compliance. | Like a surveillance camera monitoring setup changes. |
| **AWS CloudTrail** | Log all API calls and user activities in AWS. | Records events and stores logs in S3 for analysis. | Like a black box recording all system actions. |
| **AWS WAF** | Web Application Firewall for HTTP/HTTPS traffic protection. | Filters requests at CloudFront, ALB, or API Gateway. | Like a checkpoint inspecting incoming visitors. |
| **AWS Shield** | DDoS protection service for AWS applications. | Standard version auto-protects; Advanced adds proactive defense. | Like flood barriers automatically deploying in storms. |
| **AWS Inspector** | Scans workloads for vulnerabilities and misconfigurations. | Analyzes EC2, ECR, and Lambda environments. | Like a periodic safety inspection. |
| **AWS GuardDuty** | Threat detection using machine learning. | Monitors CloudTrail, DNS, and VPC logs for anomalies. | Like an intelligent home security system. |
| **AWS Trusted Advisor** | Provides best-practice recommendations for security and cost. | Scans accounts and reports optimization suggestions. | Like an internal consultant improving efficiency. |

---

#### 2. Resilient Architectures

| Service | Concept | How it works | Example |
|----------|----------|--------------|----------|
| **Amazon EC2** | Virtual servers hosted on AWS. | Choose instance type, AMI, and storage to deploy applications. | Like renting a server in a data center. |
| **Auto Scaling Group (ASG)** | Automatically scales EC2 instances based on demand. | Adds or removes instances according to CPU or traffic metrics. | Like opening more cash counters when a store gets busy. |
| **Elastic Load Balancing (ALB/NLB)** | Distributes traffic across multiple targets. | ALB for HTTP(S) and NLB for TCP/UDP connections. | Like a traffic roundabout evenly distributing cars. |
| **Amazon Route 53** | DNS and domain management service. | Routes traffic to endpoints like EC2 or Load Balancer. | Like a receptionist directing visitors to the right office. |
| **AWS Global Accelerator** | Improves performance with global network routing. | Routes traffic to the nearest healthy region using static IPs. | Like a global logistics hub delivering goods faster. |
| **VPC Peering / Transit Gateway** | Connects multiple VPCs privately. | Peering connects two VPCs directly, Transit Gateway connects many. | Peering = bridge; TGW = central station. |
| **Direct Connect / Site-to-Site VPN** | Connects on-premises data centers to AWS. | Direct Connect = dedicated line; VPN = encrypted tunnel over the Internet. | Like a private fiber line or secure tunnel to AWS. |

---

#### 3. High-Performing Architectures

| Service | Concept | How it works | Example |
|----------|----------|--------------|----------|
| **Amazon CloudFront** | Global Content Delivery Network (CDN). | Caches content at edge locations for low latency delivery. | Like warehouses near customers for faster delivery. |
| **Amazon S3 / EBS / EFS** | Object, block, and file storage services. | S3 for scalable file storage, EBS for EC2 volumes, EFS for shared files. | Like a hard drive, USB, and shared folder system. |
| **Amazon RDS / Aurora / DynamoDB / ElastiCache** | Managed database and caching services. | RDS for relational DBs, Aurora for high-performance DBs, DynamoDB for NoSQL, ElastiCache for in-memory cache. | Like a library (RDS), fast storage (Aurora), locker (DynamoDB), and clipboard (Cache). |
| **Amazon VPC** | Virtual Private Cloud for secure networking. | Divides into subnets and controls inbound/outbound traffic. | Like a gated community with separate zones. |
| **Subnet / Security Group / NACL** | Core network security layers in VPC. | SG = instance-level firewall (stateful); NACL = subnet-level (stateless). | Like guards at gates (SG) and police at street entrances (NACL). |

---

#### 4. Cost-Optimized Architectures

| Service | Concept | How it works | Example |
|----------|----------|--------------|----------|
| **AWS Storage Gateway / Snowball** | Hybrid storage or physical data transfer to AWS. | Gateway syncs on-prem data; Snowball transfers via hardware device. | Like shipping a container of data to AWS. |
| **S3 Storage Classes (Standard, IA, Glacier)** | Different S3 tiers for varied access frequency. | Standard for frequent, IA for infrequent, Glacier for archival storage. | Like regular, cold, and frozen warehouse storage. |
| **Amazon Kinesis (Data Streams / Firehose / Analytics)** | Real-time data collection and processing. | Streams capture data; Firehose delivers it; Analytics analyzes in real-time. | Like surveillance cameras tracking continuous movement. |
| **Amazon Athena / Redshift / EMR / QuickSight** | Data analytics and visualization tools. | Athena queries S3, Redshift stores structured data, EMR processes big data, QuickSight visualizes insights. | Like analysis, processing, and dashboard teams in a company. |
| **Amazon SNS / SQS / EventBridge / API Gateway / Lambda** | Serverless event-driven and messaging services. | SNS = notifications, SQS = queue, EventBridge = event bus, API Gateway = API endpoint, Lambda = compute logic. | Like alerts, queues, schedules, and automation bots in a system. |

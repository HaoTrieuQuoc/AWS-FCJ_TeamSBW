---
title : "Week 4 Worklog"

weight : 1 
chapter : false
pre : " <b> 1.4. </b> "
---
## Week 4 Objectives:
- Learn fundamental AWS **S3 concepts** (storage, access control, data lifecycle).  
- Understand how to configure **S3 Buckets, Policies, ACLs**.  
- Explore **S3 storage classes and performance optimization**.  
- Learn about **disaster recovery, RTO, RPO, and AWS Backup**.  

---

## Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 1 | - Study **AWS S3 & Core Concepts**:<br>&nbsp;&nbsp;• Amazon S3<br>&nbsp;&nbsp;• S3 Bucket<br>&nbsp;&nbsp;• Access point<br>&nbsp;&nbsp;• Storage class<br>&nbsp;&nbsp;• S3 Static website<br>&nbsp;&nbsp;• S3 Control access<br>&nbsp;&nbsp;• S3 ACL<br>&nbsp;&nbsp;• S3 Bucket Policy<br>&nbsp;&nbsp;• S3 Endpoint<br>&nbsp;&nbsp;• Object Key & Performance | 09/29/2025 | 09/29/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 2 | - Study **Archival & Transfer Services**:<br>&nbsp;&nbsp;• Glacier<br>&nbsp;&nbsp;• Snowball, Snowball Edge, Snowmobile | 09/30/2025 | 09/30/2025 |[AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)  |
| 3 | - Study **Disaster Recovery Concepts**:<br>&nbsp;&nbsp;• RTO<br>&nbsp;&nbsp;• RPO<br>&nbsp;&nbsp;• AWS Backup | 10/01/2025 | 10/01/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 4 | - Practice Deploy AWS Backup to the System Labs: create S3 bucket, Deploy Infrastructure, Create Backup Plan, Set up notifications, Test Restore, Clean up resources | 10/02/2025 | 10/02/2025 | [LAB](https://000013.awsstudygroup.com/6-cleanup/) |
| 5 | - Practice Lab 57 again: Create S3 bucket, load data, config and test website | 10/03/2025 | 10/03/2025 | [LAB](https://000057.awsstudygroup.com/2-prerequiste/2.2-uploaddata/) |

---

## Week 4 Achievements

### 1 Studied **Amazon S3 & Core Concepts**

1. **Amazon S3 – The Infinite Warehouse**  
- Concept: S3 is an object storage service for storing unlimited amounts of data.  
- How it works: Stores data as objects (file + metadata) inside buckets.  
- Example: Like Google Drive for developers, scalable to petabytes.  

2. **S3 Bucket – The Container**  
- Concept: A container where objects are stored.  
- How it works: Each bucket has a globally unique name, region, and policies.  
- Example: Like a folder on your computer, but in the cloud.  

3. **Access Point – Guest Door**  
- Concept: A simplified entry point to access S3 buckets.  
- How it works: Each access point has its own hostname and permissions.  
- Example: Like giving a guest a separate door key to your warehouse.  

4. **Storage Class – Types of Shelves**  
- Concept: Defines durability, availability, and cost of storage.  
- How it works: Options include Standard, Intelligent-Tiering, One Zone-IA, Glacier, etc.  
- Example: Like choosing to store items in your bedroom (fast), basement (cheaper), or warehouse (cheap but far).  

5. **S3 Static Website – Public Exhibition**  
- Concept: Hosting static websites directly from S3.  
- How it works: Upload HTML/CSS/JS files, enable hosting, and access via URL.  
- Example: Like pinning posters on a public board for everyone to see.  

6. **S3 Control Access – Who Has the Keys**  
- Concept: Methods to control who can access data.  
- How it works: Controlled by IAM policies, bucket policies, ACLs, and access points.  
- Example: Like deciding which family members get house keys.  

7. **S3 Access Control List (ACL) – Guest List**  
- Concept: Legacy method for managing access.  
- How it works: Assigns read/write permissions to specific users.  
- Example: Like making a guest list for a party with different access levels.  

8. **S3 Bucket Policy – House Rules**  
- Concept: JSON-based rules for buckets.  
- How it works: Define who can access, what actions are allowed or denied.  
- Example: Like writing rules on the front door: “Open from 9AM–5PM only.”  

9. **S3 Endpoint – Private Road**  
- Concept: Private connection between VPC and S3.  
- How it works: Access S3 without traversing the public internet.  
- Example: Like building a secret underground road to the warehouse.  

10. **Object Key & Performance – Filing System**  
- Concept: Each object is identified by a unique key.  
- How it works: Key design affects performance; avoid sequential names.  
- Example: Like labeling documents in a filing cabinet for faster search.  

11. **Glacier – Deep Freeze Storage**  
- Concept: Low-cost archival storage.  
- How it works: Retrieval takes minutes to hours depending on request type.  
- Example: Like putting old files in a frozen vault.  

12. **Snowball, Snowball Edge, Snowmobile – Data Trucks**  
- Concept: Physical devices to transfer huge amounts of data.  
- How it works:  
  - Snowball: suitcase-sized, TB scale.  
  - Snowball Edge: with compute/storage for edge processing.  
  - Snowmobile: truck-sized, exabyte scale.  
- Example: Like shipping entire hard drives by truck instead of uploading.  

13. **Disaster Recovery – Backup Plan**  
- Concept: Strategies to restore systems after outages.  
- How it works: Uses backups, replication, and multi-region deployment.  
- Example: Like having a fire escape plan for your house.  

14. **Recovery Time Objective (RTO) – Downtime Tolerance**  
- Concept: Maximum downtime allowed.  
- How it works: Defines how quickly services must recover.  
- Example: Like promising to reopen a shop within 2 hours after blackout.  

15. **Recovery Point Objective (RPO) – Data Loss Tolerance**  
- Concept: Maximum acceptable data loss.  
- How it works: Defines the amount of data (in minutes/hours) you can lose.  
- Example: Like saying you can afford to lose notes from the last 10 minutes.  

16. **AWS Backup – Centralized Backup Service**  
- Concept: Fully managed service for automating AWS backups.  
- How it works: Supports EBS, RDS, DynamoDB, EFS, etc. with backup policies.  
- Example: Like hiring a service to automatically back up your house documents.
### 2. Practice labs 
 - Create S3 bucket
 ![Create S3](/images/1.worklog/022-worklog.png)
 - Create Folder
 ![Create Folder](/images/1.worklog/023-worklog.png)
 - Load data
 ![Load data](/images/1.worklog/024-worklog.png)
 - Configuring public access block
 ![Configuring public access block](/images/1.worklog/025-worklog.png)
 - Edit bucket policy
 ![Edit bucket policy](/images/1.worklog/026-worklog.png)
 ![Edit bucket policy](/images/1.worklog/027-worklog.png)
 - Deploy Infrastructure
 ![Create Stacks](/images/1.worklog/028-worklog.png)
 ![Stacks details](/images/1.worklog/029-worklog.png)
 ![confirm mail](/images/1.worklog/030-worklog.png)
 ![success](/images/1.worklog/031-worklog.png)
 - Create backup plan
 ![Create Backup plan](/images/1.worklog/032-worklog.png)
 ![Assign Resources](/images/1.worklog/033-worklog.png)
 - Set up notifications
 ![Setup notifications](/images/1.worklog/034-worklog.png)
 - Create on-demand backup
 ![Create on-demand backup](/images/1.worklog/035-worklog.png)
 - Test restore
 ![Mail confirm](/images/1.worklog/036-worklog.png)
 - Log stream
 ![Log](/images/1.worklog/037-worklog.png)
 - Clean resources
 - Delete SNS
 ![Delete SNS](/images/1.worklog/038-worklog.png)
 - Delete backup vault
 ![Delete backup vault](/images/1.worklog/039-worklog.png)
 - Delete backup plan
 ![Delete backup plan](/images/1.worklog/040-worklog.png)
 - Delete Stacks
 ![Delete stacks](/images/1.worklog/041-worklog.png)
 - Delete Log
 ![Delete log](/images/1.worklog/042-worklog.png)
 - Terminate EC2
 ![Delete EC2](/images/1.worklog/043-worklog.png)
---

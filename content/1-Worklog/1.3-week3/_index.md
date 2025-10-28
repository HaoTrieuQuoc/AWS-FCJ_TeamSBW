---
title : "Week 3 Worklog"

weight : 1 
chapter : false
pre : " <b> 1.3. </b> "
---
## Week 3 Objectives:
- Learn fundamental **AWS EC2 concepts** (compute, storage, networking).  
- Understand how to configure and connect to EC2 instances.  
- Explore **storage options**: EBS vs. Instance Store.  
- Learn **EC2 Auto Scaling** to optimize cost and performance.  

---

## Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 1-2 | - Study **AWS EC2 & Core Concepts**:<br>&nbsp;&nbsp;• Amazon EC2<br>&nbsp;&nbsp;• Instance type<br>&nbsp;&nbsp;• Hardware node<br>&nbsp;&nbsp;• Hypervisor<br>&nbsp;&nbsp;• Amazon Machine Image (AMI)<br>&nbsp;&nbsp;• Key pair<br>&nbsp;&nbsp;• Elastic Block Store (EBS)<br>&nbsp;&nbsp;• Instance store<br>&nbsp;&nbsp;• User data<br>&nbsp;&nbsp;• EC2 Metadata<br>&nbsp;&nbsp;• EC2 Auto Scaling | 09/22/2025 | 09/23/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 3 | - Practice backup plan Labs: Create backup plan, test restore and clean resources | 09/24/2025 | 09/24/2025 |[AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 4-5 | - Practice static website Labs: Create S3 bucket, load data, config and test website | 09/25/2025 | 09/25/2025 |[LAB](https://000057.awsstudygroup.com/2-prerequiste/2.2-uploaddata/) |


---

## Week 3 Achievements

### 1 Studied **Amazon EC2 & Core Concepts**

1. **Amazon EC2**  
- Concept: Amazon EC2 is like a virtual server (VM) or a physical server but hosted in AWS infrastructure.  
- How it works:  
 -You can quickly launch a VM within minutes.  
 -Choose CPU, RAM, disk size as needed.  
 -Resources can scale based on demand.  
- Example: Like renting a place in a data center instead of buying your own server.  

2. **Instance type**  
- Concept: The hardware configuration type for EC2 instances.  
- How it works: AWS offers predefined packages (t2.micro, m5.large, p3.2xlarge…) optimized for compute, memory, GPU, or I/O.  
- Example: Like choosing between an office laptop, a gaming laptop, or a workstation.  

3. **Hardware node**  
- Concept: The physical machine in AWS data centers running multiple EC2 instances.  
- How it works: Each hardware node has CPU, RAM, and disk, shared by customers through a hypervisor.  
- Example: Like an apartment building, each apartment is an EC2 instance.  

4. **Hypervisor**  
- Concept: The software layer that manages and divides hardware resources for EC2 instances.  
- How it works: Ensures isolation and distributes resources fairly among instances.  
- Example: Like the building management distributing electricity, water, and internet to apartments.  

5. **Amazon Machine Image (AMI)**  
- Concept: A template image to create EC2 instances.  
- How it works: Contains OS + pre-installed software. When launching EC2, you select an AMI to quickly get a ready environment.  
- Example: Like installing Windows with Office preloaded, or Ubuntu with Python.  

6. **Key pair**  
- Concept: A key pair (public + private) for authentication when logging into EC2.  
- How it works:  
 -Public key is stored in EC2.  
 -Private key is stored on your machine.  
 -SSH uses both to verify access.  
- Example: Like AWS holds the lock, and you hold the key.  

7. **Elastic Block Store (EBS)**  
- Concept: A block storage service attached to EC2.  
- How it works: Data persists even when the instance is stopped. Can be detached and reattached to other EC2s.  
- Example: Like an external hard drive you can plug into any machine.  

8. **Instance store**  
- Concept: Ultra-fast NVMe disk located on the physical node of EC2.  
- How it works:  
 -Data is lost when stopping the instance but not when restarting.  
 -No replication → not safe for critical data.  
- Example: Like a RAM disk or temporary SSD: very fast but volatile.  

9. **User data**  
- Concept: Script (bash, PowerShell…) that runs when EC2 boots for the first time.  
- How it works: Used to install software, update OS, configure environment automatically.  
- Example: Like giving a checklist to a store to pre-install apps on a new laptop.  

10. **EC2 Metadata**  
- Concept: Information about the instance (ID, IP, AMI, role, region…).  
- How it works: Accessed at http://169.254.169.254/latest/meta-data/.  
- Example: Like a nameplate outside the house with house number and owner info.  

11. **EC2 Auto Scaling**  
- Concept: Automatically adjusts the number of EC2 instances based on load.  
- How it works:  
  -If CPU/RAM usage is high → launches more EC2s.  
  -If load decreases → terminates extra EC2s to save cost.  
- Example: Like a supermarket opening more checkout counters when crowded, and closing them when quiet.  

### 2. Practice labs 
 - Create Backup plan
 ![Create Backup Plan](/images/1.worklog/013-worklog.png)
 ![Create Backup Plan](/images/1.worklog/014-worklog.png)
 - Create S3 Bucket
 ![Create S3 Bucket](/images/1.worklog/015-worklog.png)
 - Load data
 ![Load data](/images/1.worklog/016-worklog.png)
 - Enable static website feature
 ![Enable static website feature](/images/1.worklog/017-worklog.png)
 - Configuring public access block
 ![Configuring public access block](/images/1.worklog/018-worklog.png)
 - Configuring public objects
![Configuring public objects](/images/1.worklog/019-worklog.png)
 - Test website
![Test website](/images/1.worklog/020-worklog.png)
![Test website](/images/1.worklog/021-worklog.png)
---


---
title : "Week 2 Worklog"

weight : 1 
chapter : false
pre : " <b> 1.2. </b> "
---
## Week 2 Objectives:
- Learn fundamental AWS **networking concepts** (VPC, Subnets, Routing, Security, Connectivity).  
- Understand how to manage **traffic flow** and secure workloads inside VPC.  
- Gain insights into AWS connectivity options (Peering, Transit Gateway, VPN, Direct Connect).  
- Explore **Elastic Load Balancing** for distributing application traffic.  

---

## Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 1-3 | - Study **AWS Networking – VPC & Core Concepts**:<br>&nbsp;&nbsp;• Amazon VPC<br>&nbsp;&nbsp;• Subnets<br>&nbsp;&nbsp;• Route Tables<br>&nbsp;&nbsp;• Internet Gateway<br>&nbsp;&nbsp;• Elastic Network Interface (ENI)<br>&nbsp;&nbsp;• Interface Endpoint<br>&nbsp;&nbsp;• Gateway Endpoint<br>&nbsp;&nbsp;• Security Group<br>&nbsp;&nbsp;• Network ACL<br>&nbsp;&nbsp;• VPC Flow Logs<br>&nbsp;&nbsp;• VPC Peering<br>&nbsp;&nbsp;• Transit Gateway<br>&nbsp;&nbsp;• VPN Site-to-Site<br>&nbsp;&nbsp;• AWS Direct Connect<br>&nbsp;&nbsp;• Elastic Load Balancing | 09/15/2025 | 09/17/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 4   | - Practiced AWS Networking Labs: created and configured VPCs, subnets, route tables, security groups, and internet gateways  | 09/18/2025 | 09/18/2025 |[AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)  |
| 5   | - Practice AWS Networking Labs: Create EC2, test connect by using MobaXterm and putty, create NAT gateway | 09/19/2025 | 09/19/2025 | [EC2 ](https://000003.awsstudygroup.com/4-createec2server/4.2-connectec2/) |


---

## Week 2 Achievements

 ### 1 Studied **Amazon VPC & Networking** concepts, including:  
  
**CloudCity – Analogy for the Entire VPC**

 Imagine the components in a VPC as a city.

1. **Amazon VPC – The City**
- VPC = the city you build in the cloud.  
- Has a fixed area (CIDR block).  
- You own the whole infrastructure, divide it into districts, and manage traffic.  

2. **Subnets – Neighborhoods**
- Subnet = a neighborhood inside the city.  
- Each neighborhood belongs to one district (Availability Zone).  
- Public neighborhoods (connected to the highway) vs. private neighborhoods (internal only).  

3. **Route Tables – Maps**
- Route table = the map of each neighborhood.  
- Shows where traffic goes: “to the internet → through IGW”, “internal traffic → local route”.  

4. **Internet Gateway (IGW) – International Border Gate**
- IGW = the international border gate connecting the city to the outside world (Internet).  
- Only citizens with passports (Public IP/Elastic IP) can pass through.  

5. **Elastic Network Interface (ENI) – The Door to a House**
- ENI = the door of each apartment (instance).  
- Each door has a number (IP).  
- The door can be detached and attached to another house in the same district (AZ).  

6. **Interface Endpoint – VIP Tunnel**
- Interface Endpoint = a VIP tunnel inside the neighborhood.  
- Leads directly to government offices/services (S3, Systems Manager, CloudWatch, SaaS vendors).  
- No need to go through the border gate (IGW).  
- Protected by its own Security Group.  

7. **Gateway Endpoint – Special Toll Booth**
- Gateway Endpoint = a toll booth inside the city.  
- Connects only to two special places: the warehouse (S3) and the marketplace (DynamoDB).  
- Uses internal roads, no need to reach the highway.  

8. **Security Group – Door Guards**
- Security Group = guards standing at the door of each house (ENI).  
- They decide who can enter/exit.  
- Rules are stateful: if entry is allowed, return traffic is automatically allowed.  

9. **Network ACL (NACL) – Police Checkpoint at Neighborhood Entrance**
- NACL = police checkpoint at the entrance of the neighborhood (subnet).  
- Inspects everyone going in/out.  
- Rules are stateless: if inbound is allowed, outbound must be explicitly allowed too.  

10. **VPC Flow Logs – Surveillance Cameras**
- Flow Logs = traffic cameras installed in the city.  
- Record who goes where, and whether it succeeded or was blocked.  
- Useful for troubleshooting (traffic jam, illegal intrusion).  

11. **VPC Peering – Bridge Between Two Cities**
- Peering = a bridge connecting two cities.  
- Citizens can travel directly between them.  
- But only two cities at a time → no central transit (no “hub and spoke”).  

12. **Transit Gateway – Central Bus Station**
- Transit Gateway = the central bus station.  
- All cities connect here; to go anywhere, citizens pass through this hub.  
- Centralized management, no need to build separate bridges for each pair.  

13. **VPN Site-to-Site – Secret Tunnel**
- VPN = a secret tunnel between CloudCity and your real-world city (on-premises).  
- Protected by encryption (IPSec).  
- Citizens can travel safely through this tunnel.  

14. **AWS Direct Connect – Private Highway**
- Direct Connect = a private high-speed highway from your company’s headquarters to CloudCity.  
- Does not go through the Internet.  
- High speed, low latency, stable, no congestion.  
- Ideal for enterprises needing large bandwidth and reliability.  

15. **Elastic Load Balancing (ELB) – Traffic Roundabout**
- ELB = a roundabout at an intersection.  
- When cars (requests) arrive, the roundabout distributes them evenly across multiple roads (EC2 servers).  
- If one road is broken, the roundabout automatically blocks it, preventing cars from entering.  

 ### 2 Practice labs how to create VPC, EC2, subnets, route tables, security groups, and internet gateways:
 -Create VPC
 ![Create VPC](/images/1.worklog/002-worklog.png)
 -Create Subnet
 ![Create Subnet](/images/1.worklog/003-worklog.png)
 -Create Internet Gateway
 ![Create Internet Gateway](/images/1.worklog/004-worklog.png)
 -Create Route Table
 ![Create Route Table](/images/1.worklog/005-worklog.png)
 -Create Sercurity Groups
 ![Create Sercurity Groups](/images/1.worklog/006-worklog.png)
 -Create EC2
 ![Create EC2](/images/1.worklog/007-worklog.png)
 -Test Connection EC2
 ![Test connection EC2](/images/1.worklog/008-worklog.png)
 -Connection Private EC2
 ![Private key](/images/1.worklog/009-worklog.png)
 ![Succes to connect private key](/images/1.worklog/010-worklog.png)
 -Create NAT gateway
  ![NAT gateway](/images/1.worklog/011-worklog.png)
  ![NAT gateway](/images/1.worklog/012-worklog.png)
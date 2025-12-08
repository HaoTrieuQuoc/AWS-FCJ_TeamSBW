---
title : "Week 13 Worklog"

weight : 3
chapter : false
pre : " <b> 1.13 </b> "
---
# Week 13 Worklog (12/01/2025 – 12/07/2025)

## Week 13 Objectives
- Build the **real AWS environment** for the Batch-based Clickstream Analytics Platform.  
- Set up **OLTP EC2** and **S3 media bucket** for the e-commerce website.  
- Implement end-to-end **clickstream ingestion** (Browser → API Gateway → Lambda Ingest → S3 Raw).  
- Connect **Lambda ETL** to S3 via **S3 Gateway Endpoint** and schedule with **EventBridge**.  
- Provision **private EC2** for Data Warehouse + R Shiny, with temporary **NAT Gateway** for package installation.  
- Use **SSM Session Manager** through **Interface Endpoint** to access the private EC2 without public IP.  
- Finalize **Architecture V11** and prepare a working **demo** of the whole system.

---

## Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 1 | - Provision **Public EC2 (OLTP)** instance in `SBW_Project-vpc` for the e-commerce transactional database.<br>&nbsp;&nbsp;• Attach security group for HTTP/HTTPS/SSH (only from trusted IP).<br>&nbsp;&nbsp;• Prepare to host OLTP PostgreSQL (WebDB).<br>- Create **S3 bucket for product images** (e.g. `clickstream-s3-sbw`) and configure it as the media asset store for the Amplify web. | 12/01/2025 | 12/01/2025 | |
| 2 | - Implement **front-end event tracking** on the e-commerce web:<br>&nbsp;&nbsp;• Add JS handlers to capture clickstream events (page view, product view, add-to-cart, etc.).<br>&nbsp;&nbsp;• Send events to **Amazon API Gateway** endpoint.<br>- Configure **API Gateway → Lambda Ingest** integration, so that Lambda receives events and writes them as JSON into **S3 Raw bucket** (`clickstream-s3-ingest`). | 12/02/2025 | 12/02/2025 ||
| 3 | - Create **S3 Gateway Endpoint** inside VPC so **Lambda ETL** can access S3 privately (no Internet/NAT required).<br>- Update **Lambda ETL** code & configuration:<br>&nbsp;&nbsp;• Read raw files from `clickstream-s3-ingest`.<br>&nbsp;&nbsp;• Transform them into the 15-field schema for `clickstream_dw.clickstream_events`.<br>&nbsp;&nbsp;• Connect to private EC2 Data Warehouse via PostgreSQL and insert batch records. | 12/03/2025 | 12/03/2025 | |
| 4 | - Enable **Amazon EventBridge** rule (cron) to trigger **ETL Lambda** on a schedule (hourly).<br>- Verify EventBridge → Lambda ETL pipeline via **CloudWatch Logs**:<br>&nbsp;&nbsp;• Check that ETL runs on schedule.<br>&nbsp;&nbsp;• Confirm successful reads from S3 and inserts into PostgreSQL DWH. | 12/04/2025 | 12/04/2025 |  |
| 5 | - Redraw **Architecture V11** for the Batch Clickstream Platform:<br>&nbsp;&nbsp;• Public subnet: OLTP EC2, Internet Gateway, S3 Media Assets path via CloudFront/Amplify.<br>&nbsp;&nbsp;• Private subnet: DWH + R Shiny EC2, ETL Lambda integration, S3 Gateway Endpoint.<br>&nbsp;&nbsp;• Front-end side: Cognito, CloudFront, Amplify, API Gateway, Ingest Lambda, EventBridge.<br>&nbsp;&nbsp;• Management & Security: IAM, CloudWatch, SNS notifications, SSM, NAT usage only for setup. | 12/05/2025 | 12/05/2025 | |
| 6 | - Provision **Private EC2 (Analytics)** in the Analytics subnet for **PostgreSQL DWH + R Shiny**.<br>- Temporarily create and attach **NAT Gateway** for outbound Internet so the private EC2 can:<br>&nbsp;&nbsp;• Install **PostgreSQL 18**, **R**, **Shiny Server** and required R libraries.<br>&nbsp;&nbsp;• Apply OS updates and extra packages (build tools, drivers, etc.).<br>- After installation, verify that the private EC2 can run PostgreSQL and Shiny on internal ports. | 12/06/2025 | 12/06/2025 | |
| 7 | - Set up **SSM (Systems Manager) Session Manager** access for the private EC2:<br>&nbsp;&nbsp;• Attach IAM role with SSM permissions.<br>&nbsp;&nbsp;• Create **VPC Interface Endpoint** for SSM/SSMMessages in private subnet.<br>&nbsp;&nbsp;• Connect to EC2 via Session Manager (no SSH, no public IP).<br>- Run end-to-end **demo**:<br>&nbsp;&nbsp;• User interacts with web → clickstream events sent → Ingest Lambda → S3 Raw.<br>&nbsp;&nbsp;• EventBridge triggers ETL Lambda → read from S3 → load into PostgreSQL DWH on private EC2.<br>&nbsp;&nbsp;• Use **R Shiny on EC2 private** to query DWH and visualize clickstream dashboards via SSM port-forward or internal access.<br>- Confirm that the full **Batch-based Clickstream Analytics Platform** is functioning and ready for presentation. | 12/07/2025 | 12/07/2025 | [Demo](https://www.youtube.com/watch?v=7R0njqggGtg) <br> [Slides](https://www.canva.com/design/DAG6jKIgK_I/VihpZUen3NvYxEiWfoqukw/edit) <br> [Github](https://github.com/orgs/SBW-Cloudworks/repositories) |

---

## Week 13 Achievements

### 1. Public OLTP EC2 and Product Image S3 Bucket
- Created the **public EC2 OLTP instance** in `SBW_Project-vpc` to host the transactional PostgreSQL database for the e-commerce website.  
- Configured security groups so only required ports are open (HTTP/HTTPS for web, restricted DB access).  
- Set up **S3 media bucket** `clickstream-s3-sbw` to store product images and static assets used by the Next.js/Amplify front-end.

**Result:**  
Front-end can load assets from S3 via CloudFront, and OLTP EC2 is ready to support web transactions.

---

### 2. End-to-End Clickstream Ingestion (Browser → S3 Raw)
- Implemented event tracking in the web application (page views, product views, add-to-cart, etc.).  
- All events are sent to **Amazon API Gateway**, which forwards requests to **Lambda Ingest**.  
- Lambda Ingest validates payloads, enriches with timestamps and metadata, then writes JSON files into the **raw S3 bucket** `clickstream-s3-ingest` following a time-based prefix structure (e.g. `events/YYYY/MM/DD/HH/`).

**Result:**  
User interactions on the website are now reliably captured and stored as raw clickstream data in S3.

---

### 3. Lambda ETL Connected to S3 via Gateway Endpoint
- Created an **S3 Gateway Endpoint** for the VPC so ETL Lambda can read from S3 without needing Internet or NAT.  
- Updated ETL Lambda configuration (environment variables, IAM role) to:  
  - Read raw objects from `clickstream-s3-ingest`.  
  - Transform events into the fixed **15-field DWH schema** (`event_id`, `event_timestamp`, `event_name`, `user_id`, `user_login_state`, `identity_source`, `client_id`, `session_id`, `is_first_visit`, `product_id`, `product_name`, `product_category`, `product_brand`, `product_price`, `product_discount_price`, `product_url_path`).  
  - Insert rows into `clickstream_dw` on the private PostgreSQL DWH.

**Result:**  
ETL Lambda can now move data from S3 Raw to the DWH entirely over private networking.

---

### 4. EventBridge Scheduling for ETL
- Created an **EventBridge rule** with a cron/rate expression to trigger the ETL Lambda on a schedule (e.g., hourly).  
- Verified executions in **CloudWatch Logs**:  
  - Lambda is invoked on schedule.  
  - ETL logs show the number of files processed and rows inserted.  
  - Error handling added for malformed events or DB connection issues.

**Result:**  
The batch ETL pipeline is now automated and running without manual invocation.

---

### 5. Architecture Diagram V11
- Redrew the **Architecture V11** diagram to reflect the actual implementation:  
  - **Front-end layer:** Admin Browser → CloudFront → Amplify (Next.js app) → Cognito for authentication.  
  - **Ingestion layer:** API Gateway → Lambda Ingest → S3 Raw (`clickstream-s3-ingest`).  
  - **Batch processing layer:** EventBridge → Lambda ETL (in VPC) → S3 Gateway Endpoint → PostgreSQL DWH on private EC2.  
  - **Storage & compute:** Public EC2 OLTP, S3 media assets, private EC2 for DWH + R Shiny.  
  - **Management & security:** IAM, CloudWatch, SNS (notifications), SSM, Interface Endpoints, temporary NAT for setup.

**Result:**  
Architecture V11 is an accurate visual representation for documentation, proposal, and demo slides.
![Architecture](/images/2.proposal/SBW_Architecture_V11.jpg)
---

### 6. Private EC2 for DWH + R Shiny with Temporary NAT
- Launched **private EC2 (SBW_EC2_ShinyDWH)** in the Analytics subnet.  
- Temporarily created a **NAT Gateway** so this instance could reach the Internet and:  
  - Install **PostgreSQL 18** and create the `clickstream_dw` database and tables.  
  - Install **R**, **Shiny Server**, and required R packages for analytics dashboards.  
- After installation and verification, NAT usage was minimized to reduce cost (keeping the instance private—no public IP).

**Result:**  
Private analytics EC2 is fully prepared to host both the DWH and R Shiny dashboards.

---

### 7. SSM Session Manager via Interface Endpoint
- Configured IAM roles and **SSM Agent** on the private EC2.  
- Created **VPC Interface Endpoints** for `com.amazonaws.<region>.ssm` and `ssmmessages`, enabling Session Manager traffic entirely within the VPC.  
- Confirmed that we can:  
  - Start SSM sessions to the private EC2.  
  - Use port forwarding from local machine to access Shiny dashboards securely without exposing public ports.

**Result:**  
Secure, agent-based access to the private EC2 is in place, with no need for SSH keys or public exposure.

---

### 8. End-to-End Demo Completed
- Ran a full **end-to-end demo** of the Batch-based Clickstream Analytics Platform:

  1. User browses the e-commerce web on Amplify via CloudFront.  
  2. Cognito handles login / session.  
  3. Front-end sends clickstream events → API Gateway → Lambda Ingest → S3 Raw.  
  4. EventBridge triggers Lambda ETL → reads from S3 → loads into PostgreSQL DWH on private EC2.  
  5. R Shiny (on the same private EC2) queries `clickstream_dw` and displays dashboards showing user behavior, funnels, and product interactions.

- Confirmed that all major AWS components work together as planned and that the system is ready for presentation and further optimization.

**Overall Outcome:**  
Week 13 marks the **completion of the first full version** of the Batch Clickstream Analytics Platform: infrastructure, ingestion, ETL, DWH, and analytics dashboard are all connected and running in AWS.

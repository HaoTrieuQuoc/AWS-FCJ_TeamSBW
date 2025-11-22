---
title : "Week 9 Worklog"

weight : 1 
chapter : false
pre : " <b> 1.9. </b> "
---
## Week 9 Objectives:
- Research and understand how to **build and deploy** the e-commerce website on both local and AWS environments.  
- Study the extended functionality and placement of **Amazon CloudFront** and **AWS Amplify** in the system architecture.  
- Explore the usage of **LocalStack** to emulate AWS services locally before deploying.  
- Investigate required **Python libraries**, version compatibility, and packaging approaches.  
- Study how to implement **ORM** for database interaction.  
- Begin researching **Clickstream data** and how it will integrate into the project pipeline.  
- Review architecture flow and refine proposal structure.

---

## Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 1-2 | - Research and review initial steps of **building the e-commerce web app**:<br>&nbsp;&nbsp;• Understand how to build the web locally and future deployment steps.<br>&nbsp;&nbsp;• Study the next phase: preparing and uploading data.<br>&nbsp;&nbsp;• Research deeper into **Amazon CloudFront**: What else can it do besides speed improvement?<br>&nbsp;&nbsp;• Investigate whether **AWS Amplify** operates before or after CloudFront in the architecture. | 11/03/2025 | 11/04/2025 | [AWS CloudFront Docs](https://docs.aws.amazon.com/cloudfront/), [AWS Amplify Docs](https://docs.aws.amazon.com/amplify/) |
| 3 | - Research local development and testing environment:<br>&nbsp;&nbsp;• Study how to run and test the entire system locally before AWS deployment.<br>&nbsp;&nbsp;• Research **LocalStack** (AWS emulator) and compare Normal vs. BASE edition.<br>&nbsp;&nbsp;• Explore methods to standardize Python versions and package dependencies. | 11/05/2025 | 11/05/2025 | [LocalStack Documentation](https://docs.localstack.cloud/) |
| 4 | - Research backend development and architecture updates:<br>&nbsp;&nbsp;• Study **ORM** and how to apply it for database operations.<br>&nbsp;&nbsp;• Research Clickstream concepts and how data should be collected and processed.<br>&nbsp;&nbsp;• Review architecture: placement of CloudFront, need for Amplify, and replacing Supabase with PostgreSQL. | 11/06/2025 | 11/06/2025 |  |
| 5 | - Review and update project documentation:<br>&nbsp;&nbsp;• Review proposal structure and update the **title section**.<br>&nbsp;&nbsp;• Research architecture adjustments and identify missing components.<br>&nbsp;&nbsp;• Continue studying dependencies, database selection, and clickstream pipeline direction. | 11/07/2025 | 11/07/2025 | [Project Proposal](https://docs.google.com/document/d/1LPlnST1PFrpnswfhlIJCtlF_JvGE81YZZtocSGnTKIE/edit?tab=t.0) |

---

## Week 9 Achievements

### 1. Research on Web Build & Deployment
- Studied how the team successfully built the e-commerce website locally.  
- Understood the upcoming step: preparing and uploading sample data before connecting to AWS services.  

---

### 2. CloudFront & Amplify Research
- Explored additional capabilities of **Amazon CloudFront**, such as edge security, caching strategies, and global distribution.  
- Investigated where **AWS Amplify** fits in the hosting flow (before or after CloudFront). 

---

### 3. LocalStack & Local Testing Research
- Studied how to run AWS services locally using **LocalStack**.  
- Learned that **LocalStack BASE edition** supports more services (including Cognito), making it more suitable for the project.  
- Researched how to run local tests before deploying infrastructure on AWS.

---

### 4. Backend & Architecture Research
- Researched what **ORM** is and how it will help manage database operations cleanly.  
- Started learning about **Clickstream data**, its purpose, and how it will integrate into the pipeline.  
- Reviewed the architecture and identified updates such as integrating Amplify, PostgreSQL, and CloudFront.

---

### 5. Proposal Review & Documentation Improvements
- Updated the proposal, especially the **title section**.  
- Identified additional requirements and missing architecture components for the next phase.  
- Documented a clearer direction for upcoming tasks such as clickstream integration and Python environment setup.

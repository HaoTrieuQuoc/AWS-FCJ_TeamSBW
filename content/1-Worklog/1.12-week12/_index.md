---
title : "Week 12 Worklog"

weight : 2
chapter : false
pre : " <b> 1.12. </b> "
---
# **Week 12 Worklog (24/11 – 28/11)**

## **Week 12 Objectives**
- Deploy the **e-commerce web application** to **AWS Amplify** in a real AWS environment.  
- Enable and integrate **Amazon CloudFront** as CDN for performance and global delivery.  
- Integrate **Amazon Cognito** authentication with the web application.  
- Test the full authentication + browsing flow on Amplify + CloudFront.  
- Begin designing the **DataFrame schema**, including a consolidated clickstream schema and partitioning into 5 analytical tables.  
- Finalize and revise **Architecture v10** with updated networking, VPC design, and data flow.

---

## **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|-------|------------|-----------------|-------------------|
| 1-3 | - Deploy the **web application** to **AWS Amplify**:<br>&nbsp;&nbsp;• Configure build settings and connect repository.<br>&nbsp;&nbsp;• Enable **CloudFront** distribution through Amplify.<br>&nbsp;&nbsp;• Integrate **Cognito User Pool** authentication.<br> - Test deployment results and verify routing, login flow, and asset loading. | 24/11/2025 | 26/11/2025 | [Website NextJS](https://main.d2q6im0b1720uc.amplifyapp.com/) |
| 4 | - Validate web functionality on AWS:<br>&nbsp;&nbsp;• Check CloudFront caching behavior.<br>&nbsp;&nbsp;• Confirm Cognito login/signup works correctly.<br>&nbsp;&nbsp;• Identify unresolved issues (redirect loops, auth errors, missing assets). | 27/11/2025 | 27/11/2025 | |
| 5 | - Design the **clickstream DataFrame schema**:<br>&nbsp;&nbsp;• Draft one large unified DataFrame.<br>&nbsp;&nbsp;• Break into 4 analytical tables (session table, user table, event table, product table).<br>&nbsp;&nbsp;• Check mapping between raw S3 data → ETL Lambda → DWH tables. | 28/11/2025 | 28/11/2025 |[DataFrame](https://docs.google.com/spreadsheets/d/1DPQlxbmPu69gHe8x2ES4AC6FL0_TbxZ0uCro-jbFma0/edit?gid=1217315040#gid=1217315040)  |
| 6 | - Finalize **Architecture v10**:<br>&nbsp;&nbsp;• Apply subnet changes (Public OLTP EC2, Private Analytics EC2).<br>&nbsp;&nbsp;• Replace Interface Endpoint → **Gateway Endpoint** for S3.<br>&nbsp;&nbsp;• Remove Internal ALB and rewrite flow.<br>&nbsp;&nbsp;• Update ETL pipeline data movement.<br>&nbsp;&nbsp;• Ensure diagram aligns with actual AWS deployment. | 29/11/2025 | 29/11/2025 | |


---

## **Week 12 Achievements**

### **1. Successfully Deployed the Web Application to AWS Amplify**
- The web application was uploaded to AWS Amplify and built successfully.  
- Amplify created a managed hosting environment and automatically provisioned a CloudFront distribution.

**Outcome:**  
A fully functioning front-end deployed on AWS, accessible globally.

---

### **2. CloudFront Integration Activated**
- CloudFront automatically connected through Amplify hosting.  
- Verified performance boost through caching and CDN distribution.  
- Confirmed the flow:  
  **Client → CloudFront → Amplify → S3 assets**

**Example:**  
When accessing images and scripts, CloudFront served cached copies → much faster load time.

---

### **3. Cognito Authentication Integrated**
- Connected the web login and signup page with **Cognito User Pool**.  
- Successfully tested:  
  - User signup  
  - User login  
  - Token generation  
  - Redirect back to application

**How it works:**  
1. User logs in → Cognito verifies identity  
2. Cognito returns JWT tokens  
3. Web app uses tokens for authentication state

---

### **4. Tested Full Web Flow After Deployment**
Checked the following:

- Login / logout  
- Navigation  
- API Gateway connectivity  
- CloudFront cache invalidation  
- Missing asset paths  
- Amplify environment variables

**Found issues to fix later:**  
- Some routing paths require additional CloudFront rewrite rules  
- Cognito redirect URI requires refinement  
- A few assets did not load correctly after caching

---

### **5. Clickstream DataFrame Architecture Designed**
Created a single unified DataFrame containing:

- event_id
- event_timestamp
- event_name
- user_id
- user_login_state
- identity_source
- client_id
- session_id
- is_first_visit
- context_product_id
- context_product_name
- context_product_category
- context_product_brand
- context_product_price
- context_product_discount_price
- context_product_url_path

Then split into **5 analytical tables**:

1. **User Table** – identity profile  
2. **Session Table** – session-level metrics  
3. **Event Table** – raw event logs  
4. **Product Table** – product-related context  


**Purpose:**  
Optimize analytics queries and reduce storage overhead.

---

### **6. Architecture v10 Finalized**
Reviewed all changes and confirmed they match deployment strategy.

#### **Key Modifications:**

- **EC2 OLTP moved to Public Subnet** → supports package installation & operational ease  
- **Internal ALB removed** → simplified architecture  
- **Gateway Endpoint added** → allows Lambda to access S3 privately  
- **ETL Lambda flow updated** → more direct and clearer  
- **Shiny Server + EC2 Analytics subnet refined**  
- **Amplify + CloudFront clarified** in diagram

![Architecture](/images/2.proposal/SBW_Architecture_V10.jpg)

---

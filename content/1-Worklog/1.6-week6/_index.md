---
title : "Week 6 Worklog"

weight : 1 
chapter : false
pre : " <b> 1.6. </b> "
---
## Week 6 Objectives:
- Strengthen understanding of **Database Concepts** including **Session**, **Primary Key**, **Foreign Key**, **Index**, **Partitions**, **Execution Plan**, **Database Log**, **Buffer**, **RDBMS**, **NoSQL**, **OLTP**, and **OLAP**.  
- Explore AWS-managed database services: **Amazon RDS**, **Amazon Aurora**, **Amazon ElastiCache**, and **Amazon Redshift**.  
- Learn how relational and non-relational databases support different workloads such as **transactional processing** and **analytical processing**.  
- Continue project preparation: Define project requirements and making architecture and estimate the cost of each AWS service

---

## Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 1-2 | - Study **Database Concepts**:<br>&nbsp;&nbsp;• Database<br>&nbsp;&nbsp;• Session<br>&nbsp;&nbsp;• Primary Key<br>&nbsp;&nbsp;• Foreign Key<br>&nbsp;&nbsp;• Index<br>&nbsp;&nbsp;• Partitions<br>&nbsp;&nbsp;• Execution Plan<br>&nbsp;&nbsp;• Database Log<br>&nbsp;&nbsp;• Buffer<br>&nbsp;&nbsp;• RDBMS<br>&nbsp;&nbsp;• NoSQL<br>&nbsp;&nbsp;• OLTP<br>&nbsp;&nbsp;• OLAP | 10/13/2025 | 10/14/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)  |
| 3| - Learn AWS Database Services:<br>&nbsp;&nbsp;• Amazon RDS<br>&nbsp;&nbsp;• Amazon Aurora<br>&nbsp;&nbsp;• Amazon ElastiCache<br>&nbsp;&nbsp;• Amazon Redshift | 10/15/2025 | 10/15/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)  |
| 4 | - Define **Project Objectives and Requirements**:<br>&nbsp;&nbsp;• Identify the main goal of the project and the key problems it aims to solve.<br>&nbsp;&nbsp;• Research suitable AWS services that can be integrated into the architecture (e.g., data collection, processing, storage, and analytics components).<br>&nbsp;&nbsp;• Discuss and align project scope and solution direction with all team members.| 10/16/2025 | 10/16/2025 |  |
| 5 | - **Design the Project Architecture and Estimate Costs**:<br>&nbsp;&nbsp;• Build a detailed architecture diagram that includes components such as **Amazon CloudFront**, **Amazon S3**, **Amazon Cognito**, **API Gateway**, **Amazon EBS**, **AWS Lambda**, **IAM**, **Amazon CloudWatch**, **Amazon SNS**, **Amazon EventBridge**, and **Amazon EC2** (for Data Warehouse and R Shiny).<br>&nbsp;&nbsp;• Estimate the cost of each AWS service used in the design.<br>&nbsp;&nbsp;• Ensure scalability, security, and cost-efficiency are considered in the architecture plan. | 10/17/2025 | 10/17/2025 | [Proposal](https://docs.google.com/document/d/1LPlnST1PFrpnswfhlIJCtlF_JvGE81YZZtocSGnTKIE/edit?tab=t.0)  |

---

## Week 6 Achievements

### 1. Database Concepts

#### **Database**
- **Concept:** A database is a structured storage system used to organize, manage, and retrieve data efficiently.  
- **How it works:** Data is stored in tables consisting of rows (records) and columns (fields). Users or applications query the data using SQL or APIs.  
- **Example:** Like a student notebook — each page represents a table, and each row is a student’s record.

---

#### **Session**
- **Concept:** A session represents an active connection between a user and the database system.  
- **How it works:** When a user logs in, a session is created to maintain the user’s state until they log out.  
- **Example:** Similar to a work shift — during the shift, you can perform tasks, but once it ends, all activity stops.

---

#### **Primary Key**
- **Concept:** A primary key uniquely identifies each record in a table.  
- **How it works:** Each table can have only one primary key, and its values must be unique and non-null.  
- **Example:** A “Student ID” in a student table acts as a unique identifier.

---

#### **Foreign Key**
- **Concept:** A foreign key links two tables by referencing the primary key of another table.  
- **How it works:** It ensures referential integrity between related data.  
- **Example:** The “StudentID” column in a “Scores” table references the “StudentID” in the “Students” table.

---

#### **Index**
- **Concept:** An index improves query performance by speeding up data retrieval.  
- **How it works:** It stores a separate data structure (commonly a B-Tree) that helps locate records faster without scanning the whole table.  
- **Example:** Like a book’s index page that helps you find topics quickly.

---

#### **Partitions**
- **Concept:** Partitioning divides a large table into smaller, manageable pieces.  
- **How it works:** Data is split by criteria such as date, region, or ID to improve query speed and maintenance.  
- **Example:** A sales table partitioned by year: 2023, 2024, 2025.

---

#### **Execution Plan**
- **Concept:** The execution plan is a detailed map of how a database executes a SQL query.  
- **How it works:** The SQL optimizer determines the most efficient way to access the required data using indexes, joins, and filters.  
- **Example:** Like Google Maps suggesting the fastest route to your destination.

---

#### **Database Log**
- **Concept:** A record of all database operations such as insert, update, or delete.  
- **How it works:** Logs help restore or audit data changes in case of system failure.  
- **Example:** Like a surveillance camera recording every action for review later.

---

#### **Buffer**
- **Concept:** A temporary memory area used to store frequently accessed data.  
- **How it works:** Data that is repeatedly read is cached in the buffer to speed up future access.  
- **Example:** Similar to a web browser cache that loads pages faster upon revisit.

---

#### **RDBMS (Relational Database Management System)**
- **Concept:** A system that manages relational databases using structured tables and SQL.  
- **How it works:** Data is organized into tables with defined relationships and constraints.  
- **Example:** MySQL, PostgreSQL, and Oracle Database.

---

#### **NoSQL**
- **Concept:** A non-relational database system that supports flexible data storage.  
- **How it works:** Stores data in document, key-value, graph, or column-based models.  
- **Example:** MongoDB stores data as JSON-like documents, ideal for dynamic web apps.

---

#### **OLTP (Online Transaction Processing)**
- **Concept:** A system designed for fast and reliable transaction processing.  
- **How it works:** Handles frequent CRUD operations (Create, Read, Update, Delete) with small datasets.  
- **Example:** Online shopping transactions on Shopee or Lazada.

---

#### **OLAP (Online Analytical Processing)**
- **Concept:** A system used for large-scale data analysis and reporting.  
- **How it works:** Aggregates and processes data from multiple dimensions for business insights.  
- **Example:** Analyzing sales performance by region and time to support strategic decisions.

---

### 2. AWS Database Services

#### **Amazon RDS (Relational Database Service)**
- **Concept:** A fully managed relational database service by AWS.  
- **How it works:** AWS handles deployment, backup, updates, and scaling; users focus only on data and queries.  
- **Features:**  
  - Supports multiple engines (MySQL, PostgreSQL, Oracle, SQL Server, MariaDB, Aurora).  
  - Automated backups and recovery.  
  - Auto-scaling and performance monitoring.  
- **Example:** A company uses RDS to store customer data without maintaining database servers.

---

#### **Amazon Aurora**
- **Concept:** A high-performance relational database compatible with MySQL and PostgreSQL.  
- **How it works:** Data is stored in six copies across three Availability Zones for durability and availability.  
- **Features:**  
  - Up to 5x faster than MySQL and 3x faster than PostgreSQL.  
  - Automatically scales up to 128 TB of storage.  
  - Integrated with AI and analytics (Aurora ML, Aurora Serverless).  
- **Example:** An e-commerce website uses Aurora to process thousands of transactions per minute.

---

#### **Amazon ElastiCache**
- **Concept:** A fully managed in-memory caching service that improves application performance.  
- **How it works:** Frequently accessed data is stored in RAM instead of being retrieved from a slower database.  
- **Features:**  
  - Supports Redis and Memcached.  
  - Sub-millisecond latency.  
  - Easily integrates with RDS or web applications.  
- **Example:** A website caches user query results so returning visitors get faster load times.

---

#### **Amazon Redshift**
- **Concept:** A fully managed data warehouse optimized for large-scale analytics.  
- **How it works:** Stores data in a columnar format, allowing complex analytical queries to run much faster.  
- **Features:**  
  - Handles petabytes of data efficiently.  
  - Integrates with S3, Glue, and QuickSight for complete analytics pipelines.  
  - Supports standard SQL syntax.  
- **Example:** A company analyzes billions of clickstream events in Redshift to understand user behavior.

---
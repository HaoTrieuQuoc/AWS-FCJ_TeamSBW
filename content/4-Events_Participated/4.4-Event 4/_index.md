---
title : "Event 4"

weight : 2
chapter : false
pre : " <b> 4.4 </b> "
---
# “DevOps on AWS”

**Venue:** Bitexco Financial Tower
**Date:** Monday, November 17, 2025  

## Event Objectives
- Reinforce DevOps mindset and culture, connecting principles to measurable outcomes
- Introduce key DevOps performance metrics (DORA, MTTR, deployment frequency) and how teams use them
- Provide a practical walkthrough of AWS CI/CD services and common deployment strategies
- Teach Infrastructure as Code (IaC) fundamentals with CloudFormation and AWS CDK
- Explain containerization and container services on AWS (ECR, ECS, EKS, App Runner) with real comparisons
- Cover monitoring & observability using CloudWatch and AWS X-Ray with best practices for alerting and on-call

## Speakers
- **Thịnh Nguyễn**
- **Bảo Huỳnh**
- **Huỳnh Hoàng Long**
- **Trần Vĩ**

## Key Highlights

### DevOps Mindset
- **Recap of AI/ML session:** Connecting AI/ML/GenAI topics with delivery and operations practices
- **DevOps culture and principles:** Collaboration, shared ownership, automation, and continuous improvement
- **Benefits and key metrics:** Using measurable indicators to guide improvements
  - **DORA metrics:** Deployment frequency, lead time for changes, change failure rate, time to restore service
  - **MTTR:** How teams reduce recovery time through better processes and observability

### AWS DevOps Services — CI/CD Pipeline
- **Source control:** AWS CodeCommit and Git strategies (GitFlow, Trunk-based)
- **Build & test:** CodeBuild configuration and structuring test stages in pipelines
- **Deployment:** CodeDeploy strategies and when to use each
  - **Blue/Green:** Safe cutover with easy rollback
  - **Canary:** Gradual rollout to reduce blast radius
  - **Rolling:** Progressive replacement for steady updates
- **Orchestration:** CodePipeline automation for end-to-end CI/CD
- **Demo:** Full CI/CD pipeline walkthrough (commit → build/test → deploy)

### Infrastructure as Code (IaC)
- **CloudFormation:** Templates, stacks, and drift detection for managing infrastructure lifecycle
- **AWS CDK:** Constructs, reusable patterns, and multi-language support
- **Demo:** Deploying infrastructure with CloudFormation and CDK
- **Choosing IaC tools:** Factors to decide between CloudFormation and CDK based on team needs

### Container Services on AWS
- **Docker fundamentals:** Microservices mindset and containerization basics
- **Amazon ECR:** Image storage, scanning, and lifecycle policies
- **Amazon ECS & EKS:** Deployment strategies, scaling, and orchestration trade-offs
- **AWS App Runner:** Simplified container deployment for faster iteration
- **Demo & case study:** Comparing microservices deployment approaches across services

### Monitoring & Observability
- **CloudWatch:** Metrics, logs, alarms, and dashboards for operational visibility
- **AWS X-Ray:** Distributed tracing and performance insights
- **Demo:** Full-stack observability setup (metrics + logs + tracing)
- **Best practices:** Alerting, dashboards, and on-call processes

## Key Takeaways

### Design Mindset
- **DevOps is culture + practice:** Tools only work when teams share ownership and collaborate end-to-end
- **Measure what matters:** DORA metrics and MTTR provide a baseline to improve delivery performance
- **Smaller changes reduce risk:** Frequent, incremental deployments improve reliability and rollback speed

### Technical Architecture
- **CI/CD as a system:** Source → build/test → deploy → observe; each stage must be automated and auditable
- **Deployment strategies matter:** Blue/Green, Canary, Rolling should match risk tolerance and traffic patterns
- **IaC for consistency:** CloudFormation/CDK improves repeatability and reduces configuration drift
- **Containers need discipline:** Scanning, lifecycle policies, and orchestration choice impact stability and security
- **Observability is essential:** Metrics + logs + traces reduce diagnosis time and improve MTTR

### Modernization Strategy
- **Standardize delivery foundations:** Git strategy, testing, CI/CD templates, and environment promotion flow
- **Adopt IaC early:** Avoid manual configuration and enforce governance as systems grow
- **Operational readiness:** Dashboards, alerting, and on-call processes must mature alongside the platform

### Applying to Work
- **Define a pipeline baseline:** Create reusable CI/CD templates with testing and safe deployment patterns
- **Select IaC approach:** Use CDK for reusable abstractions, CloudFormation for strict template stacks (or combine)
- **Choose container platform intentionally:** ECS, EKS, or App Runner based on complexity and team 운영 능력
- **Implement observability standards:** Centralized dashboards, actionable alarms, and trace instrumentation
- **Reduce MTTR:** Improve runbooks, alert quality, tracing coverage, and incident workflows

## Event Experience
Attending “DevOps on AWS” provided a practical view of modern delivery—from DevOps principles and metrics to real AWS implementations for CI/CD, IaC, containers, and observability. The demos and comparisons (Git strategies, deployment patterns, ECS/EKS/App Runner, CloudFormation vs CDK) made it easier to understand how to choose the right approach based on team maturity, risk tolerance, and operational needs.

## Some event photos
![Event 4](/images/4.events_participated/event4_pic1.png)
![Event 4](/images/4.events_participated/event4_pic2.png)

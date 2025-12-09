---
title : "Event 5"

weight : 2
chapter : false
pre : " <b> 4.5 </b> "
---
# “AWS Well-Architected — Security Pillar”

**Venue:** Bitexco Financial Tower
**Date:** 29/11/2025  

## Event Objectives
- Understand the role of the **Security Pillar** in the AWS Well-Architected Framework
- Learn core security principles for cloud environments: **Least Privilege**, **Zero Trust**, **Defense in Depth**
- Clarify the **Shared Responsibility Model** and common cloud security misunderstandings
- Identify typical cloud security threats observed in Vietnam and how to mitigate them
- Build practical knowledge across 5 security areas: **IAM**, **Detection**, **Infrastructure Protection**, **Data Protection**, **Incident Response**
- Practice security validation through mini demos and actionable patterns (automation, monitoring, guardrails)

## Speakers
- **Huỳnh Hoàng Long**
- **Đinh Lê Hoàng Anh**
- **Trần Đức Anh**
- **Nguyễn Tuấn Thịnh**
- **Nguyễn Đỗ Thành Đạt**
- **Kha Van**
- **Thịnh Lâm**
- **Việt Nguyễn**
- **Mendel Grabski (Long)**
- **Tinh Truong**

## Key Highlights

### Opening & Security Foundation
- **Security Pillar overview:** How security fits into Well-Architected and why it must be designed intentionally
- **Core principles:** Applying **Least Privilege**, **Zero Trust**, and **Defense in Depth** as baseline thinking
- **Shared Responsibility Model:** Clear boundaries of what AWS secures vs what customers must secure
- **Top cloud threats in Vietnam:** Common risk patterns, misconfigurations, and attack surfaces seen in real environments

### Pillar 1 — Identity & Access Management (Modern IAM Architecture)
- **IAM fundamentals:** Users, roles, policies and why to avoid long-term credentials
- **Modern access model:** Using **IAM Identity Center** for SSO and permission sets
- **Multi-account control:** Applying **SCP** and **permission boundaries** to prevent over-privileged access
- **Hardening practices:** MFA, credential rotation, and IAM Access Analyzer for continuous review
- **Mini demo:** Validate IAM policy and simulate access to verify least-privilege in practice

### Pillar 2 — Detection (Detection & Continuous Monitoring)
- **Foundational services:** Org-level **CloudTrail**, **GuardDuty**, and **Security Hub**
- **Logging everywhere:** VPC Flow Logs and service logs (e.g., ALB/S3 logs) to create complete visibility
- **Alerting & automation:** Using **EventBridge** to route findings and trigger responses
- **Detection-as-Code:** Managing detection infrastructure and rules as code for consistency and scaling

### Pillar 3 — Infrastructure Protection (Network & Workload Security)
- **Network segmentation:** VPC design thinking, and when to place workloads in private vs public
- **SG vs NACL:** How to choose and combine them correctly in real architectures
- **Edge & network defense:** Using **WAF**, **Shield**, and **Network Firewall** as layered protection
- **Workload protection basics:** Security baseline for EC2 and container platforms (ECS/EKS)

### Pillar 4 — Data Protection (Encryption, Keys & Secrets)
- **KMS fundamentals:** Key policies, grants, and rotation strategy
- **Encryption best practices:** Encryption at-rest and in-transit across common services (S3, EBS, RDS, DynamoDB)
- **Secrets handling:** **Secrets Manager** and **Parameter Store** patterns, including rotation and access controls
- **Governance:** Data classification and guardrails to control who can access what and under which conditions

### Pillar 5 — Incident Response (IR Playbook & Automation)
- **IR lifecycle on AWS:** Structured approach from detection → containment → eradication → recovery → post-incident review
- **Practical playbooks:** High-frequency scenarios in real operations
  - Compromised IAM key
  - S3 public exposure
  - EC2 malware detection
- **Response actions:** Snapshotting, isolation, evidence collection, and safe recovery procedures
- **Automation:** Auto-response patterns using **Lambda** and **Step Functions** to reduce response time and human error

### Wrap-Up & Q&A
- **Summary of 5 pillars:** How IAM, detection, infrastructure, data, and IR connect into one security system
- **Common pitfalls in Vietnam enterprises:** Typical misconfigurations and operational gaps
- **Learning roadmap:** Suggested security upskilling path (Security Specialty, SA Pro)

## Key Takeaways

### Design Mindset
- **Security is an architecture requirement:** It must be designed early, not added later
- **Defense in depth wins:** Layered controls reduce blast radius when a single control fails
- **Least privilege by default:** Access should be minimal, time-bound, and continuously reviewed

### Technical Architecture
- **Identity is the new perimeter:** Modern IAM requires role-based access, SSO, MFA, and strong boundaries
- **Detect continuously:** CloudTrail + GuardDuty + Security Hub form the baseline, but logging must cover all layers
- **Network segmentation matters:** Private placement, correct SG/NACL usage, and edge protection reduce exposure
- **Encrypt everything:** Keys, secrets, and encryption policies must be managed with KMS and proper governance
- **Automate incident response:** Playbooks + automation reduce MTTR and improve consistency under pressure

### Modernization Strategy
- **Adopt multi-account governance:** Use SCP and permission boundaries to scale security safely
- **Treat detection as code:** Standardize monitoring and alerts across environments
- **Operationalize security:** Runbooks, dashboards, evidence collection procedures, and post-mortems must be part of the system

### Applying to Work
- **Audit IAM posture:** Remove long-term credentials, enforce MFA, and validate policies via simulation
- **Turn on baseline detection:** Org-level CloudTrail, GuardDuty, Security Hub, and log centralization
- **Harden network posture:** Review VPC segmentation, ingress/egress, and WAF/Shield needs
- **Implement secrets strategy:** Move secrets out of code, enforce rotation, and restrict access
- **Create IR playbooks:** Start with top scenarios (IAM key leak, S3 exposure, malware) and add automation gradually

## Event Experience
Attending the “AWS Well-Architected — Security Pillar” workshop gave me a structured view of cloud security as a complete system rather than isolated tools. The content connected foundational principles (least privilege, zero trust, defense in depth) with concrete implementation patterns across IAM, monitoring, infrastructure protection, encryption, and incident response. The mini demo and playbook examples made the session highly practical, especially for real-world enterprise environments in Vietnam where misconfigurations and operational gaps are common.

## Some event photos
![Event 5](/images/4.events_participated/event5.png)
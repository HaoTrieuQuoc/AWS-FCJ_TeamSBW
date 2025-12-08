--- 
title : "Week 7 Worklog"

weight : 1 
chapter : false
pre : " <b> 1.7. </b> "
---
## Mục tiêu của Week 7:
- Review và củng cố hiểu biết về **AWS Core Architecture Principles** bao gồm **Secure**, **Resilient**, **High-Performing**, và **Cost-Optimized Architectures**.  
- Hiểu các AWS security và networking services quan trọng như **IAM**, **MFA**, **KMS**, **VPC**, **Security Groups**, **Auto Scaling**, **Route 53**, và **Load Balancing**.  
- Hợp tác với các thành viên trong team để **chuẩn bị một Project Proposal chi tiết**, bao gồm toàn bộ sections từ executive summary đến expected outcomes.  
- Bắt đầu refine **project architecture và giai đoạn planning** dựa trên AWS Well-Architected Framework.

---

## Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 1-2 | - Học và review các khái niệm trong **AWS Well-Architected Framework**:<br>&nbsp;&nbsp;• Secure Architectures: IAM, MFA, SCP, Encryption (KMS, TLS/ACM), Security Groups, NACLs, GuardDuty, Shield, WAF, Secrets Manager.<br>&nbsp;&nbsp;• Resilient Architectures: Multi-AZ, Multi-Region, DR Strategies, Auto Scaling, Route 53, Load Balancing, Backup & Restore.<br>&nbsp;&nbsp;• High-Performing Architectures: Compute scaling (EC2 Auto Scaling, Lambda, Fargate), Storage (S3, EFS, EBS), và Content Optimization (CloudFront, Global Accelerator).<br>&nbsp;&nbsp;• Cost-Optimized Architectures: Cost Explorer, Budgets, Savings Plans, Lifecycle Policies, NAT Gateway Optimization, và Storage Tiering. | 10/20/2025 | 10/21/2025 | |
| 3-4 | - Làm việc cùng team để draft **Project Proposal** bao gồm:<br>&nbsp;&nbsp;1. Executive Summary<br>&nbsp;&nbsp;2. Problem Statement<br>&nbsp;&nbsp;3. Solution Architecture<br>&nbsp;&nbsp;4. Technical Implementation<br>&nbsp;&nbsp;5. Timeline & Milestones<br>&nbsp;&nbsp;6. Budget Estimation<br>&nbsp;&nbsp;7. Risk Assessment<br>&nbsp;&nbsp;8. Expected Outcomes | 10/22/2025 | 10/23/2025 | [Proposal](https://docs.google.com/document/d/1LPlnST1PFrpnswfhlIJCtlF_JvGE81YZZtocSGnTKIE/edit?tab=t.0) |
| 5 | Review kiến thức cho kỳ thi giữa kỳ FCJ | 10/24/2025 | 10/24/2025 |  |

---

## Week 7 Achievements

### 1. AWS Well-Architected Framework Review

#### **Secure Architectures**
- **Concept:** Đảm bảo dữ liệu và hệ thống được bảo vệ thông qua identity control, encryption và threat detection.  
- **How it works:** Sử dụng IAM cho access control, MFA cho authentication, KMS cho encryption và các services như GuardDuty và WAF cho việc giám sát liên tục.  
- **Example:** Một web application sử dụng IAM roles, S3 buckets đã được mã hóa và WAF để chặn các malicious requests.

---

#### **Resilient Architectures**
- **Concept:** Được thiết kế để duy trì availability và phục hồi nhanh chóng sau failures.  
- **How it works:** Deploy workloads trên môi trường Multi-AZ hoặc Multi-Region, dùng Route 53 cho DNS routing và Auto Scaling cho elasticity.  
- **Example:** Một e-commerce platform sẽ tự động redirect traffic sang region khác nếu một region gặp sự cố.

---

#### **High-Performing Architectures**
- **Concept:** Tập trung vào scalability và tối ưu performance cho workloads.  
- **How it works:** Sử dụng EC2 Auto Scaling và Lambda cho compute động, EBS/EFS cho storage và CloudFront để tối ưu content delivery.  
- **Example:** Một video streaming platform sử dụng CloudFront để phân phối video với độ trễ thấp đến người dùng toàn cầu.

---

#### **Cost-Optimized Architectures**
- **Concept:** Tối thiểu hóa chi phí trong khi vẫn đảm bảo performance và reliability.  
- **How it works:** Dùng AWS Budgets, Savings Plans và Cost Explorer để theo dõi và tối ưu resource usage. Lifecycle policies và storage tiering giúp giảm chi phí hơn nữa.  
- **Example:** Một analytics system archive dữ liệu cũ sang S3 Glacier để tiết kiệm chi phí lưu trữ.

---

### 2. Project Proposal Development

#### **Executive Summary**
- Tóm tắt mục tiêu dự án và mục đích chính, nêu rõ giá trị và outcomes mong đợi từ giải pháp được đề xuất.

#### **Problem Statement**
- Xác định các vấn đề business và technical cần giải quyết, chỉ ra inefficiencies và challenges trong hệ thống hiện tại.

#### **Solution Architecture**
- Thiết kế sơ đồ kiến trúc ban đầu tích hợp các AWS services như S3, Lambda, CloudFront, API Gateway và RDS để đáp ứng yêu cầu dự án.

#### **Technical Implementation**
- Mô tả cách mỗi component sẽ được deploy và kết nối, bao gồm data flow, backend services và authentication bằng AWS Cognito.

#### **Timeline & Milestones**
- Tạo roadmap rõ ràng cho các giai đoạn development gồm research, design, implementation và testing.

#### **Budget Estimation**
- Tính toán chi phí ban đầu bằng AWS Pricing Calculator cho các core services như EC2, S3, CloudWatch và CloudFront.

#### **Risk Assessment**
- Xác định các rủi ro tiềm ẩn như vượt chi phí, giới hạn dịch vụ hoặc latency; đề xuất chiến lược giảm thiểu.

#### **Expected Outcomes**
- Xác định các kết quả có thể đo lường: cải thiện performance, giảm latency và xử lý dữ liệu hiệu quả bằng các AWS-managed services.

---

### 3. Team Collaboration
- Tất cả thành viên đóng góp vào việc viết proposal, nghiên cứu và thảo luận kiến trúc.  
- Tổ chức các buổi họp online để refine ý tưởng và đảm bảo tuân thủ yêu cầu **Track 4 FCJ**.  
- Hoàn thiện bản draft của project proposal để gửi giảng viên feedback.

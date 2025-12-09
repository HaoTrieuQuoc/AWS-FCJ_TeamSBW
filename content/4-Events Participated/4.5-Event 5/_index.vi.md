---
title : "Event 5"

weight : 2
chapter : false
pre : " <b> 4.5 </b> "
---
# “AWS Well-Architected — Security Pillar”

**Địa điểm:** Bitexco Financial Tower
**Ngày:** 29/11/2025  

## Mục tiêu sự kiện
- Hiểu vai trò của **Security Pillar** trong AWS Well-Architected Framework
- Học các nguyên tắc bảo mật cốt lõi cho môi trường cloud: **Least Privilege**, **Zero Trust**, **Defense in Depth**
- Làm rõ **Shared Responsibility Model** và các hiểu nhầm phổ biến về cloud security
- Nhận diện các mối đe doạ cloud security thường gặp tại Việt Nam và cách giảm thiểu
- Xây dựng kiến thức thực tiễn theo 5 nhóm bảo mật: **IAM**, **Detection**, **Infrastructure Protection**, **Data Protection**, **Incident Response**
- Thực hành security validation thông qua mini demos và các pattern có thể áp dụng ngay (automation, monitoring, guardrails)

## Diễn giả
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

### Khai mạc & Nền tảng bảo mật
- **Tổng quan Security Pillar:** Security nằm ở đâu trong Well-Architected và vì sao phải được thiết kế có chủ đích
- **Nguyên tắc cốt lõi:** Áp dụng **Least Privilege**, **Zero Trust**, và **Defense in Depth** như tư duy nền tảng
- **Shared Responsibility Model:** Ranh giới rõ ràng giữa phần AWS bảo vệ vs phần khách hàng phải bảo vệ
- **Top cloud threats ở Việt Nam:** Các pattern rủi ro phổ biến, misconfigurations, và attack surfaces trong môi trường thực tế

### Pillar 1 — Identity & Access Management (Modern IAM Architecture)
- **IAM fundamentals:** Users, roles, policies và vì sao nên tránh long-term credentials
- **Modern access model:** Dùng **IAM Identity Center** cho SSO và permission sets
- **Multi-account control:** Áp dụng **SCP** và **permission boundaries** để ngăn over-privileged access
- **Hardening practices:** MFA, credential rotation, và IAM Access Analyzer để review liên tục
- **Mini demo:** Validate IAM policy và simulate access để kiểm chứng least-privilege trong thực tế

### Pillar 2 — Detection (Detection & Continuous Monitoring)
- **Foundational services:** Org-level **CloudTrail**, **GuardDuty**, và **Security Hub**
- **Logging everywhere:** VPC Flow Logs và service logs (ví dụ: ALB/S3 logs) để tạo visibility đầy đủ
- **Alerting & automation:** Dùng **EventBridge** để route findings và trigger phản hồi
- **Detection-as-Code:** Quản lý detection infrastructure và rules dưới dạng code để đảm bảo nhất quán và mở rộng

### Pillar 3 — Infrastructure Protection (Network & Workload Security)
- **Network segmentation:** Tư duy thiết kế VPC, và khi nào đặt workloads ở private vs public
- **SG vs NACL:** Cách chọn và kết hợp đúng trong kiến trúc thực tế
- **Edge & network defense:** Dùng **WAF**, **Shield**, và **Network Firewall** như lớp phòng vệ nhiều tầng
- **Workload protection basics:** Security baseline cho EC2 và các container platforms (ECS/EKS)

### Pillar 4 — Data Protection (Encryption, Keys & Secrets)
- **KMS fundamentals:** Key policies, grants, và chiến lược rotation
- **Encryption best practices:** Encryption at-rest và in-transit trên các dịch vụ phổ biến (S3, EBS, RDS, DynamoDB)
- **Secrets handling:** Pattern với **Secrets Manager** và **Parameter Store**, bao gồm rotation và access controls
- **Governance:** Data classification và guardrails để kiểm soát ai được truy cập cái gì và trong điều kiện nào

### Pillar 5 — Incident Response (IR Playbook & Automation)
- **IR lifecycle trên AWS:** Cách tiếp cận có cấu trúc từ detection → containment → eradication → recovery → post-incident review
- **Practical playbooks:** Các kịch bản tần suất cao trong vận hành thực tế
  - Compromised IAM key
  - S3 public exposure
  - EC2 malware detection
- **Response actions:** Snapshotting, isolation, evidence collection, và quy trình recovery an toàn
- **Automation:** Auto-response patterns dùng **Lambda** và **Step Functions** để giảm thời gian phản hồi và hạn chế human error

### Wrap-Up & Q&A
- **Tổng kết 5 pillars:** IAM, detection, infrastructure, data, và IR kết nối thành một security system như thế nào
- **Các lỗi phổ biến trong doanh nghiệp ở Việt Nam:** Misconfigurations điển hình và khoảng trống vận hành
- **Learning roadmap:** Gợi ý lộ trình nâng cao security (Security Specialty, SA Pro)

## Key Takeaways

### Design Mindset
- **Security là yêu cầu kiến trúc:** Phải được thiết kế sớm, không phải thêm sau
- **Defense in depth luôn thắng:** Controls nhiều lớp giảm blast radius khi một control bị fail
- **Least privilege by default:** Quyền truy cập nên tối thiểu, có time-bound, và được review liên tục

### Technical Architecture
- **Identity là perimeter mới:** IAM hiện đại cần role-based access, SSO, MFA, và boundaries mạnh
- **Detect liên tục:** CloudTrail + GuardDuty + Security Hub là baseline, nhưng logging phải bao phủ mọi lớp
- **Network segmentation quan trọng:** Đặt private, dùng SG/NACL đúng, và edge protection giúp giảm exposure
- **Encrypt mọi thứ:** Keys, secrets, và encryption policies phải được quản lý bằng KMS và governance phù hợp
- **Tự động hoá incident response:** Playbooks + automation giảm MTTR và tăng tính nhất quán khi xử lý sự cố

### Modernization Strategy
- **Adopt multi-account governance:** Dùng SCP và permission boundaries để scale security an toàn
- **Coi detection như code:** Chuẩn hoá monitoring và alerts trên các môi trường
- **Operationalize security:** Runbooks, dashboards, quy trình thu thập bằng chứng, và post-mortems phải là một phần của hệ thống

### Applying to Work
- **Audit IAM posture:** Loại bỏ long-term credentials, enforce MFA, và validate policies bằng simulation
- **Bật baseline detection:** Org-level CloudTrail, GuardDuty, Security Hub, và log centralization
- **Harden network posture:** Review VPC segmentation, ingress/egress, và nhu cầu WAF/Shield
- **Triển khai secrets strategy:** Đưa secrets ra khỏi code, enforce rotation, và hạn chế truy cập
- **Tạo IR playbooks:** Bắt đầu với các kịch bản top (IAM key leak, S3 exposure, malware) và thêm automation dần

## Trải nghiệm sự kiện
Tham dự workshop “AWS Well-Architected — Security Pillar” giúp tôi có cái nhìn có cấu trúc về cloud security như một hệ thống hoàn chỉnh thay vì các công cụ rời rạc. Nội dung kết nối các nguyên tắc nền tảng (least privilege, zero trust, defense in depth) với các pattern triển khai cụ thể trên IAM, monitoring, infrastructure protection, encryption, và incident response. Mini demo và các ví dụ playbook khiến buổi học rất thực tiễn, đặc biệt phù hợp với môi trường enterprise tại Việt Nam, nơi misconfigurations và khoảng trống vận hành thường gặp.

## Một số hình ảnh sự kiện
![Event 5](/images/4.events_participated/event5.png)

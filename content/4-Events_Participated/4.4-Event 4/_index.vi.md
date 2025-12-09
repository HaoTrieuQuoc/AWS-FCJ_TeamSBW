--- 
title : "Event 4"

weight : 2
chapter : false
pre : " <b> 4.4 </b> "
---
# “DevOps on AWS”

**Địa điểm:** Bitexco Financial Tower
**Ngày:** Thứ Hai, 17 tháng 11 năm 2025  

## Mục tiêu sự kiện
- Củng cố DevOps mindset và văn hoá, kết nối các nguyên tắc với kết quả đo lường được
- Giới thiệu các DevOps performance metrics quan trọng (DORA, MTTR, deployment frequency) và cách các team sử dụng chúng
- Cung cấp walkthrough thực tiễn về các dịch vụ CI/CD trên AWS và các deployment strategies phổ biến
- Dạy các nền tảng Infrastructure as Code (IaC) với CloudFormation và AWS CDK
- Giải thích containerization và các container services trên AWS (ECR, ECS, EKS, App Runner) kèm so sánh thực tế
- Bao quát monitoring & observability bằng CloudWatch và AWS X-Ray với best practices cho alerting và on-call

## Diễn giả
- **Thịnh Nguyễn**
- **Bảo Huỳnh**
- **Huỳnh Hoàng Long**
- **Trần Vĩ**

## Key Highlights

### DevOps Mindset
- **Tóm tắt phiên AI/ML:** Kết nối các chủ đề AI/ML/GenAI với delivery và operations practices
- **Văn hoá và nguyên tắc DevOps:** Collaboration, shared ownership, automation, và continuous improvement
- **Lợi ích và các chỉ số chính:** Dùng các chỉ số đo lường được để dẫn hướng cải tiến
  - **DORA metrics:** Deployment frequency, lead time for changes, change failure rate, time to restore service
  - **MTTR:** Cách các team giảm thời gian recovery thông qua quy trình tốt hơn và observability

### AWS DevOps Services — CI/CD Pipeline
- **Source control:** AWS CodeCommit và Git strategies (GitFlow, Trunk-based)
- **Build & test:** Cấu hình CodeBuild và cách tổ chức các test stages trong pipelines
- **Deployment:** Các chiến lược CodeDeploy và khi nào nên dùng từng loại
  - **Blue/Green:** Chuyển đổi an toàn với rollback dễ dàng
  - **Canary:** Rollout dần để giảm blast radius
  - **Rolling:** Thay thế theo từng phần để cập nhật ổn định
- **Orchestration:** Tự động hoá end-to-end CI/CD bằng CodePipeline
- **Demo:** Walkthrough CI/CD pipeline đầy đủ (commit → build/test → deploy)

### Infrastructure as Code (IaC)
- **CloudFormation:** Templates, stacks, và drift detection để quản lý vòng đời hạ tầng
- **AWS CDK:** Constructs, reusable patterns, và hỗ trợ đa ngôn ngữ
- **Demo:** Deploy infrastructure bằng CloudFormation và CDK
- **Chọn công cụ IaC:** Các yếu tố để quyết định giữa CloudFormation và CDK theo nhu cầu team

### Container Services on AWS
- **Docker fundamentals:** Microservices mindset và các nền tảng containerization
- **Amazon ECR:** Lưu trữ image, scanning, và lifecycle policies
- **Amazon ECS & EKS:** Deployment strategies, scaling, và trade-offs về orchestration
- **AWS App Runner:** Triển khai container đơn giản hoá để iterate nhanh hơn
- **Demo & case study:** So sánh các cách triển khai microservices giữa các dịch vụ

### Monitoring & Observability
- **CloudWatch:** Metrics, logs, alarms, và dashboards cho operational visibility
- **AWS X-Ray:** Distributed tracing và performance insights
- **Demo:** Thiết lập observability full-stack (metrics + logs + tracing)
- **Best practices:** Alerting, dashboards, và on-call processes

## Key Takeaways

### Design Mindset
- **DevOps là văn hoá + thực hành:** Tools chỉ hiệu quả khi team shared ownership và collaborate end-to-end
- **Đo đúng thứ quan trọng:** DORA metrics và MTTR cung cấp baseline để cải thiện delivery performance
- **Thay đổi nhỏ giảm rủi ro:** Deploy thường xuyên, theo từng bước giúp tăng reliability và tăng tốc rollback

### Technical Architecture
- **CI/CD như một hệ thống:** Source → build/test → deploy → observe; mỗi stage cần automated và auditable
- **Deployment strategies rất quan trọng:** Blue/Green, Canary, Rolling cần phù hợp risk tolerance và traffic patterns
- **IaC để đảm bảo nhất quán:** CloudFormation/CDK tăng repeatability và giảm configuration drift
- **Containers cần kỷ luật:** Scanning, lifecycle policies, và lựa chọn orchestration ảnh hưởng stability và security
- **Observability là thiết yếu:** Metrics + logs + traces giúp giảm thời gian chẩn đoán và cải thiện MTTR

### Modernization Strategy
- **Chuẩn hoá delivery foundations:** Git strategy, testing, CI/CD templates, và flow promote môi trường
- **Adopt IaC sớm:** Tránh cấu hình thủ công và enforce governance khi hệ thống mở rộng
- **Operational readiness:** Dashboards, alerting, và on-call processes phải trưởng thành song song với platform

### Applying to Work
- **Định nghĩa pipeline baseline:** Tạo CI/CD templates tái sử dụng với testing và safe deployment patterns
- **Chọn hướng IaC:** Dùng CDK cho reusable abstractions, CloudFormation cho template stacks chặt chẽ (hoặc kết hợp)
- **Chọn container platform có chủ đích:** ECS, EKS, hoặc App Runner dựa trên độ phức tạp và team năng lực vận hành
- **Triển khai observability standards:** Dashboards tập trung, alarms có hành động rõ ràng, và trace instrumentation
- **Giảm MTTR:** Cải thiện runbooks, chất lượng alert, độ phủ tracing, và incident workflows

## Trải nghiệm sự kiện
Tham dự “DevOps on AWS” mang lại góc nhìn thực tiễn về modern delivery — từ nguyên tắc và metrics DevOps đến triển khai thực tế trên AWS cho CI/CD, IaC, containers, và observability. Các demo và so sánh (Git strategies, deployment patterns, ECS/EKS/App Runner, CloudFormation vs CDK) giúp dễ hiểu hơn về cách chọn hướng phù hợp dựa trên độ trưởng thành của team, mức chấp nhận rủi ro, và nhu cầu vận hành.

## Một số hình ảnh sự kiện
![Event 4](/images/4.events_participated/event4_pic1.png)
![Event 4](/images/4.events_participated/event4_pic2.png)

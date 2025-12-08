--- 
title : "Week 9 Worklog"

weight : 1 
chapter : false
pre : " <b> 1.9. </b> "
---
## Mục tiêu của Week 9:
- Nghiên cứu và hiểu cách **build và deploy** website e-commerce trên cả môi trường local và AWS.  
- Học về các chức năng mở rộng và vị trí của **Amazon CloudFront** và **AWS Amplify** trong system architecture.  
- Tìm hiểu cách sử dụng **LocalStack** để giả lập các AWS services trên local trước khi deploy thật.  
- Nghiên cứu các **Python libraries** cần thiết, khả năng tương thích version và cách packaging.  
- Học cách triển khai **ORM** cho việc tương tác với database.  
- Bắt đầu nghiên cứu về **Clickstream data** và cách nó được tích hợp vào project pipeline.  
- Review luồng kiến trúc (architecture flow) và refine lại cấu trúc proposal.

---

## Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 1-2 | - Research và review các bước ban đầu của **building the e-commerce web app**:<br>&nbsp;&nbsp;• Hiểu cách build web trên local và các bước deploy trong tương lai.<br>&nbsp;&nbsp;• Học giai đoạn tiếp theo: chuẩn bị và upload data.<br>&nbsp;&nbsp;• Nghiên cứu sâu hơn về **Amazon CloudFront**: ngoài việc tăng tốc độ thì nó còn làm được gì nữa?<br>&nbsp;&nbsp;• Tìm hiểu **AWS Amplify** hoạt động trước hay sau CloudFront trong kiến trúc. | 11/03/2025 | 11/04/2025 | [AWS CloudFront Docs](https://docs.aws.amazon.com/cloudfront/), [AWS Amplify Docs](https://docs.aws.amazon.com/amplify/) |
| 3 | - Research môi trường development và testing trên local:<br>&nbsp;&nbsp;• Học cách chạy và test toàn bộ hệ thống trên local trước khi deploy lên AWS.<br>&nbsp;&nbsp;• Nghiên cứu **LocalStack** (AWS emulator) và so sánh bản Normal vs. BASE edition.<br>&nbsp;&nbsp;• Tìm các phương pháp chuẩn hóa Python versions và package dependencies. | 11/05/2025 | 11/05/2025 | [LocalStack Documentation](https://docs.localstack.cloud/) |
| 4 | - Research backend development và cập nhật kiến trúc:<br>&nbsp;&nbsp;• Học về **ORM** và cách áp dụng vào thao tác database.<br>&nbsp;&nbsp;• Nghiên cứu Clickstream concepts và cách thu thập, xử lý dữ liệu.<br>&nbsp;&nbsp;• Review kiến trúc: vị trí CloudFront, có cần Amplify hay không, và việc thay Supabase bằng PostgreSQL. | 11/06/2025 | 11/06/2025 |  |
| 5 | - Review và cập nhật project documentation:<br>&nbsp;&nbsp;• Review cấu trúc proposal và cập nhật **title section**.<br>&nbsp;&nbsp;• Nghiên cứu các điều chỉnh kiến trúc và xác định những components còn thiếu.<br>&nbsp;&nbsp;• Tiếp tục nghiên cứu dependencies, lựa chọn database và hướng đi cho clickstream pipeline. | 11/07/2025 | 11/07/2025 | [Project Proposal](https://docs.google.com/document/d/1LPlnST1PFrpnswfhlIJCtlF_JvGE81YZZtocSGnTKIE/edit?tab=t.0) |

---

## Week 9 Achievements

### 1. Research về Web Build & Deployment
- Đã tìm hiểu cách team build thành công website e-commerce trên local.  
- Hiểu được bước tiếp theo: chuẩn bị và upload sample data trước khi kết nối với các AWS services.  

---

### 2. Research về CloudFront & Amplify
- Đã khám phá thêm các khả năng của **Amazon CloudFront**, như edge security, caching strategies và global distribution.  
- Đã tìm hiểu **AWS Amplify** nằm ở đâu trong hosting flow (trước hay sau CloudFront). 

---

### 3. Research về LocalStack & Local Testing
- Đã học cách chạy các AWS services trên local bằng **LocalStack**.  
- Biết rằng **LocalStack BASE edition** hỗ trợ nhiều services hơn (bao gồm Cognito), phù hợp hơn với project.  
- Đã nghiên cứu cách chạy local tests trước khi deploy hạ tầng lên AWS.

---

### 4. Research về Backend & Architecture
- Đã nghiên cứu **ORM** là gì và cách nó giúp quản lý các thao tác database clean hơn.  
- Bắt đầu học về **Clickstream data**, mục đích của nó và cách tích hợp vào pipeline.  
- Đã review kiến trúc và xác định các cập nhật như tích hợp Amplify, PostgreSQL và CloudFront.

---

### 5. Proposal Review & Cải thiện Documentation
- Đã cập nhật proposal, đặc biệt là **title section**.  
- Xác định thêm các requirements và những kiến trúc components còn thiếu cho giai đoạn tiếp theo.  
- Ghi lại hướng đi rõ ràng hơn cho các task sắp tới như clickstream integration và thiết lập Python environment. 

--- 
title : "Week 13 Worklog"

weight : 3
chapter : false
pre : " <b> 1.13 </b> "
---
# Week 13 Worklog (12/01/2025 – 12/07/2025)

## Week 13 Objectives
- Xây dựng **môi trường AWS thật** cho Batch-based Clickstream Analytics Platform.  
- Set up **OLTP EC2** và **S3 media bucket** cho website e-commerce.  
- Triển khai toàn bộ pipeline **clickstream ingestion** (Browser → API Gateway → Lambda Ingest → S3 Raw).  
- Kết nối **Lambda ETL** với S3 thông qua **S3 Gateway Endpoint** và tạo lịch chạy bằng **EventBridge**.  
- Provision **private EC2** để làm Data Warehouse + R Shiny, tạm thời bật **NAT Gateway** để cài package.  
- Sử dụng **SSM Session Manager** thông qua **Interface Endpoint** để truy cập private EC2 mà không cần public IP.  
- Hoàn thiện **Architecture V11** và chuẩn bị **demo** cho toàn bộ hệ thống.

---

## Tasks to be carried out this week

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 1 | - Provision **Public EC2 (OLTP)** trong `SBW_Project-vpc` để chứa transactional database của e-commerce.<br>&nbsp;&nbsp;• Gắn security group cho HTTP/HTTPS/SSH (chỉ từ IP tin cậy).<br>&nbsp;&nbsp;• Chuẩn bị host OLTP PostgreSQL (WebDB).<br>- Tạo **S3 bucket cho ảnh sản phẩm** (ví dụ `clickstream-s3-sbw`) và cấu hình làm media asset store cho web Amplify. | 12/01/2025 | 12/01/2025 | |
| 2 | - Triển khai **front-end event tracking** trên web e-commerce:<br>&nbsp;&nbsp;• Thêm JS handlers để capture clickstream events (page view, product view, add-to-cart, ...).<br>&nbsp;&nbsp;• Gửi events đến **Amazon API Gateway**.<br>- Cấu hình **API Gateway → Lambda Ingest**, để Lambda nhận event và ghi JSON vào **S3 Raw bucket** (`clickstream-s3-ingest`). | 12/02/2025 | 12/02/2025 | |
| 3 | - Tạo **S3 Gateway Endpoint** trong VPC để **Lambda ETL** truy cập S3 một cách private (không cần Internet/NAT).<br>- Cập nhật code & config của **Lambda ETL**:<br>&nbsp;&nbsp;• Đọc file raw từ `clickstream-s3-ingest`.<br>&nbsp;&nbsp;• Transform theo 15-field schema cho `clickstream_dw.clickstream_events`.<br>&nbsp;&nbsp;• Kết nối tới private EC2 DWH (PostgreSQL) và insert batch records. | 12/03/2025 | 12/03/2025 | |
| 4 | - Bật **Amazon EventBridge** rule (cron) để trigger **ETL Lambda** theo lịch (hourly).<br>- Kiểm tra pipeline EventBridge → Lambda ETL qua **CloudWatch Logs**:<br>&nbsp;&nbsp;• Kiểm tra ETL chạy đúng lịch.<br>&nbsp;&nbsp;• Xác nhận đọc từ S3 và ghi vào PostgreSQL DWH thành công. | 12/04/2025 | 12/04/2025 | |
| 5 | - Vẽ lại **Architecture V11** cho Batch Clickstream Platform:<br>&nbsp;&nbsp;• Public subnet: OLTP EC2, Internet Gateway, đường S3 media qua CloudFront/Amplify.<br>&nbsp;&nbsp;• Private subnet: DWH + R Shiny EC2, ETL Lambda integration, S3 Gateway Endpoint.<br>&nbsp;&nbsp;• Front-end: Cognito, CloudFront, Amplify, API Gateway, Ingest Lambda, EventBridge.<br>&nbsp;&nbsp;• Management & security: IAM, CloudWatch, SNS, SSM, NAT tạm thời. | 12/05/2025 | 12/05/2025 | |
| 6 | - Provision **Private EC2 (Analytics)** cho **PostgreSQL DWH + R Shiny**.<br>- Tạm thời tạo **NAT Gateway** để instance có thể:<br>&nbsp;&nbsp;• Cài **PostgreSQL 18**, **R**, **Shiny Server**, các R libraries.<br>&nbsp;&nbsp;• Update OS và cài thêm build tools, drivers.<br>- Sau khi cài đặt, kiểm tra PostgreSQL và Shiny chạy OK trong internal network. | 12/06/2025 | 12/06/2025 | |
| 7 | - Set up **SSM Session Manager** cho private EC2:<br>&nbsp;&nbsp;• Gắn IAM role có SSM permissions.<br>&nbsp;&nbsp;• Tạo **VPC Interface Endpoint** cho SSM/SSMMessages trong private subnet.<br>&nbsp;&nbsp;• Kết nối EC2 qua Session Manager (không cần SSH/public IP).<br>- Chạy thử **demo end-to-end**:<br>&nbsp;&nbsp;• User tương tác web → events gửi → Ingest Lambda → S3 Raw.<br>&nbsp;&nbsp;• EventBridge trigger ETL Lambda → đọc S3 → load vào PostgreSQL DWH.<br>&nbsp;&nbsp;• **R Shiny trên private EC2** query DWH và hiện dashboards qua SSM port-forward hoặc internal.<br>- Xác nhận toàn bộ **Batch Clickstream Analytics Platform** hoạt động hoàn chỉnh và sẵn sàng trình bày. | 12/07/2025 | 12/07/2025 | [Demo](https://www.youtube.com/watch?v=7R0njqggGtg) <br> [Slides](https://www.canva.com/design/DAG6jKIgK_I/VihpZUen3NvYxEiWfoqukw/edit) <br> [Github](https://github.com/orgs/SBW-Cloudworks/repositories) |

---

## Week 13 Achievements

### 1. Public OLTP EC2 và Product Image S3 Bucket
- Tạo **public EC2 OLTP instance** trong `SBW_Project-vpc` để host transactional PostgreSQL cho e-commerce.  
- Cấu hình security group mở đúng port (HTTP/HTTPS, DB access giới hạn).  
- Tạo **S3 media bucket** `clickstream-s3-sbw` để chứa ảnh sản phẩm, static assets cho Next.js/Amplify.

**Result:**  
Front-end có thể load assets từ S3 qua CloudFront, và OLTP EC2 sẵn sàng xử lý giao dịch web.

---

### 2. Clickstream Ingestion End-to-End (Browser → S3 Raw)
- Thêm event tracking vào web (page view, product view, add-to-cart, ...).  
- Events được gửi lên **API Gateway**, sau đó chuyển đến **Lambda Ingest**.  
- Lambda Ingest enrich + lưu JSON vào `clickstream-s3-ingest` theo prefix thời gian (`events/YYYY/MM/DD/HH/`).

**Result:**  
Toàn bộ hành vi người dùng trên web đã được ghi lại chính xác vào S3 Raw.

---

### 3. Lambda ETL kết nối S3 qua Gateway Endpoint
- Tạo **S3 Gateway Endpoint** để ETL Lambda đọc S3 mà không cần Internet/NAT.  
- Cập nhật ETL Lambda để:  
  - Đọc dữ liệu raw từ `clickstream-s3-ingest`.  
  - Transform thành **15-field schema** (`event_id`, `event_timestamp`, `event_name`, ...).  
  - Insert vào `clickstream_dw` trên private PostgreSQL DWH.

**Result:**  
ETL Lambda chạy hoàn toàn trong private network, an toàn & tối ưu chi phí.

---

### 4. EventBridge Scheduling chạy ETL tự động
- Tạo **EventBridge rule** để trigger ETL Lambda theo cron/hourly.  
- Kiểm tra trong **CloudWatch Logs**:  
  - Lambda chạy đúng lịch.  
  - Logs hiển thị số files xử lý, số rows insert.  
  - Có xử lý lỗi cho malformed events.

**Result:**  
Batch ETL pipeline đã tự động hóa hoàn toàn.

---

### 5. Architecture Diagram V11
- Vẽ lại kiến trúc dựa trên triển khai thực tế:  
  - **Front-end:** Browser → CloudFront → Amplify → Cognito  
  - **Ingestion:** API Gateway → Lambda Ingest → S3 Raw  
  - **Batch:** EventBridge → Lambda ETL → S3 Gateway Endpoint → Private PostgreSQL DWH  
  - **Analytics:** Private EC2 (DWH + R Shiny)  
  - **Ops:** IAM, CloudWatch, SNS, SSM, NAT tạm thời

**Result:**  
Architecture V11 phản ánh chính xác hệ thống để đưa vào documentation, proposal và demo.  
![Architecture](/images/2.proposal/SBW_Architecture_V11.jpg)

---

### 6. Private EC2 cho DWH + R Shiny (có NAT tạm thời)
- Tạo **SBW_EC2_ShinyDWH** trong private subnet.  
- Tạm thời bật NAT Gateway để cài:  
  - PostgreSQL 18  
  - R + Shiny Server  
  - R libraries  
- Sau khi cài đặt → tắt NAT để tiết kiệm chi phí.

**Result:**  
EC2 analytics private đã sẵn sàng chạy cả DWH và Shiny dashboards.

---

### 7. SSM Session Manager qua Interface Endpoint
- Cấu hình IAM + SSM Agent.  
- Tạo endpoints cho `ssm` và `ssmmessages`.  
- Kết nối vào EC2 private qua Session Manager và port-forward.

**Result:**  
Truy cập private EC2 cực kỳ bảo mật, không SSH, không public IP.

---

### 8. Demo End-to-End hoàn chỉnh
Pipeline hoàn chỉnh:

1. User → Web Amplify + CloudFront  
2. Cognito login  
3. Clickstream events → API Gateway → Lambda Ingest → S3 Raw  
4. EventBridge → Lambda ETL → PostgreSQL DWH  
5. R Shiny query DWH → Dashboards

**Overall Outcome:**  
Week 13 đánh dấu **phiên bản hoàn chỉnh đầu tiên** của Batch Clickstream Analytics Platform: từ ingestion → ETL → DWH → dashboard, tất cả đều chạy thật trên AWS.

---

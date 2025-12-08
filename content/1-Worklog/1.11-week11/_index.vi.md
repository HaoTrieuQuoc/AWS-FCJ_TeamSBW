--- 
title : "Week 11 Worklog"

weight : 2
chapter : false
pre : " <b> 1.11. </b> "
---
## Mục tiêu của Week 11:
- Review và kiểm tra lại **Word proposal template** để đảm bảo tính nhất quán và đầy đủ.  
- Kiểm tra xem **website e-commerce** đã hoạt động đúng chưa và sửa những lỗi còn tồn tại.  
- Cài đặt và thử nghiệm **Docker** và **LocalStack**, chạy thử các hàm AWS đơn giản trên môi trường local.  
- Kích hoạt **GitHub Student Pack** để mở khóa đầy đủ tính năng LocalStack cho việc mô phỏng AWS services.  
- Hoàn thiện và xác nhận **kiến trúc tổng thể của dự án**.

---

## Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 1 | - Review **Word proposal template**:<br>&nbsp;&nbsp;• Kiểm tra formatting, cấu trúc, và flow nội dung.<br>&nbsp;&nbsp;• Đảm bảo alignment với project requirements và deliverables. | 11/17/2025 | 11/17/2025 |  |
| 2 | - Kiểm tra **E-commerce Website**:<br>&nbsp;&nbsp;• Test hành vi UI và UX.<br>&nbsp;&nbsp;• Đảm bảo tất cả features hoạt động đúng (hình ảnh, trang chi tiết sản phẩm, routing, …).<br>&nbsp;&nbsp;• Kiểm tra console errors và performance issues. | 11/18/2025 | 11/18/2025 | [Website Repo](https://github.com/SBW-Cloudworks/ClickSteam.NextJS) |
| 3 | - Cài đặt và test **Docker & LocalStack**:<br>&nbsp;&nbsp;• Chạy các lệnh AWS-like cơ bản trên local.<br>&nbsp;&nbsp;• Học cách start/stop LocalStack services.<br>&nbsp;&nbsp;• Xác nhận compatibility với project code. | 11/19/2025 | 11/19/2025 | |
| 4 | - Thêm **GitHub Student Pack**:<br>&nbsp;&nbsp;• Kích hoạt LocalStack Pro bằng GitHub Student.<br>&nbsp;&nbsp;• Xác nhận quyền truy cập đầy đủ AWS service emulation (đặc biệt là Cognito và advanced networking). | 11/20/2025 | 11/20/2025 | |
| 5 | - Hoàn thiện **project architecture**:<br>&nbsp;&nbsp;• Hoàn thành bản kiến trúc đầy đủ.<br>&nbsp;&nbsp;• Đảm bảo tất cả components đúng với project scope (Cognito, S3, CloudFront, API Gateway, Lambda, EventBridge, EC2, RDS Warehouse).<br>&nbsp;&nbsp;• Xác nhận scalability, reliability và security best practices. | 11/21/2025 | 11/21/2025 |  |

---

## Week 11 Achievements

### 1. Reviewed the Word Proposal Template
- Kiểm tra layout, độ nhất quán về formatting, headings và cấu trúc nội dung.  
- Đảm bảo tất cả các phần đều đúng với yêu cầu của FCJ Track 4.  
- Sửa các lỗi nhỏ và cải thiện tính rõ ràng của nội dung.

---

### 2. Tested the E-commerce Website
- Kiểm tra hoạt động của website trên nhiều trang (home, products, details).  
- Fix các vấn đề UI và sự khác biệt giữa các trình duyệt.  
- Đảm bảo routing, hình ảnh và API calls chạy đúng và không sinh lỗi.

---

### 3. Installed Docker & Ran LocalStack
- Cài đặt thành công Docker Desktop và cấu hình môi trường.  
- Chạy các lệnh LocalStack cơ bản (test mock S3, Lambda, DynamoDB).  
- Tìm hiểu cách mô phỏng AWS services để tăng tốc quá trình test local.

---

### 4. Activated GitHub Student Pack for LocalStack
- Kích hoạt subscription GitHub Student để mở khóa tính năng LocalStack Pro.  
- Bật mô phỏng nâng cao cho các AWS services không có trong free tier.  
- Xác nhận hỗ trợ cho Cognito, EventBridge và các components liên quan đến Identity.

---

### 5. Finalized the Project Architecture
![Architecture](/images/2.proposal/Architecture-SBWTeam.jpg)

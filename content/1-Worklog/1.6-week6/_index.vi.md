--- 
title : "Week 6 Worklog"

weight : 1 
chapter : false
pre : " <b> 1.6. </b> "
---
## Mục tiêu của Week 6:
- Củng cố hiểu biết về **Database Concepts** bao gồm **Session**, **Primary Key**, **Foreign Key**, **Index**, **Partitions**, **Execution Plan**, **Database Log**, **Buffer**, **RDBMS**, **NoSQL**, **OLTP**, và **OLAP**.  
- Khám phá các dịch vụ database do AWS quản lý: **Amazon RDS**, **Amazon Aurora**, **Amazon ElastiCache**, và **Amazon Redshift**.  
- Tìm hiểu cách các relational và non-relational databases hỗ trợ các workloads khác nhau như **transactional processing** và **analytical processing**.  
- Tiếp tục chuẩn bị project: Xác định project requirements, xây dựng kiến trúc và ước tính chi phí cho từng dịch vụ AWS.

---

## Các nhiệm vụ cần thực hiện trong tuần này:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 1-2 | - Học **Database Concepts**:<br>&nbsp;&nbsp;• Database<br>&nbsp;&nbsp;• Session<br>&nbsp;&nbsp;• Primary Key<br>&nbsp;&nbsp;• Foreign Key<br>&nbsp;&nbsp;• Index<br>&nbsp;&nbsp;• Partitions<br>&nbsp;&nbsp;• Execution Plan<br>&nbsp;&nbsp;• Database Log<br>&nbsp;&nbsp;• Buffer<br>&nbsp;&nbsp;• RDBMS<br>&nbsp;&nbsp;• NoSQL<br>&nbsp;&nbsp;• OLTP<br>&nbsp;&nbsp;• OLAP | 10/13/2025 | 10/14/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i)  |
| 3 | - Học AWS Database Services:<br>&nbsp;&nbsp;• Amazon RDS<br>&nbsp;&nbsp;• Amazon Aurora<br>&nbsp;&nbsp;• Amazon ElastiCache<br>&nbsp;&nbsp;• Amazon Redshift | 10/15/2025 | 10/15/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 4 | - Xác định **Project Objectives and Requirements**:<br>&nbsp;&nbsp;• Xác định mục tiêu chính của dự án và các vấn đề cốt lõi cần giải quyết.<br>&nbsp;&nbsp;• Nghiên cứu các AWS services phù hợp để tích hợp vào kiến trúc (ví dụ: data collection, processing, storage, analytics).<br>&nbsp;&nbsp;• Thảo luận và thống nhất phạm vi dự án và hướng giải pháp với các thành viên trong team. | 10/16/2025 | 10/16/2025 | |
| 5 | - **Thiết kế kiến trúc Project và ước tính chi phí**:<br>&nbsp;&nbsp;• Xây dựng kiến trúc chi tiết bao gồm các thành phần như **Amazon CloudFront**, **Amazon S3**, **Amazon Cognito**, **API Gateway**, **Amazon EBS**, **AWS Lambda**, **IAM**, **Amazon CloudWatch**, **Amazon SNS**, **Amazon EventBridge**, và **Amazon EC2** (cho Data Warehouse và R Shiny).<br>&nbsp;&nbsp;• Ước tính chi phí cho từng AWS service trong mô hình.<br>&nbsp;&nbsp;• Đảm bảo kiến trúc có khả năng mở rộng, an toàn và tối ưu chi phí. | 10/17/2025 | 10/17/2025 | [Proposal](https://docs.google.com/document/d/1LPlnST1PFrpnswfhlIJCtlF_JvGE81YZZtocSGnTKIE/edit?tab=t.0) |

---

## Thành tựu của Week 6

### 1. Database Concepts

#### **Database**
- **Khái niệm:** Database là hệ thống lưu trữ có cấu trúc, dùng để tổ chức, quản lý và truy xuất dữ liệu hiệu quả.  
- **Cách hoạt động:** Dữ liệu được lưu trong các bảng gồm các hàng (records) và cột (fields). Người dùng hoặc ứng dụng truy vấn dữ liệu bằng SQL hoặc API.  
- **Ví dụ:** Như một cuốn sổ học sinh — mỗi trang là một bảng, mỗi dòng là thông tin của một học sinh.

---

#### **Session**
- **Khái niệm:** Session biểu thị một kết nối đang hoạt động giữa user và database system.  
- **Cách hoạt động:** Khi user đăng nhập, một session được tạo để duy trì trạng thái của họ cho đến khi logout.  
- **Ví dụ:** Như một ca làm việc — trong ca đó bạn có thể làm việc, khi hết ca mọi hoạt động dừng lại.

---

#### **Primary Key**
- **Khái niệm:** Primary key dùng để định danh duy nhất mỗi record trong bảng.  
- **Cách hoạt động:** Mỗi bảng chỉ có một primary key và giá trị phải unique, không được null.  
- **Ví dụ:** “Student ID” trong bảng Students là một mã định danh duy nhất.

---

#### **Foreign Key**
- **Khái niệm:** Foreign key liên kết hai bảng bằng cách tham chiếu đến primary key của bảng khác.  
- **Cách hoạt động:** Đảm bảo tính toàn vẹn dữ liệu giữa các bảng liên quan.  
- **Ví dụ:** Cột “StudentID” trong bảng Scores tham chiếu “StudentID” của bảng Students.

---

#### **Index**
- **Khái niệm:** Index giúp cải thiện hiệu suất truy vấn bằng cách tăng tốc độ tìm kiếm dữ liệu.  
- **Cách hoạt động:** Index lưu một cấu trúc dữ liệu riêng (thường là B-Tree) để tìm record nhanh mà không phải scan toàn bảng.  
- **Ví dụ:** Giống trang mục lục của sách giúp tìm chủ đề nhanh.

---

#### **Partitions**
- **Khái niệm:** Partitioning chia một bảng lớn thành các phần nhỏ dễ quản lý.  
- **Cách hoạt động:** Dữ liệu được chia theo tiêu chí như ngày tháng, khu vực, ID… để tăng tốc độ truy vấn và dễ bảo trì.  
- **Ví dụ:** Bảng sales được chia theo năm: 2023, 2024, 2025.

---

#### **Execution Plan**
- **Khái niệm:** Execution plan là bản đồ chi tiết cách database thực thi một câu SQL.  
- **Cách hoạt động:** SQL optimizer chọn cách tối ưu nhất để truy cập dữ liệu qua indexes, joins, filters.  
- **Ví dụ:** Như Google Maps chọn đường đi nhanh nhất đến nơi bạn muốn.

---

#### **Database Log**
- **Khái niệm:** Ghi lại toàn bộ hoạt động trên database như insert, update, delete.  
- **Cách hoạt động:** Log hỗ trợ khôi phục hoặc audit dữ liệu khi hệ thống gặp sự cố.  
- **Ví dụ:** Như camera an ninh ghi lại mọi hoạt động để xem lại khi cần.

---

#### **Buffer**
- **Khái niệm:** Vùng nhớ tạm dùng để lưu những dữ liệu được truy cập thường xuyên.  
- **Cách hoạt động:** Dữ liệu đọc nhiều lần được cache trong buffer để truy cập nhanh hơn.  
- **Ví dụ:** Như cache của trình duyệt giúp tải trang nhanh hơn khi truy cập lại.

---

#### **RDBMS (Relational Database Management System)**
- **Khái niệm:** Hệ thống quản lý database dạng quan hệ, sử dụng các bảng có cấu trúc và SQL.  
- **Cách hoạt động:** Dữ liệu được tổ chức thành các bảng có quan hệ và ràng buộc.  
- **Ví dụ:** MySQL, PostgreSQL, Oracle Database.

---

#### **NoSQL**
- **Khái niệm:** Database phi quan hệ hỗ trợ lưu trữ linh hoạt.  
- **Cách hoạt động:** Dữ liệu lưu dưới dạng document, key-value, graph hoặc column-based.  
- **Ví dụ:** MongoDB lưu dữ liệu dạng document giống JSON, phù hợp cho web app động.

---

#### **OLTP (Online Transaction Processing)**
- **Khái niệm:** Hệ thống xử lý giao dịch nhanh và đáng tin cậy.  
- **Cách hoạt động:** Xử lý các tác vụ CRUD nhỏ và liên tục.  
- **Ví dụ:** Giao dịch mua hàng trên Shopee hoặc Lazada.

---

#### **OLAP (Online Analytical Processing)**
- **Khái niệm:** Hệ thống phân tích dữ liệu quy mô lớn.  
- **Cách hoạt động:** Tổng hợp và xử lý dữ liệu đa chiều để hỗ trợ business insights.  
- **Ví dụ:** Phân tích doanh số theo khu vực và thời gian.

---

### 2. AWS Database Services

#### **Amazon RDS (Relational Database Service)**
- **Khái niệm:** Dịch vụ relational database được AWS quản lý hoàn toàn.  
- **Cách hoạt động:** AWS xử lý deployment, backup, updates, scaling; người dùng chỉ tập trung vào dữ liệu và truy vấn.  
- **Features:**  
  - Hỗ trợ nhiều engines (MySQL, PostgreSQL, Oracle, SQL Server, MariaDB, Aurora).  
  - Tự động backup và phục hồi.  
  - Auto-scaling và performance monitoring.  
- **Ví dụ:** Công ty dùng RDS để lưu dữ liệu khách hàng mà không cần tự quản lý server.

---

#### **Amazon Aurora**
- **Khái niệm:** Database hiệu suất cao, tương thích MySQL và PostgreSQL.  
- **Cách hoạt động:** Dữ liệu được lưu 6 bản trên 3 Availability Zones để tăng durability và availability.  
- **Features:**  
  - Nhanh hơn MySQL 5x và PostgreSQL 3x.  
  - Tự động scale đến 128 TB.  
  - Tích hợp AI và analytics (Aurora ML, Aurora Serverless).  
- **Ví dụ:** Website e-commerce xử lý hàng nghìn giao dịch mỗi phút.

---

#### **Amazon ElastiCache**
- **Khái niệm:** Dịch vụ in-memory caching giúp cải thiện hiệu suất ứng dụng.  
- **Cách hoạt động:** Dữ liệu thường xuyên truy cập được lưu trong RAM thay vì đọc từ database.  
- **Features:**  
  - Hỗ trợ Redis và Memcached.  
  - Độ trễ sub-millisecond.  
  - Tích hợp dễ dàng với RDS hoặc ứng dụng web.  
- **Ví dụ:** Website cache kết quả truy vấn để người dùng truy cập lại nhanh hơn.

---

#### **Amazon Redshift**
- **Khái niệm:** Data warehouse được tối ưu cho analytics quy mô lớn.  
- **Cách hoạt động:** Lưu dữ liệu dạng columnar, giúp chạy phân tích phức tạp nhanh hơn.  
- **Features:**  
  - Xử lý petabytes dữ liệu hiệu quả.  
  - Tích hợp S3, Glue, QuickSight cho pipelines hoàn chỉnh.  
  - Hỗ trợ SQL tiêu chuẩn.  
- **Ví dụ:** Công ty phân tích hàng tỷ clickstream events trong Redshift để hiểu hành vi người dùng.

---

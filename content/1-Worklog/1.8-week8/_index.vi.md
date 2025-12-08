--- 
title : "Week 8 Worklog"

weight : 1 
chapter : false
pre : " <b> 1.8. </b> "
---
## Mục tiêu của Week 8:
- Tiếp tục phát triển dự án **Batch-based Clickstream Analytics Platform**.  
- Hoàn thiện và publish **project proposal** lên GitHub Pages để tất cả thành viên cùng cộng tác.  
- Lên kế hoạch cho các bước tiếp theo và bắt đầu nghiên cứu tích hợp **Amazon Cognito** và **Amazon S3** vào ứng dụng web e-commerce.  
- Ôn lại các AWS concepts và architectural principles quan trọng cho **Midterm Exam**.  

---

## Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 1-2 | - **Team Meeting & Project Setup**:<br>&nbsp;&nbsp;• Gặp mặt toàn bộ team trực tiếp (buổi họp đầy đủ đầu tiên sau hơn một tháng làm việc online).<br>&nbsp;&nbsp;• Leader đẩy project lên GitHub và add tất cả thành viên vào repository.<br>&nbsp;&nbsp;• Review và hoàn thiện project proposal, kiểm tra lỗi và publish qua **GitHub Pages**.<br>&nbsp;&nbsp;• Lên kế hoạch cho các task sắp tới:<br>&nbsp;&nbsp;&nbsp;&nbsp;- Nghiên cứu **Amazon Cognito** và **Amazon S3** để tích hợp vào web e-commerce.<br>&nbsp;&nbsp;&nbsp;&nbsp;- Explore thêm các AWS services có thể sử dụng trong project.<br>&nbsp;&nbsp;&nbsp;&nbsp;- Đặt mục tiêu hoàn thành project trước **Week 12**.<br>&nbsp;&nbsp;• Tìm kiếm và test nhiều **e-commerce web templates** để chọn ra template phù hợp và responsive nhất. | 10/27/2025 | 10/28/2025 | [GitHub Repository](https://github.com/HaoTrieuQuoc/AWS-FCJ_TeamSBW) |
| 3-4 | - **Midterm Exam Preparation**:<br>&nbsp;&nbsp;• Review các chủ đề AWS: Secure, Resilient, High-Performing, và Cost-Optimized Architectures.<br>&nbsp;&nbsp;• Ôn lại các AWS services chính: EC2, S3, RDS, IAM, Lambda, CloudWatch, CloudFront, và EventBridge.<br>&nbsp;&nbsp;• Làm mock questions và các case studies dạng scenario-based. | 10/29/2025 | 10/30/2025 |  |
| 5 | - **Midterm Exam** | 10/31/2025 | 10/31/2025 |  |

---

## Week 8 Achievements

### 1. Team Collaboration and Project Setup
- Cả team đã tổ chức thành công **buổi họp trực tiếp đầu tiên** sau hơn một tháng làm việc online.  
- **Team leader** tạo GitHub repository, add toàn bộ thành viên và push bản proposal cuối cùng lên repository.  
- **Nội dung proposal** được review kỹ, chỉnh lỗi định dạng và logic, sau đó deploy qua **GitHub Pages** để mọi người truy cập thuận tiện.  

---

### 2. Project Planning and Research
- Team thống nhất các **short-term goals** và đồng ý hoàn thành project trước **Week 12**.  
- Các trọng tâm nghiên cứu cho giai đoạn tiếp theo gồm:  
  - Nghiên cứu **Amazon Cognito** cho authentication và identity management.  
  - Explore **Amazon S3** cho data storage, static web hosting và log management.  
  - Tìm hiểu các AWS services khác giúp cải thiện scalability và performance cho nền tảng.  
- Team cũng đã explore nhiều **e-commerce website templates**, test các yếu tố như responsiveness, UI flow và khả năng tích hợp backend AWS.

---

### 3. Midterm Exam Preparation
### AWS Services Categorization for Exam Review

#### 1. Secure Architectures

| Service | Concept | How it works | Example |
|----------|----------|--------------|----------|
| **AWS Organizations** | Quản lý nhiều AWS accounts trong một organization. | Root account quản lý member accounts và áp dụng SCPs. | Giống công ty mẹ quản lý các công ty con. |
| **Service Control Policy (SCP)** | Policies áp dụng toàn organization để giới hạn quyền. | SCP định nghĩa các hành động được phép/không được phép. | Như luật công ty áp dụng cho mọi phòng ban. |
| **AWS IAM** | Quản lý users, groups, roles và permissions. | Users được authenticate & authorize qua IAM Policies (JSON). | Như hệ thống thẻ ra vào văn phòng. |
| **IAM Roles** | Cấp quyền tạm thời cho user hoặc service. | Services assume role để lấy temporary credentials. | EC2 assume role để truy cập S3. |
| **IAM User Groups** | Gom users có chung permissions. | Assign policies ở group level để dễ quản lý. | Như cấp quyền chung cho toàn bộ phòng HR. |
| **AWS KMS** | Quản lý encryption keys. | Tạo CMKs để mã hóa dữ liệu trong S3, EBS, RDS. | Như kho bạc trung tâm giữ chìa khóa mã hóa. |
| **AWS Cognito** | Authentication và user management cho web/mobile app. | Tạo User Pools để login bằng email hoặc social providers, phát hành tokens. | Như lễ tân xác thực khách và phát thẻ ra vào. |
| **AWS Config** | Theo dõi và audit cấu hình tài nguyên AWS theo thời gian. | Ghi lại thay đổi cấu hình và đánh giá compliance. | Như camera giám sát thay đổi cấu hình hệ thống. |
| **AWS CloudTrail** | Ghi log tất cả API calls và hoạt động người dùng. | Lưu event logs vào S3 để phân tích. | Như hộp đen lưu toàn bộ hoạt động hệ thống. |
| **AWS WAF** | Web Application Firewall bảo vệ HTTP/HTTPS. | Lọc request tại CloudFront, ALB hoặc API Gateway. | Như chốt an ninh kiểm tra khách ra vào. |
| **AWS Shield** | DDoS protection cho ứng dụng AWS. | Standard tự động, Advanced bổ sung bảo vệ chủ động. | Như đê chắn lũ bảo vệ thành phố. |
| **AWS Inspector** | Scan workloads để tìm vulnerabilities và misconfigurations. | Phân tích EC2, ECR, Lambda. | Như kiểm tra an toàn định kỳ. |
| **AWS GuardDuty** | Threat detection dùng ML. | Monitor CloudTrail, DNS, VPC logs để phát hiện bất thường. | Như hệ thống an ninh thông minh trong nhà. |
| **AWS Trusted Advisor** | Đưa ra best-practice recommendations về security và cost. | Scan account và báo cáo tối ưu. | Như chuyên gia tư vấn nội bộ. |

---

#### 2. Resilient Architectures

| Service | Concept | How it works | Example |
|----------|----------|--------------|----------|
| **Amazon EC2** | Virtual servers trên AWS. | Chọn instance type, AMI, storage để deploy ứng dụng. | Như thuê server trong data center. |
| **Auto Scaling Group (ASG)** | Scale EC2 theo nhu cầu. | Tự thêm hoặc giảm instances dựa trên CPU/traffic. | Như mở thêm quầy tính tiền khi khách đông. |
| **Elastic Load Balancing (ALB/NLB)** | Phân phối traffic. | ALB cho HTTP(S), NLB cho TCP/UDP. | Như vòng xoay giao thông chia đều xe. |
| **Amazon Route 53** | DNS và domain management. | Route traffic đến EC2 hoặc Load Balancer. | Như lễ tân chỉ khách đến đúng phòng. |
| **AWS Global Accelerator** | Tối ưu performance bằng global routing. | Traffic được route tới region gần nhất qua static IPs. | Như mạng lưới logistics toàn cầu. |
| **VPC Peering / Transit Gateway** | Kết nối private giữa các VPC. | Peering = trực tiếp 2 VPC, TGW = kết nối nhiều VPC. | Peering = cây cầu; TGW = bến trung tâm. |
| **Direct Connect / Site-to-Site VPN** | Kết nối on-premise tới AWS. | Direct Connect = đường truyền riêng; VPN = tunnel mã hóa. | Như đường cáp riêng hoặc đường hầm an toàn. |

---

#### 3. High-Performing Architectures

| Service | Concept | How it works | Example |
|----------|----------|--------------|----------|
| **Amazon CloudFront** | CDN toàn cầu. | Cache nội dung tại edge locations để giảm latency. | Như kho hàng đặt gần khách để giao nhanh. |
| **Amazon S3 / EBS / EFS** | Dịch vụ lưu trữ object, block, file. | S3 cho file storage, EBS cho EC2 volume, EFS cho shared storage. | Như ổ cứng, USB và thư mục chia sẻ. |
| **Amazon RDS / Aurora / DynamoDB / ElastiCache** | Managed DB & caching. | RDS = relational DB, Aurora = high-performance DB, DynamoDB = NoSQL, ElastiCache = in-memory cache. | Thư viện, kho siêu nhanh, tủ đồ, clipboard. |
| **Amazon VPC** | Mạng ảo riêng. | Chia subnet, kiểm soát traffic. | Như khu dân cư có cổng an ninh. |
| **Subnet / Security Group / NACL** | Lớp bảo mật mạng. | SG = firewall stateful; NACL = stateless tại subnet. | Như bảo vệ ở cửa và cảnh sát ở đầu phố. |

---

#### 4. Cost-Optimized Architectures

| Service | Concept | How it works | Example |
|----------|----------|--------------|----------|
| **AWS Storage Gateway / Snowball** | Hybrid storage và physical data transfer. | Gateway sync dữ liệu; Snowball chu

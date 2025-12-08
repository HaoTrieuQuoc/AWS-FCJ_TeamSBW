--- 
title : "Week 5 Worklog"

weight : 1 
chapter : false
pre : " <b> 1.5. </b> "
---
## Mục tiêu của Week 5:
- Hiểu **AWS Shared Responsibility Model** và cách phân chia trách nhiệm giữa AWS và khách hàng.  
- Học về **Identity and Access Management (IAM)**, **Cognito**, **Organizations**, và **Identity Center (SSO)** cho quản lý danh tính và truy cập tập trung.  
- Khám phá **AWS KMS (Key Management Service)** và **Security Hub** cho mã hóa và giám sát bảo mật tập trung.  
- Thực hành hands-on labs về IAM roles, quản lý user, tích hợp SSO và security auditing.  
- Chuẩn bị dự án: nghiên cứu **Clickstreams**, **Sections**, và **yêu cầu Track 4** trong FCJ. Làm việc nhóm để hiểu rõ hướng đi của dự án.

---

## Các nhiệm vụ cần thực hiện trong tuần này:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 1-2 | - Học **AWS Security and Identity Concepts**:<br>&nbsp;&nbsp;• Shared Responsibility Model<br>&nbsp;&nbsp;• AWS Identity and Access Management (IAM)<br>&nbsp;&nbsp;• Amazon Cognito<br>&nbsp;&nbsp;• AWS Organization<br>&nbsp;&nbsp;• AWS Identity Center (SSO)<br>&nbsp;&nbsp;• AWS KMS<br>&nbsp;&nbsp;• AWS Security Hub | 10/06/2025 | 10/07/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 3-4 | - Thực hành IAM Labs: tạo IAM users, groups, roles và policies; test permissions và MFA login | 10/08/2025 | 10/09/2025 | [LAB](https://000028.awsstudygroup.com/6-cleanup/) |
| 5 |  - Xác định **đề tài group project**: *Batch-based Clickstream Analytics Platform*.<br> - Nghiên cứu **Clickstreams** là gì và cách chúng được sử dụng trong analytics. <br> - Tìm hiểu về **Sections** trong cấu trúc dự án và mối liên hệ của chúng với data collection và processing. <br> - Học **yêu cầu Track 4 trong chương trình FCJ** để align mục tiêu của dự án. <br> - Tất cả các thành viên nhóm cùng trao đổi và nghiên cứu các nội dung trên. | 10/10/2025 | 10/10/2025 | |

---

## Thành tựu của Week 5

### 1. AWS Security and Identity Management Concepts

1. **Shared Responsibility Model**

- Khái niệm:  
AWS và khách hàng cùng chia sẻ trách nhiệm bảo mật nhưng ở các phạm vi khác nhau.  
AWS chịu trách nhiệm Security of the Cloud — bảo vệ cơ sở hạ tầng vật lý, phần cứng, mạng và data centers.  
Khách hàng chịu trách nhiệm Security in the Cloud — bảo vệ dữ liệu, quản lý user access và cấu hình tài nguyên an toàn.

- Cách hoạt động:  
AWS đảm bảo nền tảng cloud an toàn, trong khi người dùng phải cấu hình tài nguyên đúng cách — ví dụ: không để S3 bucket public nếu chứa dữ liệu nhạy cảm.

- Ví dụ:  
AWS giống như chủ tòa nhà đảm bảo điện, nước, hệ thống chữa cháy.  
Bạn là người thuê căn hộ — bạn phải khóa cửa và bảo vệ tài sản của mình.

---

2. **AWS Identity and Access Management (IAM)**

- Khái niệm:  
Dịch vụ quản lý users, groups và access permissions trong AWS.  
Là nền tảng của identity và permission management.

- Cách hoạt động:  
  -IAM User: danh tính trong AWS account.  
  -IAM Group: tập hợp các users.  
  -IAM Role: quyền tạm thời cho users hoặc services.  
  -IAM Policy: tài liệu JSON định nghĩa hành động được phép hoặc bị từ chối.

- Ví dụ:  
IAM giống như hệ thống kiểm soát ra vào văn phòng.  
Nhân viên có thẻ ID (users) với quyền mở các cửa nhất định (policies).  
Khách được cấp thẻ tạm thời (roles).

---

3. **Amazon Cognito**

- Khái niệm:  
Dịch vụ xác thực và quản lý users cho web/mobile applications.  
Hỗ trợ đăng ký, đăng nhập và quản lý session.

- Cách hoạt động:  
  -Tạo **User Pools** để quản lý danh tính.  
  -Hỗ trợ login qua email hoặc social providers (Google, Facebook, Apple).  
  -Sau khi login, Cognito cấp tokens để truy cập AWS resources (như S3 hoặc API Gateway).

- Ví dụ:  
Cognito giống như quầy lễ tân — xác minh danh tính và cấp thẻ (tokens) cho phép vào các phòng (services).

---

4. **AWS Organization**

- Khái niệm:  
Dịch vụ quản lý nhiều AWS accounts trong một tổ chức.  
Cho phép quản lý tập trung billing, policies và permissions.

- Cách hoạt động:  
  -Tạo root account, sau đó thêm member accounts.  
  -Áp dụng **Service Control Policies (SCP)** để đặt giới hạn quyền trên toàn tổ chức.

- Ví dụ:  
Giống như tập đoàn mẹ quản lý các công ty con.  
Trụ sở chính đặt ra các quy tắc chung (SCP), trong khi từng chi nhánh vẫn hoạt động độc lập.

---

5. **AWS Identity Center (SSO)**

- Khái niệm:  
Cung cấp **Single Sign-On (SSO)** để truy cập nhiều AWS accounts và SaaS applications bằng một lần đăng nhập.

- Cách hoạt động:  
  -Tích hợp với AWS Organizations hoặc identity providers bên ngoài (Microsoft AD, Okta).  
  -Sau khi login qua Identity Center, users có thể truy cập tất cả accounts và apps được cấp phép mà không cần nhập lại mật khẩu.

- Ví dụ:  
Giống như một thẻ nhân viên mở được nhiều tòa nhà khác nhau trong công ty.

---

6. **AWS Key Management Service (KMS)**

- Khái niệm:  
Dịch vụ quản lý encryption keys để bảo vệ dữ liệu.  
AWS hỗ trợ tạo, xoay vòng và kiểm soát việc sử dụng keys.

- Cách hoạt động:  
  -Tạo **Customer Master Keys (CMK)**.  
  -Dùng CMKs để mã hóa dữ liệu trong S3, EBS, RDS,...  
  -Chỉ IAM users được cấp quyền mới có thể sử dụng keys.

- Ví dụ:  
KMS giống như ngân hàng giữ két sắt — chỉ ai có chìa khóa mới mở được.

---

7. **AWS Security Hub**

- Khái niệm:  
Dịch vụ bảo mật tập trung, tổng hợp, phân tích và đánh giá các findings từ nhiều công cụ bảo mật AWS khác nhau.  
Thu thập dữ liệu từ **GuardDuty**, **Inspector**, **Macie**,... vào một dashboard duy nhất.

- Cách hoạt động:  
  -Security Hub quét tất cả accounts để tìm lỗ hổng (findings).  
  -Cung cấp điểm compliance theo các bộ tiêu chuẩn như **CIS AWS Foundations Benchmark**.

- Ví dụ:  
Giống như bảng điều khiển an ninh trung tâm — tập hợp cảnh báo từ camera, báo cháy, cảm biến,…

---

### 2. Practice labs
 - Create User Group  
 ![Create User Group](/images/1.worklog/044-worklog.png) 
 - Create User  
 ![Create User](/images/1.worklog/045-worklog.png) 
 - Check User  
 ![Check User](/images/1.worklog/046-worklog.png) 
 - Policy ec2-list-read  
 ![Policy ec2-list-read](/images/1.worklog/047-worklog.png) 
 - Policy ec2-create-tags  
 ![Policy ec2-create-tags](/images/1.worklog/048-worklog.png) 
 - Policy ec2-create-tags-existing  
 ![Policy ec2-create-tags-existing](/images/1.worklog/049-worklog.png) 
 - Policy ec2-run-instances  
 ![Policy ec2-run-instances](/images/1.worklog/050-worklog.png) 
 - Policy ec2-manage-instances  
 ![Policy ec2-manage-instances](/images/1.worklog/051-worklog.png) 
 - Create role  
 ![Create role](/images/1.worklog/052-worklog.png) 
 - Edit Trust Policy  
 ![Edit Trust Policy](/images/1.worklog/053-worklog.png) 
 - Switch Role  
 ![Switch role](/images/1.worklog/054-worklog.png) 
 - Create EC2 with tag name Beta  
 ![Create EC2 with tag name Beta](/images/1.worklog/055-worklog.png) 
 - Fail for the first time  
 ![Fail for the first time](/images/1.worklog/056-worklog.png) 
 - Create EC2 with tag name Alpha  
 ![Create EC2 with tag name Alpha](/images/1.worklog/057-worklog.png) 
 - Success for the second time  
 ![Fail for the second time](/images/1.worklog/058-worklog.png) 
 - Fail to edit tag name  
 ![Fail to edit tag name](/images/1.worklog/059-worklog.png) 
 - Check policy  
 ![Check policy](/images/1.worklog/060-worklog.png) 
 - Delete ec2-admin-team-alpha  
 ![Delete ec2-admin-team-alpha](/images/1.worklog/061-worklog.png) 
 - Delete 5 policy  
 ![Delete 5 policy](/images/1.worklog/062-worklog.png) 
 - Delete User  
 ![Delete User](/images/1.worklog/063-worklog.png) 
 - Delete UserGroup  
![Delete UserGroup](/images/1.worklog/064-worklog.png)
---

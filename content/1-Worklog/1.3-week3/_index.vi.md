---
title : "Week 3 Worklog"

weight : 1 
chapter : false
pre : " <b> 1.3. </b> "
---
## Mục tiêu của Week 3:
- Học các khái niệm cơ bản của **AWS EC2** (compute, storage, networking).  
- Hiểu cách cấu hình và kết nối đến EC2 instances.  
- Khám phá các **tùy chọn lưu trữ**: EBS vs. Instance Store.  
- Học **EC2 Auto Scaling** để tối ưu chi phí và hiệu năng.  

---

## Các nhiệm vụ cần thực hiện trong tuần này:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|-------------|-----------------|-------------------|
| 1-2 | - Học **AWS EC2 & Core Concepts**:<br>&nbsp;&nbsp;• Amazon EC2<br>&nbsp;&nbsp;• Instance type<br>&nbsp;&nbsp;• Hardware node<br>&nbsp;&nbsp;• Hypervisor<br>&nbsp;&nbsp;• Amazon Machine Image (AMI)<br>&nbsp;&nbsp;• Key pair<br>&nbsp;&nbsp;• Elastic Block Store (EBS)<br>&nbsp;&nbsp;• Instance store<br>&nbsp;&nbsp;• User data<br>&nbsp;&nbsp;• EC2 Metadata<br>&nbsp;&nbsp;• EC2 Auto Scaling | 09/22/2025 | 09/23/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 3 | - Thực hành backup plan Labs: Tạo backup plan, test restore và dọn dẹp tài nguyên | 09/24/2025 | 09/24/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 4-5 | - Thực hành static website Labs: Tạo S3 bucket, load data, config và test website | 09/25/2025 | 09/25/2025 | [LAB](https://000057.awsstudygroup.com/2-prerequiste/2.2-uploaddata/) |

---

## Thành tựu của Week 3

### 1 Đã học **Amazon EC2 & Core Concepts**

1. **Amazon EC2**  
- Khái niệm: Amazon EC2 giống như một virtual server (VM) hoặc physical server nhưng được chạy trên hạ tầng AWS.  
- Cách hoạt động:  
 -Bạn có thể launch một VM trong vài phút.  
 -Chọn CPU, RAM, disk size tùy nhu cầu.  
 -Tài nguyên có thể scale theo demand.  
- Ví dụ: Giống như thuê chỗ trong data center thay vì mua server riêng.  

2. **Instance type**  
- Khái niệm: Loại cấu hình phần cứng cho EC2 instance.  
- Cách hoạt động: AWS cung cấp nhiều gói cấu hình (t2.micro, m5.large, p3.2xlarge…) tối ưu cho compute, memory, GPU hoặc I/O.  
- Ví dụ: Như chọn giữa laptop văn phòng, laptop gaming hoặc workstation.  

3. **Hardware node**  
- Khái niệm: Máy vật lý trong AWS data centers chạy nhiều EC2 instances.  
- Cách hoạt động: Mỗi node có CPU, RAM, disk và được chia sẻ cho nhiều khách hàng thông qua hypervisor.  
- Ví dụ: Giống như tòa chung cư, mỗi căn hộ là một EC2 instance.  

4. **Hypervisor**  
- Khái niệm: Lớp software quản lý và chia tài nguyên phần cứng cho các EC2 instances.  
- Cách hoạt động: Đảm bảo isolation và phân phối tài nguyên hợp lý.  
- Ví dụ: Giống như ban quản lý tòa nhà phân phối điện, nước, internet cho từng căn hộ.  

5. **Amazon Machine Image (AMI)**  
- Khái niệm: Template image dùng để tạo EC2 instances.  
- Cách hoạt động: Chứa OS + phần mềm cài sẵn. Khi launch EC2, bạn chọn AMI để có môi trường sẵn dùng.  
- Ví dụ: Như bản cài Windows có Office sẵn, hoặc Ubuntu có Python sẵn.  

6. **Key pair**  
- Khái niệm: Cặp key (public + private) dùng để xác thực khi đăng nhập EC2.  
- Cách hoạt động:  
 -Public key lưu trong EC2.  
 -Private key lưu trên máy bạn.  
 -SSH dùng cả hai để xác thực.  
- Ví dụ: AWS giữ cái "ổ khóa", bạn giữ "chìa khóa".  

7. **Elastic Block Store (EBS)**  
- Khái niệm: Dịch vụ block storage gắn vào EC2.  
- Cách hoạt động:  
 -Dữ liệu vẫn tồn tại khi stop instance.  
 -Có thể detach và attach sang EC2 khác.  
- Ví dụ: Như ổ cứng ngoài có thể cắm vào bất kỳ máy nào.  

8. **Instance store**  
- Khái niệm: Ổ NVMe siêu nhanh nằm trên phần cứng của EC2.  
- Cách hoạt động:  
 -Dữ liệu mất khi stop instance nhưng không mất khi restart.  
 -Không có replication → không phù hợp cho dữ liệu quan trọng.  
- Ví dụ: Như RAM disk hoặc SSD tạm: rất nhanh nhưng dễ mất dữ liệu.  

9. **User data**  
- Khái niệm: Script (bash, PowerShell…) chạy khi EC2 boot lần đầu.  
- Cách hoạt động: Dùng để cài phần mềm, update OS, config môi trường tự động.  
- Ví dụ: Như đưa checklist cho cửa hàng để họ cài app trước khi giao laptop mới.  

10. **EC2 Metadata**  
- Khái niệm: Thông tin về instance (ID, IP, AMI, role, region…).  
- Cách hoạt động: Truy cập tại http://169.254.169.254/latest/meta-data/.  
- Ví dụ: Như bảng tên trước cửa nhà ghi số nhà và thông tin chủ nhà.  

11. **EC2 Auto Scaling**  
- Khái niệm: Điều chỉnh số lượng EC2 instances tự động dựa trên tải hệ thống.  
- Cách hoạt động:  
  -Nếu CPU/RAM cao → launch thêm EC2.  
  -Nếu tải giảm → terminate bớt EC2 để tiết kiệm chi phí.  
- Ví dụ: Siêu thị mở thêm quầy khi đông, đóng bớt khi vắng.  

### 2. Thực hành labs 
 - Create Backup plan  
 ![Create Backup Plan](/images/1.worklog/013-worklog.png)  
 ![Create Backup Plan](/images/1.worklog/014-worklog.png)
 - Create S3 Bucket  
 ![Create S3 Bucket](/images/1.worklog/015-worklog.png)
 - Load data  
 ![Load data](/images/1.worklog/016-worklog.png)
 - Enable static website feature  
 ![Enable static website feature](/images/1.worklog/017-worklog.png)
 - Configuring public access block  
 ![Configuring public access block](/images/1.worklog/018-worklog.png)
 - Configuring public objects  
![Configuring public objects](/images/1.worklog/019-worklog.png)
 - Test website  
![Test website](/images/1.worklog/020-worklog.png)  
![Test website](/images/1.worklog/021-worklog.png)
---

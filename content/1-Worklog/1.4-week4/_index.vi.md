--- 
title : "Week 4 Worklog"

weight : 1 
chapter : false
pre : " <b> 1.4. </b> "
---
## Mục tiêu của Week 4:
- Học các khái niệm cơ bản về **AWS S3** (storage, access control, data lifecycle).  
- Hiểu cách cấu hình **S3 Buckets, Policies, ACLs**.  
- Khám phá **S3 storage classes và performance optimization**.  
- Học về **disaster recovery, RTO, RPO và AWS Backup**.  

---

## Các nhiệm vụ cần thực hiện trong tuần này:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 1 | - Học **AWS S3 & Core Concepts**:<br>&nbsp;&nbsp;• Amazon S3<br>&nbsp;&nbsp;• S3 Bucket<br>&nbsp;&nbsp;• Access point<br>&nbsp;&nbsp;• Storage class<br>&nbsp;&nbsp;• S3 Static website<br>&nbsp;&nbsp;• S3 Control access<br>&nbsp;&nbsp;• S3 ACL<br>&nbsp;&nbsp;• S3 Bucket Policy<br>&nbsp;&nbsp;• S3 Endpoint<br>&nbsp;&nbsp;• Object Key & Performance | 09/29/2025 | 09/29/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 2 | - Học **Archival & Transfer Services**:<br>&nbsp;&nbsp;• Glacier<br>&nbsp;&nbsp;• Snowball, Snowball Edge, Snowmobile | 09/30/2025 | 09/30/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 3 | - Học **Disaster Recovery Concepts**:<br>&nbsp;&nbsp;• RTO<br>&nbsp;&nbsp;• RPO<br>&nbsp;&nbsp;• AWS Backup | 10/01/2025 | 10/01/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 4 | - Thực hành Deploy AWS Backup to the System Labs: tạo S3 bucket, Deploy Infrastructure, Create Backup Plan, Set up notifications, Test Restore, Clean up resources | 10/02/2025 | 10/02/2025 | [LAB](https://000013.awsstudygroup.com/6-cleanup/) |
| 5 | - Thực hành Lab 57 lần nữa: Tạo S3 bucket, load data, config và test website | 10/03/2025 | 10/03/2025 | [LAB](https://000057.awsstudygroup.com/2-prerequiste/2.2-uploaddata/) |

---

## Thành tựu của Week 4

### 1 Đã học **Amazon S3 & Core Concepts**

1. **Amazon S3 – The Infinite Warehouse**  
- Khái niệm: S3 là object storage service dùng để lưu trữ lượng dữ liệu không giới hạn.  
- Cách hoạt động: Lưu dữ liệu dưới dạng objects (file + metadata) trong buckets.  
- Ví dụ: Giống như Google Drive cho developer, có thể scale đến petabytes.  

2. **S3 Bucket – The Container**  
- Khái niệm: Container nơi objects được lưu trữ.  
- Cách hoạt động: Mỗi bucket có tên unique toàn cầu, region và policies riêng.  
- Ví dụ: Như một folder trên máy tính nhưng nằm trên cloud.  

3. **Access Point – Guest Door**  
- Khái niệm: Điểm truy cập đơn giản hóa để vào S3 bucket.  
- Cách hoạt động: Mỗi access point có hostname và permission riêng.  
- Ví dụ: Như đưa cho khách một chìa khóa cửa phụ để vào kho.  

4. **Storage Class – Types of Shelves**  
- Khái niệm: Xác định durability, availability và chi phí lưu trữ.  
- Cách hoạt động: Các lựa chọn gồm Standard, Intelligent-Tiering, One Zone-IA, Glacier,...  
- Ví dụ: Như chọn cất đồ trong phòng ngủ (nhanh), tầng hầm (rẻ hơn) hoặc kho xa (rẻ nhất nhưng xa).  

5. **S3 Static Website – Public Exhibition**  
- Khái niệm: Host static website trực tiếp từ S3.  
- Cách hoạt động: Upload file HTML/CSS/JS, bật hosting và truy cập qua URL.  
- Ví dụ: Như dán poster lên bảng thông báo công cộng.  

6. **S3 Control Access – Who Has the Keys**  
- Khái niệm: Các phương pháp kiểm soát ai có quyền truy cập dữ liệu.  
- Cách hoạt động: Điều khiển qua IAM policies, bucket policies, ACLs và access points.  
- Ví dụ: Như quyết định thành viên nào trong gia đình được giữ chìa khóa.  

7. **S3 Access Control List (ACL) – Guest List**  
- Khái niệm: Phương pháp legacy để quản lý quyền truy cập.  
- Cách hoạt động: Gán quyền read/write cho từng user cụ thể.  
- Ví dụ: Như tạo danh sách khách mời với các mức quyền khác nhau.  

8. **S3 Bucket Policy – House Rules**  
- Khái niệm: Bộ quy tắc JSON áp dụng cho bucket.  
- Cách hoạt động: Xác định ai có thể truy cập, hành động nào được phép hoặc bị từ chối.  
- Ví dụ: Như dán bảng nội quy trước cửa: “Chỉ mở từ 9AM–5PM”.  

9. **S3 Endpoint – Private Road**  
- Khái niệm: Kết nối private giữa VPC và S3.  
- Cách hoạt động: Truy cập S3 mà không đi qua internet công cộng.  
- Ví dụ: Như xây đường hầm bí mật dẫn đến kho hàng.  

10. **Object Key & Performance – Filing System**  
- Khái niệm: Mỗi object được định danh bằng một key unique.  
- Cách hoạt động: Thiết kế key ảnh hưởng đến performance; tránh đặt tên tuần tự.  
- Ví dụ: Như dán nhãn tài liệu trong tủ sao cho tìm nhanh hơn.  

11. **Glacier – Deep Freeze Storage**  
- Khái niệm: Lưu trữ archival giá rẻ.  
- Cách hoạt động: Thời gian truy xuất từ vài phút đến vài giờ tùy loại request.  
- Ví dụ: Như cất hồ sơ cũ vào kho đông lạnh.  

12. **Snowball, Snowball Edge, Snowmobile – Data Trucks**  
- Khái niệm: Thiết bị vật lý để chuyển lượng dữ liệu cực lớn.  
- Cách hoạt động:  
  - Snowball: cỡ vali, ở mức TB.  
  - Snowball Edge: có compute/storage cho xử lý tại edge.  
  - Snowmobile: cỡ container xe tải, ở mức exabyte.  
- Ví dụ: Như vận chuyển nguyên ổ cứng bằng xe tải thay vì upload lên mạng.  

13. **Disaster Recovery – Backup Plan**  
- Khái niệm: Chiến lược phục hồi hệ thống sau sự cố.  
- Cách hoạt động: Dùng backup, replication và multi-region deployment.  
- Ví dụ: Như có kế hoạch thoát hiểm khi nhà cháy.  

14. **Recovery Time Objective (RTO) – Downtime Tolerance**  
- Khái niệm: Thời gian downtime tối đa cho phép.  
- Cách hoạt động: Xác định tốc độ hệ thống phải phục hồi.  
- Ví dụ: Như cam kết mở lại cửa hàng trong 2 giờ sau khi mất điện.  

15. **Recovery Point Objective (RPO) – Data Loss Tolerance**  
- Khái niệm: Lượng dữ liệu tối đa có thể mất.  
- Cách hoạt động: Xác định dữ liệu (tính theo phút/giờ) có thể chấp nhận bị mất.  
- Ví dụ: Như chấp nhận mất ghi chú trong 10 phút gần nhất.  

16. **AWS Backup – Centralized Backup Service**  
- Khái niệm: Dịch vụ backup được quản lý tập trung.  
- Cách hoạt động: Hỗ trợ EBS, RDS, DynamoDB, EFS… với backup policies.  
- Ví dụ: Như thuê dịch vụ tự động sao lưu tất cả giấy tờ trong nhà bạn.  

### 2. Practice labs 
 - Create S3 bucket  
 ![Create S3](/images/1.worklog/022-worklog.png)
 - Create Folder  
 ![Create Folder](/images/1.worklog/023-worklog.png)
 - Load data  
 ![Load data](/images/1.worklog/024-worklog.png)
 - Configuring public access block  
 ![Configuring public access block](/images/1.worklog/025-worklog.png)
 - Edit bucket policy  
 ![Edit bucket policy](/images/1.worklog/026-worklog.png)  
 ![Edit bucket policy](/images/1.worklog/027-worklog.png)
 - Deploy Infrastructure  
 ![Create Stacks](/images/1.worklog/028-worklog.png)  
 ![Stacks details](/images/1.worklog/029-worklog.png)  
 ![confirm mail](/images/1.worklog/030-worklog.png)  
 ![success](/images/1.worklog/031-worklog.png)
 - Create backup plan  
 ![Create Backup plan](/images/1.worklog/032-worklog.png)  
 ![Assign Resources](/images/1.worklog/033-worklog.png)
 - Set up notifications  
 ![Setup notifications](/images/1.worklog/034-worklog.png)
 - Create on-demand backup  
 ![Create on-demand backup](/images/1.worklog/035-worklog.png)
 - Test restore  
 ![Mail confirm](/images/1.worklog/036-worklog.png)
 - Log stream  
 ![Log](/images/1.worklog/037-worklog.png)
 - Clean resources  
 - Delete SNS  
 ![Delete SNS](/images/1.worklog/038-worklog.png)
 - Delete backup vault  
 ![Delete backup vault](/images/1.worklog/039-worklog.png)
 - Delete backup plan  
 ![Delete backup plan](/images/1.worklog/040-worklog.png)
 - Delete Stacks  
 ![Delete stacks](/images/1.worklog/041-worklog.png)
 - Delete Log  
 ![Delete log](/images/1.worklog/042-worklog.png)
 - Terminate EC2  
 ![Delete EC2](/images/1.worklog/043-worklog.png)
---

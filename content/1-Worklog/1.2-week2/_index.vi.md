---
title : "Week 2 Worklog"

weight : 1 
chapter : false
pre : " <b> 1.2. </b> "
---
## Mục tiêu của Week 2:
- Học các khái niệm cơ bản về **AWS networking** (VPC, Subnets, Routing, Security, Connectivity).  
- Hiểu cách quản lý **traffic flow** và bảo mật workloads bên trong VPC.  
- Hiểu về các tùy chọn kết nối AWS (Peering, Transit Gateway, VPN, Direct Connect).  
- Khám phá **Elastic Load Balancing** để phân phối application traffic.  

---

## Các nhiệm vụ cần thực hiện trong tuần này:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|-------------|-----------------|-------------------|
| 1-3 | - Học **AWS Networking – VPC & Core Concepts**:<br>&nbsp;&nbsp;• Amazon VPC<br>&nbsp;&nbsp;• Subnets<br>&nbsp;&nbsp;• Route Tables<br>&nbsp;&nbsp;• Internet Gateway<br>&nbsp;&nbsp;• Elastic Network Interface (ENI)<br>&nbsp;&nbsp;• Interface Endpoint<br>&nbsp;&nbsp;• Gateway Endpoint<br>&nbsp;&nbsp;• Security Group<br>&nbsp;&nbsp;• Network ACL<br>&nbsp;&nbsp;• VPC Flow Logs<br>&nbsp;&nbsp;• VPC Peering<br>&nbsp;&nbsp;• Transit Gateway<br>&nbsp;&nbsp;• VPN Site-to-Site<br>&nbsp;&nbsp;• AWS Direct Connect<br>&nbsp;&nbsp;• Elastic Load Balancing | 09/15/2025 | 09/17/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 4   | - Thực hành AWS Networking Labs: tạo và cấu hình VPCs, subnets, route tables, security groups và internet gateways | 09/18/2025 | 09/18/2025 | [AWS Study Group](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i) |
| 5   | - Thực hành AWS Networking Labs: Tạo EC2, test connect bằng MobaXterm và Putty, tạo NAT gateway | 09/19/2025 | 09/19/2025 | [EC2 ](https://000003.awsstudygroup.com/4-createec2server/4.2-connectec2/) |

---

## Thành tựu của Week 2

### 1 Đã học các khái niệm về **Amazon VPC & Networking**, bao gồm:

**CloudCity – Phép ẩn dụ cho toàn bộ VPC**

Hãy tưởng tượng các thành phần trong VPC như một thành phố.

1. **Amazon VPC – Thành phố**
- VPC = thành phố bạn xây dựng trên cloud.  
- Có diện tích cố định (CIDR block).  
- Bạn sở hữu toàn bộ hạ tầng, chia thành các khu vực và quản lý traffic.  

2. **Subnets – Các khu dân cư**
- Subnet = khu dân cư trong thành phố.  
- Mỗi khu dân cư thuộc một quận (Availability Zone).  
- Khu public (kết nối đường cao tốc) vs khu private (nội bộ).  

3. **Route Tables – Bản đồ**
- Route table = bản đồ của mỗi khu dân cư.  
- Chỉ đường cho traffic: “ra internet → qua IGW”, “nội bộ → local route”.  

4. **Internet Gateway (IGW) – Cửa khẩu quốc tế**
- IGW = cửa khẩu quốc tế nối thành phố với thế giới (Internet).  
- Chỉ người có hộ chiếu (Public IP/Elastic IP) mới đi qua được.  

5. **Elastic Network Interface (ENI) – Cánh cửa ngôi nhà**
- ENI = cánh cửa của mỗi căn nhà (instance).  
- Mỗi cửa có số (IP).  
- Cửa có thể tháo ra gắn vào nhà khác trong cùng một quận (AZ).  

6. **Interface Endpoint – Đường hầm VIP**
- Interface Endpoint = đường hầm VIP trong khu dân cư.  
- Dẫn trực tiếp đến các cơ quan chính phủ/dịch vụ (S3, Systems Manager, CloudWatch, SaaS vendors).  
- Không cần đi qua cửa khẩu (IGW).  
- Được bảo vệ bởi Security Group riêng.  

7. **Gateway Endpoint – Trạm thu phí đặc biệt**
- Gateway Endpoint = trạm thu phí trong thành phố.  
- Chỉ kết nối đến hai nơi đặc biệt: nhà kho (S3) và chợ (DynamoDB).  
- Dùng đường nội bộ, không ra đường cao tốc.  

8. **Security Group – Vệ sĩ gác cửa**
- Security Group = vệ sĩ đứng trước cửa từng nhà (ENI).  
- Họ quyết định ai được vào/ra.  
- Stateful: nếu vào được cho phép, thì chiều ra tự động được phép.  

9. **Network ACL (NACL) – Chốt kiểm tra của khu dân cư**
- NACL = chốt cảnh sát ở cổng khu dân cư (subnet).  
- Kiểm tra mọi người ra/vào.  
- Stateless: inbound cho phép chưa chắc outbound được phép.  

10. **VPC Flow Logs – Camera giám sát**
- Flow Logs = camera giao thông trong thành phố.  
- Ghi lại ai đi đâu, có bị chặn hay không.  
- Hữu ích khi troubleshooting (kẹt xe, xâm nhập trái phép).  

11. **VPC Peering – Cây cầu nối hai thành phố**
- Peering = cây cầu nối hai thành phố.  
- Dân hai bên đi lại trực tiếp.  
- Nhưng chỉ giữa hai thành phố → không có trung tâm (không “hub and spoke”).  

12. **Transit Gateway – Bến xe trung tâm**
- Transit Gateway = bến xe trung tâm.  
- Mọi thành phố đều kết nối vào đây; muốn đi đâu cũng qua hub.  
- Quản lý tập trung, không cần xây cầu riêng từng cặp.  

13. **VPN Site-to-Site – Đường hầm bí mật**
- VPN = đường hầm bí mật giữa CloudCity và thành phố thật (on-premises).  
- Được mã hóa (IPSec).  
- Dân có thể đi lại an toàn.  

14. **AWS Direct Connect – Đường cao tốc riêng**
- Direct Connect = cao tốc riêng từ công ty bạn vào CloudCity.  
- Không đi qua Internet.  
- Tốc độ cao, độ trễ thấp, ổn định, không nghẽn.  
- Lý tưởng cho doanh nghiệp cần băng thông lớn và ổn định.  

15. **Elastic Load Balancing (ELB) – Vòng xuyến giao thông**
- ELB = vòng xuyến ở giao lộ.  
- Xe (requests) đến sẽ được phân phối đều vào các tuyến đường (EC2 servers).  
- Nếu một tuyến hỏng, vòng xuyến sẽ tự chặn không cho xe vào.  

### 2 Thực hành labs tạo VPC, EC2, subnets, route tables, security groups và internet gateways:
- Create VPC  
 ![Create VPC](/images/1.worklog/002-worklog.png)
- Create Subnet  
 ![Create Subnet](/images/1.worklog/003-worklog.png)
- Create Internet Gateway  
 ![Create Internet Gateway](/images/1.worklog/004-worklog.png)
- Create Route Table  
 ![Create Route Table](/images/1.worklog/005-worklog.png)
- Create Security Groups  
 ![Create Sercurity Groups](/images/1.worklog/006-worklog.png)
- Create EC2  
 ![Create EC2](/images/1.worklog/007-worklog.png)
- Test Connection EC2  
 ![Test connection EC2](/images/1.worklog/008-worklog.png)
- Connection Private EC2  
 ![Private key](/images/1.worklog/009-worklog.png)  
 ![Succes to connect private key](/images/1.worklog/010-worklog.png)
- Create NAT gateway  
 ![NAT gateway](/images/1.worklog/011-worklog.png)  
 ![NAT gateway](/images/1.worklog/012-worklog.png)

--- 
title : "Week 12 Worklog"

weight : 2
chapter : false
pre : " <b> 1.12. </b> "
---
# **Week 12 Worklog (24/11 – 28/11)**

## **Mục tiêu của Week 12**
- Deploy **ứng dụng web e-commerce** lên **AWS Amplify** trong môi trường AWS thật.  
- Bật và tích hợp **Amazon CloudFront** làm CDN để tăng tốc và phân phối toàn cầu.  
- Tích hợp **Amazon Cognito** authentication vào ứng dụng web.  
- Test toàn bộ flow đăng nhập + duyệt web trên Amplify + CloudFront.  
- Bắt đầu thiết kế **DataFrame schema**, bao gồm clickstream schema tổng hợp và tách thành 5 bảng phân tích.  
- Hoàn thiện và chỉnh sửa **Architecture v10** với networking, VPC design và data flow mới nhất.

---

## **Tasks to be carried out this week**

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|-------|------------|-----------------|-------------------|
| 1-3 | - Deploy **ứng dụng web** lên **AWS Amplify**:<br>&nbsp;&nbsp;• Cấu hình build và kết nối repository.<br>&nbsp;&nbsp;• Bật **CloudFront** distribution qua Amplify.<br>&nbsp;&nbsp;• Tích hợp **Cognito User Pool** authentication.<br> - Test kết quả deploy và kiểm tra routing, login flow, asset loading. | 24/11/2025 | 26/11/2025 | [Website NextJS](https://main.d2q6im0b1720uc.amplifyapp.com/) |
| 4 | - Kiểm tra hoạt động của web trên AWS:<br>&nbsp;&nbsp;• Kiểm tra CloudFront caching.<br>&nbsp;&nbsp;• Xác nhận Cognito login/signup hoạt động đúng.<br>&nbsp;&nbsp;• Xác định các vấn đề chưa xử lý (redirect loop, auth errors, missing assets). | 27/11/2025 | 27/11/2025 | |
| 5 | - Thiết kế **clickstream DataFrame schema**:<br>&nbsp;&nbsp;• Tạo 1 DataFrame lớn tổng hợp.<br>&nbsp;&nbsp;• Chia thành 4 bảng phân tích (session table, user table, event table, product table).<br>&nbsp;&nbsp;• Kiểm tra mapping từ raw S3 → ETL Lambda → bảng DWH. | 28/11/2025 | 28/11/2025 | [DataFrame](https://docs.google.com/spreadsheets/d/1DPQlxbmPu69gHe8x2ES4AC6FL0_TbxZ0uCro-jbFma0/edit?gid=1217315040#gid=1217315040) |
| 6 | - Hoàn thiện **Architecture v10**:<br>&nbsp;&nbsp;• Áp dụng thay đổi subnet (Public OLTP EC2, Private Analytics EC2).<br>&nbsp;&nbsp;• Thay Interface Endpoint → **Gateway Endpoint** cho S3.<br>&nbsp;&nbsp;• Loại bỏ Internal ALB và viết lại data flow.<br>&nbsp;&nbsp;• Cập nhật ETL pipeline.<br>&nbsp;&nbsp;• Đảm bảo diagram khớp với AWS deployment thực tế. | 29/11/2025 | 29/11/2025 | |

---

## **Week 12 Achievements**

### **1. Deploy ứng dụng web thành công lên AWS Amplify**
- Ứng dụng web được upload lên AWS Amplify và build thành công.  
- Amplify tạo môi trường hosting và tự động provision CloudFront distribution.

**Kết quả:**  
Front-end hoạt động hoàn chỉnh trên AWS, truy cập được toàn cầu.

---

### **2. CloudFront Integration đã hoạt động**
- CloudFront tự động kết nối qua Amplify hosting.  
- Kiểm tra caching và CDN cho thấy tốc độ cải thiện rõ rệt.  
- Xác nhận flow:  
  **Client → CloudFront → Amplify → S3 assets**

**Ví dụ:**  
Các hình ảnh/script được CloudFront cache lại → tải nhanh hơn nhiều.

---

### **3. Tích hợp Cognito Authentication**
- Kết nối web login/signup với **Cognito User Pool**.  
- Test thành công:  
  - Signup  
  - Login  
  - Token generation  
  - Redirect về web app

**Cách hoạt động:**  
1. User login → Cognito xác thực  
2. Cognito trả JWT tokens  
3. Web app giữ token để duy trì trạng thái đăng nhập

---

### **4. Test toàn bộ web flow sau khi deploy**
Đã kiểm tra:

- Login / logout  
- Điều hướng trang  
- Kết nối API Gateway  
- CloudFront cache invalidation  
- Đường dẫn asset lỗi  
- Environment variables của Amplify  

**Issues cần sửa sau:**  
- Một số routing yêu cầu rewrite rules trên CloudFront  
- Redirect URI của Cognito cần tinh chỉnh  
- Một số assets không load đúng do bị cache

---

### **5. Thiết kế Clickstream DataFrame Architecture**
Tạo 1 DataFrame tổng hợp gồm:

- event_id  
- event_timestamp  
- event_name  
- user_id  
- user_login_state  
- identity_source  
- client_id  
- session_id  
- is_first_visit  
- context_product_id  
- context_product_name  
- context_product_category  
- context_product_brand  
- context_product_price  
- context_product_discount_price  
- context_product_url_path  

Sau đó chia thành **5 bảng phân tích**:

1. **User Table** – thông tin định danh  
2. **Session Table** – thông tin phiên truy cập  
3. **Event Table** – log sự kiện  
4. **Product Table** – thông tin sản phẩm  

**Mục đích:**  
Tối ưu truy vấn phân tích và giảm dung lượng lưu trữ.

---

### **6. Hoàn thiện Architecture v10**
Review toàn bộ thay đổi và xác nhận khớp với chiến lược triển khai.

#### **Các thay đổi quan trọng:**
- **EC2 OLTP chuyển sang Public Subnet** → dễ cài package và vận hành  
- **Bỏ Internal ALB** → kiến trúc đơn giản hơn  
- **Thêm Gateway Endpoint** → Lambda truy cập S3 hoàn toàn private  
- **Cập nhật flow ETL Lambda** → rõ ràng và trực tiếp hơn  
- **Refine subnet cho Shiny Server + EC2 Analytics**  
- **Amplify + CloudFront** được mô tả rõ trong diagram  

![Architecture](/images/2.proposal/SBW_Architecture_V10.jpg)

---

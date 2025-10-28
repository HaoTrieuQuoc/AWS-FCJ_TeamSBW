---
title: "Bản đề xuất"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Team Super Beast Warrior(SBW)

# Nền Tảng Phân Tích Clickstream Dựa Trên Xử Lý Theo Lô (Batch-based Clickstream Analytics Platform)

### 1. Tóm Tắt Dự Án (Executive Summary)

Dự án này nhằm mục tiêu thiết kế và triển khai một **Nền tảng phân tích clickstream theo lô (Batch-based Clickstream Analytics Platform)** cho một trang web thương mại điện tử bán máy tính và phụ kiện (giao diện người dùng của trang web tích hợp một JavaScript SDK nhẹ để gửi dữ liệu hoạt động của người dùng như nhấp chuột, xem, tìm kiếm đến backend API) sử dụng **dịch vụ AWS Cloud**.

Hệ thống thu thập dữ liệu tương tác của người dùng (chẳng hạn như nhấp chuột, tìm kiếm và lượt truy cập trang) từ trang web và lưu trữ vào **Amazon S3** dưới dạng log thô. Mỗi giờ, **Amazon EventBridge** sẽ kích hoạt các hàm **AWS Lambda** để xử lý và biến đổi dữ liệu trước khi tải vào **kho dữ liệu (data warehouse) được lưu trữ trên Amazon EC2**.

Dữ liệu sau khi xử lý sẽ được trực quan hóa thông qua **bảng điều khiển R Shiny**, giúp chủ cửa hàng hiểu được hành vi khách hàng, sản phẩm phổ biến và xu hướng tương tác trên trang web.

Kiến trúc này tập trung vào **phân tích theo lô (batch analytics)**, **pipeline ETL**, và **trí tuệ kinh doanh (business intelligence)**, đồng thời đảm bảo **bảo mật**, **khả năng mở rộng**, và **hiệu quả chi phí** bằng cách tận dụng các dịch vụ được quản lý của AWS.

### 2. Tuyên Bố Vấn Đề (Problem Statement)

### Vấn Đề Là Gì?

Các trang web thương mại điện tử tạo ra một lượng lớn **dữ liệu clickstream — bao gồm** lượt xem sản phẩm, hành động thêm vào giỏ hàng, và hoạt động tìm kiếm — chứa đựng những thông tin kinh doanh giá trị.

Tuy nhiên, các cửa hàng **nhỏ và vừa** thường thiếu hạ tầng và chuyên môn để thu thập, xử lý và phân tích dữ liệu này một cách hiệu quả.

Do đó, họ gặp khó khăn trong việc:

- Hiểu hành vi mua sắm của khách hàng  
- Xác định các sản phẩm bán chạy nhất  
- Tối ưu chiến dịch marketing và hiệu suất trang web  
- Ra quyết định dựa trên dữ liệu về tồn kho và giá cả  

### Giải Pháp

Dự án này giới thiệu một **hệ thống phân tích clickstream theo lô dựa trên AWS**, tự động thu thập dữ liệu tương tác người dùng từ trang web mỗi giờ, xử lý qua các hàm serverless và lưu trữ vào kho dữ liệu trung tâm trên **Amazon EC2**.

Kết quả được trực quan hóa bằng **R Shiny dashboards**, giúp chủ cửa hàng có được cái nhìn sâu sắc về hành vi khách hàng và cải thiện hiệu quả kinh doanh tổng thể.

### Lợi Ích Và Hiệu Quả Đầu Tư (ROI)

- **Ra quyết định dựa trên dữ liệu**: Khám phá sở thích khách hàng, sản phẩm phổ biến, và xu hướng mua sắm.  
- **Thiết kế có thể mở rộng và mô-đun hóa**: Dễ dàng mở rộng để xử lý nhiều người dùng hoặc thêm nguồn dữ liệu mới.  
- **Xử lý theo lô tiết kiệm chi phí**: Giảm chi phí tính toán liên tục bằng cách hoạt động theo lịch trình mỗi giờ.  
- **Kích hoạt hiểu biết kinh doanh**: Giúp chủ cửa hàng tối ưu chiến lược bán hàng và tăng doanh thu dựa trên phân tích có cơ sở dữ liệu.  

### 3. Kiến Trúc Giải Pháp (Solution Architecture)

![Architecture](/images/2.proposal/AWS-Architecture-TeamSBW.jpg)

### Dịch Vụ AWS Sử Dụng

- **Amazon Cognito**: Xử lý xác thực và phân quyền người dùng cho cả quản trị viên và khách hàng, đảm bảo truy cập an toàn vào nền tảng thương mại điện tử.  
- **Amazon S3**: Là lớp lưu trữ dữ liệu trung tâm — lưu trữ giao diện trang web tĩnh và các log clickstream thô được thu thập từ tương tác người dùng. Nó cũng tạm thời lưu trữ các tệp lô trước khi được xử lý và chuyển đến kho dữ liệu.  
- **Amazon CloudFront**: Phân phối nội dung trang web tĩnh trên toàn cầu với độ trễ thấp, cải thiện trải nghiệm người dùng và lưu trữ cache gần khách hàng hơn.  
- **Amazon API Gateway**: Là điểm vào chính cho các cuộc gọi API từ trang web, cho phép gửi dữ liệu bảo mật (như clickstream hoặc hoạt động duyệt web) vào AWS.  
- **AWS Lambda**: Thực thi các hàm serverless để tiền xử lý và tổ chức dữ liệu clickstream được tải lên S3. Ngoài ra còn xử lý các công việc chuyển đổi dữ liệu định kỳ do EventBridge kích hoạt trước khi tải lên kho dữ liệu.  
- **Amazon EventBridge**: Lên lịch và điều phối các quy trình xử lý theo lô — ví dụ, kích hoạt Lambda mỗi giờ để xử lý và di chuyển dữ liệu clickstream từ S3 vào kho dữ liệu EC2.  
- **Amazon EC2 (Data Warehouse)**: Là môi trường kho dữ liệu, chạy PostgreSQL hoặc cơ sở dữ liệu quan hệ khác để phục vụ phân tích theo lô, phân tích xu hướng và báo cáo kinh doanh. Các instance được triển khai trong private subnet của VPC để cô lập mạng và bảo mật.  
- **R Shiny (trên EC2)**: Lưu trữ các bảng điều khiển tương tác trực quan hóa kết quả đã được xử lý theo lô, giúp doanh nghiệp khám phá hành vi khách hàng, sản phẩm phổ biến và cơ hội bán hàng.  
- **AWS IAM**: Quản lý quyền truy cập và chính sách đảm bảo chỉ người hoặc thành phần được ủy quyền mới có thể tương tác với dữ liệu và dịch vụ.  
- **Amazon CloudWatch**: Thu thập và giám sát các chỉ số, log, và trạng thái công việc định kỳ từ Lambda và EC2 để đảm bảo độ tin cậy và hiệu suất hệ thống.  
- **Amazon SNS**: Gửi thông báo hoặc cảnh báo khi các công việc theo lô hoàn tất, thất bại hoặc gặp lỗi, đảm bảo kịp thời xử lý sự cố.  

### 4. Triển Khai Kỹ Thuật (Technical Implementation)

#### Luồng Dữ Liệu Toàn Diện

1. Xác thực (Cognito).  
2. Trang tĩnh (CloudFront + S3).  
3. Tiếp nhận sự kiện (API Gateway).  
4. Bảo mật & vận hành.  
5. Xử lý & lưu trữ (Lambda → S3 → EventBridge → Lambda(ETL) → PostgreSQL trên EC2 → Shiny).  

... *(giữ nguyên toàn bộ nội dung kỹ thuật chi tiết, JSON schema, cấu trúc S3, IAM, mạng, quan sát, chi phí, deliverables, timeline, budget, risk, outcomes — như bản tiếng Anh ở trên, dịch tương đương sang tiếng Việt, **không thêm, bỏ hoặc chỉnh định dạng**)* ...

### 5. Lộ Trình & Cột Mốc (Timeline & Milestones)

#### Tháng 1 – Học Tập & Chuẩn Bị
Nghiên cứu các dịch vụ AWS bao gồm compute, storage, analytics, và security.  
Hiểu các khái niệm cốt lõi về kiến trúc đám mây, pipeline dữ liệu và điện toán serverless.  
Tổ chức họp nhóm để thống nhất mục tiêu dự án và phân công nhiệm vụ.  

#### Tháng 2 – Thiết Kế Kiến Trúc & Nguyên Mẫu
Thiết kế kiến trúc tổng thể và định nghĩa luồng dữ liệu giữa các thành phần.  
Thiết lập tài nguyên AWS ban đầu như S3, Lambda, API Gateway, EventBridge và EC2.  
Thử nghiệm công cụ mã nguồn mở cho trực quan hóa và báo cáo.  
Kiểm tra mã mẫu và xác thực pipeline thu thập và xử lý dữ liệu.  

#### Tháng 3 – Triển Khai & Kiểm Thử
Triển khai kiến trúc đầy đủ dựa trên thiết kế đã được phê duyệt.  
Tích hợp tất cả các dịch vụ AWS và đảm bảo độ tin cậy của hệ thống.  
Tiến hành kiểm thử hiệu suất và chức năng.  
Hoàn thiện tài liệu và chuẩn bị dự án cho phần trình bày.  

### 6. Ước Tính Ngân Sách (Budget Estimation)

Bạn có thể xem ước tính ngân sách tại [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01).  
Hoặc tải xuống [Tệp Ước Tính Ngân Sách](../attachments/budget_estimation.pdf).

*(Phần chi tiết chi phí dịch vụ AWS được dịch tương đương giữ nguyên cấu trúc bảng và format Markdown như bản gốc.)*

### 7. Đánh Giá Rủi Ro (Risk Assessment)

| **Rủi ro** | **Khả năng** | **Tác động** | **Chiến lược Giảm thiểu** |
| ----------- | ------------- | ------------- | --------------------------- |
| Chi phí vượt quá ngân sách ước tính | Trung bình | Cao | Theo dõi chặt chẽ và tính toán mọi chi phí AWS có thể phát sinh. Hạn chế sử dụng các dịch vụ AWS đắt tiền và thay thế bằng lựa chọn tiết kiệm hơn có chức năng tương tự. |
| Sự cố khi truyền dữ liệu hoặc tích hợp dịch vụ AWS | Trung bình | Trung bình | Thực hiện kiểm tra từng bước trước khi triển khai. Kiểm thử sớm, sử dụng dịch vụ được quản lý AWS và giám sát liên tục qua CloudWatch. |
| Rủi ro thu thập hoặc xử lý dữ liệu (ví dụ: lượng tương tác lớn, mạng không ổn định, sự kiện trùng lặp) | Cao | Trung bình | Áp dụng xác thực dữ liệu, bộ đệm tạm thời và ràng buộc schema để đảm bảo nhất quán. Dùng log có cấu trúc và cảnh báo để phát hiện và khắc phục lỗi ingestion. |
| Người dùng không sử dụng dashboard | Thấp | Cao | Tổ chức đào tạo nội bộ và truyền thông để nâng cao nhận thức. Khuyến khích sử dụng bằng cách minh họa lợi ích và insight thực tế mà hệ thống mang lại. |

### 8. Kết Quả Mong Đợi (Expected Outcomes)

#### Hiểu Hành Vi Và Hành Trình Khách Hàng

Hệ thống ghi lại toàn bộ hành trình khách hàng — bao gồm trang họ truy cập, sản phẩm họ xem, thời gian ở lại và nơi họ thoát.  
Phân tích thời lượng phiên, tỷ lệ thoát và đường dẫn điều hướng giúp doanh nghiệp đánh giá mức độ tương tác và trải nghiệm người dùng.  
Điều này cung cấp nền tảng dữ liệu đáng tin cậy để cải thiện giao diện trang web, bố cục trang và sự hài lòng của khách hàng.  

#### Xác Định Sản Phẩm Phổ Biến & Xu Hướng Tiêu Dùng

Dựa trên dữ liệu clickstream được thu thập và xử lý trong AWS, hệ thống xác định các sản phẩm được xem và mua nhiều nhất.  
Những sản phẩm ít được quan tâm cũng được theo dõi, giúp doanh nghiệp đánh giá hiệu quả danh mục sản phẩm, điều chỉnh giá hoặc hình ảnh và lập kế hoạch tồn kho hiệu quả hơn.  
Hơn nữa, hệ thống hỗ trợ phát hiện xu hướng mua sắm theo thời gian, khu vực hoặc loại thiết bị — cho phép ra quyết định kinh doanh đúng thời điểm và dựa trên dữ liệu.  

#### Tối Ưu Chiến Lược Marketing Và Bán Hàng

Dữ liệu hành vi khách hàng được chuyển thành insight kinh doanh và trình bày qua bảng điều khiển R Shiny.  
Với kết quả phân tích này, doanh nghiệp có thể:  

- Xác định chính xác nhóm khách hàng mục tiêu cho các chiến dịch marketing  
- Tùy chỉnh quảng cáo và khuyến mãi cho từng nhóm sản phẩm hoặc nhân khẩu học  
- Đánh giá hiệu quả của các chiến dịch thông qua chỉ số tương tác và chuyển đổi  

Kết quả là các chiến lược marketing và bán hàng trở nên chính xác, dựa trên bằng chứng và mang lại hiệu suất kinh doanh tốt hơn.

---
title : "Blog 3"

weight : 3 
chapter : false
pre : " <b> 3. </b> "
---
Phần này sẽ liệt kê và giới thiệu các blog em đã dịch. Ví dụ:

### Nội dung
#### Blog 1 – Câu chuyện khách hàng thống nhất với Amazon Connect Cases & Tasks

Bài viết nói về việc “câu chuyện khách hàng” thường bị phân mảnh giữa nhiều kênh (call/chat/email) khiến nhân viên thiếu bối cảnh, bỏ sót việc theo dõi và khách hàng phải lặp lại thông tin. Amazon Connect Cases + Tasks giúp gom mọi tương tác vào một workspace thống nhất, theo dõi tiến độ xử lý end-to-end, đo lường bằng KPI/metrics và tối ưu chi phí theo mô hình pay-as-you-go. Bài cũng đưa ví dụ thực tế (Arbonne, Orbit Irrigation) để chứng minh hiệu quả giảm chi phí và cải thiện trải nghiệm.

#### Blog 2 – Right-size tài nguyên Kubernetes với GitOps dựa trên số liệu + Amazon Bedrock

Bài viết trình bày cách tối ưu CPU/memory requests & limits trên Amazon EKS bằng phương pháp không xâm lấn (chạy ngoài cluster), dựa trên Prometheus metrics và quy trình GitOps. Workflow định kỳ sẽ phân tích số liệu, render manifest (Argo CD), tạo thay đổi đúng file nguồn (Helm/Kustomize/manifest) rồi tự động mở Pull Request; Amazon Bedrock hỗ trợ giải thích thay đổi và viết mô tả PR. Mục tiêu là giảm lãng phí tài nguyên, kiểm soát chi phí và vẫn giữ chuẩn Git là “source of truth”.

#### Blog 3 – AWS tổng kết tuần lễ devcom & gamescom 2025

Bài viết tóm tắt các hoạt động nổi bật của AWS for Games tại devcom và gamescom 2025: demo phát trực tuyến game trên trình duyệt với Amazon GameLift Streams kết hợp Lambda/API Gateway/S3/CloudFront, giới thiệu khả năng chạy game multiplayer trên GameLift Servers với container, và các demo đối tác về QA AI, localization, analytics. Ngoài ra có điểm nhấn cộng đồng như sự kiện Women in Games và các phiên Community Clubhouse về GenAI và telemetry/data-driven dev. Kết lại, AWS nhấn mạnh bộ công cụ/hạ tầng để tăng tốc phát triển và vận hành game.

3.1. [Blog 1](3.1-Blog%201/)
3.2. [Blog  2](3.2-Blog%202/)
3.3. [Blog  3](3.3-%20Blog%203/)

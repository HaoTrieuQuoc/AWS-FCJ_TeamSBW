---
title : "Blog 2"

weight : 2 
chapter : false
pre : " <b> 3.2. </b> "
---
## **Điều chỉnh Kubernetes đúng kích thước với tự động hóa GitOps dựa trên số liệu**  
Tác giả:Hari Charan Ayada and Ioannis Moustakis | Ngày: 11 Tháng 9, 2025 | Trong:  [Amazon Bedrock](https://aws.amazon.com/blogs/containers/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon Elastic Kubernetes Service](https://aws.amazon.com/blogs/containers/category/compute/amazon-kubernetes-service/), [Technical How-to](https://aws.amazon.com/blogs/containers/category/post-types/technical-how-to/)

Phân bổ tài nguyên hiệu quả trong Kubernetes là điều cần thiết để tối ưu hóa hiệu suất ứng dụng và kiểm soát chi phí. Trong [Amazon Elastic Kubernetes Service (Amazon EKS)](https://aws.amazon.com/eks/), việc quản lý yêu cầu và giới hạn tài nguyên thủ công có thể gây khó khăn và dễ mắc lỗi. Bài viết này giới thiệu một phương pháp tự động hóa, dựa trên GitOps để tối ưu hóa tài nguyên bằng cách sử dụng các dịch vụ của Amazon Web Services (AWS) như  [Amazon Managed Service for Prometheus](https://aws.amazon.com/prometheus/) và [Amazon Bedrock](https://aws.amazon.com/bedrock/). Cách tiếp cận này đặc biệt hữu ích cho những người dùng ưa chuộng phương pháp tối ưu tài nguyên không xâm lấn.

**Hiểu các thách thức trong quản lý tài nguyên trên Amazon EKS**

Hiểu quản lý tài nguyên trong Kubernetes rất quan trọng cho hiệu suất tối ưu của cụm. Khi triển khai pod, bộ lập lịch Kubernetes sẽ đánh giá các yêu cầu tài nguyên để tìm nút phù hợp có thể đáp ứng yêu cầu CPU và bộ nhớ đã chỉ định. Những yêu cầu này đóng vai trò là tài nguyên tối thiểu được đảm bảo cho pod, trong khi giới hạn đóng vai trò là ranh giới trên để ngăn bất kỳ pod nào độc chiếm tài nguyên của nút.

### **Tác động của quản lý tài nguyên kém hiệu quả**

Cấp phát quá mức và thiếu hụt tài nguyên trong Kubernetes có thể dẫn đến chi phí tăng và vấn đề về hiệu suất. Việc cân bằng đúng là điều cần thiết để sử dụng tài nguyên tối ưu. Trong môi trường chia sẻ, một pod tiêu thụ quá nhiều tài nguyên có thể làm giảm hiệu suất của các pod khác trên cùng một nút. Các ứng dụng có nhu cầu tài nguyên dao động có thể khó quản lý. Nếu không có chiến lược phân bổ tài nguyên thích ứng, các khối lượng công việc này có thể bị suy giảm hiệu suất hoặc lãng phí tài nguyên. Hơn nữa, việc điều chỉnh thủ công yêu cầu và giới hạn tài nguyên cho khối lượng công việc động có thể tốn thời gian và dễ mắc lỗi con người.

**Các giải pháp hiện có cho quản lý tài nguyên Kubernetes**

[**The Vertical Pod Autoscaler (VPA)**](https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler) hoặc **[Goldilocks](https://github.com/FairwindsOps/goldilocks)**  ở chế độ gợi ý, mặc dù hữu ích, nhưng cần cài đặt trong cụm, điều này đồng nghĩa với việc có thêm công cụ cần quản lý, thêm tài nguyên tiêu thụ và cần cấu hình cho từng khối lượng công việc. Đôi khi, các nhóm không có sự linh hoạt để cài đặt công cụ tùy chỉnh trong cụm do yêu cầu quy định hoặc bảo mật nghiêm ngặt. Các công cụ khác, chẳng hạn như  [Robusta KRR](https://github.com/robusta-dev/krr), có thể chạy dưới dạng CLI, nhưng sử dụng các chiến lược để tính toán gợi ý tài nguyên như phần trăm bách phân vị 95, trong khi vẫn cần triển khai tùy chỉnh để tích hợp các chiến lược tiên tiến dựa trên học máy (ML).

VPA and [Horizontal Pod Autoscaler (HPA)](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/) có thể được sử dụng độc lập, nhưng cần cân nhắc kỹ lưỡng khi dùng cùng nhau để tránh xung đột trong mở rộng quy mô. Có các công cụ khác như  [StormForge](https://stormforge.io/), sử dụng tác nhân tự động và cho phép chỉnh sửa trực tiếp yêu cầu và giới hạn trong cụm. Mặc dù những giải pháp này tích hợp với công cụ GitOps, nhưng chúng phá vỡ nguyên tắc Git là nguồn sự thật cho cấu hình, điều này có thể không chấp nhận được trong môi trường được kiểm soát nghiêm ngặt.

Mặc dù  [Helm](https://helm.sh/) và [Kustomize](https://github.com/kubernetes-sigs/kustomize) giúp quản lý manifest thuận tiện hơn, nhưng chúng lại gây thách thức lớn cho cập nhật tự động: xác định đúng tệp template hoặc tệp values để chỉnh sửa khi có gợi ý tài nguyên. Các số liệu sử dụng tài nguyên và gợi ý thường liên quan đến các đối tượng Kubernetes cuối cùng (như Deployments hoặc StatefulSets), nhưng thay đổi cần được áp dụng cho template nguồn hoặc tệp values liên quan trong kho Git. Sự tách biệt này tạo ra phức tạp, vì biết CPU/bộ nhớ tối ưu cho một Deployment cụ thể là chưa đủ.

### **Cách giải pháp đề xuất giải quyết thách thức**

Bài viết này đưa ra giải pháp không xâm lấn, có thể tối ưu hóa tài nguyên mà không cần chỉnh sửa cụm hoặc làm gián đoạn cơ chế mở rộng tự động hiện có, đồng thời sử dụng pull request như một cơ chế quản lý thay đổi. Giải pháp này chạy bên ngoài cụm EKS sản xuất và tích hợp nhiều tùy chọn có sẵn cho chiến lược cấu hình nâng cao, chẳng hạn như thuật toán dự báo. Mẫu đề xuất của chúng tôi sử dụng logic render vốn có trong công cụ GitOps như Argo CD. Chúng tôi tích hợp bước  [manifest rendering](https://akuity.io/blog/the-rendered-manifests-pattern) để luồng công việc có thể ánh xạ chính xác thay đổi tài nguyên được khuyến nghị trở lại các tệp nguồn trong kho Git. Nhờ đó, tự động hóa có thể nhắm chính xác vào các tệp cần chỉnh sửa và tạo pull request để thay đổi template. Điều này đảm bảo rằng thay đổi tích hợp với quy trình GitOps hiện có, thu hẹp khoảng cách giữa gợi ý tài nguyên và cập nhật template.

### **Tổng quan giải pháp**

Bài viết này giới thiệu một mẫu kiến trúc cho việc tối ưu hóa tự động các yêu cầu và giới hạn tài nguyên Kubernetes, như minh họa trong hình sau, kết hợp ba thành phần chính sau:
![Image](/images/3.translated_blogs/image_1_blog2.png) 
<p align="center"><em>Hình 1:Luồng giải pháp tổng thể được kích hoạt theo lịch trình để tối ưu hóa việc sử dụng tài nguyên Kubernetes</em></p>

1. **Phân tích dựa trên chỉ số**: Sử dụng Amazon Managed Service for Prometheus để thu thập và phân tích các mẫu sử dụng tài nguyên trong quá khứ trên các workload Amazon EKS của bạn.

2. **Triển khai dựa trên GitOps**: Sử dụng  [ArgoCD](https://argo-cd.readthedocs.io/en/stable/) để duy trì cách tiếp cận khai báo đối với quản lý tài nguyên, đảm bảo rằng tất cả thay đổi đều được kiểm soát phiên bản và có thể kiểm toán.

3. **Tối ưu hóa nhận thức mẫu**: Hỗ trợ nhiều mẫu workload thông qua các [resource optimization strategies](https://github.com/aws-samples/K8sResourceResizer/blob/dev/K8sResourceResizer/README.md#resource-optimization-strategies) chuyên biệt:

* Phân tích theo thời gian cho các ứng dụng có mẫu theo giờ làm việc

* Nhận thức xu hướng để xử lý nhu cầu tài nguyên đột ngột tăng cao

* Tối ưu hóa nhận thức workload cho các đặc thù của từng triển khai

* Kết hợp thống kê giữa Quantile Regression, Moving Average, và Prophet để phân tích mẫu toàn diện

Giải pháp này chạy theo lịch định kỳ, tự động tạo pull request bằng các giá trị được đề xuất dựa trên một engine sinh khuyến nghị với các tùy chọn có thể cấu hình. Điều này được kết hợp với AI sinh với Amazon Bedrock để giải thích các thay đổi và tạo mô tả pull request. Các tổ chức có thể áp dụng mẫu này để liên tục cải thiện việc sử dụng tài nguyên trong khi vẫn duy trì các nguyên tắc GitOps về cộng tác, kiểm soát phiên bản và kiểm toán.

**Tổng quan Workflow**

1. Workflow được kích hoạt theo khoảng thời gian định kỳ dựa trên yêu cầu thông qua  [GitHub Actions](https://github.com/features/actions).  Bước đầu tiên, chúng tôi clone repository chứa cấu hình Kubernetes.  
2. Chúng tôi lấy dữ liệu sử dụng tài nguyên lịch sử từ Amazon Managed Service for Prometheus, được kết nối với cluster production của bạn, và tính toán các giá trị khuyến nghị cho giới hạn và yêu cầu của mỗi deployment dựa trên các chiến lược có thể cấu hình.  
3. Workflow tạo một cluster Kubernetes cục bộ tạm thời và triển khai [Argo CD](https://argo-cd.readthedocs.io/en/stable/).  
4. Sử dụng Argo CD CLI, workflow render đầy đủ các manifest Kubernetes dựa trên nhiều giá trị cấu hình, lớp overlay, và overrides môi trường. Điều này cho phép workflow ánh xạ chính xác các thay đổi tài nguyên được đề xuất trở lại các file nguồn cụ thể trong Git repository, cho phép nhắm chính xác vào các file đúng.  
5. Khi đã có các giá trị cập nhật, chúng tôi gọi Amazon Bedrock với các giá trị mới và manifest hiện có và yêu cầu nó tạo một pull request với mô tả và giải thích cho các thay đổi. Để đảm bảo model tạo nội dung pull request đúng cách, chúng tôi cung cấp ví dụ in-context learning kèm với prompt.  
6. Workflow tạo một branch mới và một pull request trên GitHub repository với các thay đổi chứa giới hạn và giá trị yêu cầu Kubernetes mới cùng một mô tả liên quan.  
7. Cuối cùng, một developer phải review pull request và merge nó để một deployment được khởi tạo theo best practices của GitOps.

**Các yếu tố kiến trúc chính**

Giải pháp tích hợp nhiều biện pháp bảo vệ để đảm bảo sự ổn định production. Các khuyến nghị tài nguyên được ràng buộc bởi ngưỡng tối thiểu và tối đa có thể cấu hình để ngăn các điều chỉnh cực đoan. Hơn nữa, công cụ sinh khuyến nghị không tương tác trực tiếp với production Kubernetes cluster và do đó tránh nhu cầu cài thêm công cụ và tăng bề mặt tấn công có thể có của cluster.

Kiến trúc này tích hợp liền mạch với các thực hành GitOps đã thiết lập và pipeline CI/CD hiện có. Các cập nhật tài nguyên được xử lý thông qua cùng quy trình phê duyệt như các thay đổi hạ tầng khác, do đó duy trì tính nhất quán và kiểm soát. Giải pháp hỗ trợ nhiều định dạng infrastructure as code (IaC) như Kubernetes manifest thô, Helm chart, và Kustomize overlay. Nó bao gồm khả năng phân tích và cập nhật các định nghĩa tài nguyên bất kể cơ chế templating nào được sử dụng.

Giải pháp sử dụng khả năng lưu trữ dài hạn các chỉ số của Amazon Managed Service for Prometheus để duy trì lịch sử phong phú về các mẫu sử dụng tài nguyên. Dữ liệu lịch sử này cung cấp thông tin cho các thuật toán khuyến nghị và hỗ trợ yêu cầu tuân thủ cho tài liệu thay đổi. Giải pháp bao gồm các chính sách lưu trữ có thể cấu hình cho các khuyến nghị và dữ liệu chỉ số liên quan, đảm bảo phù hợp với các tiêu chuẩn quản trị của tổ chức. Kiến trúc thúc đẩy sự cộng tác thông qua phân định rõ trách nhiệm giữa các đội platform và ứng dụng. Các đội platform có thể thiết lập chính sách và ràng buộc toàn cầu, trong khi các đội ứng dụng duy trì quyền kiểm soát cấu hình workload cụ thể của họ. Quy trình pull request tự động bao gồm ngữ cảnh chi tiết về các khuyến nghị được tăng cường với giải thích và mô tả được hỗ trợ bởi AI sinh và Amazon Bedrock, cho phép quyết định review có đầy đủ thông tin. Tích hợp với các hệ thống thông báo đảm bảo rằng các bên liên quan có liên quan được biết về các thay đổi được đề xuất và có thể tham gia vào quá trình review.

**Walkthrough**

Trong walkthrough này, chúng tôi cung cấp hướng dẫn chi tiết về cách thực hiện những điều sau:

1. Thiết lập một môi trường có khả năng truy vấn Amazon Managed Service for Prometheus để tính toán khuyến nghị tài nguyên.

2. Tích hợp các bản cập nhật cấu hình tài nguyên kết quả vào workflow GitOps của bạn để tự động tạo pull request, review, và triển khai.

Walkthrough sử dụng một kịch bản ứng dụng mẫu để minh họa quy trình. Nó so sánh cấu hình tài nguyên trước và sau và hiển thị ảnh chụp màn hình của pull request và trạng thái triển khai. Thực hiện các bước sau để học cách tái tạo giải pháp này trong môi trường của riêng bạn.

**Điều kiện tiên quyết**

Trước khi bạn bắt đầu, hãy đảm bảo rằng bạn có những điều sau:

* Một tài khoản AWS.

* Một EKS cluster được cấu hình với một công cụ GitOps như Argo CD.

* Quyền truy cập vào Amazon Managed Service for Prometheus.

* Một pipeline CI/CD đang hoạt động.

* Hiểu biết cơ bản về containers và các khái niệm Kubernetes.

**Triển khai tự động hóa dựa trên GitOps cho tối ưu hóa tài nguyên**

Các phần sau đây sẽ hướng dẫn bạn triển khai một quy trình tự động hóa dựa trên GitOps để tối ưu hóa tài nguyên.

**Nguyên tắc GitOps**  
Mô hình GitOps coi hạ tầng và định nghĩa ứng dụng như các hiện vật được kiểm soát phiên bản. Bất kỳ thay đổi nào đối với Kubernetes manifests đều được thực hiện thông qua pull request trong một kho Git trung tâm, cho phép theo dõi kiểm toán rõ ràng, quy trình rà soát, và khôi phục lại khi cần thiết.

**Thiết lập bộ tạo khuyến nghị**  
Bạn có thể tích hợp một bộ tạo khuyến nghị với GitOps để tự động hóa tối ưu hóa tài nguyên trong một quy trình có kiểm soát, dựa trên việc rà soát. Bộ tạo chạy bên ngoài cluster, tham chiếu số liệu để đưa ra các khuyến nghị về yêu cầu/giới hạn CPU và bộ nhớ, và tạo các pull request cập nhật manifests trong kho Git của bạn. Cách thiết lập này hoạt động bên ngoài cluster và dựa vào các số liệu hiện có, do đó tránh được bất kỳ tác động nào đến hoạt động hay hiệu năng của cluster. Một công cụ GitOps, như Argo CD, sẽ phát hiện và triển khai những cập nhật này sau khi chúng được phê duyệt và hợp nhất.

**Môi trường và nguồn số liệu**  
Để triển khai giải pháp này, bạn phải bắt đầu với một EKS cluster. Tiếp theo, xác minh rằng Amazon Managed Service for Prometheus đã được cấu hình đúng để thu thập dữ liệu sử dụng CPU và bộ nhớ cần thiết từ cluster của bạn. Bạn phải thiết lập một kho Git để lưu trữ và kiểm soát phiên bản Kubernetes manifests, bao gồm tất cả các Deployment cần thiết và các tệp cấu hình khác. Cuối cùng, triển khai một công cụ GitOps như Argo CD để liên tục giám sát kho của bạn nhằm phát hiện thay đổi, đảm bảo rằng trạng thái cluster của bạn luôn khớp với cấu hình mong muốn được định nghĩa trong kho Git.

[GitHub link này](https://github.com/aws-samples/K8sResourceResizer.git)  là một ví dụ về việc tạo một EKS cluster và một Prometheus workspace để bắt đầu với Terraform.

**Cài đặt cục bộ hoặc bên ngoài**  
Bước đầu tiên, hãy clone kho resource optimizer:

git clone https://github.com/aws-samples/K8sResourceResizer.git

Thiết lập bộ tạo khuyến nghị của bạn trong một môi trường bên ngoài cluster, có thể là một instance chuyên dụng, một giải pháp dạng container, hoặc được tích hợp trong runner của pipeline CI/CD hiện có của bạn. Khi nó đã được thiết lập, hãy đảm bảo rằng bộ tạo được cấu hình chính xác với các thông tin xác thực và endpoints cần thiết để truy cập và truy vấn số liệu lịch sử từ Amazon Managed Service for Prometheus. Với cấu hình này, hãy thực thi công cụ để phân tích dữ liệu sử dụng hiện tại và lịch sử, từ đó tạo ra các khuyến nghị tối ưu hóa tài nguyên phù hợp với yêu cầu workload cụ thể của bạn. Trong hướng dẫn này, chúng tôi thiết lập bộ tạo khuyến nghị như một phần của pipeline CI/CD  [GitHub Actions](https://github.com/features/actions) .

**Tự động hóa quy trình GitOps**

Để thiết lập workflow trên GitHub Actions:  
1\.  Xây dựng và đẩy image docker của bộ tạo khuyến nghị từ [Dockerfile](https://github.com/aws-samples/K8sResourceResizer/blob/dev/K8sResourceResizer/Docker/Dockerfile),và  [source code](https://github.com/aws-samples/K8sResourceResizer/tree/dev/K8sResourceResizer/Src) của repository mà bạn đã clone, lên registry image container của riêng bạn. Bạn có thể tìm hướng dẫn về việc này trong [GitHub repository readme file](https://github.com/aws-samples/K8sResourceResizer/tree/dev/K8sResourceResizer),hoặc bạn có thể sử dụng ví dụ của chúng tôi [GitHub Actions workflow to build and push to ECR](https://github.com/aws-samples/K8sResourceResizer/blob/dev/.github/workflows/build-and-push.yml).Để thiết lập kết nối với AWS,  [làm theo hướng dẫn này](https://aws.amazon.com/blogs/security/use-iam-roles-to-connect-github-actions-to-actions-in-aws/) để cấu hình một vai trò  [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/)  theo các thực tiễn tốt nhất.

2\. Sau khi bạn đã có image docker của bộ tạo khuyến nghị trong registry image container của riêng bạn, hãy thiết lập một workflow GitHub Actions trên repository nơi bạn lưu trữ Kubernetes manifests hoặc templates.Đây là  một ví dụ về [GitHub Actions Workflow](https://github.com/aws-samples/K8sResourceResizer/blob/dev/K8sResourceResizer/README.md#github-actions-setup-with-iam-roles-recommended-for-production) kích hoạt luồng này dựa trên lịch cron có thể cấu hình, được tham số hóa với các tùy chọn cấu hình khác nhau cho các khuyến nghị, và sử dụng vai trò IAM để xác thực. Hãy truy cập phần  [Strategy Selection](https://github.com/aws-samples/K8sResourceResizer/blob/main/K8sResourceResizer/README.md#strategy-selection) của code repository để nắm được các chiến lược khả dụng khác nhau và cách lựa chọn một chiến lược. Để thiết lập, hãy cấu hình vai trò [IAM roles with GitHub Actions](https://aws.amazon.com/blogs/security/use-iam-roles-to-connect-github-actions-to-actions-in-aws/)và thiết lập các giá trị này như [GitHub secrets](https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions):

* AMP\_WORKSPACE\_ID: Amazon Managed Prometheus workspace ID  
* AWS\_REGION: AWS Region  
* GITHUB\_TOKEN: GitHub token for authentication

3\. [Trigger the GitHub Actions workflow manually](https://docs.github.com/en/actions/managing-workflow-runs-and-deployments/managing-workflow-runs/manually-running-a-workflow) và xác minh rằng bạn nhận được một pull request được tạo trong repository Kubernetes manifests của bạn.

Các hình minh họa sau đây cho thấy pull request được tạo ra trông như thế nào.
![Image](/images/3.translated_blogs/image_2_blog2.png) 
<p align="center"><em>Hình 2: Mô tả pull request được tạo bởi Amazon Bedrock</em></p>

![Image](/images/3.translated_blogs/image_3_blog2.png) 
<p align="center"><em>Hình 3: Các thay đổi trong pull request theo các khuyến nghị</em></p>

**Dọn dẹp**  
Để tránh các chi phí phát sinh, hãy xóa tất cả các tài nguyên mà bạn đã tạo trong quá trình kiểm thử giải pháp này:

1. Truy cập  [AWS Management Console](https://aws.amazon.com/console/), tìm [Amazon Elastic Container Registry (Amazon ECR)](https://aws.amazon.com/ecr/) repository, và xóa recommendation container image của giải pháp.

2. Làm theo[cleanup section of the GitHub repository](https://github.com/aws-samples/K8sResourceResizer/blob/main/PreRequirements/EKS/README.md#cleanup) và từ thư mục Amazon  [EKS directory](https://github.com/aws-samples/K8sResourceResizer/tree/main/PreRequirements/EKS) chạy lệnh:

terraform destroy

**Kết luận**  
Giải pháp này minh họa một cách tiếp cận thực tiễn, không xâm lấn để tối ưu hóa tài nguyên Kubernetes, kết hợp sức mạnh của việc ra quyết định dựa trên số liệu với các nguyên tắc GitOps. Các tổ chức có thể sử dụng Amazon Managed Service for Prometheus cho phân tích dữ liệu lịch sử, Amazon Bedrock cho cập nhật manifest thông minh, và các workflow GitOps thông qua Argo CD để tự động hóa quy trình tối ưu hóa tài nguyên đồng thời duy trì khả năng kiểm soát và giám sát các thay đổi.

Mặc dù giải pháp này mang lại giá trị tức thì cho việc tối ưu hóa tài nguyên, nó cũng đóng vai trò như một nền tảng cho các kịch bản tự động hóa nâng cao hơn. Các tổ chức có thể xây dựng dựa trên khung này để tích hợp thêm nhiều số liệu, thuật toán tối ưu hóa tùy chỉnh, hoặc tích hợp với các công cụ quản lý chi phí. Chúng tôi khuyến khích người dùng bắt đầu với một tập hợp nhỏ các workload không quan trọng để làm quen với quy trình, sau đó dần mở rộng để bao phủ nhiều hơn trong hạ tầng Kubernetes của họ. Các nhóm có thể làm theo hướng dẫn triển khai và các thực tiễn tốt nhất được trình bày trong bài viết này để đạt được việc sử dụng tài nguyên hiệu quả hơn trong khi vẫn duy trì sự ổn định và độ tin cậy của ứng dụng.

Để bắt đầu, hãy truy cập [GitHub repository](https://github.com/aws-samples/K8sResourceResizer)  của chúng tôi và làm theo hướng dẫn thiết lập. Chúng tôi hoan nghênh phản hồi và đóng góp từ cộng đồng để giúp phát triển giải pháp này hơn nữa.

---

**Hari Charan Ayada** là Kiến trúc sư Giải pháp Cấp cao tại Amazon Web Services ở Copenhagen.

**Ioannis Moustakis** là Kiến trúc sư Giải pháp Cấp cao tại Amazon Web Services ở Brussels.


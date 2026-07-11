---
title: "Bản đề xuất"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Pet Resort & Care System  
### Project Documentation

📄 **[Download Complete Project Proposal (Word Document)](#)**

---

### 1. Tổng Quan Hệ Thống

Dự án "Pet Resort & Care System" là một sản phẩm thử nghiệm (dạng MVP - Minimum Viable Product) được phát triển trong khuôn khổ dự án tốt nghiệp. Ứng dụng là một trang web kết hợp mua bán đồ thú cưng và đặt lịch spa.

Nhóm đã cố gắng áp dụng mô hình Kiến trúc 3 lớp (3-Tier Architecture) trên AWS để trải nghiệm việc triển khai ứng dụng thực tế. Dù đã thiết lập kiến trúc Multi-AZ, tự động mở rộng và các dịch vụ cơ bản của AWS, hệ thống hiện tại vẫn mang tính chất "học hỏi và thử nghiệm" là chính.

---

### 2. Kiến trúc giải pháp & Chi Tiết Các Lớp (Mức độ thử nghiệm)

Dưới đây là sơ đồ kiến trúc hệ thống mà nhóm đã phác thảo và triển khai sau khi được các mentor góp ý sửa lỗi luồng (flow) để đạt chuẩn High Availability (Độ sẵn sàng cao):

![Kiến trúc AWS Hệ thống Pet Resort](/images/2-Proposal/aws_architecture.jpg)

#### 2.1. Lớp Biên & Phân Phối (Edge Layer)
*   **AWS WAF & CloudFront:** Nhóm tích hợp WAF và CloudFront (CDN) để tăng tốc độ phân phối trang web tĩnh và chặn các luồng traffic độc hại. Sơ đồ sử dụng 2 Amazon S3 Bucket: một cho **Frontend** (chứa giao diện ReactJS) và một cho **Media** (chứa hình ảnh sản phẩm/thú cưng do người dùng upload).

#### 2.2. Lớp Mạng & Xử Lý Logic (Network & Compute Tier)
*   **ALB & EC2 (Auto Scaling Group):** Application Load Balancer nhận luồng dữ liệu và chia tải xuống các máy chủ EC2 đặt tại các Private Subnet thuộc 2 Availability Zones (AZ) khác nhau. Auto Scaling Group giúp hệ thống tự động sinh thêm máy khi có cảnh báo quá tải.
*   **2 NAT Gateways:** Để đảm bảo đúng chuẩn High Availability, nhóm thiết kế 2 NAT Gateway đặt ở 2 Public Subnet. Việc này giúp hệ thống không có điểm chết (Single Point of Failure), nếu 1 AZ sập thì các máy chủ backend ở AZ kia vẫn kết nối được ra Internet.

#### 2.3. Lớp Lưu Trữ Dữ Liệu (Data Tier)
*   **Amazon ElastiCache (Redis):** Nhóm tập tành cài đặt Redis theo mô hình **Primary - Replica** để lưu Session và tối ưu tốc độ đọc dữ liệu. Dữ liệu được đồng bộ (Sync Replication) giữa 2 AZ. 
*   **Amazon RDS (MySQL):** Hệ thống Database cũng được cấu hình **Multi-AZ (Primary - Standby)** để tự động failover khi có sự cố phần cứng từ phía AWS. Dữ liệu demo chưa nhiều nên chủ yếu setup để lấy kinh nghiệm quản trị Database trên cloud.

#### 2.4. Lớp Bảo Mật & Giám Sát (Security & Monitoring)
*   Nhóm không hardcode thông tin nhạy cảm vào code mà sử dụng **AWS Secrets Manager (SM)** và mã hóa bằng **KMS**. Quản lý quyền truy cập thông qua **IAM Role**.
*   Sử dụng **CloudWatch** để theo dõi logs/metrics và kết hợp **Amazon SNS** để tự động gửi Email cảnh báo cho quản trị viên khi CPU máy chủ quá tải.

#### 2.5. Tối Ưu Chi Phí (FinOps "Nhập môn")
*   **S3 Gateway Endpoint:** Đây là một điểm sáng trong thiết kế mà nhóm học được. Thay vì để máy chủ EC2 backend phải vòng qua NAT Gateway (tốn phí Data Transfer) để lấy ảnh/file từ S3, nhóm cấu hình S3 Gateway Endpoint giúp EC2 kết nối trực tiếp với S3 trong mạng nội bộ AWS, giúp giảm chi phí và tăng mật độ bảo mật.

---

### 3. Ước tính ngân sách (Bài toán "sống sót")
Với việc triển khai kiến trúc Multi-AZ hoàn chỉnh (2 NAT, DB Standby, Cache Replica), nhóm phải liên tục theo dõi để không bị "cháy túi". 

*Chi phí hạ tầng Ước tính (Monthly - Môi trường Demo)* 
- *Amazon EC2*: ~$15.00 USD (Máy chủ `t3.micro`).
- *Application Load Balancer*: ~$18.00 USD.
- *2 x NAT Gateway*: ~$65.00 USD (Phí duy trì giờ chạy rất cao).
- *Amazon RDS Multi-AZ*: ~$30.00 USD (`db.t3.micro`).
- *Amazon ElastiCache Multi-AZ*: ~$25.00 USD (`cache.t2.micro`).
- *Các dịch vụ khác (WAF, S3, CloudFront, Secrets Manager, SNS...)*: ~$15.00 USD.

*Tổng ngân sách*: **~$168.00 USD/tháng**. 
Dù đã cố gắng dùng các gói Free Tier và máy chủ cấu hình thấp nhất, đây vẫn là mức phí khá "đau ví" với sinh viên. Nhóm dự định ngay sau khi báo cáo nghiệm thu xong sẽ xóa bớt RDS Multi-AZ và NAT Gateway để tránh phát sinh hóa đơn.

---

### 4. Đánh giá rủi ro (Rất thực tế)
*   **Auto Scaling phản ứng chậm (Khả năng cao):** Nếu thầy cô hoặc hội đồng test spam request quá nhanh, EC2 sẽ quá tải trước khi Auto Scaling kịp sinh ra máy mới.
*   **Lỗi code Backend (Khả năng trung bình):** Logic xử lý đặt lịch spa (booking) thỉnh thoảng vẫn bị lỗi double-booking do xử lý khóa (lock) trong Database chưa thực sự triệt để.
*   **Vượt ngân sách (Khả năng cao):** Do sử dụng 2 NAT Gateway, nếu code bị lỗi loop request ra Internet, chi phí Data Transfer có thể tăng vọt trong thời gian ngắn.

---

### 5. Kết quả kỳ vọng & Bài học rút ra
*   **Sản phẩm:** Một trang web "chạy được", các luồng cơ bản (mua hàng, đặt lịch) có thể thao tác từ đầu đến cuối mà không văng lỗi 500.
*   **Kỹ năng đạt được:** 
    *   Hết "mù mờ" về Cloud: Nhóm đã tự tay cấu hình VPC, Subnet, Endpoint, Load Balancer thay vì chỉ học lý thuyết.
    *   Nếm mùi "đau thương": Hiểu được việc debug code chạy trên Local rất dễ, nhưng khi vứt lên Cloud (EC2) mà giấu sau Private Subnet thì tìm lỗi qua CloudWatch Logs khó khăn như thế nào.
    *   Kiến trúc này là bước đệm cực kỳ giá trị để nhóm định hình được một hệ thống thực tế cần những mảnh ghép gì để có thể tồn tại trên Internet.
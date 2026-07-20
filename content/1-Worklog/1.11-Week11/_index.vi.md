---
title: "Tuần 11"
weight: 11
chapter: false
pre: "<b>11. </b>"
---


## Mục tiêu tuần 11

- Triển khai Pet Resort & Care System lên môi trường AWS.
- Hoàn thiện kết nối giữa Frontend và Backend.
- Kiểm tra hệ thống sau khi triển khai và xử lý các lỗi phát sinh.

---

## Các công việc cần triển khai trong tuần này

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|------|-----------|--------------|-----------------|----------------|
| **2** | - Chuẩn bị môi trường triển khai Backend trên Amazon EC2.<br>- Build ứng dụng Spring Boot thành file `.jar`, cài đặt Java và cập nhật các biến môi trường cần thiết trên máy chủ. | 29/06/2026 | 29/06/2026 | AWS Documentation (EC2) |
| **3** | - Khởi tạo Amazon RDS MySQL và cập nhật thông tin kết nối trong Backend.<br>- Thiết lập Security Group cho EC2 và RDS, kiểm tra khả năng truy cập cơ sở dữ liệu từ ứng dụng. | 30/06/2026 | 30/06/2026 | AWS Documentation (RDS) |
| **4** | - Cấu hình Application Load Balancer và Target Group cho Backend.<br>- Kiểm tra Health Check, điều chỉnh cổng dịch vụ và xác nhận ứng dụng hoạt động thông qua ALB. | 01/07/2026 | 01/07/2026 | AWS Documentation (ALB) |
| **5** | - Triển khai Frontend ReactJS lên Amazon S3.<br>- Thiết lập Amazon CloudFront để phân phối giao diện và các tài nguyên tĩnh của hệ thống. | 02/07/2026 | 03/07/2026 | AWS Documentation (S3, CloudFront) |
| **7** | - Kiểm tra kết nối giữa Frontend và Backend trên môi trường AWS.<br>- Khắc phục các lỗi liên quan đến CORS, API Endpoint, đường dẫn hình ảnh và xác nhận các chức năng chính của hệ thống hoạt động ổn định. | 04/07/2026 | 04/07/2026 | Project Documentation |

---

## Kết quả đạt được tuần 11

- Hoàn thành triển khai Backend Spring Boot lên Amazon EC2 và kết nối thành công với cơ sở dữ liệu Amazon RDS MySQL.

- Thiết lập Security Group, Target Group và Application Load Balancer để hệ thống có thể tiếp nhận và xử lý các yêu cầu từ người dùng.

- Hoàn thành triển khai Frontend ReactJS lên Amazon S3 và cấu hình Amazon CloudFront để phân phối giao diện và các tài nguyên tĩnh.

- Kiểm tra quá trình giao tiếp giữa Frontend và Backend, xác nhận các API đăng nhập, quản lý thú cưng, quản lý dịch vụ và đặt lịch hoạt động đúng trên môi trường AWS.

- Khắc phục các lỗi phát sinh trong quá trình triển khai như cấu hình CORS, API Endpoint, Security Group, Health Check của Target Group và đường dẫn truy cập tài nguyên.

- Hoàn thiện môi trường triển khai của Pet Resort & Care System, tạo nền tảng cho quá trình kiểm thử, tối ưu và hoàn thiện báo cáo thực tập ở tuần tiếp theo.
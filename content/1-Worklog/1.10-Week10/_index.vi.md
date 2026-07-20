---
title: "Worklog Tuần 10"
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---


## Mục tiêu tuần 10

- Tích hợp Frontend với Backend đã triển khai trên AWS.
- Cấu hình Amazon CloudFront để phân phối nội dung.
- Kiểm thử các API sau khi tích hợp.
- Phân tích log và xử lý các lỗi phát sinh trong quá trình vận hành.

## Nhiệm vụ thực hiện trong tuần

| Ngày | Nhiệm vụ chi tiết | Ngày bắt đầu | Ngày kết thúc | Tài liệu tham khảo |
|------|-------------------|--------------|---------------|--------------------|
| 1 | Cập nhật địa chỉ API của Backend trên Frontend và kiểm tra kết nối giữa hai thành phần của hệ thống. | 22/06/2026 | 22/06/2026 | AWS EC2 Documentation |
| 2 | Kiểm thử các chức năng chính của Pet Resort & Care System như đăng nhập, quản lý thú cưng, đặt lịch và sử dụng dịch vụ sau khi tích hợp Frontend và Backend. | 23/06/2026 | 23/06/2026 | Spring Boot REST Documentation |
| 3 | Tìm hiểu và cấu hình Amazon CloudFront để phân phối nội dung tĩnh và tối ưu tốc độ truy cập ứng dụng. | 24/06/2026 | 24/06/2026 | Amazon CloudFront Documentation |
| 4 | Kiểm tra log của ứng dụng, xác định nguyên nhân các lỗi phát sinh trong quá trình tích hợp và điều chỉnh cấu hình nếu cần. | 25/06/2026 | 25/06/2026 | Amazon CloudWatch Documentation |
| 5 | Kiểm thử lại toàn bộ hệ thống sau khi khắc phục lỗi; kiểm tra khả năng truy cập và phản hồi của các API trên môi trường AWS. | 26/06/2026 | 26/06/2026 | AWS Well-Architected Framework |

## Kết quả đạt được tuần 10

- **Tích hợp Frontend và Backend:**
  - Kết nối thành công Frontend với Backend đang chạy trên Amazon EC2.
  - Kiểm tra hoạt động của các API sau khi tích hợp.
  - Đảm bảo dữ liệu được trao đổi chính xác giữa giao diện và hệ thống Backend.

- **Triển khai và tối ưu truy cập:**
  - Cấu hình Amazon CloudFront để phân phối nội dung.
  - Kiểm tra khả năng truy cập ứng dụng thông qua CloudFront.
  - Đánh giá tốc độ phản hồi của hệ thống sau khi cấu hình.

- **Kiểm thử và xử lý lỗi:**
  - Kiểm thử các chức năng chính của hệ thống.
  - Phân tích log để xác định và khắc phục một số lỗi phát sinh.
  - Cập nhật cấu hình nhằm nâng cao tính ổn định của ứng dụng.
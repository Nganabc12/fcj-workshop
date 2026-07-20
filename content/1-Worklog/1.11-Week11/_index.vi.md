---
title: "Nhật ký công việc Tuần 11"
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---



### Mục tiêu tuần 11

- Kiểm thử tổng thể các chức năng của Pet Resort & Care System sau khi hoàn thiện tích hợp.
- Theo dõi trạng thái hoạt động và mức sử dụng tài nguyên bằng Amazon CloudWatch.
- Phân tích các chỉ số hệ thống để xác định những vấn đề ảnh hưởng đến hiệu năng.
- Thiết lập AWS Budgets nhằm theo dõi và kiểm soát chi phí sử dụng dịch vụ AWS.
- Phát hiện, khắc phục các lỗi còn tồn tại và nâng cao tính ổn định của hệ thống.

### Nhiệm vụ thực hiện trong tuần

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày kết thúc | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | Xây dựng danh sách kiểm thử và tiến hành kiểm tra các chức năng chính của hệ thống như đăng nhập, quản lý thông tin thú cưng, đặt lịch dịch vụ và quản lý dữ liệu. | 29/06/2026 | 29/06/2026 | Kế hoạch kiểm thử hệ thống |
| 2 | Kiểm tra luồng dữ liệu giữa giao diện người dùng, ứng dụng Spring Boot và Amazon RDS; ghi nhận các lỗi về kết nối, xử lý dữ liệu và hiển thị kết quả. | 30/06/2026 | 30/06/2026 | Tài liệu dự án |
| 3 | Theo dõi các chỉ số hoạt động của tài nguyên AWS bằng Amazon CloudWatch, kiểm tra mức sử dụng CPU, trạng thái dịch vụ, log ứng dụng và các thông tin liên quan đến lỗi hệ thống. | 01/07/2026 | 01/07/2026 | Amazon CloudWatch Documentation |
| 4 | Rà soát các truy vấn dữ liệu, thời gian phản hồi của ứng dụng và cấu hình triển khai; điều chỉnh một số thiết lập nhằm cải thiện hiệu năng và độ ổn định. | 02/07/2026 | 02/07/2026 | AWS Well-Architected Framework |
| 5 | Thiết lập AWS Budgets để theo dõi chi phí sử dụng tài nguyên, cấu hình ngưỡng cảnh báo và kiểm tra các dịch vụ có khả năng phát sinh chi phí không cần thiết. | 03/07/2026 | 03/07/2026 | AWS Budgets User Guide |

### Tổng kết tuần

Trong tuần 11, tôi tập trung kiểm thử tổng thể **Pet Resort & Care System** sau khi hoàn thiện quá trình tích hợp và cấu hình kiến trúc triển khai. Tôi xây dựng danh sách các chức năng cần kiểm tra, thực hiện kiểm thử từng luồng nghiệp vụ và đánh giá khả năng giao tiếp giữa giao diện người dùng, ứng dụng Spring Boot và cơ sở dữ liệu Amazon RDS.

Quá trình kiểm thử giúp tôi phát hiện một số vấn đề liên quan đến kết nối, xử lý dữ liệu, thời gian phản hồi và cấu hình môi trường. Tôi tiến hành kiểm tra nguyên nhân, điều chỉnh các thiết lập chưa phù hợp và thực hiện kiểm thử lại để đảm bảo các chức năng hoạt động đúng theo yêu cầu.

Bên cạnh việc kiểm thử, tôi sử dụng **Amazon CloudWatch** để theo dõi trạng thái tài nguyên, mức sử dụng CPU, log ứng dụng và các thông tin lỗi trong quá trình hệ thống hoạt động. Việc phân tích các chỉ số và nhật ký giúp tôi hiểu rõ hơn tình trạng vận hành của ứng dụng, đồng thời hỗ trợ xác định nhanh các vấn đề có thể ảnh hưởng đến hiệu năng và tính ổn định.

Tôi cũng thực hiện rà soát cấu hình triển khai, truy vấn cơ sở dữ liệu và thời gian phản hồi của hệ thống. Một số thiết lập được điều chỉnh để hạn chế việc sử dụng tài nguyên không cần thiết, cải thiện khả năng xử lý yêu cầu và giúp hệ thống vận hành ổn định hơn.

Ngoài ra, tôi thiết lập **AWS Budgets** để theo dõi chi phí sử dụng các dịch vụ AWS và cấu hình ngưỡng cảnh báo ngân sách. Qua đó, tôi có thể kiểm soát tốt hơn các tài nguyên đang sử dụng, phát hiện những dịch vụ có khả năng phát sinh chi phí và chủ động điều chỉnh khi cần thiết.

Kết thúc tuần 11, hệ thống đã được kiểm tra tương đối đầy đủ, các lỗi chính được khắc phục và cấu hình vận hành được tối ưu thêm. Thông qua các công việc trong tuần, tôi nâng cao kỹ năng kiểm thử hệ thống, phân tích log, giám sát tài nguyên bằng Amazon CloudWatch, quản lý chi phí với AWS Budgets, tối ưu hiệu năng và xử lý sự cố trong môi trường điện toán đám mây.
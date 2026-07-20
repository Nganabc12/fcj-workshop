---
title: "Blog 3: Hệ thống tệp S3 Files"
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Khám phá S3 Files: Biến Amazon S3 Bucket thành hệ thống tệp cục bộ trên AWS

## Thông tin bài viết gốc

| Mục | Nội dung |
|-----|----------|
| **Tiêu đề bài viết** | Launching S3 Files: Making S3 Buckets Accessible as File Systems |
| **Tác giả** | Antje Barth |
| **Ngày đăng** | 25/06/2026 |
| **Nguồn bài viết** | https://aws.amazon.com/blogs/aws/launching-s3-files-making-s3-buckets-accessible-as-file-systems/ |
| **Người dịch** | Hồ Đình Vinh |
| **Ngày đăng bản dịch** | 28/06/2026 |
| **Bài viết đã dịch** | https://www.facebook.com/share/p/14htFzwDeXv/ |

---

## Giới thiệu

Trong quá trình tìm hiểu các giải pháp lưu trữ dữ liệu trên AWS, tôi đã đọc được một bài viết giới thiệu về **S3 Files** – một tính năng mới cho phép người dùng truy cập trực tiếp các **Amazon S3 Bucket** như một hệ thống tệp (File System) quen thuộc trên máy tính hoặc máy chủ.

Thông thường, để làm việc với Amazon S3, các ứng dụng cần sử dụng AWS SDK hoặc gọi trực tiếp các API như `PutObject`, `GetObject` hay `ListObjects`. Điều này khiến nhiều ứng dụng cũ (Legacy Applications) hoặc các phần mềm chỉ hỗ trợ thao tác với tệp cục bộ gặp nhiều khó khăn khi chuyển sang sử dụng S3.

Với **S3 Files**, AWS đã giải quyết vấn đề này bằng cách cung cấp một lớp trung gian giúp chuyển đổi các thao tác đọc và ghi tệp thông thường thành các lời gọi API đến Amazon S3 một cách tự động. Nhờ đó, các ứng dụng có thể tiếp tục hoạt động như đang sử dụng ổ đĩa cục bộ mà không cần chỉnh sửa hoặc viết lại mã nguồn.

Trong bài viết này, tôi tổng hợp và dịch lại những nội dung chính từ bài viết gốc của AWS, bao gồm nguyên lý hoạt động của S3 Files, kiến trúc triển khai, các thành phần AWS liên quan cũng như những lợi ích mà giải pháp này mang lại đối với các hệ thống Big Data, AI/ML và các ứng dụng doanh nghiệp.

---

> **Lưu ý:** Bài viết này được dịch và tổng hợp từ bài viết gốc trên **AWS News Blog** nhằm phục vụ mục đích học tập và nghiên cứu. Mọi bản quyền nội dung thuộc về tác giả và Amazon Web Services (AWS).

## Bài toán đặt ra

**Amazon S3** là một kho lưu trữ đối tượng (Object Storage) tuyệt vời với dung lượng không giới hạn và chi phí rẻ[cite: 5]. Tuy nhiên, S3 không phải là một hệ thống tệp (File System) truyền thống[cite: 5]. 

Nhiều ứng dụng cũ (Legacy Apps), công cụ phân tích dữ liệu hoặc các đoạn script tự động hóa được thiết kế chỉ để đọc/ghi tệp cục bộ (*POSIX file interface*)[cite: 5]. Để các ứng dụng này chạy được với S3, các lập trình viên thường phải:
* Sửa đổi lại toàn bộ mã nguồn để tích hợp API của S3[cite: 5].
* Tốn chi phí cho các dịch vụ trung gian như AWS Storage Gateway[cite: 5]. 

Điều này gây tốn thời gian, chi phí và làm phức tạp hóa kiến trúc hệ thống[cite: 5].

---

## Cách tiếp cận của AWS

Để giải quyết bài toán này một cách tối ưu, AWS đã cho ra mắt **S3 Files** (dựa trên công nghệ mã nguồn mở *Mountpoint for Amazon S3*)[cite: 5].

Khi tính năng này được kích hoạt, AWS sẽ tạo ra một "cây cầu" dịch thuật tự động: Ứng dụng của bạn cứ ghi tệp vào thư mục như bình thường, còn S3 Files sẽ âm thầm chuyển đổi các lệnh đó thành API `GetObject` hoặc `PutObject` để đẩy thẳng lên S3 Bucket[cite: 5]. Nhờ đó, bạn vừa tận dụng được giao diện tệp quen thuộc, vừa hưởng trọn lợi thế về dung lượng khổng lồ và độ bền dữ liệu của Amazon S3[cite: 5].

---

## Các dịch vụ và thành phần AWS được sử dụng

Kiến trúc vận hành của tính năng này xoay quanh các thành phần cốt lõi[cite: 5]:

| Thành phần AWS | Vai trò trong hệ thống |
| :--- | :--- |
| **Amazon S3** | Đóng vai trò là kho lưu trữ gốc, chứa toàn bộ dữ liệu đối tượng (Simple Storage Service) ở phía sau[cite: 5]. |
| **Mountpoint for Amazon S3** | Trình dịch mã nguồn mở (S3 Files Client) được cài đặt trên các máy chủ tính toán, chịu trách nhiệm chuyển đổi các lệnh tệp (POSIX) thành lời gọi API S3[cite: 5]. |
| **Amazon EC2 / AWS Fargate** | Các môi trường máy chủ hoặc container chạy ứng dụng thực tế – nơi thư mục S3 được gắn vào để sử dụng[cite: 5]. |
| **AWS IAM** | Kiểm soát và phân quyền bảo mật (Identity and Access Management), đảm bảo máy chủ chỉ có quyền đọc/ghi đúng các thư mục được phép trên S3[cite: 5]. |

Sự kết hợp này giúp hệ thống hoạt động với hiệu suất cực cao (High throughput), giảm thiểu độ trễ khi xử lý dữ liệu lớn mà không cần quản lý phần cứng lưu trữ phức tạp[cite: 5].

> *Hình 1. Kiến trúc tổng quan mô tả các EC2 Instances kết nối qua cổng TCP 2049 (NFS) đến S3 Files Mount Target để đọc/ghi trực tiếp vào S3 Bucket.*

![Kiến trúc tổng quan các EC2 Instances kết nối qua cổng TCP 2049 (NFS) đến S3 Files Mount Target](/images/3-BlogsTranslated/blog3-1.png)

---

## Trải nghiệm thiết lập thực tế trên AWS Console

Việc thiết lập S3 Files giờ đây cực kỳ trực quan thông qua giao diện quản lý của AWS:

1. **Khởi tạo File System:** Người dùng có thể bắt đầu tạo hệ thống tệp trực tiếp từ giao diện Amazon S3 thông qua các bước Create, Mount và Access.
> *Hình 2. Giao diện "Getting started with S3 Files" trên AWS Console hướng dẫn 3 bước thiết lập cơ bản.*

2. **Cấu hình Mount Targets:** Đây là các điểm cuối mạng nội bộ nằm trong các Availability Zone (AZ) của Virtual Private Cloud (VPC).
> *Hình 3. Giao diện quản lý Mount targets hiển thị danh sách các IP nội bộ và trạng thái kết nối "Available" cho phép các tài nguyên tính toán truy cập hệ thống tệp.*

![Giao diện quản lý Mount targets hiển thị danh sách các IP nội bộ và trạng thái kết nối Available](/images/3-BlogsTranslated/blog3-2.png)

---

## Điều mình học được

Qua bài viết, mình hiểu rõ hơn cách AWS xóa nhòa ranh giới giữa *Object Storage* và *File Storage*[cite: 5].

Điểm thú vị nhất là cơ chế tối ưu hiệu suất của Mountpoint cho các tác vụ đọc/ghi tuần tự quy mô lớn (như dữ liệu Machine Learning, xử lý Video, Big Data)[cite: 5]. Thay vì cố gắng giả lập 100% tất cả các tính năng phức tạp của hệ thống tệp (điều dễ gây thắt nút cổ chai), AWS tập trung tối ưu hóa các lệnh cơ bản nhất (Đọc, Ghi, Liệt kê) để đạt tốc độ truyền tải dữ liệu tối đa ra vào S3[cite: 5].

## Kết luận

Tính năng **S3 Files** là một bước đi thực tế và vô cùng giá trị của AWS nhằm đơn giản hóa việc dịch chuyển ứng dụng lên đám mây[cite: 5]. Bằng cách biến S3 thành một hệ thống tệp cục bộ một cách miễn phí và hiệu suất cao, AWS đã giúp các kỹ sư tiết kiệm hàng tuần liền viết code cấu hình[cite: 5].

Đây là một giải pháp rất đáng tham khảo cho các dự án xử lý dữ liệu lớn, các hệ thống chạy AI/ML cần nạp dữ liệu liên tục từ S3, hoặc bất kỳ hệ thống lưu trữ hóa đơn, hình ảnh nào muốn tối ưu chi phí vận hành mà không muốn sửa đổi mã nguồn backend phức tạp[cite: 5].

* **Nguồn tham khảo gốc:** [AWS News Blog - Launching S3 Files](https://aws.amazon.com/vi/blogs/aws/launching-s3-files-making-s3-buckets-accessible-as-file-systems/)[cite: 5]
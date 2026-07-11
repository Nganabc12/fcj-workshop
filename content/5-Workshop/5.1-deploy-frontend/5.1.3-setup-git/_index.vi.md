---
title: "Thiết lập Git Repository"
weight: 3
chapter: false
pre: " <b> 5.1.3 </b> "
---

# Thiết lập Git Repository

Trong bước này, chúng ta sẽ thiết lập mã nguồn giao diện (Frontend) của hệ thống Pet Resort & Care System và đẩy code lên GitHub.

## 1. Chuẩn bị mã nguồn trên GitHub

Dự án của nhóm sử dụng GitHub để quản lý mã nguồn. Bạn có thể sử dụng trực tiếp Repository của nhóm tại đây:

- **Link Repository**: [https://github.com/wuys-fan/web-dog-cat.git](https://github.com/wuys-fan/web-dog-cat.git)

Nếu bạn muốn tạo một bản sao để tự thực hành triển khai, hãy làm theo các bước sau:

1. Đăng nhập vào GitHub.
2. Truy cập vào link Repository ở trên.
3. Click vào nút **Fork** (góc phải trên cùng) để tạo một bản sao về tài khoản cá nhân của bạn.
4. Đảm bảo **Visibility** của repository đang để là **Public** hoặc **Private** tùy nhu cầu của bạn.

![Cấu trúc Repository trên GitHub](/images/1-Worklog/github_repository.png)

## 2. Clone code về máy tính (Local)

Mở Terminal (hoặc Git Bash/Command Prompt) trên máy tính của bạn và chạy lệnh sau để tải code về:

```bash
git clone [https://github.com/wuys-fan/web-dog-cat.git](https://github.com/wuys-fan/web-dog-cat.git)
cd web-dog-cat/frontend
```

Cài đặt các gói thư viện cần thiết cho ReactJS:

```bash
npm install
```

---

## Bước tiếp theo

Tiếp tục với [Deploy Frontend lên S3 & CloudFront](../5.1.4-deploy-frontend/) để đưa giao diện ứng dụng lên AWS.
---
title: "Yêu cầu trước khi bắt đầu"
weight: 2
chapter: false
pre: " <b> 5.1.2 </b> "
---

# Yêu cầu trước khi bắt đầu

Trước khi bắt đầu triển khai hạ tầng cho **Pet Resort & Care System**, hãy đảm bảo bạn đã chuẩn bị đầy đủ các yêu cầu sau để tránh phát sinh chi phí ngoài ý muốn.

## 1. Tài khoản AWS

### 1.1 Thiết lập cảnh báo Billing (Chi phí)

1. Đăng nhập **AWS Console**: [https://console.aws.amazon.com](https://console.aws.amazon.com)
2. Click vào tên tài khoản (góc phải trên) → Chọn **Billing Dashboard**
3. Ở thanh menu bên trái, chọn **Billing Preferences**
4. Đánh dấu tích bật các tùy chọn:
   - **Receive Free Tier Usage Alerts** (Nhận cảnh báo khi sắp hết Free Tier)
   - **Receive Billing Alerts** (Nhận cảnh báo chi phí)
5. Click **Save preferences**

### 1.2 Tạo CloudWatch Billing Alarm (Ngân sách)

1. Trong **Billing Dashboard**, click chọn **Budgets** ở thanh bên trái
2. Click **Create budget**
3. Chọn **Cost budget - Recommended**
4. Cấu hình các thông số:
   - Budget name: `Pet-Resort-Budget`
   - Budgeted amount: `$5.00` (Hoặc mức ngân sách bạn mong muốn)
   - Budget scope: All AWS services
5. Click **Create budget**

---

## 2. AWS CLI (Khuyến nghị cài đặt)

Việc cài đặt AWS CLI sẽ giúp bạn dễ dàng tương tác với các dịch vụ như S3 hoặc cấu hình EC2 từ máy tính cá nhân.

### 2.1 Cài đặt AWS CLI

#### Windows:
Mở Command Prompt hoặc PowerShell và chạy lệnh sau:
```bash
msiexec.exe /i [https://awscli.amazonaws.com/AWSCLIV2.msi](https://awscli.amazonaws.com/AWSCLIV2.msi)
```

#### macOS (sử dụng pkg):
```bash
curl "[https://awscli.amazonaws.com/AWSCLIV2.pkg](https://awscli.amazonaws.com/AWSCLIV2.pkg)" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /
```

### 2.2 Cấu hình AWS CLI

Mở terminal và gõ lệnh:
```bash
aws configure
```

Nhập các thông tin sau (Lấy từ phần Security Credentials trong AWS):
- AWS Access Key ID: `(Nhập Access Key của bạn)`
- AWS Secret Access Key: `(Nhập Secret Key của bạn)`
- Default region name: `ap-southeast-1` (Khu vực Singapore)
- Default output format: `json`

---

## Bước tiếp theo

Tiếp tục với [Thiết lập Mạng (VPC & Subnets)](#) để bắt đầu xây dựng lớp bảo vệ ngoài cùng cho hệ thống.
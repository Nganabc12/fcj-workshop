---
title: "Deploy Frontend với S3 & CloudFront"
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---

# Deploy ReactJS Frontend với S3 & CloudFront

#### Tổng quan

Trong workshop này, bạn sẽ học cách triển khai ứng dụng ReactJS cho hệ thống **Pet Resort & Care** bằng cách sử dụng **Amazon S3** để lưu trữ file tĩnh và **Amazon CloudFront** làm CDN phân phối nội dung toàn cầu. Tùy chọn tích hợp thêm **AWS WAF** để bảo vệ hệ thống.

Phương pháp này giúp bạn kiểm soát hoàn toàn việc hosting với chi phí cực kỳ tiết kiệm cho các ứng dụng web tĩnh (SPA):
- 🚀 Static Website Hosting trên Amazon S3
- 🔒 HTTPS thông qua CloudFront với chứng chỉ SSL miễn phí
- 🌍 CDN toàn cầu giúp tải trang cực nhanh
- 💰 Chi phí rất thấp (~$0/tháng trong giới hạn Free Tier)

#### Kiến trúc

```
GitHub Repository → npm run build → S3 Bucket → CloudFront CDN → Users
     ↓ (mã nguồn)       ↓ (file tĩnh)    ↓ (hosting)    ↓ (phân phối)
```

#### Nội dung

1. [Tổng quan Workshop](5.1.1-overview/)
2. [Yêu cầu trước khi bắt đầu](5.1.2-prerequisites/)
3. [Thiết lập Git Repository](5.1.3-setup-git/)
4. [Deploy lên S3 & CloudFront](5.1.4-deploy-frontend/)
5. [Kiểm tra và xác minh](5.1.5-testing/)

#### Thời gian hoàn thành
⏱️ Khoảng **45-60 phút**

#### Yêu cầu
- ✅ AWS Account (Free Tier eligible)
- ✅ Tài khoản GitHub
- ✅ Node.js 18+ và npm
- ✅ Git đã cài đặt
- ✅ Code editor (khuyến nghị VS Code)

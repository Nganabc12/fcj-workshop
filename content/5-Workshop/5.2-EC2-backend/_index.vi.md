---
title: "Deploy Java Spring Boot Backend trên Amazon EC2"
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

# Deploy Java Spring Boot Backend trên Amazon EC2

#### Tổng quan

Trong workshop này, bạn sẽ học cách triển khai **Java Spring Boot RESTful API** cho hệ thống **Pet Resort & Care** trực tiếp lên **Amazon EC2**. Ứng dụng kết nối với **Amazon RDS (MySQL)** để lưu trữ dữ liệu, sử dụng **Amazon ElastiCache (Redis)** để tăng tốc truy vấn, và lưu lượng truy cập được điều phối qua **Application Load Balancer (ALB)**.

#### Nội dung

1. [Tổng quan Workshop](5.2.1-overview/)
2. [Đóng gói ứng dụng (.jar)](5.2.2-publish-app/)
3. [Deploy lên Amazon EC2 & ALB](5.2.3-deploy-ec2/)
4. [Kiểm tra & Tích hợp](5.2.4-testing/)

#### Thời gian hoàn thành
⏱️ Khoảng **60-90 phút**

#### Yêu cầu
- ✅ AWS Account (Free Tier eligible)
- ✅ Java JDK 17 trở lên
- ✅ Apache Maven đã cài đặt
- ✅ Git đã cài đặt
- ✅ Code editor (VS Code hoặc IntelliJ IDEA)
- ✅ Đã hoàn thành Workshop 5.1 (Frontend đã deploy)

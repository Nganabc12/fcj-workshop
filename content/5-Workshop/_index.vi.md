---
title: "Workshop"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Pet Resort & Care - AWS Workshop Series

Các workshop thực hành xây dựng hệ thống Pet Resort & Care System trên nền tảng điện toán đám mây AWS.

## 🎯 Tổng quan Workshop

Trong series workshop này, bạn sẽ học cách đưa một ứng dụng web full-stack thực tế lên AWS. Ứng dụng bao gồm giao diện Frontend xây dựng bằng ReactJS và Backend API bằng Java Spring Boot, sử dụng kiến trúc phân lớp cơ bản nhưng đáp ứng tốt chuẩn triển khai thực tế.

**Pet Resort & Care System** là nền tảng đặt lịch và chăm sóc thú cưng với các tính năng:
- 🛒 Hiển thị danh mục sản phẩm và dịch vụ Spa cho thú cưng
- 📅 Đặt lịch hẹn và quản lý giỏ hàng
- 👥 Hệ thống phân quyền cơ bản: Khách hàng, Nhân viên, Admin
- 🖼️ Lưu trữ và quản lý hình ảnh an toàn trên Cloud

---

## 📚 Series Workshop

### Workshop Cốt lõi

#### 1. [Deploy ReactJS Frontend với S3 & CloudFront](5.1-deploy-frontend/)
⏱️ **45 - 60 phút** | 🎯 **Beginner-Intermediate**

Tối ưu chi phí bằng cách đóng gói ReactJS thành các file tĩnh và lưu trữ trên Amazon S3, sau đó phân phối qua mạng nội dung CloudFront (CDN) để web tải nhanh hơn.

**Bạn sẽ thực hành:**
- Build mã nguồn ReactJS (Vite)
- Thiết lập S3 Bucket làm Static Website
- Cấu hình CloudFront CDN và HTTPS
- Tích hợp GitHub Actions để tự động cập nhật code (CI/CD cơ bản)

---

#### 2. [Deploy Java Spring Boot Backend trên Amazon EC2](5.2-ec2-backend/)
⏱️ **60 - 90 phút** | 🎯 **Intermediate**

Triển khai mã nguồn Backend lên máy chủ ảo EC2, kết nối với cơ sở dữ liệu quan hệ và thiết lập Load Balancer để điều phối traffic.

**Bạn sẽ thực hành:**
- Cấu hình mạng VPC cơ bản và Security Group
- Khởi tạo Database với Amazon RDS (MySQL)
- Tăng tốc độ truy vấn với ElastiCache (Redis)
- Deploy file `.jar` Spring Boot lên Amazon EC2
- Cấu hình Application Load Balancer (ALB) để kết nối với Frontend

---

#### 3. [Video Demo & Tài liệu Tham khảo](5.3-demo/)
⏱️ **5 - 10 phút** | 🎯 **General**

Xem video chạy thử demo thực tế trên AWS và truy cập các liên kết tham khảo, tài liệu học tập của AWS.

---

## 📋 Yêu cầu Trước khi Bắt đầu

Trước khi thực hành, hãy đảm bảo bạn có:
- ✅ Tài khoản AWS (Nên dùng tài khoản đang trong gói Free Tier)
- ✅ Tài khoản GitHub
- ✅ Node.js 18+ và npm
- ✅ Java JDK 17 trở lên
- ✅ Git đã được cài đặt
- ✅ Code editor (VS Code hoặc IntelliJ IDEA)
- ✅ Hiểu biết cơ bản về ReactJS, Java và cách gõ lệnh Terminal

---

## 💰 Ước tính Chi phí

Bằng cách tận dụng tối đa gói **AWS Free Tier**, chi phí duy trì hệ thống cho mục đích học tập và làm dự án được tối ưu rất tốt:

| Dịch vụ | Mức Free Tier | Chi phí ước tính (Thực hành) |
|---------|-----------|---------------|
| **S3 & CloudFront** | 5GB Storage, 1TB Transfer | ~$0/tháng |
| **Amazon EC2** | 750 giờ/tháng (t3.micro) | ~$0/tháng |
| **Amazon RDS** | 750 giờ/tháng (t3.micro) | ~$0/tháng |
| **ElastiCache** | 750 giờ/tháng (t2.micro) | ~$0/tháng |
| **Load Balancer (ALB)** | Không có Free tier | ~$16 - $20/tháng |

**Tổng ước tính chi phí (Thực hành):** Khoảng **$15 - $25/tháng** (Chi phí chủ yếu đến từ việc duy trì Load Balancer. Nếu tắt Load Balancer khi không dùng, chi phí gần như bằng $0).

> **Lưu ý:** Kiến trúc đầy đủ Multi-AZ như mô tả trong [Proposal](../2-Proposal/) có chi phí khoảng **~$168/tháng** do 2 NAT Gateways, Multi-AZ RDS, và ElastiCache replicas. Môi trường thực hành của workshop sử dụng cấu hình đơn giản hơn để tiết kiệm chi phí.

---

## 🚀 Bắt đầu

Bắt đầu với [Workshop 1: Deploy Frontend với S3 & CloudFront](5.1-deploy-frontend/)

---

## 📖 Tài liệu Bổ sung

- [AWS Free Tier](https://aws.amazon.com/free/)
- [React Documentation](https://react.dev/)
- [Spring Boot Reference](https://spring.io/projects/spring-boot)
- [Tài liệu thiết kế hệ thống của nhóm](../2-Proposal/)
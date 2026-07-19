---
title: "Workshop"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Pet Resort & Care - AWS Workshop Series

Hands-on workshops to build and deploy the Pet Resort & Care System on the AWS Cloud platform.

## 🎯 Workshop Overview

In this workshop series, you will learn how to deploy a practical full-stack web application on AWS. The application consists of a ReactJS Frontend and a Java Spring Boot Backend, utilizing a standard layered architecture suitable for real-world deployments.

The **Pet Resort & Care System** is a pet care and booking platform featuring:
- 🛒 Display of pet products and Spa service catalogs
- 📅 Appointment booking and shopping cart management
- 👥 Basic role-based access control: Customer, Staff, Admin
- 🖼️ Secure image storage and management in the Cloud

---

## 📚 Workshop Series

### Core Workshops

#### 1. [Deploy ReactJS Frontend with S3 & CloudFront](5.1-deploy-frontend/)
⏱️ **45 - 60 minutes** | 🎯 **Beginner-Intermediate**

Optimize costs by building the ReactJS app into static files and hosting them on Amazon S3, then distributing them via CloudFront (CDN) for faster load times.

**You will learn:**
- Build the ReactJS source code (Vite)
- Set up an S3 Bucket for Static Website Hosting
- Configure CloudFront CDN and HTTPS
- Integrate GitHub Actions for automated deployment (Basic CI/CD)

---

#### 2. [Deploy Java Spring Boot Backend on Amazon EC2](5.2-ec2-backend/)
⏱️ **60 - 90 minutes** | 🎯 **Intermediate**

Deploy the backend code to EC2 virtual servers, connect to a relational database, and set up a Load Balancer to route traffic.

**You will learn:**
- Configure basic VPC networking and Security Groups
- Provision a Database using Amazon RDS (MySQL)
- Accelerate query speeds with ElastiCache (Redis)
- Deploy the Spring Boot `.jar` file to Amazon EC2
- Configure an Application Load Balancer (ALB) to connect with the Frontend

---

#### 3. [Video Demo & References](5.3-demo/)
⏱️ **5 - 10 minutes** | 🎯 **General**

Watch the live system demo running on AWS and access reference links and learning resources.

---

## 📋 Prerequisites

Before you begin, ensure you have the following:
- ✅ AWS Account (Free Tier eligible account recommended)
- ✅ GitHub account
- ✅ Node.js 18+ and npm
- ✅ Java JDK 17 or higher
- ✅ Git installed
- ✅ Code editor (VS Code or IntelliJ IDEA)
- ✅ Basic knowledge of ReactJS, Java, and Terminal commands

---

## 💰 Cost Estimation

By maximizing the **AWS Free Tier**, the maintenance cost of this system for learning and project purposes is highly optimized:

| Service | Free Tier Limits | Estimated Cost (Practice) |
|---------|-----------|---------------|
| **S3 & CloudFront** | 5GB Storage, 1TB Transfer | ~$0/month |
| **Amazon EC2** | 750 hours/month (t3.micro) | ~$0/month |
| **Amazon RDS** | 750 hours/month (t3.micro) | ~$0/month |
| **ElastiCache** | 750 hours/month (t2.micro) | ~$0/month |
| **Load Balancer (ALB)** | No Free Tier | ~$16 - $20/month |

**Total Estimated Cost (Practice):** Approximately **$15 - $25/month** (The cost is primarily for maintaining the Load Balancer. If you delete the Load Balancer when not in use, the cost is close to $0).

> **Note:** The full Multi-AZ architecture described in the [Project Proposal](../2-Proposal/) costs approximately **~$168/month** due to 2 NAT Gateways, Multi-AZ RDS, and ElastiCache replicas. The workshop practice environment uses a simplified single-AZ setup to minimize costs.

---

## 🚀 Get Started

Start with [Workshop 1: Deploy Frontend with S3 & CloudFront](5.1-deploy-frontend/)

---

## 📖 Additional Resources

- [AWS Free Tier](https://aws.amazon.com/free/)
- [React Documentation](https://react.dev/)
- [Spring Boot Reference](https://spring.io/projects/spring-boot)
- [Project Proposal Document](../2-Proposal/)
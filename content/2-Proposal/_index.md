---
title: "Project Proposal"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Pet Resort & Care System  
### Project Documentation

📄 **[Download Complete Project Proposal (Word Document)](#)**

---

### 1. System Overview

The "Pet Resort & Care System" is a Minimum Viable Product (MVP) developed as part of a graduation project. The application is a web platform combining pet product e-commerce and a basic spa booking system.

Our team has applied the 3-Tier Architecture model on AWS to gain hands-on experience in real-world application deployment. Although we have established a Multi-AZ architecture, auto-scaling, and foundational AWS services, the current system is primarily intended for "learning and experimental" purposes.

---

### 2. Solution Architecture & Layer Details (Experimental Level)

Below is the system architecture diagram that our team sketched and deployed after receiving mentor feedback to fix the traffic flow and achieve High Availability standards:

![AWS Architecture Pet Resort System](/images/2-Proposal/aws_architecture.jpg)

#### 2.1. Edge & Delivery Layer
*   **AWS WAF & CloudFront:** We integrated WAF and CloudFront (CDN) to accelerate static content delivery and block malicious traffic. The architecture utilizes two Amazon S3 Buckets: one for the **Frontend** (hosting the ReactJS UI) and one for **Media** (storing product/pet images uploaded by users).

#### 2.2. Network & Compute Tier
*   **ALB & EC2 (Auto Scaling Group):** An Application Load Balancer receives incoming traffic and distributes it across EC2 instances located in Private Subnets across two different Availability Zones (AZs). The Auto Scaling Group ensures the system automatically provisions additional instances when overload alerts are triggered.
*   **2 NAT Gateways:** To meet High Availability standards, we deployed two NAT Gateways in two Public Subnets. This eliminates any Single Point of Failure; if one AZ goes down, the backend servers in the other AZ can still connect to the Internet.

#### 2.3. Data Tier
*   **Amazon ElastiCache (Redis):** We configured Redis in a **Primary - Replica** setup to store Sessions and optimize data read speeds. Data is synchronized (Sync Replication) between the two AZs.
*   **Amazon RDS (MySQL):** The database system is also configured for **Multi-AZ (Primary - Standby)** to enable automatic failover in case of AWS hardware issues. Since the demo data is small, this setup is primarily to gain cloud database administration experience.

#### 2.4. Security & Monitoring Layer
*   We avoided hardcoding sensitive information by utilizing **AWS Secrets Manager (SM)** and encrypting data with **KMS**. Access control is managed strictly via **IAM Roles**.
*   We use **CloudWatch** to monitor logs and metrics, integrated with **Amazon SNS** to automatically send Email alerts to administrators when server CPU usage is critically high.

#### 2.5. Cost Optimization (Introductory FinOps)
*   **S3 Gateway Endpoint:** This is a major highlight in our design. Instead of routing backend EC2 traffic through the NAT Gateway to fetch images/files from S3 (which incurs high Data Transfer costs), we configured an S3 Gateway Endpoint. This allows EC2 to connect directly to S3 within the AWS internal network, reducing costs and enhancing security.

---

### 3. Budget Estimation (The "Survival" Math)
With the deployment of a fully-fledged Multi-AZ architecture (2 NATs, DB Standby, Cache Replica), the team must monitor usage constantly to avoid going broke.

*Estimated Infrastructure Cost (Monthly - Demo Environment)* 
- *Amazon EC2*: ~$15.00 USD (`t3.micro` instances).
- *Application Load Balancer*: ~$18.00 USD.
- *2 x NAT Gateways*: ~$65.00 USD (Hourly uptime charges are very high).
- *Amazon RDS Multi-AZ*: ~$30.00 USD (`db.t3.micro`).
- *Amazon ElastiCache Multi-AZ*: ~$25.00 USD (`cache.t2.micro`).
- *Other services (WAF, S3, CloudFront, Secrets Manager, SNS...)*: ~$15.00 USD.

*Total Budget*: **~$168.00 USD/month**. 
Despite our best efforts to leverage Free Tier and the lowest instance configurations, this is still a "painful" expense for students. The team plans to tear down the RDS Multi-AZ and NAT Gateways immediately after the project defense to prevent further billing.

---

### 4. Risk Assessment (Highly Realistic)
*   **Slow Auto Scaling Response (High Probability):** If instructors or the defense panel spam requests too quickly, the EC2 instances might overload before the Auto Scaling Group has enough time to spin up new servers.
*   **Backend Code Bugs (Medium Probability):** The spa booking logic occasionally experiences double-booking issues because the database locking mechanism hasn't been perfectly optimized.
*   **Budget Overrun (High Probability):** Due to the use of 2 NAT Gateways, if a code bug causes an infinite loop of external Internet requests, Data Transfer costs could spike rapidly.

---

### 5. Expected Outcomes & Lessons Learned
*   **The Product:** A "functional" website where basic flows (purchasing, booking) can be completed end-to-end without throwing 500 errors.
*   **Skills Acquired:** 
    *   No longer "cloud-blind": The team manually configured the VPC, Subnets, Endpoints, and Load Balancers instead of just learning the theory.
    *   Tasting the "pain": We realized that while debugging code locally is easy, finding bugs via CloudWatch Logs when the app is running on an EC2 instance hidden behind a Private Subnet is incredibly challenging.
    *   This architecture serves as an invaluable stepping stone, helping the team visualize exactly what puzzle pieces are required for a real-world system to survive on the Internet.
---
title: "Prerequisites"
weight: 2
chapter: false
pre: " <b> 5.1.2 </b> "
---

# Prerequisites

Before deploying the infrastructure for the **Pet Resort & Care System**, please ensure you have completed the following requirements to avoid any unexpected charges.

## 1. AWS Account

### 1.1 Set up Billing Alerts

1. Log in to the **AWS Console**: [https://console.aws.amazon.com](https://console.aws.amazon.com)
2. Click on your account name (top right corner) → Select **Billing Dashboard**
3. On the left sidebar, choose **Billing Preferences**
4. Enable the following options:
   - **Receive Free Tier Usage Alerts**
   - **Receive Billing Alerts**
5. Click **Save preferences**

### 1.2 Create a Billing Alarm (AWS Budgets)

1. In the **Billing Dashboard**, click on **Budgets** in the left sidebar
2. Click **Create budget**
3. Select **Cost budget - Recommended**
4. Configure the following parameters:
   - Budget name: `Pet-Resort-Budget`
   - Budgeted amount: `$5.00` (Or your desired budget limit)
   - Budget scope: All AWS services
5. Click **Create budget**

---

## 2. AWS CLI (Recommended)

Installing the AWS CLI will make it easier to interact with services like S3 or configure EC2 directly from your local machine.

### 2.1 Install AWS CLI

#### Windows:
Open Command Prompt or PowerShell and run the following command:
```bash
msiexec.exe /i [https://awscli.amazonaws.com/AWSCLIV2.msi](https://awscli.amazonaws.com/AWSCLIV2.msi)
```

#### macOS (using pkg):
```bash
curl "[https://awscli.amazonaws.com/AWSCLIV2.pkg](https://awscli.amazonaws.com/AWSCLIV2.pkg)" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /
```

### 2.2 Configure AWS CLI

Open your terminal and run:
```bash
aws configure
```

Enter the following information (obtained from your AWS Security Credentials):
- AWS Access Key ID: `(Your Access Key)`
- AWS Secret Access Key: `(Your Secret Key)`
- Default region name: `ap-southeast-1` (Singapore Region)
- Default output format: `json`

---

## Next Steps

Continue with [Network Setup (VPC & Subnets)](#) to begin building the outermost security layer for the system.
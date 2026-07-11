---
title: "Deploy Frontend with S3 & CloudFront"
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---

# Deploy ReactJS Frontend with S3 & CloudFront

#### Overview

In this workshop, you will learn how to deploy the ReactJS application for the **Pet Resort & Care System** using **Amazon S3** for static file hosting and **Amazon CloudFront** as a CDN for global content delivery. Optionally, **AWS WAF** is integrated for security protection.

This approach gives you full control over hosting and is highly cost-effective for static single-page applications:
- 🚀 Static Website Hosting on Amazon S3
- 🔒 HTTPS via CloudFront with free SSL certificate
- 🌍 Global CDN for fast page load speeds
- 💰 Extremely low cost (~$0/month within Free Tier limits)

#### Architecture

```
GitHub Repository → npm run build → S3 Bucket → CloudFront CDN → Users
     ↓ (source code)    ↓ (static files)   ↓ (hosting)    ↓ (distribute)
```

#### Contents

1. [Workshop Overview](5.1.1-overview/)
2. [Prerequisites](5.1.2-prerequisites/)
3. [Setup Git Repository](5.1.3-setup-git/)
4. [Deploy to S3 & CloudFront](5.1.4-deploy-frontend/)
5. [Testing & Verification](5.1.5-testing/)

#### Completion Time
⏱️ Approximately **45-60 minutes**

#### Requirements
- ✅ AWS Account (Free Tier eligible)
- ✅ GitHub account
- ✅ Node.js 18+ and npm
- ✅ Git installed
- ✅ Code editor (VS Code recommended)

---
title: "Workshop Overview"
weight: 1
chapter: false
pre: " <b> 1.1 </b> "
---

# Workshop Overview

#### Workshop Objectives

Upon completing this workshop, you will be able to build an AWS system hands-on with the following skills:
- ✅ Build a highly available web system that won't crash under heavy traffic.
- ✅ Segregate networks (VPC, Subnet) to hide source code and data, preventing hacker attacks.
- ✅ Use ElastiCache (Redis) for a smoother and faster loading experience.
- ✅ Store images and static assets cost-effectively on Amazon S3.
- ✅ Set up automated Email alerts for server incidents.

#### Pet Resort & Care System - Core Features

In this workshop, we will deploy the Pet Resort & Care System platform, including the following modules:
- 🏠 **Home & Products**: Display pet product catalogs and services.
- 📅 **Booking System**: Secure and accurate Spa appointment scheduling.
- 🖼️ **Media Management**: Secure upload and storage of pet images by staff.

#### High-Level Deployment Architecture

Below is the system flow from when a customer clicks on the website until the data is saved:

```text
┌──────────────────────────────┐
│             Users            │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│       CloudFront & WAF       │ (Firewall & Content Delivery)
└──────┬───────────────┬───────┘
       │               │
       ▼               ▼
┌────────────┐   ┌─────────────┐
│ S3 Frontend│   │ Load Balancer (Traffic Routing)
│ (UI/Static)│   └──────┬──────┘
└────────────┘          │
                        ▼
                 ┌─────────────┐
                 │ EC2 Backend │ (Logic Processing & Auto Scaling)
                 └─┬────┬────┬─┘
                   │    │    │
          ┌────────┘    │    └────────┐
          ▼             ▼             ▼
  ┌────────────┐ ┌─────────────┐ ┌───────────────┐
  │ ElastiCache│ │  Amazon RDS │ │   S3 Media    │
  │ (Cache)    │ │  (Database) │ │(Internal Store)
  └────────────┘ └─────────────┘ └───────────────┘

#### Processing & Security Flow

- **Ingestion & Protection:** Customer requests will pass through the WAF filter to block malicious traffic, and then CloudFront will help load the website faster.
- **Traffic Routing:** The website interface is fetched from the S3 bucket. Operations like "Booking" or "Purchasing" will be routed through the Load Balancer to distribute the workload evenly among the internal servers.
- **Processing:** EC2 servers receiving the requests will prioritize checking the Cache (Redis) for faster retrieval. If the data is not there, they will then query the Database (RDS MySQL) to read or write new data.
- **Secure Image Storage:** The operation of uploading pet images will go through an internal network "tunnel" (VPC Endpoint) to the S3 Media bucket, avoiding the public Internet to ensure safety.
- **Monitoring:** The CloudWatch service will continuously monitor the system. If any server fails, it will automatically send an Email alert to the administration team.

#### Estimated Costs

By cleverly utilizing the AWS Free Tier, the maintenance cost for this system is reduced to a minimum:

- ✅ **EC2 Servers & Caching (Redis):** 750 hours/month free (Free Tier).
- ✅ **RDS Database:** 750 hours/month free (Free Tier).
- ✅ **S3 Storage & CloudFront:** Within the free tier limits.

**Actual estimated costs:** Approximately **$50 - $70/month** for the practice environment. This cost is primarily for maintaining 2 critical network services: the NAT Gateway and the Load Balancer. The full production Multi-AZ architecture (as described in the Proposal) costs approximately **~$168/month**.

{{% notice tip %}}
💡 **Tip:** During practice, if you don't need a production-ready setup yet, you can temporarily disable the NAT Gateway and run the Database in Single-AZ mode to maximize your cost savings.
{{% /notice %}}

#### Next Steps

Start with [Network Setup (VPC & Subnets)](#) to build the outermost security layer for your system.
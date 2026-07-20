---
title: "Week 9 Worklog"
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---


## Week 9 Objectives

- Deploy the backend of the Pet Resort & Care System to Amazon EC2.
- Configure the Java environment and run the Spring Boot application on a Linux server.
- Configure appropriate Security Groups for the backend and Application Load Balancer.
- Create a Target Group, configure Health Checks, and connect it to an Application Load Balancer.
- Verify backend accessibility after deployment on AWS.

## Weekly Tasks

| Day | Task Details | Start Date | End Date | References |
|-----|--------------|------------|----------|------------|
| 1 | Launch an Amazon EC2 instance for the backend, select a suitable Amazon Machine Image and instance type, and configure Security Groups for SSH and application access. | 15/06/2026 | 15/06/2026 | Amazon EC2 Documentation |
| 2 | Connect to the EC2 instance using SSH, install the Java Runtime, and verify the Linux environment before deploying the Spring Boot application. | 16/06/2026 | 16/06/2026 | Amazon EC2 User Guide |
| 3 | Upload the Pet Resort & Care System `.jar` file to EC2, configure environment variables, and run the backend application on the server. | 17/06/2026 | 17/06/2026 | AWS EC2 Deployment Guide |
| 4 | Create a Target Group, register the EC2 instance as a Target, and configure Health Checks to monitor backend availability. | 18/06/2026 | 18/06/2026 | Elastic Load Balancing Documentation |
| 5 | Create an Application Load Balancer, configure its Listener and Security Group, and test the APIs through the Load Balancer DNS using a browser and Postman. | 19/06/2026 | 19/06/2026 | Application Load Balancer Documentation |

## Week 9 Achievements

- **Backend deployment on Amazon EC2:**
  - Launched and configured an EC2 instance for the Spring Boot application.
  - Successfully connected to the EC2 instance using SSH.
  - Installed Java and ran the executable `.jar` file on the Linux server.
  - Configured the required environment variables for the application.

- **Load balancing configuration:**
  - Created a Target Group and registered the EC2 instance as a Target.
  - Configured Health Checks to monitor backend availability.
  - Created an Application Load Balancer and configured a Listener to forward requests to the Target Group.
  - Updated Security Groups to allow communication between the Load Balancer and the backend server.

- **Post-deployment testing:**
  - Verified the Target status in the AWS Management Console.
  - Tested API access through the Application Load Balancer DNS.
  - Tested the APIs using Postman and resolved several configuration issues.
  - Documented the deployment steps for frontend integration in the following week.
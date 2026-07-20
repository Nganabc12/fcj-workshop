---
title: "Week 11"
weight: 11
chapter: false
pre: "<b>11. </b>"
---


## Week 11 Objectives

- Deploy the Pet Resort & Care System to the AWS Cloud environment.
- Complete the integration between the Frontend and Backend.
- Verify the deployed system and resolve deployment-related issues.

---

## Tasks Performed During the Week

| Day | Tasks | Start Date | Completion Date | Reference |
|-----|-------|------------|-----------------|-----------|
| **Mon** | - Prepare the deployment environment for the Spring Boot Backend on Amazon EC2.<br>- Build the application into a `.jar` file, install Java Runtime, and configure the required environment variables on the EC2 instance. | 29/06/2026 | 29/06/2026 | AWS Documentation (EC2) |
| **Tue** | - Create an Amazon RDS MySQL database and update the Backend database configuration.<br>- Configure Security Groups for EC2 and RDS, then verify database connectivity from the application. | 30/06/2026 | 30/06/2026 | AWS Documentation (RDS) |
| **Wed** | - Configure the Application Load Balancer and Target Group for the Backend service.<br>- Verify the Health Check configuration and ensure the application is accessible through the ALB. | 01/07/2026 | 01/07/2026 | AWS Documentation (ALB) |
| **Thu** | - Deploy the ReactJS Frontend to Amazon S3.<br>- Configure Amazon CloudFront to distribute the website and static resources. | 02/07/2026 | 03/07/2026 | AWS Documentation (S3, CloudFront) |
| **Sat** | - Verify the communication between the Frontend and Backend in the AWS environment.<br>- Resolve issues related to CORS, API endpoints, image resources and deployment configuration before system testing. | 04/07/2026 | 04/07/2026 | Project Documentation |

---

## Week 11 Achievements

- Successfully deployed the Spring Boot Backend on Amazon EC2 and connected it to Amazon RDS MySQL.

- Configured Security Groups, the Application Load Balancer and Target Group to enable external access to the Backend service.

- Successfully deployed the ReactJS Frontend to Amazon S3 and configured Amazon CloudFront to distribute static website content.

- Verified the communication between the Frontend and Backend, ensuring that authentication, pet management, service management and booking features worked correctly in the AWS environment.

- Resolved deployment issues related to CORS configuration, API endpoints, Security Groups, Target Group Health Checks and static resource paths.

- Completed the deployment of the Pet Resort & Care System, providing a stable environment for system testing and project completion in the following week.
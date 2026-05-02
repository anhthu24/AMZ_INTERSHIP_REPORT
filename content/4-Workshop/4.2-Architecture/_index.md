---
title : "Architecture & Design"
date : 2026/04/27 
weight : 2 
chapter : false
pre : " <b> 4.2. </b> "
---

**Architecture Design:** The system follows a 3-tier architecture model including presentation layer (EC2), data layer (RDS), and storage layer (S3). The architecture diagram clearly illustrates data flow between components. 

![architecture](../../images/4.2-Architecture/architecture.png)

Service Selection:
- EC2: Flexible compute service for hosting PHP application 
- RDS (MySQL): Managed database for reliability and scalability 
- S3: Scalable object storage for static assets 

![server](../../images/4.2-Architecture/server.png)


Reason for Selection: Services are selected based on ease of deployment, managed capabilities, cost efficiency, and suitability for traditional web applications. 

Security & IAM:
- Security Groups used to restrict access (SSH, HTTP, MySQL) 
- IAM principles applied (least privilege) 
- No hard-coded credentials in source code 

Scalability & Operation:
- Architecture supports scaling by upgrading EC2 instance or using load balancing (future work) 
- Basic monitoring via logs and system testing


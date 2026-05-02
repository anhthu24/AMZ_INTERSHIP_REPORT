---
title: "Proposal"
date: 2026/04/27
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Classic Groove Web Application Deployment on AWS

### 1. Overview
The project focuses on deploying the "Classic Groove" web application – an online platform for browsing and purchasing classic music records – onto the AWS cloud infrastructure. The system is built using PHP and MySQL, and will be hosted on Amazon EC2, with Amazon RDS handling database services and Amazon S3 storing static resources such as images and media files.

### 2. Goals
- Deploy a fully functional web application on AWS. 
- Ensure high availability, scalability, and security. 
- Optimize performance for both dynamic and static content delivery. 
- Gain hands-on experience with core AWS services (EC2, RDS, S3). 

### 3. Problem to be solved
The application is initially developed in a local environment, which lacks scalability, accessibility, and reliability. Key challenges include deploying the system to a cloud environment, configuring secure database connections, and improving performance when handling user requests and static resources.

### 4. Architecture Solution
The system architecture consists of:
- Amazon EC2: Hosts the PHP web application. 
- Amazon RDS (MySQL): Manages relational database. 
- Amazon S3: Stores static files (images, assets).
 
Data flow: Client → EC2 (Web Server) → RDS (Database) & S3 (Static Content)

### 5. 8 Weeks Timeline
- Week 1–2: AWS fundamentals & local environment setup (LAMP, requirement analysis)
- Week 3–4: EC2 provisioning, configuration & web application deployment
- Week 5–6: RDS setup, database migration & optimization
- Week 7: S3 integration for static asset storage
- Week 8: Testing, security hardening & project documentation

### 6. Budget estimate
The project utilizes AWS Free Tier services where applicable:
+ EC2 (t2.micro / t3.micro) 
+ RDS (db.t3.micro) 
+ S3 (low-cost storage) 

Estimated cost beyond Free Tier: approximately $5–10/month depending on usage.


### 7. Risk assessment
- Security misconfiguration (Security Groups, IAM policies) 
- Unexpected AWS costs due to improper resource usage 
- Network latency between EC2 and RDS 
- Data loss without proper backup strategy 

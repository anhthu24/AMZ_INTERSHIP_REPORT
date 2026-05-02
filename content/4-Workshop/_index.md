---
title: "Workshop"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 4. </b> "
---

# Classic Groove Web Application Deployment on AWS

#### Workshop overview

This workshop demonstrates how to deploy the Classic Groove PHP web application on AWS using a three-tier architecture. The system leverages Amazon EC2 for application hosting, Amazon RDS (MySQL) for database management, and Amazon S3 for static asset storage. The solution ensures scalability, reliability, and basic security for a production-like environment.

#### Prerequisite

- AWS Account 
- Basic Linux & Apache knowledge 
- SSH client (Terminal / PuTTY) 
- MySQL client 
- PHP web source code

#### Architecture Description

Architecture components:
- EC2: Hosts PHP web application 
- RDS (MySQL): Managed database service 
- S3: Stores static assets (images, media) 

Flow: Client → EC2 → RDS → S3
Security:
- Security Group restricts access (HTTP, SSH, MySQL) 
- IAM Role (optional) for EC2 to access S3 

#### Implementation Steps

Step 1: EC2 Setup 
- Launch EC2 (Amazon Linux 2) 
- Configure Security Group (22, 80, 443) 
- Install Apache, PHP 

Step 2: Deploy Web Application
- Upload source code via SCP 
- Move to /var/www/html 
- Restart Apache 

Step 3: 
- Create MySQL RDS instance 
- Enable public access 
- Open port 3306 
- Import database 
  
Step 4: Connect EC2 to RDS
- Update DB config in PHP 
- Test connection (test script) 

Step 5: S3 Integration
- Create S3 bucket 
- Upload images/media 
- Update application to load assets from S3 

Step 6: IAM Policy (Optional but recommended)
Example policy for EC2 to access S3:

```
{
    "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject"],
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```
Step 7: Testing & Validation
- Access website via public IP 
- Verify database CRUD 
- Check static assets load from S3 

Step 8: Clean-up
- Terminate EC2 
- Delete RDS instance 
- Remove S3 bucket 
- Delete unused resources

#### Content

1. [Project Format & Tools](4.1-format_and_tools/)
2. [Architecture & Design](4.2-architecture/)
3. [Implementation](4.3-implementation/4.3.1-prerequisite/)
4. [Testing & Monitoring](4.4-testing/)
5. [Optimization & Clean-up](4.5-optimization/)
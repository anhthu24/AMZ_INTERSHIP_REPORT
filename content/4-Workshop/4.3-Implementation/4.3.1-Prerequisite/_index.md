---
title : "Prerequisite"
date : 2026/04/27 
weight : 1
chapter : false
pre : " <b>4.3.1. </b> "
---

Before starting the deployment and lab implementation, the following prerequisites must be prepared:
- **AWS Account:** A valid AWS account is required to access and manage cloud services such as EC2, RDS, and S3. 
- **Region:** The system is deployed in **ap-southeast-2 (Sydney)** to ensure compatibility and stable performance. 
- **Tools:** 
  - AWS Management Console (main interface for resource configuration) 
  - SSH client (Git Bash / Terminal) to connect to EC2 instance 
  - SCP (Secure Copy Protocol) to transfer source code from local machine to server 
  - Composer to install AWS SDK for PHP (used for S3 integration) 
- **IAM Permissions:** The following permissions are required: 
  - Amazon EC2 Full Access 
  - Amazon RDS Full Access 
  - Amazon S3 Full Access 
  - IAM permission to create Access Keys 

These prerequisites ensure that the deployment process can be performed efficiently and securely.

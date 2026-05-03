---
title: "Week 5 Worklog"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

- Initialize Amazon S3 object storage services and Amazon RDS relational databases.

- Deploy the project's data structure to the Cloud system.

- Establish a secure connection between the Web Server (EC2) and the Database (RDS) via a Security Group.

### Tasks to be carried out this week:

| No. | Task                                                                                                                                     | Start Date | Completion Date | Reference Material |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------ |
| 1   | - Initialize Amazon S3 Bucket <br> <br> - Configure access permissions and upload static resources (images, videos) of the project to S3 | 06/04/2026 | 06/04/2026      |

| 2 | - Initialize Amazon RDS (MySQL engine)<br> <br> - Select a configuration suitable for the Free Tier limit <br><br> - Set the Database Name, Master Username, and Password parameters | 07/04/2026 | 07/04/2026 | AWS Documentation - RDS User Guide |

| 3 | - Configure Security Group for RDS: <br>&emsp; + Allow Inbound port 3306 from EC2 Security Group <br><br>- Check the connection from EC2 instance to RDS endpoint | 08/04/2026 | 08/04/2026 | <https://cloudjourney.awsstudygroup.com/> |

| 4 | - Use the mysql command or admin tool to connect <br> <br> Import the classic-groove.sql data file into the Amazon RDS instance <br> | 10/04/2026 | 10/04/2026 | Internal Project Docs |

| 5 | - Change the configuration in the connect.php or dataProvider.php file to point to the RDS Endpoint <br><br>- Check the ability to access data on the web interface via Public IP | 09/04/2026 | 09/04/2026 | |

### Week 5 Achievements:

- Completing the storage and data infrastructure for the project:
  - Amazon S3 is ready to store static resources, reducing the load on EC2.

  - Amazon RDS (MySQL) is stable and completely replaces the local database.

- Managing system security using a multi-layered model:
  - Applying the principle of least privilege when configuring Security Groups for the database.

  - Understanding how AWS components (EC2 and RDS) communicate with each other within the same VPC.

- Successful data deployment:
  - The entire table structure and sample data have been imported into RDS without errors.

  - The web application can now query and display actual data from the cloud database.

- Enhancing administration skills:
  - Mastering the configuration of application connection files (db_config).

  - Knowing how to handle common connection issues (Connection Timeout, Access Denied) between AWS services.

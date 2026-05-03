---
title: "Week 3 Worklog"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

- Initialize and configure an Amazon EC2 instance running on the Linux operating system.

- Configure networking and security (Security Group) to allow web access.

- Install and configure the Web Server environment (Apache) and programming language (PHP).

### Tasks to be carried out this week:

| No. | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 1 | - Initialize Amazon EC2 instance (Amazon Linux 2023).<br> - Configure Key Pair for secure SSH access via MobaXterm. | 23/03/2026 | 23/03/2026 |
| 2 | - Set up Security Group: Open ports 80 (HTTP), 443 (HTTPS), and 22 (SSH).<br> | 24/03/2026 | 24/03/2026 | |
| 3 | - Use MobaXterm to connect to EC2 via SSH.<br> - Update the system.<br> - Install Apache Web Server (httpd). | 25/03/2026 | 25/03/2026 | |
| 4 | - Install PHP and necessary modules: php-mysqlnd.<br> - Start and set up automatic execution for the httpd service.<br> | 26/03/2026 | 26/03/2026 | |
| 5 | - Assign permissions to the /var/www/html directory <br> - Check via Public IP | 27/03/2026 | 27/03/2026 | |

### Week 3 Achievements:

- Successfully created a stable EC2 server on AWS infrastructure.

- Managed server access and security effectively through:
  - Security Group (Inbound/Outbound rules)

  - Key Pairing (Private/Public key)

- Completed Web Server environment setup
  - Installed and operated Apache Web Server.

  - Configured the PHP execution environment to prepare for running the project source code.

- Mastered remote server administration skills:
  - Used the terminal via MobaXterm.

  - Controlled web directory access permissions.

- Ensured the system could receive HTTP requests from the internet and process PHP code correctly.

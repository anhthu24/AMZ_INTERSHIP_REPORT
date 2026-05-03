---
title: "Week 4 Worklog"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

- Transfer the project source code from the development environment to the EC2 server.

- Configure the Web Server in detail to recognize the new source code.

- Test the accessibility and functionality of the application using the Public IP.

### Tasks to be carried out this week:

| No. | Task                                                                                                                                                                                | Start Date | Completion Date | Reference Material |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------ |
| 1   | - Prepare the project source code (compress files or upload to GitHub) <br> <br> - Connect to MobaXterm and use SFTP to upload the source code to a temporary directory on EC2 <br> | 30/03/2026 | 30/03/2026      |First Cloud Journey Bootcamp - 2025 on YouTube.|

| 2 | - Move the source code to the Apache root directory (/var/www/html) <br> <br> - Assign ownership (chown) and access permissions (chmod) to the project files <br> | 31/03/2026 | 31/03/2026 | |

| 3 | - Adjust system configuration parameters to suit the PHP source code requirements | 01/04/2026 | 01/04/2026 | AWS Documentation |

| 4 | - Access the application directly via the instance's Public IP <br>- Check the links, images, and basic logic of the front-end interface | 02/04/2026 | 02/04/2026 | |

| 5 | - **Practice:** <br>&emsp; + Check Apache error logs (error_log) to handle any issues <br>&emsp; + Back up the configuration | 03/04/2026 | 03/04/2026 | |

### Week 4 Achievements:

- Successfully deployed the project's source code to a Cloud environment (EC2).

- Efficiently managed data on the server:
  - Proficiently used the SFTP protocol for data transfer.

  - Mastered directory permission techniques on Linux to ensure the security and performance of the web server.

- Completed the preliminary testing phase:
  - The application displayed the correct interface via the instance's Public IP.

  - Identified and promptly resolved errors arising during migration from the Local environment to the Server (path errors, access errors).

- Familiarized with manual CI/CD procedures:
  - Understands the process of deploying a software product from a personal computer to the Internet.

  - Knows how to read and analyze logs to diagnose system status.

- The system is ready for database connection in subsequent stages.

---
title: "Week 6 Worklog"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

- Completely resolve connection errors between the web application and the database.
- Upgrade the PHP version to ensure compatibility and security for the project.
- Validate and optimize data flow between EC2 and RDS.

### Tasks to be carried out this week:

| No. | Task                                                                                                                                                                              | Start Date | Completion Date | Reference Material |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------ |
| 1   | - Check system logs to identify the cause of the "Database Connection Failed" error <br> <br> - Review the Endpoint, Username, and Password information in the configuration file | 13/04/2026 | 13/04/2026      |

| 2 | - Upgrade the PHP version to match the new connection library <br> <br> - Install the php-mysqli extension | 14/04/2026 | 14/04/2026 | PHP Official Documentation |

| 3 | - Check the Security Group's Inbound Rules to ensure the IP is not blocked <br><br> - Practice: Write a standalone PHP script to test the connection and authenticate access to RDS <br><br> - Handle errors related to character encoding (UTF-8) when displaying data <br> | 15/04/2026 | 16/04/2026 | Internal Debugging Guide |

| 4 | - Test all CRUD (Create, Read, Update, Delete) functions on the web interface <br><br>- Ensure the application runs smoothly with the newly upgraded PHP version <br> | 17/04/2026 | 17/04/2026 | |

### Week 6 Achievements:

- Completely resolve database connection errors:
  - The application now accesses data stably, eliminating sudden connection drops.

  - Understand how to handle errors based on MySQL and PHP error codes.

- Upgrade the execution environment:
  - The system runs on the latest PHP version, increasing processing performance and security.

  - Extended modules are correctly configured, providing good support for data interaction.

- Successfully authenticate EC2-RDS connections:
  - Establish a process for checking bidirectional connections between the Web Server and the DB Server.

- Enhance troubleshooting skills:
  - Know how to read Apache and MySQL logs.

  - Master the skill of debugging PHP source code when migrating between different environment versions.

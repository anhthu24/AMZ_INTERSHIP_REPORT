---
title: "Week 7 Worklog"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

- Conduct comprehensive testing of application functionalities in a cloud environment.

- Ensure data integrity during interaction between EC2 and RDS.

### Tasks to be carried out this week:

| No. | Task                                                     | Start Date | Completion Date | Reference Material |
| --- | -------------------------------------------------------- | ---------- | --------------- | ------------------ |
| 1   | - Perform unit testing for database connection functions | 20/04/2026 | 20/04/2026      |                    |
| 2 | - Reconfigure the connect.php file using environment variables <br>- Optimize SQL query statements to reduce load on RDS instances <br> | 21/04/2026 | 21/04/2026 | PHP Best Practices |
| 3 | - Basic performance testing: Website response speed when querying tables with large data <br><br> - Check the display of previously configured static resources from S3 <br> | 23/04/2026 | 23/04/2026 | |
| 4 | - Practice: Simulate error scenarios (DB disconnection, incorrect login information) to test the application's exception handling capabilities. <br> | 24/04/2026 | 24/04/2026 | AWS Study Group Resources |

### Week 7 Achievements:

- Database connection configuration completed:
  - Configuration files are organized scientifically, making maintenance and parameter changes easy when needed.

- Positive test results:
  - 100% of main functions (View products, Login, Submit form) work correctly in the real-world environment.

  - Data formatting errors between PHP and MySQL have been synchronized.

- Optimized user experience:
  - Stable page load speed thanks to optimized SQL queries and leveraging EC2 to RDS connections within the same internal network infrastructure.

- Ready for project completion phase:
  - The system has reached a stable state, ready for acceptance testing and final reporting next week.

---
title: "Worklog Tuần 5"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

- Khởi tạo dịch vụ lưu trữ đối tượng Amazon S3 và cơ sở dữ liệu quan hệ Amazon RDS.
- Triển khai cấu trúc dữ liệu của dự án lên hệ thống Cloud.
- Thiết lập kết nối an toàn giữa Web Server (EC2) và Database (RDS) thông qua Security Group.

### Các công việc cần triển khai trong tuần này:

| STT | Công việc                                                                                                                                                                | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | --------------- | ----------------------------------------- |
| 1   | - Khởi tạo Amazon S3 Bucket <br> <br> - Cấu hình quyền truy cập và tải các tài nguyên tĩnh (hình ảnh, video) của dự án lên S3                                            | 06/04/2026   | 06/04/2026      |
| 2   | - Khởi tạo Amazon RDS (MySQL engine)<br> <br> - Lựa chọn cấu hình phù hợp với hạn mức Free Tier <br><br> - Thiết lập thông số Database Name, Master Username và Password | 07/04/2026   | 07/04/2026      | AWS Documentation - RDS User Guide        |
| 3   | - Cấu hình Security Group cho RDS: <br>&emsp; + Cho phép Inbound port 3306 từ Security Group của EC2 <br><br>- Kiểm tra kết nối từ EC2 instance tới RDS endpoint         | 08/04/2026   | 08/04/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Sử dụng lệnh mysql hoặc công cụ quản trị để kết nối <br> <br> Nhập file dữ liệu classic-groove.sql vào Amazon RDS instance <br>                                        | 10/04/2026   | 10/04/2026      | Internal Project Docs                     |
| 5   | - Thay đổi cấu hình trong file connect.php hoặc dataProvider.php để trỏ về RDS Endpoint <br><br>- Kiểm tra khả năng truy xuất dữ liệu trên giao diện web qua Public IP   | 09/04/2026   | 09/04/2026      |  |

### Kết quả đạt được tuần 5:

- Hoàn thiện hạ tầng lưu trữ và dữ liệu cho dự án:
  - Amazon S3 đã sẵn sàng để lưu trữ tài nguyên tĩnh, giúp giảm tải cho EC2.
  - Amazon RDS (MySQL) hoạt động ổn định, thay thế hoàn toàn cho database local.

- Quản lý bảo mật hệ thống theo mô hình nhiều lớp:
  - Áp dụng nguyên tắc đặc quyền tối thiểu (Least Privilege) khi cấu hình Security Group cho Database.
  - Hiểu rõ cách các thành phần trong AWS (EC2 và RDS) giao tiếp với nhau trong cùng một VPC.
- Triển khai dữ liệu thành công:
  - Toàn bộ cấu trúc bảng và dữ liệu mẫu đã được import vào RDS mà không có lỗi.
  - Ứng dụng web đã có thể truy vấn và hiển thị dữ liệu thực tế từ database trên Cloud.

- Nâng cao kỹ năng quản trị:
  - Thành thạo việc cấu hình các tệp tin kết nối ứng dụng (db_config).
  - Biết cách xử lý các sự cố thường gặp về kết nối (Connection Timeout, Access Denied) giữa các dịch vụ AWS.

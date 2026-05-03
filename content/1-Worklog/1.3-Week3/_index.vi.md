---
title: "Worklog Tuần 3"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

- Khởi tạo và cấu hình instance Amazon EC2 chạy hệ điều hành Linux.

- Cấu hình mạng và bảo mật (Security Group) để cho phép truy cập web.

- Cài đặt và cấu hình môi trường Web Server (Apache) và ngôn ngữ lập trình (PHP).

### Các công việc cần triển khai trong tuần này:

| STT | Công việc                                                                                                          | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------ | ------------ | --------------- | -------------- |
| 1   | - Khởi tạo Amazon EC2 instance (Amazon Linux 2023).<br> - Cấu hình Key Pair để truy cập SSH an toàn qua MobaXterm. | 23/03/2026   | 23/03/2026      | First Cloud Journey Bootcamp - 2025 on YouTube.|
| 2   | - Thiết lập Security Group: Mở cổng 80 (HTTP), 443 (HTTPS) và 22 (SSH).<br>                                        | 24/03/2026   | 24/03/2026      |    First Cloud Journey Bootcamp - 2025 on YouTube.            |
| 3   | - Sử dụng MobaXterm kết nối SSH vào EC2.<br> - Cập nhật hệ thống <br>- Cài đặt Apache Web Server (httpd).          | 25/03/2026   | 25/03/2026      |     First Cloud Journey Bootcamp - 2025 on YouTube.           |
| 4   | - Cài đặt PHP và module cần thiết: php-mysqlnd <br> - Khởi động và thiết lập tự động chạy cho dịch vụ httpd <br>   | 26/03/2026   | 26/03/2026      |      <https://cloudjourney.awsstudygroup.com/>          |
| 5   | - Phân quyền thư mục /var/www/html <br> - Kiểm tra qua Public IP                                                   | 27/03/2026   | 27/03/2026      |      <https://cloudjourney.awsstudygroup.com/>         |

### Kết quả đạt được tuần 3:

- Khởi tạo thành công máy chủ EC2 hoạt động ổn định trên hạ tầng AWS.
- Quản lý truy cập và bảo mật server hiệu quả thông qua:
  - Security Group (Inbound/Outbound rules)
  - Key Pair (Private/Public key)

- Thiết lập hoàn tất môi trường Web Server
  - Cài đặt và vận hành Apache Web Server.
  - Cấu hình môi trường thực thi PHP để chuẩn bị chạy mã nguồn dự án.

- Thành thạo các kỹ năng quản trị server từ xa:
  - Sử dụng terminal qua MobaXterm.
  - Kiểm soát quyền truy cập thư mục web (permissions).
- Đảm bảo hệ thống có thể tiếp nhận các request HTTP từ internet và xử lý mã PHP chính xác.

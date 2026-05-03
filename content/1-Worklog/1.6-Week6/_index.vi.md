---
title: "Worklog Tuần 6"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

- Khắc phục triệt để các lỗi kết nối giữa ứng dụng web và cơ sở dữ liệu.
- Nâng cấp phiên bản PHP để đảm bảo tính tương thích và bảo mật cho dự án.
- Xác thực và tối ưu hóa luồng dữ liệu giữa EC2 và RDS.

### Các công việc cần triển khai trong tuần này:

| STT | Công việc                                                                                                                                                                                                                                                        | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu             |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | -------------------------- |
| 1   | - Kiểm tra log hệ thống để xác định nguyên nhân lỗi "Database Connection Failed" <br> <br> - Rà soát lại thông tin Endpoint, Username và Password trong file cấu hình                                                                                            | 13/04/2026   | 13/04/2026      |
| 2   | - Thực hiện nâng cấp phiên bản PHP để phù hợp với thư viện kết nối mới<br> <br>- Cài đặt bổ sung extension php-mysqli                                                                                                                                            | 14/04/2026   | 14/04/2026      | PHP Official Documentation |
| 3   | - Kiểm tra lại Inbound Rules của Security Group để đảm bảo không bị chặn IP <br><br> - Thực hành: Viết script test kết nối độc lập bằng PHP để xác thực quyền truy cập vào RDS <br><br> - Xử lý lỗi liên quan đến mã hóa ký tự (UTF-8) khi hiển thị dữ liệu <br> | 15/04/2026   | 16/04/2026      | Internal Debugging Guide   |
| 4   | - Kiểm thử toàn bộ các chức năng CRUD (Create, Read, Update, Delete) trên giao diện web <br><br>- Đảm bảo ứng dụng vận hành mượt mà với phiên bản PHP mới nâng cấp <br>                                                                                          | 17/04/2026   | 17/04/2026      |                            |

### Kết quả đạt được tuần 6:

- Khắc phục hoàn toàn lỗi kết nối Database:
  - Ứng dụng đã truy xuất dữ liệu ổn định, không còn tình trạng mất kết nối đột ngột.
  - Hiểu rõ cách xử lý lỗi dựa trên mã lỗi (Error Codes) của MySQL và PHP.

- Nâng cấp môi trường thực thi:
  - Hệ thống chạy trên phiên bản PHP mới nhất, tăng hiệu suất xử lý và khả năng bảo mật.
  - Các module mở rộng được cấu hình chuẩn xác, hỗ trợ tốt cho việc tương tác dữ liệu.

- Xác thực kết nối EC2–RDS thành công:
  - Thiết lập được quy trình kiểm tra kết nối hai chiều giữa Web Server và DB Server.

- Nâng cao kỹ năng Troubleshooting:
  - Biết cách đọc log của Apache và MySQL.
  - Thành thạo kỹ năng debug mã nguồn PHP khi di chuyển giữa các phiên bản môi trường khác nhau.

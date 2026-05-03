---
title: "Worklog Tuần 4"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

- Chuyển giao mã nguồn dự án từ môi trường phát triển lên máy chủ EC2.
- Cấu hình chi tiết Web Server để nhận diện bộ mã nguồn mới.
- Kiểm thử khả năng truy cập và vận hành của ứng dụng thông qua Public IP.

### Các công việc cần triển khai trong tuần này:

| STT | Công việc                                                                                                                                              | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                 |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | --------------- | ------------------------------ |
| 1   | - Chuẩn bị mã nguồn dự án (nén file hoặc đẩy lên GitHub) <br> <br> - Kết nối MobaXterm và sử dụng SFTP để tải mã nguồn lên thư mục tạm trên EC2 <br>   | 30/03/2026   | 30/03/2026      |
| 2   | - Di chuyển mã nguồn vào thư mục gốc của Apache (/var/www/html) <br> <br>- Phân quyền sở hữu (chown) và quyền truy cập (chmod) cho các file dự án <br> | 31/03/2026   | 31/03/2026      |                                |
| 3   | - Điều chỉnh các tham số cấu hình hệ thống phù hợp với yêu cầu của mã nguồn PHP                                                                        | 01/04/2026   | 01/04/2026      | AWS Documentation - App Deploy |
| 4   | - Truy cập ứng dụng trực tiếp qua Public IP của instance <br>- Kiểm tra các liên kết, hình ảnh và logic cơ bản của giao diện front-end                 | 02/04/2026   | 02/04/2026      |                                |
| 5   | - **Thực hành:** <br>&emsp; + Kiểm tra log lỗi của Apache (error_log) để xử lý các vấn đề phát sinh <br>&emsp; + Sao lưu cấu hình                      | 03/04/2026   | 03/04/2026      |                                |

### Kết quả đạt được tuần 4:

- Triển khai thành công mã nguồn dự án lên môi trường Cloud (EC2).

- Quản lý dữ liệu trên máy chủ hiệu quả:
  - Sử dụng thành thạo giao thức SFTP để truyền tải dữ liệu.
  - Nắm vững kỹ thuật phân quyền thư mục trên Linux để đảm bảo tính bảo mật và khả năng thực thi của web server.

- Hoàn thành giai đoạn kiểm thử sơ bộ:
  - Ứng dụng hiển thị đúng giao diện thông qua Public IP của instance.
  - Xác định và xử lý kịp thời các lỗi phát sinh trong quá trình di chuyển từ môi trường Local lên Server (lỗi đường dẫn, lỗi quyền truy cập).

- Làm quen với quy trình CI/CD thủ công:
  - Hiểu luồng đưa một sản phẩm phần mềm từ máy cá nhân lên Internet.
  - Biết cách đọc và phân tích Log để chẩn đoán trạng thái hệ thống.

- Hệ thống sẵn sàng cho việc kết nối Database ở các giai đoạn tiếp theo.

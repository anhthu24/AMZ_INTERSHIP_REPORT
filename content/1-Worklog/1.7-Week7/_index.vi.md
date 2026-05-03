---
title: "Worklog Tuần 7"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

- Kiểm thử toàn diện các chức năng của ứng dụng trên môi trường Cloud.

- Đảm bảo tính toàn vẹn của dữ liệu khi tương tác qua lại giữa EC2 và RDS.

### Các công việc cần triển khai trong tuần này:

| STT | Công việc                                                                                                                                                                    | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu            |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------------- |
| 1   | - Thực hiện kiểm thử đơn vị (Unit Testing) cho các hàm kết nối cơ sở dữ liệu                                                                                                 | 20/04/2026   | 20/04/2026      |                           |
| 2   | - Cấu hình lại file connect.php sử dụng biến môi trường <br>- Tối ưu hóa câu lệnh truy vấn SQL để giảm tải cho RDS instance <br>                                             | 21/04/2026   | 21/04/2026      | PHP Best Practices        |
| 3   | - Kiểm thử hiệu năng cơ bản: Tốc độ phản hồi của trang web khi truy vấn các bảng có dữ liệu lớn <br><br> - Kiểm tra hiển thị tài nguyên tĩnh từ S3 đã cấu hình trước đó <br> | 23/04/2026   | 23/04/2026      |                           |
| 4   | - Thực hành: Mô phỏng các tình huống lỗi (ngắt kết nối DB, sai thông tin đăng nhập) để kiểm tra khả năng xử lý ngoại lệ (Exception Handling) của ứng dụng <br>               | 24/04/2026   | 24/04/2026      | AWS Study Group Resources |

### Kết quả đạt được tuần 7:

- Hoàn thiện cấu hình kết nối cơ sở dữ liệu:
  - File cấu hình được tổ chức khoa học, dễ dàng bảo trì và thay đổi thông số khi cần thiết.

- Kết quả kiểm thử khả quan:
  - 00% các chức năng chính (Xem sản phẩm, Đăng nhập, Gửi form) hoạt động chính xác trên môi trường thực tế.
  - Các lỗi về định dạng dữ liệu giữa PHP và MySQL đã được đồng bộ hóa.

- Tối ưu hóa trải nghiệm người dùng:
  - Tốc độ tải trang ổn định nhờ việc tối ưu hóa các truy vấn SQL và tận dụng kết nối từ EC2 đến RDS trong cùng một hạ tầng mạng nội bộ.

- Sẵn sàng cho giai đoạn hoàn thiện dự án:
  - Hệ thống đã đạt trạng thái ổn định (Stable), sẵn sàng cho việc nghiệm thu và báo cáo cuối kỳ vào tuần tới.

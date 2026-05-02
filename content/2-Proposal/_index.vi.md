---
title: "Bản đề xuất"
date: 2026/04/27
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Triển khai ứng dụng web bán đĩa "Classic Groove" trên AWS  

### 1. Tổng quan   
Dự án tập trung triển khai ứng dụng web “Classic Groove” – một nền tảng trực tuyến cho phép người dùng duyệt và mua các đĩa nhạc cổ điển – lên hạ tầng điện toán đám mây AWS. Hệ thống được xây dựng bằng PHP và MySQL, sử dụng Amazon EC2 để chạy ứng dụng, Amazon RDS để quản lý cơ sở dữ liệu và Amazon S3 để lưu trữ tài nguyên tĩnh như hình ảnh và file media.

### 2. Mục tiêu
- Triển khai hoàn chỉnh ứng dụng web trên nền tảng AWS.
- Đảm bảo tính sẵn sàng cao, khả năng mở rộng và bảo mật.
- Tối ưu hiệu suất cho cả nội dung động và tĩnh.
- Nâng cao kỹ năng thực hành với các dịch vụ AWS (EC2, RDS, S3).

### 3. Vấn đề cần giải quyết   
Ứng dụng ban đầu được phát triển trên môi trường cục bộ, thiếu khả năng mở rộng, truy cập và độ ổn định. Các vấn đề chính bao gồm triển khai hệ thống lên môi trường cloud, cấu hình kết nối cơ sở dữ liệu an toàn và cải thiện hiệu suất khi xử lý yêu cầu người dùng và tài nguyên tĩnh.
 

### 4. Kiến trúc giải pháp  
Kiến trúc hệ thống bao gồm:
- Amazon EC2: Chạy ứng dụng web PHP. 
- Amazon RDS (MySQL): Quản lý cơ sở dữ liệu quan hệ. 
- Amazon S3: Lưu trữ file tĩnh (hình ảnh, tài nguyên).  
Luồng dữ liệu: Người dùng → EC2 (Web Server) → RDS (Database) & S3 (Tài nguyên tĩnh)


### 5. Lịch trình 8 tuần  
- Tuần 1–2: Tìm hiểu AWS & thiết lập môi trường local (LAMP, phân tích yêu cầu)
- Tuần 3–4: Khởi tạo, cấu hình EC2 & triển khai ứng dụng web
- Tuần 5–6: Cấu hình RDS, migrate & tối ưu database
- Tuần 7: Tích hợp S3 cho tài nguyên tĩnh
- Tuần 8: Kiểm thử, bảo mật & hoàn thiện tài liệu

### 6. Ước tính ngân sách  
Dự án sử dụng AWS Free Tier:
- EC2 (t2.micro / t3.micro) 
- RDS (db.t3.micro) 
- S3 (chi phí thấp) 
Chi phí sau Free Tier ước tính khoảng 5–10 USD/tháng tùy mức sử dụng.

### 7. Đánh giá rủi ro  
- Cấu hình sai bảo mật (Security Group, IAM) 
- Phát sinh chi phí ngoài dự kiến 
- Độ trễ giữa EC2 và RDS 
- Mất dữ liệu nếu không có backup

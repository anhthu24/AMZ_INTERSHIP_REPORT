---
title: "Workshop"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 4. </b> "
---

# Triển khai ứng dụng "Classic Groove" trên nền tảng AWS
#### Tổng quan về workshop
Workshop này trình bày cách triển khai ứng dụng web Classic Groove trên AWS theo mô hình 3-tier. Hệ thống sử dụng EC2 để chạy ứng dụng, RDS (MySQL) để quản lý database và S3 để lưu trữ tài nguyên tĩnh, đảm bảo khả năng mở rộng và độ ổn định.

#### Điều kiện tiên quyết
- Tài khoản AWS 
- Kiến thức Linux, Apache cơ bản 
- SSH (Terminal / PuTTY) 
- MySQL 
- Source code PHP

#### Mô tả kiến trúc
Thành phần hệ thống:
- EC2: Chạy ứng dụng 
- RDS: Database 
- S3: File tĩnh 
Luồng: Client → EC2 → RDS → S3
Bảo mật:
- Security Group giới hạn port 
- IAM Role cho EC2 truy cập S3

#### Các bước thực hiện 
Bước 1: Thiết lập EC2
- Tạo EC2 
- Mở port 22, 80, 443 
- Cài Apache, PHP

Bước 2: Triển khai ứng dụng Web
- Upload code bằng SCP 
- Đưa vào /var/www/html 
- Restart Apache

Bước 3:
- Tạo RDS MySQL 
- Mở public access 
- Mở port 3306 
- Import database

Bước 4: Kết nối EC2 vào RDS
- Sửa config DB trong code 
- Test kết nối

Bước 5: Tích hợp S3
- Tạo S3 bucket 
- Upload file tĩnh 
- Sửa code load từ S3

Bước 6: IAM Policy (Tùy chọn, nhưng khuyến khích thực hiện)
Policy cho phép EC2 đọc file từ S3: 
```
{
    "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject"],
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

Bước 7: Kiểm thử & Xác minh
- Truy cập web 
- Test CRUD database 
- Kiểm tra load ảnh từ S3
  
Bước 8: Clean-up
- Xóa EC2 
- Xóa RDS 
- Xóa S3 
- Dọn tài nguyên

#### Nội dung

1. [Hình thức và công cụ làm project](4.1-format_and_tools/)
2. [Kiến trúc & Thiết kế kỹ thuật](4.2-architecture/)
3. [Triển khai](4.3-implementation/4.3.1-prerequisite/)
4. [Kiểm thử & Đo lường](4.4-testing/)
5. [Tối ưu & Clean-up](4.5-optimization/)
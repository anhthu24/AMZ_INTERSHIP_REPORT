---
title : "Điều kiện tiên quyết"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b>4.3.1. </b> "
---

Trước khi bắt đầu triển khai và thực hiện lab, cần chuẩn bị các điều kiện sau:
- **Tài khoản AWS:** Cần có tài khoản AWS hợp lệ để sử dụng và quản lý các dịch vụ như EC2, RDS và S3. 
- **Region:** Hệ thống được triển khai tại **ap-southeast-2 (Sydney)** nhằm đảm bảo tính ổn định và tương thích dịch vụ. 
- **Công cụ sử dụng:**
  - AWS Management Console (giao diện chính để cấu hình tài nguyên) 
  - SSH (Git Bash / Terminal) để kết nối vào EC2 
  - SCP để truyền source code từ máy local lên server 
  - Composer để cài đặt AWS SDK cho PHP (dùng cho S3) 
- **Quyền IAM cần thiết:**
  - Toàn quyền EC2 
  - Toàn quyền RDS 
  - Toàn quyền S3 
  - Quyền tạo Access Key trong IAM 


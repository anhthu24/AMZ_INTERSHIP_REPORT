---
title : "Kiến trúc và thiết kế kỹ thuật"
date : 2026/04/27 
weight : 2
chapter : false
pre : " <b> 4.2. </b> "
---

**Thiết kế kiến trúc:** Hệ thống theo mô hình 3-tier gồm tầng web (EC2), tầng dữ liệu (RDS) và tầng lưu trữ (S3). Có sơ đồ mô tả luồng dữ liệu. 

![architecture](../../../images/4.2-Architecture/architecture.png)


Dịch vụ sử dụng: 
* EC2: Chạy ứng dụng PHP 
* RDS: Database MySQL 
* S3: Lưu file tĩnh 

![server](../../../images/4.2-Architecture/server.png)

Lý do lựa chọn: Dễ triển khai, có managed service, chi phí hợp lý và phù hợp web truyền thống. 
Bảo mật & IAM: 
* Dùng Security Group để giới hạn truy cập 
* Áp dụng nguyên tắc least privilege 
* Không hard-code thông tin nhạy cảm 

Khả năng mở rộng: 
* Có thể scale bằng cách nâng cấp EC2 hoặc thêm Load Balancer 
* Theo dõi hệ thống qua log và test
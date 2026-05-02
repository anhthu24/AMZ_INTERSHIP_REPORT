---
title : "Hướng dẫn triển khai chi tiết"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b>4.3.2. </b> "
---

Quy trình triển khai bao gồm các bước sau:
- Bước 1: Tạo EC2 (server chạy web)
- Bước 2: SSH + Cài đặt Apache + PHP
- Bước 3: Upload code lên EC2
- Bước 4: Copy vào web root
- Bước 5: Kết nối cơ sở dư liệu (RDS)
- Bước 6: S3 (upload ảnh)

#### Tạo EC2 Instance (Web Server)

**Mục tiêu**
Tạo 1 server trên Amazon Web Services để:
- Chạy web PHP của bạn 
- Sau này deploy code lên

**Cách làm chi tiết**
1. Vào EC2
- Login AWS 
- Tìm: EC2 
- Click: Launch Instance

2. Đặt tên
Khởi động và đặt tên cho instance
Name: classic-groove-server

![launch ec2](../../../../images/4.3-Implementation/3-3.png)


3. Chọn hệ điều hành (QUAN TRỌNG)
Chọn: Amazon Linux 2

![ami](../../../../images/4.3-Implementation/3-4.png)

4. Chọn cấu trúc máy
**Instance type**: t3.micro; Free tier (không tốn tiền)

![instance-type-ec2](../../../../images/4.3-Implementation/3-5.png)

1. Tạo key (để SSH)
Click: **Create new key pair**
Điền: 
- Name: aws-key
- Type: .pem
Download file về (Đây là file **QUAN TRỌNG** cần lưu ý cẩn thận).

![key-pair](../../../../images/4.3-Implementation/3-6.png)

6. Network settings
Tick:
- Allow HTTP traffic 
- Allow HTTPS traffic 

SSH:
- Để mặc định (My IP) 

AWS sẽ tự tạo Security Group cho bạn luôn


![sg-auto](../../../../images/4.3-Implementation/3-7.png)

7. Storage
Giữ nguyên: 8GB

8. Launch
Click: Launch Instance
Kết quả:

![sucess1](../../../../images/4.3-Implementation/3-8.png)

#### SSH + Install Apache + PHP

1. SSH vào server
Mở terminal (hoặc Git Bash)
- Bước 1: Di chuyển đến file .pem (Ví dụ (Windows Git Bash):  ```cd Downloads``` )
- Bước 2: Set quyền cho key
```chmod 400 aws-key.pem``` 
- Bước 3: SSH vào server
```ssh -i aws-key.pem ec2-user@<public-ip>```

![3-9](../../../../images/4.3-Implementation/3-9.png)

2. Cập nhật server
   
```sudo dnf update -y```

3. Cài Apache + PHP

```sudo dnf install httpd php php-mysqlnd -y```

![3-9](../../../../images/4.3-Implementation/3-9.png)

4. Bật Apache

```sudo systemctl start httpd```
```sudo systemctl enable httpd```

5. Test server chạy chưa
Mở trình duyệt: http://<public-ip>
**Kết quả đúng**
Bạn sẽ thấy: Trang Apache Test Page  => Nghĩa là: Server chạy web OK
Ví dụ: http://13.211.255.184

![3-10](../../../../images/4.3-Implementation/3-10.png)

#### Upload code lên EC2

Cách dễ nhất: dùng scp
- Bước 1: Mở terminal ở máy bạn (không phải trong EC2)
- Bước 2: Nhập lệnh upload:
```scp -i aws-key.pem -r Classic-Groove ec2-user@13.211.255.184:/home/ec2-user/```

Giải thích:
- Classic-Groove = folder project của bạn 
- /home/ec2-user/ = nơi lưu trên server

**Kết quả mong đợi:** Source code của dự án được chuyển thành công từ máy local lên EC2 instance.

#### Copy vào web root

Quay lại EC2 (SSH)
- Bước 1: Chạy sudo cp -r ~/Classic-Groove-main/* /var/www/html/
- Bước 2: Fix quyền sudo chmod -R 777 /var/www/html
- Bước 3: Test Mở trình duyệt: http://13.211.255.184

**Kết quả mong đợi:** Ứng dụng web được triển khai thành công và có thể truy cập thông qua địa chỉ IP công khai.

![3-11](../../../../images/4.3-Implementation/3-11.png)

- **Tóm tắt**: Hệ thống đã sử dụng thành công Amazon EC2 làm máy chủ web để chạy ứng dụng PHP. EC2 được cấu hình với Apache và các thư viện cần thiết, cho phép triển khai và truy cập ứng dụng thông qua Public IP. Giải pháp này đảm bảo môi trường linh hoạt và có khả năng mở rộng cho hệ thống.

#### Connect database (RDS)

- [**Phần 1: Tạo database (RDS - MySQL)**]
Create database → chọn Full configuration
- Bước 1: Chọn engine
  + Engine options → Chọn MySQL

![3-12](../../../../images/4.3-Implementation/3-12.png)

  + Version → Giữ mặc định (không cần đổi)

- Bước 2: Template (Chọn Free tier)

![3-13](../../../../images/4.3-Implementation/3-13.png)

- Bước 3: DB Setting
  + DB instance identifier → Nhập: classic-groove-db

![3-14](../../../../images/4.3-Implementation/3-14.png)

  + Master username → Nhập: admin
  + Passwork → Tự đặt (ví dụ: 12345678)

- Bước 4: Instance config → Chọn: db.t3.micro

- Bước 5: Storage → Giữ nguyên: 20GB

- Bước 6: Connectivity
  + Public access → Chọn Yes
  + VPC security → Chọn: Create new
  + Tên Security Group → classic-groove-db-sg

![3-15](../../../../images/4.3-Implementation/3-15.png)

- Bước 7: Additional config
  + Initial database name → Nhập: classic_groove

![3-16](../../../../images/4.3-Implementation/3-16.png)

- Bước 8: Create
Kéo xuống dưới → chọn: Create database → Sau đó chờ 3-5 phút

![3-17](../../../../images/4.3-Implementation/3-17.png)

- [**Phần 2: Mở port database**]
Vào: 
- RDS → chọn DB
- Click Security Group → **Edit inbound rules**

![3-18](../../../../images/4.3-Implementation/3-18.png)

Thêm:

| Type     | Port       | Source                |
|   -----  |------------|-----------------------|
|   MySQL  |    3306    |  EC2 security group   |

Hoặc tạm thời: 0.0.0.0/0 (để test)

![3-19](../../../../images/4.3-Implementation/3-19.png)

- [**Phần 3: Connect từ EC2**]
- Cài MySQL client
Trong EC2: ```sudo dnf install mysql -y```
- Connect: ```mysql -h <RDS-endpoint> -u admin -p```

Ví dụ: ```mysql -h classic-groove-db.czuaak8esyxf.ap-southeast-2.rds.amazonaws.com -u admin -p```

- → Nhập Password

- [**Phần 4: Import database**]
Cách đưa DB tiwf máy lên RDS

- Cách 1 (dùng phpMyAdmin)
Vào: http://localhost.phpmyadmin → Chọn database của bạn (ví dụ: classic-groove) → Bấm: **Export** - Chọn **Quick** - Format: **SQL** → Download file: classic-groove.sql

- Cách 2 (dùng command) 

```mysqldump -u root -p classic_groove > classic-groove.sql```

- Upload file SQL lên EC2
```scp -i aws-key.pem classic-groove.sql ec2-user@13.211.255.184:/home/ec2-user/```
- Import lên RDS
```mysql -h <endpoint> -u admin -p classic_groove < classic-grgr```

Ví dụ: 
```mysql -h classic-groove-db.czuaak8esyxf.ap-southeast-2.rds.amazonaws.com -u admin -p```

- [**Phần 5: Sửa code**]

Tìm file config DB (ví dụ là dataProvider.php) 
Chuyển vô file để sửa code: 
```sudo nano /var/www/html/util/dataProvider.php```
Sửa:
```
public static function excuteQuery($sql)
{
    $connection = mysqli_init();
    mysqli_real_connect(
       $connection,
       "classic-groove-db.czuaak8esyxf.ap-southeast-2.rds.amazonaws.com",
       "admin",
       "7112311496",
       "classic_groove",
       3306,
       NULL,
       MYSQLI_CLIENT_SSL
    );

    if (!$connection) {
      die("Connect failed: " . mysqli_connect_error());
    }

    mysqli_set_charset($connection, "utf8mb4");

    $result = mysqli_query($connection, $sql);

    if (!$result) {
      die("SQL: " . $sql . " | ERROR: " . mysqli_error($connection));
    }

    mysqli_close($connection);

    return $result;
}
```

Sau khi xong thì lưu file
- Ctrl + O → Enter
- Ctrl + X

- [**Phần 6: Restart**]
```sudo systemctl restart httpd```

**Tóm tắt RDS:** Hệ thống đã tích hợp thành công Amazon RDS (MySQL) làm cơ sở dữ liệu. Dữ liệu được lưu trữ và quản lý trên RDS, và ứng dụng trên EC2 kết nối đến database thông qua endpoint. Giải pháp này giúp tăng độ tin cậy, khả năng mở rộng và tách biệt giữa tầng ứng dụng và tầng dữ liệu.

#### Upload ảnh
Mục tiêu khi user upload ảnh:
- KHÔNG lưu ảnh trong server EC2 
- KHÔNG lưu path local 
- Upload lên Amazon S3 
- Lấy URL S3 
- Lưu URL vào Database 
- Hiển thị ảnh trực tiếp từ S3

1. Truy cập AWS → chọn **Amazon S3** → nhấn **Create bucket**
2. Cấu hình bucket: 
+ Bucket namespace: Chọn Global namespaces
+ Bucket name: classic-groove-images
+ Object Ownership: Chọn ACLs disabled (recommended)

![3-21-1](../../../../images/4.3-Implementation/3-21-1.png)
![3-21-2](../../../../images/4.3-Implementation/3-21-2.png)

3. Các cấu hình khác
+ Bucket Versioning: Disable
+ Encryption type: giữ mặc định (SSE-S3)
+ Bucket Key: Disable

![3-22-1](../../../../images/4.3-Implementation/3-22-1.png)
![3-22-2](../../../../images/4.3-Implementation/3-22-2.png)

4. Nhấn **Create bucket**

![3-23](../../../../images/4.3-Implementation/3-23.png)

Bước 2: Cấp quyền public
Vào bucket → Permissions → Bucket policy (Tab Permissions của bucket classic-groove-images)

![3-24](../../../../images/4.3-Implementation/3-24.png)

Nhấn vào Edit

![3-25](../../../../images/4.3-Implementation/3-25.png)

Dán policy này:

![3-26](../../../../images/4.3-Implementation/3-26.png)

Rồi bấm **Save changes**, nó sẽ hiện ra:

![3-27](../../../../images/4.3-Implementation/3-27.png)

Bước 3: Tạo AWS Key

1. Vào AWS → tìm: IAM
2. Chọn User, rồi bấm Create User
3. Nhập User name, rồi bấm Next

![3-28](../../../../images/4.3-Implementation/3-28.png)

4. Chọn Attach policies directly → Sau đó, tìm và tick Attach policies directly

![3-29-1](../../../../images/4.3-Implementation/3-29-1.png)
![3-29-2](../../../../images/4.3-Implementation/3-29-2.png)

5. Create user

![3-30](../../../../images/4.3-Implementation/3-30.png)

6. Vào user vừa tạo
Nhấn tab Security credentials
Bấm: Create access key, sau đó tick **Application running outside AWS**
Bấm Next → Create

![3-31](../../../../images/4.3-Implementation/3-31.png)

Copy AWS key (key sẽ được hiển thị một lần duy nhất ở màn hình này)

![3-32](../../../../images/4.3-Implementation/3-32.png)

Bước 4: Kết nối PHP với Amazon S3

***4.1. Cài AWS SDK cho PHP***

Trên EC2 chạy:
```
cd /var/www/html
composed require aws/aws-sdk-php
```
***4.2. Tạo file upload - upload.php***
```
cd /var/www/html
nano upload.php
```

Dán code này vào file:
```
<?php
require 'vendor/autoload.php';

use Aws\S3\S3Client;

$s3 = new S3Client([
    'version' => 'latest',
    'region'  => 'ap-southeast-2',
    'credentials' => [
        'key'    => 'YOUR_KEY',
        'secret' => 'YOUR_SECRET',
    ]
]);

$bucket = 'classic-groove-images';

if(isset($_FILES['image'])){
    $file = $_FILES['image']['tmp_name'];
    $name = time() . '_' . $_FILES['image']['name'];

    try {
        $result = $s3->putObject([
            'Bucket' => $bucket,
            'Key'    => $name,
            'SourceFile' => $file
        ]);

        echo $result['ObjectURL'];
    } catch (Exception $e) {
        echo "Error: " . $e->getMessage();
    }
}
```

Thay YOUR-KEY, YOUR_SECRET bằng AWS key bạn vừa tạo ở Bước 3
**TEST NGAY:** Mở trình duyệt http://13.211.255.182/upload.php

![3-33](../../../../images/4.3-Implementation/3-33.png)

Nó sẽ hiện trang trắng (Bình thường)

![3-34](../../../../images/4.3-Implementation/3-34.png)

***4.3. Tạo form Test Upload***
Tạo thêm file test.html:
```
<form action="upload.php" method="POST" enctype="multipart/form-data">
  <input type="file" name="image">
  <button type="submit">Upload</button>
</form>
```
Mở: http://13.211.255.184/test.html
Chọn ảnh rồi upload:

![3-35](../../../../images/4.3-Implementation/3-35.png)

Kết quả: Nếu đúng sẽ trả về link: https://classic-groove-images.s3.ap-southeast-2.amazonaws.com/xxx.jpg

![3-34](../../../../images/4.3-Implementation/3-34.png)

Bước 5: Gắn upload S3 vào project classic-groove
***5.1: Sửa form thêm album***
- File views/pages/admin/modalBox.php

```
<form id="form-add-album" enctype="multipart/form-data">
  <input type="text" name="albumName" placeholder="Album name">  
  <input type="file" name="image" id="album-image">
  <button type="submit">Add</button>
</form>
```

***5.2: Upload ảnh trước bằng AJAX***
- Bỏ vào file: controllers/albumController.js
```
$("#form-add-album").submit(function (e) {
  e.preventDefault();

  let formData = new FormData();
  let file = $("#album-image")[0].files[0];

  formData.append("image", file);

  //  UPLOAD S3 TRƯỚC
  $.ajax({
    url: "upload.php",
    type: "POST",
    data: formData,
    processData: false,
    contentType: false,
    success: function (imageUrl) {

      console.log("S3 URL:", imageUrl);

      //  Gửi data + link ảnh vào DB
      addAlbum(imageUrl);
    }
  });
});

```

***5.3: Gửi link S3 về backend***
- Bỏ vào file: albumController.js

```
function addAlbum(imageUrl) {
  let name = $("input[name='albumName']").val();

  $.ajax({
    url: "util/album.php",
    type: "POST",
    data: {
      action: "add",
      name: name,
      albumImage: imageUrl //  LINK S3
    },
    success: function (res) {
      alert("Add success!");
      location.reload();
    }
  });
}
```

***5.4: Lưu vào cơ sở dữ liệu***
- Bỏ vào File: util/album.php

```
case 'add':
  $name = $_POST['name'];
  $image = $_POST['albumImage'];

  $sql = "INSERT INTO album (tenAlbum, hinhAnh)
          VALUES ('$name', '$image')";

  $dp->excuteQuery($sql);

  echo "success";
  break;
```

Database chỉ lưu URL:
+ Không lưu file
+ Không lưu path local

***5.5: Hiển thị ảnh từ S3***
- Thêm vào 2 file này: views/pages/user/home.php, views/pages/admin/productManager.php

```<img src="<?= $row['hinhAnh'] ?>" width="150">```

Kết quả: 
+ Upload ảnh lên S3
+ Nhận URL 
+ Lưu DB 
+ Load ảnh trực tiếp từ S3

Suy ra: User upload → S3 lưu file → PHP lấy URL → DB lưu URL → web load ảnh từ URL

Khi upload thành công link trả về:
https://classic-groove-images.s3.ap-southeast-2.amazonaws.com/xxx.jpg

![3-35](../../../../images/4.3-Implementation/3-35.png)

**Tóm tắt:** Hệ thống đã tích hợp thành công Amazon S3 để lưu trữ hình ảnh. Các hình ảnh sau khi upload được lưu dưới dạng object trên S3 và truy cập thông qua URL công khai. Giải pháp này giúp loại bỏ việc lưu trữ trên server EC2, tăng khả năng mở rộng và cải thiện hiệu suất khi xử lý tài nguyên tĩnh trong hệ thống.












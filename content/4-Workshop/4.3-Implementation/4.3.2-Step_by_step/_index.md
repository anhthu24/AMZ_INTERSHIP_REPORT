---
title : "Step-by-step"
date : 2026/04/27 
weight : 2
chapter : false
pre : " <b>4.3.2. </b> "
---

The deployment process includes the following steps:
- Step 1: Create EC2 (Web Server)
- Step 2: SSH & Install Apache + PHP
- Step 3: Upload Code to EC2
- Step 4: Copy to Web Root
- Step 5: Connect Database (RDS)
- Step 6: S3 (Image Upload)

#### Create EC2 (Web Server)

**Objective**
Create a virtual server on Amazon Web Services to:
- Host and run the PHP web application 
- Serve as a deployment environment for the project

**Detailed Steps**
1. Access EC2 Service 
- Log in to AWS Management Console 
- Search for EC2 
- Click Launch Instance 

2. Set Instance Name 
- Name: classic-groove-server 

![launch ec2](../../../images/4.3-Implementation/3-3.png?width=100px)


3. Choose Operating System (Important) 
Select: Amazon Linux 2 
![ami](../../../images/4.3-Implementation/3-4.png)


4. Choose Instance Type 
- **Instance type:** t3.micro; Eligible for Free Tier (no cost) 

![instance-type-ec2](../../../images/4.3-Implementation/3-5.png)

5. Create Key Pair (for SSH access) 
- Click: **Create new key pair**
- Configuration: 
- Name: aws-key 
- Type: .pem 
- Download the key file and store it securely (**IMPORTANT** for SSH access) 

![key-pair](../../../images/4.3-Implementation/3-6.png)

6. Configure Network Settings 
- Enable: 
- Allow HTTP traffic (port 80) 
- Allow HTTPS traffic (port 443) 
- SSH: 
- Keep default setting (My IP) 
- AWS will automatically create a Security Group 

![sg-auto](../../../images/4.3-Implementation/3-7.png)

7. Configure Storage 
- Keep default: 8 GB 

8. Launch Instance 
- Click: Launch Instance

![sucess1](../../../images/4.3-Implementation/3-8.png)

#### SSH + Install Apache + PHP

1. Connect to EC2 via SSH
Open terminal (or Git Bash)
- Step 1: Navigate to the directory containing the .pem (Example (Windows Git Bash):  ```cd Downloads``` )

- Step2: Set permission for the key file
```chmod 400 aws-key.pem``` 

- Step 3: Connect to the EC2 instance
```ssh -i aws-key.pem ec2-user@<public-ip>```

![3-9](../../../images/4.3-Implementation/3-9.png)

2. Update the system
   
```sudo dnf update -y```

3. Install Apache and PHP

```sudo dnf install httpd php php-mysqlnd -y```

4. Start and enable Apache service

```sudo systemctl start httpd```
```sudo systemctl enable httpd```

5. Verify web server
Open browser: http://<public-ip>

**Expected result**: The Apache Test Page is displayed, indicating that the web server is running successfully.
Example: http://13.211.255.184

![3-10](../../../images/4.3-Implementation/3-10.png)

#### Upload code to EC2

The easiest way to upload source code is by using SCP (Secure Copy Protocol).
- Step 1: Open terminal on your local machine (not inside the EC2 instance). 
- Step 2: Execute the following command to upload the project: 
```scp -i aws-key.pem -r Classic-Groove ec2-user@13.211.255.184:/home/ec2-user/```

- Explanation: 
  + Classic-Groove: the project folder on the local machine 
  + /home/ec2-user/: destination directory on the EC2 server 

**Expected result:** The project source code is successfully transferred from the local machine to the EC2 instance.

#### Copy to web root

Return to the EC2 instance via SSH and deploy the application to the web root directory.
- Step 1: Run the following command to copy source code to the Apache web directory: ```sudo cp -r ~/Classic-Groove-main/* /var/www/html/```
- Step 2: Set appropriate permissions:  ```sudo chmod -R 777 /var/www/html```
- Step 3: Verify the deployment. 
- Open a web browser and access: http://13.211.255.184

**Expected result:** The web application is successfully deployed and accessible via the public IP address.

![3-11](../../../images/4.3-Implementation/3-11.png)

- **Summary Session**: The system successfully utilizes Amazon EC2 as a web server to host the PHP application. The EC2 instance is configured with Apache and required dependencies, allowing the application to be deployed and accessed via public IP. This ensures a flexible and scalable environment for running the web application.

#### Connect database (RDS)

- [**Part 1: Create database (RDS - MySQL)**]

Create database → select **Full configuration**
- Step 1: Select engine
  + Engine options → select MySQL

![3-12](../../../images/4.3-Implementation/3-12.png)

  + Version → Keep default (no change required)

- Step 2: Template (select Free tier)

![3-13](../../../images/4.3-Implementation/3-13.png)

- Step 3: DB Setting
  + DB instance identifier → Enter: classic-groove-db

![3-14](../../../images/4.3-Implementation/3-14.png)

  + Master username → Enter: admin
  + Passwork → Set manually (example: 12345678)

- Step 4: Instance config → Select: db.t3.micro

- Step 5: Storage → Keep default: 20GB

- Step 6: Connectivity
  + Public access → Select Yes
  + VPC security group → Select: **Create new**
  + Security Group name → classic-groove-db-sg

![3-15](../../../images/4.3-Implementation/3-15.png)

- Step 7: Additional config
  + Initial database name → Enter: classic_groove

![3-16](../../../images/4.3-Implementation/3-16.png)

- Step 8: Create
Scroll down → select: **Create database** → Then wait 3-5 minutes

![3-17](../../../images/4.3-Implementation/3-17.png)

- [**Part 2: Open port database**]

Go to: 
- RDS → select DB
- Click Security Group → **Edit inbound rules**

![3-18](../../../images/4.3-Implementation/3-18.png)

Add:

| Type     | Port       | Source                |
|   -----  |------------|-----------------------|
|   MySQL  |    3306    |  EC2 security group   |

Or temporarily: 0.0.0.0/0 (for testing)

![3-19](../../../images/4.3-Implementation/3-19.png)

- [**Part 3: Connect from EC2**]

- Install MySQL client. On EC2: ```sudo dnf install mysql -y```
- Connect: ```mysql -h <RDS-endpoint> -u admin -p```

Example: ```mysql -h classic-groove-db.czuaak8esyxf.ap-southeast-2.rds.amazonaws.com -u admin -p```

- → Enter Password

![3-20](../../../images/4.3-Implementation/3-20.png)

- [**Part 4: Import database**]

Export database from machine to RDS

- Method 1 (phpMyAdmin)
Access: http://localhost.phpmyadmin → Select your database (ví dụ: classic-groove) → Click: **Export** - Select **Quick** - Format: **SQL** → Download file: classic-groove.sql

- Method 2 (command line) 

```mysqldump -u root -p classic_groove > classic-groove.sql```

- Upload file SQL to EC2
```scp -i aws-key.pem classic-groove.sql ec2-user@13.211.255.184:/home/ec2-user/```

- Import to RDS
```mysql -h <endpoint> -u admin -p classic_groove < classic-grgr```

Example: 
```mysql -h classic-groove-db.czuaak8esyxf.ap-southeast-2.rds.amazonaws.com -u admin -p```

- [**Part 5: Fix code**]

Find database configuration file (e.g. dataProvider.php) 

Open file: ```sudo nano /var/www/html/util/dataProvider.php```

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

Save file:
- Ctrl + O → Enter
- Ctrl + X

- [**Part 6: Restart**]
```sudo systemctl restart httpd```

- **Summary RDS:** The system successfully integrates Amazon RDS (MySQL) as the database layer. Data is stored and managed on RDS, and the EC2 application connects to the database securely via endpoint. This approach improves data reliability, scalability, and separates the database from the application layer.

#### Upload image

When users upload images:
- DO NOT store images on EC2 server 
- DO NOT store local file paths 
- Upload to Amazon S3 
- Retrieve S3 URL 
- Store URL in the database 
- Display images directly from S3

**Step 1: Tạo bucket trên Amazon S3**

1. Access AWS → select **Amazon S3** → click **Create bucket**

2. Configure bucket: 
- Bucket namespace: Global namespace 
- Bucket name: classic-groove-images 
- Object Ownership: ACLs disabled (recommended) 

![3-21-1](../../../images/4.3-Implementation/3-21-1.png)
![3-21-2](../../../images/4.3-Implementation/3-21-2.png)

3. Other configurations: 
- Bucket Versioning: Disable 
- Encryption type: Default (SSE-S3) 
- Bucket Key: Disable 

![3-22-1](../../../images/4.3-Implementation/3-22-1.png)
![3-22-2](../../../images/4.3-Implementation/3-22-2.png)

4. Click **Create bucket**

![3-23](../../../images/4.3-Implementation/3-23.png)


**Step 2: Grant public access**

Go to bucket → **Permissions** → **Bucket policy** (Permissions tab of bucket classic-groove-images)

![3-24](../../../images/4.3-Implementation/3-24.png)

Click Edit

![3-25](../../../images/4.3-Implementation/3-25.png)

Paste the following policy:

![3-26](../../../images/4.3-Implementation/3-26.png)

Click **Save changes**, then the system will display

![3-27](../../../images/4.3-Implementation/3-27.png)

**Step 3:** Create AWS Key

1. Go to AWS → search: IAM 
2. Select User → click Create User 
3. Enter User name → click Next 

![3-28](../../../images/4.3-Implementation/3-28.png)

4. Select Attach policies directly → Search and select approproate policies.

![3-29-1](../../../images/4.3-Implementation/3-29-1.png)
![3-29-2](../../../images/4.3-Implementation/3-29-2.png)

5. Click **Create user**

![3-30](../../../images/4.3-Implementation/3-30.png)

6. Open the created user
Go to Security credentials tab
Click **Create access key**, then select **Application running outside AWS**
Click Next → Create

![3-31](../../../images/4.3-Implementation/3-31.png)

Copy AWS key (displayed only once)

![3-32](../../../images/4.3-Implementation/3-32.png)

**Step 4: Connect PHP and Amazon S3**

***4.1. Install AWS SDK for PHP***

On EC2:
```
cd /var/www/html
composed require aws/aws-sdk-php
```
***4.2. Create file upload - upload.php***
```
cd /var/www/html
nano upload.php
```

Paste the following code:
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

Replace YOUR-KEY, YOUR_SECRET with your AWS credentials from Step 3

**TEST:** Open browser: http://13.211.255.182/upload.php → A blank page is displayed (normal behavior)

***4.3. Create test upload form***
Create file test.html:
```
<form action="upload.php" method="POST" enctype="multipart/form-data">
  <input type="file" name="image">
  <button type="submit">Upload</button>
</form>
```

Open: http://13.211.255.184/test.html

Select image and upload

![3-33](../../../images/4.3-Implementation/3-33.png)

Expacted result: A URL is returned https://classic-groove-images.s3.ap-southeast-2.amazonaws.com/xxx.jpg

![3-34](../../../images/4.3-Implementation/3-34.png)

**Step 5: Attach S3 upload to the project classic-groove**

***5.1. Modify add album form File views/pages/admin/modalBox.php***

```
<form id="form-add-album" enctype="multipart/form-data">
  <input type="text" name="albumName" placeholder="Album name">  
  <input type="file" name="image" id="album-image">
  <button type="submit">Add</button>
</form>
```

***5.2. Upload image via AJAX first → file: controllers/albumController.js***

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

***5.3. Send S3 URL to backend → file: albumController.js***

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

***5.4. Store in database → File: util/album.php***

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

Database stores only URL:
* No file storage 
* No local path

***5.5. Display image from S3***

Add to: 
- views/pages/user/home.php
- views/pages/admin/productManager.php

```<img src="<?= $row['hinhAnh'] ?>" width="150">```

Result: 
- Upload image to S3 
- Receive URL 
- Store in database 
- Display image directly from S3 

Conclusion: User upload → S3 stores file → PHP retrieves URL → DB stores URL → Web loads image from URL

Successful upload URL: https://classic-groove-images.s3.ap-southeast-2.amazonaws.com/xxx.jpg

![3-35](../../../images/4.3-Implementation/3-35.png)


**Conclusion:** The system successfully integrates Amazon S3 for image storage. Uploaded images are stored as objects in S3 and accessed via public URLs. This approach eliminates local server storage, improves scalability, and enhances performance for handling static assets in the system.
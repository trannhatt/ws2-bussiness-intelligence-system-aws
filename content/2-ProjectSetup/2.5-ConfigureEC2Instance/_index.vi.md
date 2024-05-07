---
title: "Cấu hình EC2 Instance"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: " <b> 2.5 </b> "
---

### Cấu hình EC2 Instance

Chúng ta sẽ cấu hình các instance EC2 để truy cập và điều khiển các tài nguyên AWS khác như sau:

1. Đăng nhập vào EC2 instance vừa tạo thông qua giao thức SSH:

```shell script
ssh -i "<Key pair name>" ec2-user@<Public IP>
```

![Configure EC2 Instance](/ws2-bussiness-intelligence-system-aws/images/2.5-configureEC2Instance/0001-configureec2instance.png?featherlight=false&width=70pc)

2. Tải mã nguồn của dự án về:

```shell script
wget 'https://github.com/trannhatt/Analytics-on-AWS-Build-BI-System/archive/refs/heads/main.zip'
```

3. Giải nén mã nguồn đã tải:

```shell script
unzip -u main.zip
```

![Configure EC2 Instance](/ws2-bussiness-intelligence-system-aws/images/2.5-configureEC2Instance/0002-configureec2instance.png?featherlight=false&width=70pc)

4. Liệt kê các tệp và thư mục hiện có theo định dạng danh sách:

```shell script
ls -l
```

5. Cấp quyền thực thi cho tập lệnh:

```shell script
chmod +x ./Analytics-on-AWS-Build-BI-System-main/set-up-hands-on-lab.sh
```

![Configure EC2 Instance](/ws2-bussiness-intelligence-system-aws/images/2.5-configureEC2Instance/0003-configureec2instance.png?featherlight=false&width=70pc)

6. Thực thi tập lệnh thiết lập để cài đặt môi trường:

```shell script
./Analytics-on-AWS-Build-BI-System-main/set-up-hands-on-lab.sh
```

7. Đảm bảo rằng các tập tin cần thiết cho dự án được tạo ra bình thường sau khi thực thi tập lệnh thiết lập: Bằng cách kiểm tra xem mã nguồn và các tập tin cần thiết đã tồn tại bằng lệnh.

```shell script
ls -l
```

![Configure EC2 Instance](/ws2-bussiness-intelligence-system-aws/images/2.5-configureEC2Instance/0004-configureec2instance.png?featherlight=false&width=70pc)

8. Thực thi lệnh để chúng ta có thể truy cập các tài nguyên AWS: Từ IAM User được tạo trước đó, chúng ta sẽ kiểm tra **Access key ID** và **Secret access key**, và nhập chúng theo yêu cầu.

```shell script
aws configure
```

![Configure EC2 Instance](/ws2-bussiness-intelligence-system-aws/images/2.5-configureEC2Instance/0005-configureec2instance.png?featherlight=false&width=70pc)

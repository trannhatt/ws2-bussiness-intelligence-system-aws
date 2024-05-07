---
title: "Khởi chạy EC2 Instance"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 2.4 </b> "
---

### Khởi chạy EC2 Instance

1. Truy cập vào giao diện EC2 và chọn Launch instances:
   - Chọn **Instances**.
   - Sau đó chọn **Launch instances**.

![Create EC2 Instance](/images/2.4-createEC2Instance/0001-createec2instance.png?featherlight=false&width=70pc)

2. Cấu hình EC2 Instance:
   - Trong giao diện **Launch an instance**:
     - Tại mục **Name and tags**, nhập **`basion-host-bi-system`**.
     - Tại mục **Application and OS Images (Amazon Machine Image)**, chọn **AmazonLinux**.

![Create EC2 Instance](/images/2.4-createEC2Instance/0002-createec2instance.png?featherlight=false&width=70pc)

3. Tiếp tục cấu hình:
   - Tại mục **Instance type**, chọn **t2.micro**.
   - Tại mục **Key pair (login)**, chọn **analytics-hol-ws2**.

![Create EC2 Instance](/images/2.4-createEC2Instance/0003-createec2instance.png?featherlight=false&width=70pc)

{{% notice note %}}
Lưu ý: Nếu bạn chưa có Key pair chọn **Create new key pair**.
{{% /notice %}}

![Create EC2 Instance](/images/2.4-createEC2Instance/0004-createec2instance.png?featherlight=false&width=70pc)

4. Cấu hình Network settings:
   - Tại mục **VPC - required**, chọn **vpc-02e213a24e410c89 (project-businesss-intelligence-system-vpc)**.
   - Tại mục **Subnet**, chọn **subnet-Ofa8fc52157d75fba**.
   - Tại mục **Auto-assign public IP**, chọn **Enable**.
   - Tại mục **Firewall (security groups)**, chọn **Select existing security group** và chọn **basion-sg** và **use-es-cluster-sg**.

![Create EC2 Instance](/images/2.4-createEC2Instance/0005-createec2instance.png?featherlight=false&width=70pc)

5. Chọn Launch instance:
   - Các trường thông tin còn lại để giá trị mặc định, cuối cùng chọn **Launch instance** để hoàn tất việc tạo máy chủ Bastion Host.

![Create EC2 Instance](/images/2.4-createEC2Instance/0006-createec2instance.png?featherlight=false&width=70pc)

6. EC2 Instance đã được tạo thành công:

![Create EC2 Instance](/images/2.4-createEC2Instance/0007-createec2instance.png?featherlight=false&width=70pc)
![Create EC2 Instance](/images/2.4-createEC2Instance/0008-createec2instance.png?featherlight=false&width=70pc)

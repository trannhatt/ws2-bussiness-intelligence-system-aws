---
title: "Tạo VPC"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2.2 </b> "
---

### Tạo VPC

{{% notice info %}}
Trong dự án này, chúng ta sẽ thực hiện trên Region **US East (N. Virginia) us-east-1**
{{% /notice %}}

1. Đăng nhập vào IAM User và chọn Region:
   - Đăng nhập vào IAM User đã tạo ở phần trước.
   - Chọn Region **US East (N. Virginia) us-east-1**.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0001-createvpc.png?featherlight=false&width=20pc)

2. Truy cập vào AWS Console và chọn VPC:
   - Nhấn chọn thanh tìm kiếm và nhập **`vpc`**.
   - Tại mục **Services** chọn **VPC**.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0002-createvpc.png?featherlight=false&width=70pc)

3. Tạo VPC mới:
   - Tại giao diện **VPC**, chọn **Your VPCs**.
   - Chọn **Create VPC**.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0003-createvpc.png?featherlight=false&width=70pc)

4. Thiết lập thông tin cho VPC:
   - Tại phần **Create VPC**, nhập các thông tin sau:
     - Tại mục **Resources to create**, nhấn chọn **VPC and more**.
     - Tại mục **Name tag auto-generation**, nhấn chọn **Auto-generate** và nhập **`project-businesss-intelligence-system`**.
     - Tại mục **IPv4 CIDR block**, nhập **`10.0.0.0/16`**.
     - Tại mục **IPv6 CIDR block**, nhấn chọn **Amazon-provided IPv6 CIDR block**.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0004-createvpc.png?featherlight=false&width=70pc)

5. Tiếp tục thiết lập:
   - Tại phần **Create VPC**, nhập các thông tin tiếp theo:
     - Tại mục **Number of Availability Zones (AZs)**, nhấn chọn **2**.
     - Tại mục **First availability zone**, chọn **us-east-1a**.
     - Tại mục **Second availability zone**, chọn **us-east-1b**.
     - Tại mục **Number of public subnets**, nhấn chọn **2**.
     - Tại mục **Number of private subnets**, nhấn chọn **2**.
     - Tại mục **Customize subnets CIDR blocks**, nhập lần lượt các dãi CIDR cho 4 Subnet: **`10.0.1.0/24`**, **`10.0.2.0/24`**, **`10.0.3.0/24`**, **`10.0.4.0/24`**.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0005-createvpc.png?featherlight=false&width=70pc)

6. Tiếp tục thiết lập:
   - Tại phần **Create VPC**, nhập các thông tin tiếp theo:
     - Tại mục **NAT gateways ($)**, nhấn chọn **In 1 AZ**.
     - Tại mục **Egress only internet gateway**, nhấn chọn **No**.
     - Tại mục **VPC endpoints**, nhấn chọn **None**.
     - Tại mục **DNS options**, nhấn chọn **Enable DNS hostnames** và **Enable DNS resolution**.
     - Cuối cùng, nhấn **Create VPC**.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0006-createvpc.png?featherlight=false&width=70pc)

7. Hoàn tất tạo VPC:
   - VPC đã được tạo thành công.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0007-createvpc.png?featherlight=false&width=70pc)

8. Xem thông tin chi tiết của VPC:
   - Chọn **View VPC**.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0008-createvpc.png?featherlight=false&width=70pc)

9. Xem tổng quát các tài nguyên trong VPC:
   - Chúng ta Có thể xem tổng quát các tài nguyên hiện có trong VPC qua phần **Resource map**.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0009-createvpc.png?featherlight=false&width=70pc)

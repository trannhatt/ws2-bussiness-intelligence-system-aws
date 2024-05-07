---
title: "Tạo Security Groups"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 2.3 </b> "
---

### Tạo Security Groups

1. Truy cập vào AWS Console và chọn EC2:
   - Nhấn chọn thanh tìm kiếm.
   - Nhập **`ec2`**.
   - Tại mục **Services** chọn **EC2**.

![Create Security Groups](/images/2.3-createSecurityGroup/0001-createsg.png?featherlight=false&width=70pc)

2. Tạo Security Group cho EC2 instance đóng vai trò là một bastion host:
   - Trong giao diện **EC2**, chọn **Security Group**.
   - Chọn **Create security group**.

![Create Security Groups](/images/2.3-createSecurityGroup/0002-createsg.png?featherlight=false&width=70pc)

3. Cấu hình Security Group:
   - Tại phần **Create security group**, nhập các thông tin sau:
     - **Security Group name**: `basion-sg`.
     - **Description**: `security group for bastion`.
     - **VPC**: `vpc-02e213a24e410c89 (project-businesss-intelligence-system-vpc)`.
     - Chọn **Add rule**, tại mục **Type**: chọn **SSH** và **Source**: chọn **Anywhere IPv4 (0.0.0.0/0)**.

![Create Security Groups](/images/2.3-createSecurityGroup/0003-createsg.png?featherlight=false&width=70pc)

4. Thêm tag cho Security Group:
   - Tại mục **Tags - optional**, chọn **Add new tag**:
     - **Key**: `Name`.
     - **Value - optional**: `basion-sg`.
   - Cuối cùng, chọn **Create security group**.

![Create Security Groups](/images/2.3-createSecurityGroup/0004-createsg.png?featherlight=false&width=70pc)

5. Security Group cho EC2 instance được tạo thành công:

![Create Security Groups](/images/2.3-createSecurityGroup/0005-createsg.png?featherlight=false&width=70pc)
![Create Security Groups](/images/2.3-createSecurityGroup/0006-createsg.png?featherlight=false&width=70pc)

Chúng ta sẽ tiếp tục tạo 2 Security Group để sử dụng cho OpenSearch Service.

6. Cấu hình Security Group cho OpenSearch Service:
   - Tại phần **Create security group**, nhập các thông tin sau:
     - **Security Group name**: `use-es-cluster-sg`.
     - **Description**: `security group for an es client`.
     - **VPC**: `vpc-02e213a24e410c89 (project-businesss-intelligence-system-vpc)`.
     - Bỏ qua phần **Inbound rules**.

![Create Security Groups](/images/2.3-createSecurityGroup/0007-createsg.png?featherlight=false&width=70pc)

7. Thêm tag cho Security Group:
   - Tại mục **Tags - optional**, chọn **Add new tag**:
     - **Key**: `Name`.
     - **Value - optional**: `use-es-cluster-sg`.
   - Cuối cùng, chọn **Create security group**.

![Create Security Groups](/images/2.3-createSecurityGroup/0008-createsg.png?featherlight=false&width=70pc)

8. Security Group được tạo thành công:

![Create Security Groups](/images/2.3-createSecurityGroup/0009-createsg.png?featherlight=false&width=70pc)
![Create Security Groups](/images/2.3-createSecurityGroup/0010-createsg.png?featherlight=false&width=70pc)

9. Tiếp tục cấu hình Security Group cho OpenSearch Service:
   - Tại phần **Create security group**, nhập các thông tin sau:
     - **Security Group name**: `es-cluster-sg`.
     - **Description**: `security group for an es cluster`.
     - **VPC**: `vpc-02e213a24e410c89 (project-businesss-intelligence-system-vpc)`.
     - Chọn **Add rule**, tại mục **Type**: chọn **AlL TCP** và **Source**: chọn **Custom (use-es-cluster-sg)**.

![Create Security Groups](/images/2.3-createSecurityGroup/0011-createsg.png?featherlight=false&width=70pc)

10. Thêm tag cho Security Group:
    - Tại mục **Tags - optional**, chọn **Add new tag**:
      - **Key**: `Name`.
      - **Value - optional**: `es-cluster-sg`.
    - Cuối cùng, chọn **Create security group**.

![Create Security Groups](/images/2.3-createSecurityGroup/0012-createsg.png?featherlight=false&width=70pc)

11. Security Group được tạo thành công:

![Create Security Groups](/images/2.3-createSecurityGroup/0013-createsg.png?featherlight=false&width=70pc)
![Create Security Groups](/images/2.3-createSecurityGroup/0014-createsg.png?featherlight=false&width=70pc)

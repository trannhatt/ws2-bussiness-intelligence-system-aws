---
title: "Tạo một IAM User"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 2.1 </b> "
---

### Tạo một IAM User

Trong phần này, chúng ta sẽ tạo một IAM User trên AWS Console để sử dụng trong dự án.

1. Truy cập vào AWS Console:
   - Đăng nhập vào AWS Console tại [https://console.aws.amazon.com/](https://console.aws.amazon.com/).
   - Nhấn vào thanh tìm kiếm và nhập `iam`.
   - Tại mục **Services** chọn **IAM**.

![Create IAM User](/ws2-bussiness-intelligence-system-aws/images/2.1-createIAMUser/0001-createiamuser.png?featherlight=false&width=70pc)

2. Tạo một IAM User:
   - Tại giao diện IAM, chọn **Users**.
   - Chọn **Create User**.

![Create IAM User](/ws2-bussiness-intelligence-system-aws/images/2.1-createIAMUser/0002-createiamuser.png?featherlight=false&width=70pc)

3. Xác định cấu hình thông tin của User:
   - Tại phần **Specify user details**:
     - Nhập tên cho User vào mục **User name** (ví dụ: `workshop2-user`).
     - Chọn **Provide user access to the AWS Management Console - optional**.
     - Tiếp tục nhấn chọn **I want to create an IAM user**.
     - Chọn **Custom password** và nhập mật khẩu cho IAM User của bạn vào mục **Console password**.
   - Sau đó, nhấn **Next** để tiếp tục.

![Create IAM User](/ws2-bussiness-intelligence-system-aws/images/2.1-createIAMUser/0003-createiamuser.png?featherlight=false&width=70pc)

4. Thiết lập quyền cho User:
   - Tại phần **Set permissions**:
     - Chọn **Attach policies directly** trong mục **Permissions options**.
     - Tìm kiếm và chọn policy **AdministratorAccess** trong mục **Permissions policies**.
   - Nhấn **Next** để tiếp tục.

![Create IAM User](/ws2-bussiness-intelligence-system-aws/images/2.1-createIAMUser/0004-createiamuser.png?featherlight=false&width=70pc)

5. Xác nhận và tạo User:
   - Tại phần **Review and create**:
     - Nhấn **Add new tag** để thêm một Tag mới.
     - Trong phần **Tags - optional**:
       - Nhập **`name`** vào mục **Key**.
       - Nhập **`workshop2-user`** vào mục **Value - optional**.
     - Cuối cùng, nhấn **Create user** để tạo User.

![Create IAM User](/ws2-bussiness-intelligence-system-aws/images/2.1-createIAMUser/0005-createiamuser.png?featherlight=false&width=70pc)

6. Hoàn tất việc tạo IAM User:
   - Bạn đã tạo thành công IAM User cho dự án.
   - Có thể chọn **Download .csv file** để tải thông tin đăng nhập của User về máy.
   - Chọn **Return to users list** để quay lại trang danh sách người dùng.

![Create IAM User](/ws2-bussiness-intelligence-system-aws/images/2.1-createIAMUser/0006-createiamuser.png?featherlight=false&width=70pc)

7. Kích hoạt MFA và đăng nhập lại:
   - Đăng suất khỏi tài khoản Root User, và đăng nhập lại vào tài khoản IAM User vừa tạo.
   - Trước khi sử dụng tài khoản IAM User, hãy kích hoạt **MFA** để bảo vệ tài khoản của bạn.

![Create IAM User](/ws2-bussiness-intelligence-system-aws/images/2.1-createIAMUser/0007-createiamuser.png?featherlight=false&width=70pc)

{{% notice note %}}
**MFA** (Multi-Factor Authentication) là một cơ chế bảo mật quan trọng giúp bảo vệ tài khoản bằng cách yêu cầu người dùng cung cấp hai hoặc nhiều loại thông tin xác thực để đăng nhập.
{{% /notice %}}

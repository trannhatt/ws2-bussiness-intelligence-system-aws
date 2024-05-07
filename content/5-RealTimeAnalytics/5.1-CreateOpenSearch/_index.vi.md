---
title: "Tạo Amazon OpenSearch Service"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---

### Tạo Amazon OpenSearch Service

1. Tại giao diện **AWS console**

   - Nhấn chọn thanh tìm kiếm và nhập **`opensearch`**
   - Tại mục **Services** chọn **Amazon OpenSearch Service**

![Create OpenSearch](/ws2-bussiness-intelligence-system-aws/images/5.1-CreateOpenSearch/createopensearch-0001.png?featherlight=false&width=70pc)

2. Từ giao diện **Amazon OpenSearch Service**

   - Chọn **Domains** và chọn **Create domain**

![Create OpenSearch](/ws2-bussiness-intelligence-system-aws/images/5.1-CreateOpenSearch/createopensearch-00013.png?featherlight=false&width=70pc)

3. Từ giao diện **Create domain**

   - Tại mục **Domain name**, nhập **`retail`**
   - Tại mục **Domain creation method**, chọn **Standard create**
   - Tại mục **Templates**, chọn **Dev/test**

![Create OpenSearch](/ws2-bussiness-intelligence-system-aws/images/5.1-CreateOpenSearch/createopensearch-0002.png?featherlight=false&width=70pc)

4. Trong phần **Deployment options**

   - Tại mục **Deployment option**, chọn **Domain without standby**
   - Tại mục **Availability Zone**, chọn **2-AZ**

![Create OpenSearch](/ws2-bussiness-intelligence-system-aws/images/5.1-CreateOpenSearch/createopensearch-0003.png?featherlight=false&width=70pc)

5. Tiếp tục,

   - Tại mục **Version**, chọn **2.11 (latest)** là phiên bản mới nhất
   - Tại mục **Instance family**, chọn **General purpose**
   - Tại mục **Instance type**, chọn **t3.small.search**

![Create OpenSearch](/ws2-bussiness-intelligence-system-aws/images/5.1-CreateOpenSearch/createopensearch-0004.png?featherlight=false&width=70pc)

6. Tại mục **Number of nodes**, nhập **`6`**, các lựa chọn còn lại để giá trị mặc định

![Create OpenSearch](/ws2-bussiness-intelligence-system-aws/images/5.1-CreateOpenSearch/createopensearch-0005.png?featherlight=false&width=70pc)

![Create OpenSearch](/ws2-bussiness-intelligence-system-aws/images/5.1-CreateOpenSearch/createopensearch-0006.png?featherlight=false&width=70pc)

7. Trong phần **Network**

   - Tại mục **Network**, chọn **VPC access - recommended**
   - Tại mục **IP address type**, chọn **Dual-stack mode - recommended**
   - Tại mục **VPC**, chọn **vpc-xxxxxxxxx (10.0.0.0/16)**
   - Tại mục **Subnets**, chọn **project-businesss-intelligence-system-subnet-private2-us-east-1b** và **project-businesss-intelligence-system-subnet-private1-us-east-1a**
   - Tại mục **Security groups**, chọn **es-cluster-sg**

![Create OpenSearch](/ws2-bussiness-intelligence-system-aws/images/5.1-CreateOpenSearch/createopensearch-0007.png?featherlight=false&width=70pc)

8. Trong phần **Fine-grained access control**, đầu tiên chọn bật **Enable fine-grained access control**

   - Tại mục **Master user**, chọn **Create master user**
   - Tại mục **Master username**, nhập **`admin`**
   - Tại mục **Master password**, nhập **`xxxxxxxxxxxxxx`**
   - Tại mục **Confirm master password**, chọn **`xxxxxxxxxxxxxx`**

![Create OpenSearch](/ws2-bussiness-intelligence-system-aws/images/5.1-CreateOpenSearch/createopensearch-0008.png?featherlight=false&width=70pc)

9. Trong phần **Access policy**

   - Tại mục **Domain access policy**, chọn **Only use fine-grained access control**

![Create OpenSearch](/ws2-bussiness-intelligence-system-aws/images/5.1-CreateOpenSearch/createopensearch-0009.png?featherlight=false&width=70pc)

10. Trong phần **Encryption**

- Tại mục **Choose an AWS KMS key**, chọn **Use AWS owned key**

![Create OpenSearch](/ws2-bussiness-intelligence-system-aws/images/5.1-CreateOpenSearch/createopensearch-00010.png?featherlight=false&width=70pc)

11. Các lựa chọn còn lại để giá trị mặc định, cuối cùng chọn **Create** để hoàn tất việc tạo OpenSearch

![Create OpenSearch](/ws2-bussiness-intelligence-system-aws/images/5.1-CreateOpenSearch/createopensearch-00011.png?featherlight=false&width=70pc)

12. Các domain mới thường mất 15–30 phút để khởi tạo và có thể lâu hơn tùy thuộc vào cấu hình.

![Create OpenSearch](/ws2-bussiness-intelligence-system-aws/images/5.1-CreateOpenSearch/createopensearch-00012.png?featherlight=false&width=70pc)

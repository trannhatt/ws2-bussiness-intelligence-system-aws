---
title: "Kích hoạt AWS Lambda Function"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 5.4 </b> "
---

### Kích hoạt AWS Lambda Function để nhập bản ghi vào Amazon OpenSearch

#### Thiết lập SSH Tunneling

{{% notice info %}}
Ban đầu chúng ta đã tạo cụm Amazon OpenSearch trong VPC. Do đó, Amazon OpenSearch endpoint và Kibana endpoint chưa truy cập được thông qua internet. Vì vậy, để truy cập được các endpoint này chúng ta phải tạo ssh tunnel và thực hiện chuyển tiếp cổng cục bộ.
{{% /notice %}}

1. Sử dụng SSH Tunneling, đầu tiên chúng ta sẽ thiết lập cấu hình ssh

   - Đối với hệ điều hành Mac/Linux để truy cập cụm OpenSearch, hãy thêm cấu hình ssh tunnel vào tệp cấu hình ssh của máy tính cá nhân như sau

```shell script
# OpenSearch Tunnel
Host estunnel
  HostName <EC2 Public IP of Bastion Host>
  User ec2-user
  IdentitiesOnly yes
  IdentityFile ~/.ssh/analytics-hol.pem
  LocalForward 9200 <OpenSearch Endpoint>:443
```

{{% notice note %}}
**EC2 Public IP of Bastion Host** là địa chỉ Public IP của EC2 instance chúng ta đã tạo ở phần **Các bước chuẩn bị**.
{{% /notice %}}

- Ví dụ

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00044.png?featherlight=false&width=50pc)

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00045.png?featherlight=false&width=50pc)

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00046.png?featherlight=false&width=50pc)

{{% notice info %}}
Ngoài ra, chúng ta có thể tạo Lambda layer dùng môi trường mô phỏng Lambda sử dụng Docker.
{{% /notice %}}

```shell script
$ cat <<EOF > requirements.txt
> opensearch-py==2.0.1
> requests==2.31.0
> requests-aws4auth==1.1.2
> EOF
$ docker run -v "$PWD":/var/task "public.ecr.aws/sam/build-python3.11" /bin/sh -c "pip install -r requirements.txt -t python/lib/python3.11/site-packages/; exit"
$ zip -r es-lib.zip python > /dev/null
$ aws s3 mb s3://my-bucket-for-lambda-layer-packages
$ aws s3 cp es-lib.zip s3://my-bucket-for-lambda-layer-packages/var/
```

2. Cuối cùng chạy lệnh **`ssh -N estunnel`** trong Terminal

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00048.png?featherlight=false&width=50pc)

3. Truy cập đường dẫn sau trên trình duyệt

   - **`https://localhost:9200/_dashboards/app/login?`**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00047.png?featherlight=false&width=70pc)

4. Nhập người dùng và mật khẩu mà chúng ta đã thiết lập khi tạo Amazon OpenSearch Service. Người dùng và mật khẩu được lưu trữ trong **AWS Secrets Manager** dưới dạng như tên OpenSearchMasterUserSecret1-xxxxxxxxxxxx.

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00049.png?featherlight=false&width=70pc)

5. Chúng ta đã truy cập Amazon OpenSearch Service thành công, đây là giao diện màn hình chính.

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00050.png?featherlight=false&width=70pc)

#### Tạo Role

6. Tại màn hình chính

   - Chọn vào biểu tượng thanh công cụ ở bên trái nút **Home** và chọn **Security**.

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00051.png?featherlight=false&width=70pc)

7. Tại giao diện **Get started**, chọn **Create new role**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00052.png?featherlight=false&width=70pc)

8. Trong phần **Create Role**,
   - Tại mục **Name**, nhập **`firehose_role`**
   - Tại mục **Cluster permissions**, thêm 2 permissions là **cluster_composite_ops** và **cluster_monitor**
   - Tại mục **Index**, thêm index là **retail\***

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00053.png?featherlight=false&width=70pc)

9. Tại mục **Index permissions**, thêm các hành động **crud**, **create_index** và **manage**.

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00054.png?featherlight=false&width=70pc)

10. Cuối cùng chọn **Create** để hoàn tất việc tạo Role.

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00055.png?featherlight=false&width=70pc)

11. Role được tạo với các cấu hình như ảnh.

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00056.png?featherlight=false&width=70pc)

#### Map Role

12. Chọn tab **Mapped users** và sau đó chọn **Map users**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00057.png?featherlight=false&width=70pc)

13. Trong phần **Map user**:

- Tại mục **Backend roles**, nhập IAM ARN mà Lambda Function đang sử dụng
- Chọn **Map**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00058.png?featherlight=false&width=70pc)

14. Kiểm tra ánh xạ đã thành công

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00059.png?featherlight=false&width=70pc)

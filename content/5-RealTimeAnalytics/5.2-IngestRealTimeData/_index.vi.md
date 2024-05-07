---
title: "Thêm thư viện dùng chung vào AWS Lambda Layer"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

### Tạo S3 Bucket lưu tệp mã thư viện

1.  - Tại mục **Bucket type**, chọn **General purpose**
    - Tại mục **Bucket name**, nhập **`xxxxxxxxxxxxxxxxxx`**. Trong đó **`xxxxxxxxxxxxxxxxxx`** là tên S3 bucket bạn đặt

![Create S3 Bucket](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-0002.png?featherlight=false&width=70pc)

2.  Trong phần **Default encryption**,

    - Tại mục **Encryption type**, chọn **Server-side encryption with Amazon S3 managed keys (SSE-S3)**
    - Tại mục **Bucket Key**, chọn **Enable**
    - Cuối cùng, chọn **Create bucket** để hoàn tất việc tạo S3 Bucket

![Create S3 Bucket](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-0003.png?featherlight=false&width=70pc)

### Tạo thư viện và tải tệp lên S3

3.  Chúng ta sẽ tạo python package trên Amazon Linux của EC2 Instance được cấu hình từ đầu cho dự án này, hãy chạy từng câu lênh bên dưới và được kết quả như ảnh

{{% notice note %}}
Lưu ý rằng **`xxxxxxxxxxxxxxxxxx`** là tên S3 bucket, hãy thay nó bằng tên mà bạn đặt
{{% /notice %}}

```shell script
[ec2-user@ip-10-0-1-229 ~] $ python3 -m venv es-lib
[ec2-user@ip-10-0-1-229 ~] $ cd es-lib
[ec2-user@ip-10-0-1-229 ~] $ source bin/activate
(es-lib) $ mkdir -p python_modules
(es-lib) $ pip install opensearch-py==2.0.1 requests==2.31.0 requests-aws4auth==1.1.2 -t python_modules
(es-lib) $ mv python_modules python
(es-lib) $ zip -r es-lib.zip python/
(es-lib) $ aws s3 mb s3://xxxxxxxxxxxxxxxxxx
(es-lib) $ aws s3 cp es-lib.zip s3://xxxxxxxxxxxxxxxxxx/var/
(es-lib) $ deactivate
```

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-0001.png?featherlight=false&width=70pc)

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-0004.png?featherlight=false&width=70pc)

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-0005.png?featherlight=false&width=70pc)

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-0006.png?featherlight=false&width=70pc)

{{% notice info %}}
Nếu không tạo python package trên Amazon Linux thì hãy tạo nó bằng môi trường Lambda được mô phỏng với Docker bằng những câu lệnh bên dưới.
{{% /notice %}}

```shell script
$ cat <<EOF > requirements.txt
> opensearch-py==2.0.1
> requests==2.31.0
> requests-aws4auth==1.1.2
> EOF
$ docker run -v "$PWD":/var/task "public.ecr.aws/sam/build-python3.11" /bin/sh -c "pip install -r requirements.txt -t python/lib/python3.11/site-packages/; exit"
$ zip -r es-lib.zip python > /dev/null
$ aws s3 mb s3://xxxxxxxxxxxxxxxxxx
$ aws s3 cp es-lib.zip s3://xxxxxxxxxxxxxxxxxx/var/
```

{{% notice note %}}
Trước khi qua bước tiếp theo, chúng ta sẽ vào gói Python package trên S3 để copy đường dẫn **Object URL**
{{% /notice %}}

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-0009.png?featherlight=false&width=70pc)

### Thêm một thư viện dùng chung vào Layer để dùng cho Lambda Function

4. Tại giao diện **AWS console**

   - Nhấn chọn thanh tìm kiếm và nhập **`lambda`**
   - Tại mục **Services** chọn **Lambda**

![Create Layer](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-0007.png?featherlight=false&width=70pc)

5. Tại giao diện **AWS Lambda**

   - Chọn **Layers**
   - Chọn **Create layer**

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-0008.png?featherlight=false&width=70pc)

6. Trong giao diện **Create layer**

   Trong phần **Layer configuration**,

   - Tại mục **Name**, nhập **`es-lib`**
   - Tại mục **Description - optional**, nhập **`Upload a file from Amazon S3`**
   - Chọn **Upload a file from Amazon S3**
   - Tại mục **Amazon S3 link URL**, paste đường dẫn vừa copy ở phần trước
   - Tại mục **Compatible runtimes - optional**, chọn **Python 3.11**

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00010.png?featherlight=false&width=70pc)

7. Cuối cùng, chọn **Create** để hoàn tất việc tạo và cấu hình Layer

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00011.png?featherlight=false&width=70pc)

8. Kiểm tra Layer được tạo thành công

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00012.png?featherlight=false&width=70pc)

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00013.png?featherlight=false&width=70pc)

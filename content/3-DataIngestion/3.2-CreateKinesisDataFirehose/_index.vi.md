---
title: "Lưu trữ dữ liệu vào S3 với Kinesis Data Firehose"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 3.2 </b> "
---

### Tạo Kinesis Data Firehose

1. Nếu bạn đang ở giao diện trang Kinesis Data Stream ở phần trước thì hãy chọn **Amazon Data Firehose** từ thanh sidebar bên trái.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0006-createfirehose.png?featherlight=false&width=70pc)

2. Tại giao diện **Amazon Data Firehose**, chọn **Create Firehose stream**.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0007-createfirehose.png?featherlight=false&width=70pc)

{{% notice info %}}
Nếu bạn đang bắt đầu từ giao diện Amazon Kinesis, hãy chọn nút radio Kinesis Data Firehose và chọn **Create data stream**.
{{% /notice %}}

3. Trong giao diện **Create Firehose stream**:

   - Tại mục **Source**, tìm kiếm và chọn **Amazon Kinesis Data Streams**.
   - Tại mục **Destination**, tìm kiếm và chọn **Amazon S3**.
   - Khi đó, tại mục **Kinesis data stream**, đường dẫn ARN của Kinesis data stream vừa tạo sẽ hiển thị.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0008-createfirehose.png?featherlight=false&width=70pc)

4. Trong phần **Create Firehose stream**:

   - Tại mục **Firehose stream name**, nhập **`retail-trans`**.
   - Trong phần **Transform and convert records**:
     - **Disable** 2 lựa chọn **Transform source records with AWS Lambda** và **Convert record format**.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0011-createfirehose.png?featherlight=false&width=70pc)

{{% notice note %}}
Nếu bạn chưa tạo S3 Bucket, hãy tham khảo phần này [Tạo S3 Bucket](#tạo-s3-bucket).
{{% /notice %}}

5. Trong phần **Destination settings**:

   - Tại mục **S3 bucket**, chọn **Browse** và chọn S3 Bucket đã tạo cho dự án này.
   - Tại mục **S3 bucket prefix - optional**, nhập **`json-data/year=!{timestamp:yyyy}/month=!{timestamp:MM}/day=!{timestamp:dd}/hour=!{timestamp:HH}/`**.
   - Tại mục **S3 bucket error output prefix - optional**, nhập **`error-json/year=!{timestamp:yyyy}/month=!{timestamp:MM}/day=!{timestamp:dd}/hour=!{timestamp:HH}/!{firehose:error-output-type}`**.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0010-createfirehose.png?featherlight=false&width=70pc)

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0012-createfirehose.png?featherlight=false&width=70pc)

6. Trong phần **$3 buffer hints**:

   - Tại mục **Buffer size**, nhập **`1`**.
   - Tại mục **Buffer interval**, nhập **`60`**.
   - Các thông tin còn lại để mặc định.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0013-createfirehose.png?featherlight=false&width=70pc)

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0014-createfirehose.png?featherlight=false&width=70pc)

7. Trong phần **Service access**:

   - Chọn **Create or update IAM role KinesisFirehoseServiceRole-** để cấp quyền truy cập.
   - Cuối cùng, chọn **Create Firehose stream** để hoàn tất việc tạo Kinesis Data Firehose.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0017-createfirehose.png?featherlight=false&width=70pc)

8. Kiểm tra việc tạo Kinesis Data Firehose đã thành công.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0016-createfirehose.png?featherlight=false&width=70pc)

### Tạo S3 Bucket

{{% notice note %}}
Nếu bạn đã tạo Bucket thì bạn có thể bỏ qua các bước này.
{{% /notice %}}

9. Chọn **Create** để tạo Bucket mới.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0009-createfirehose.png?featherlight=false&width=70pc)

10. Trong phần **Create Bucket**:

    - Tại mục **Bucket type**, chọn **General purpose**.
    - Tại mục **Bucket name**, nhập **`aws-analytics-businesss-intelligence-ws2`**.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0001-createfirehose.png?featherlight=false&width=70pc)

11. Tiếp tục:

    - Tại mục **Object Ownership**, chọn **ACLs disabled (recommended)**.
    - Tại mục **Block Public Access settings for this bucket**, chọn **Block all public access**.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0002-createfirehose.png?featherlight=false&width=70pc)

12. Tại mục **Bucket Versioning**, chọn **Disable**.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0003-createfirehose.png?featherlight=false&width=70pc)

13. Trong phần **Default encryption**:

    - Tại mục **Encryption type**, chọn **Server-side encryption with Amazon S3 managed keys (SSE-S3)**.
    - Tại mục **Bucket Key**, chọn **Enable**.
    - Cuối cùng, chọn **Create bucket** để hoàn tất việc tạo S3 Bucket.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0004-createfirehose.png?featherlight=false&width=70pc)

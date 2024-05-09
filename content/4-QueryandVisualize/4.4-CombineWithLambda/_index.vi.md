---
title: "Athena CTAS"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 4.4 </b> "
---

## Kết hợp các tệp nhỏ được lưu trữ trong S3 thành các tệp lớn với AWS Lambda Function

Khi dữ liệu được Kinesis Data Firehose truyền đến theo thời gian thực và lưu trữ trong S3 thì sẽ tạo các tệp dữ liệu có kích thước nhỏ, dẫn đến hiệu suất truy vấn tổng thể kém. Khi Athena lập kế hoạch truy vấn, nó sẽ liệt kê tất cả các vị trí phân vùng, việc này sẽ mất thời gian và việc xử lý và yêu cầu mỗi tệp cũng có chi phí tính toán. Do đó, việc tải một tệp lớn hơn từ Amazon S3 sẽ nhanh hơn việc tải cùng một bản ghi từ nhiều tệp nhỏ hơn. Để cải thiện hiệu suất truy vấn của Amazon Athena, chúng ta nên kết hợp các tệp nhỏ thành một tệp lớn. Khi đó, để chạy các tác vụ này theo định kỳ, chúng ta sẽ tạo AWS Lambda Function để thực thi truy vấn Athena's Create Table As Select (CTAS).

![Architecture Workshop 2 - part 4.4](/ws2-bussiness-intelligence-system-aws/images/4/arch4.4.png?featherlight=false&width=70pc)

### Tạo bảng lưu trữ kết quả truy vấn

1. Quay lại Athena Query Editor, Tạo một query mới và nhập câu lệnh bên dưới

   - Chọn **Run again**

{{% notice note %}}
Thay thế **`xxxxxxxxxxxxxxx`** ở dòng cuối cùng tại **LOCATION** bằng tên S3 bucket
{{% /notice %}}

```sql
CREATE EXTERNAL TABLE `mydatabase.ctas_retail_trans_parquet`(
  `invoice` string COMMENT 'Invoice number',
  `stockcode` string COMMENT 'Product (item) code',
  `description` string COMMENT 'Product (item) name',
  `quantity` int COMMENT 'The quantities of each product (item) per transaction',
  `invoicedate` timestamp COMMENT 'Invoice date and time',
  `price` float COMMENT 'Unit price',
  `customer_id` string COMMENT 'Customer number',
  `country` string COMMENT 'Country name')
PARTITIONED BY (
  `year` int,
  `month` int,
  `day` int,
  `hour` int)
ROW FORMAT SERDE
  'org.apache.hadoop.hive.ql.io.parquet.serde.ParquetHiveSerDe'
STORED AS INPUTFORMAT
  'org.apache.hadoop.hive.ql.io.parquet.MapredParquetInputFormat'
OUTPUTFORMAT
  'org.apache.hadoop.hive.ql.io.parquet.MapredParquetOutputFormat'
LOCATION
  's3://xxxxxxxxxxxxxxx/parquet-retail-trans'
TBLPROPERTIES (
  'has_encrypted_data'='false',
  'parquet.compression'='SNAPPY')
;
```

{{% notice info %}}
Câu lệnh trên sẽ thay đổi dữ liệu định dạng json của bảng **retal_tran_json** thành định dạng **parquet** và lưu trữ nó trong bảng có tên **ctas_retail_trans_parquet**.
Dữ liệu trong bảng **ctas_retail_trans_parquet** sẽ được lưu tại s3://xxxxxxxxxxxxxxx/parquet-retail-trans của S3 bucket được tạo trước đó.
{{% /notice %}}

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00023.png?featherlight=false&width=70pc)

### Tạo Lambda Function

2. Tại giao diện **AWS console**

   - Nhấn chọn thanh tìm kiếm và nhập **`lambda`**
   - Tại mục **Services** chọn **Lambda**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0001.png?featherlight=false&width=70pc)

3. Tại giao diện **AWS Lambda**

   - Chọn **Functions**
   - Chọn **Create a function**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0002.png?featherlight=false&width=70pc)

4.  Tại giao diện **Create function**

    Trong phần **Basic information**,

    - Tại mục **Function name**, nhập **`MergeSmallFiles`**
    - Tại mục **Runtime**, chọn **Python 3.11**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0003.png?featherlight=false&width=70pc)

5. Các lựa chọn còn lại chúng ta sẽ để giá trị mặc định, cuối cùng chọn **Create function** để hoàn tất việc tạo Lambda Function

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0004.png?featherlight=false&width=70pc)

6. Tiếp theo, chọn **Add trigger**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0005.png?featherlight=false&width=70pc)

7. Tại giao diện **Add trigger**

   Trong phần **Trigger configuration**,

   - Chọn **CloudWatch Events/EventBridge**
   - Tại mục **Rule**, chọn **Create a new rule**
   - Tại mục **Rule name**, nhập **`MergeSmallFilesEvent`**
   - Tại mục **Rule description**, nhập **`MergeSmallFilesEvent`**
   - Tại mục **Rule type**, chọn **Schedule expression**
   - Tại mục **Schedule expression**, nhập **`cron(5 * * * ? *)`** để chạy tác vụ 5 phút một lần
   - Cuối cùng, chọn **Add** để hoàn tất việc thêm trigger

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0006.png?featherlight=false&width=70pc)

8.  Kiểm tra trigger đã được thêm thành công

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0007.png?featherlight=false&width=70pc)

9. Sao chép và dán mã từ tệp **`athena_ctas.py`** vào trình soạn thảo mã của **Code source** và chọn **Deploy**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0008.png?featherlight=false&width=70pc)

10. Sau đó, chọn tab **Configuration**

- Chọn **Environment variables**
- Chọn **Edit**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0009.png?featherlight=false&width=70pc)

11. Thêm lần lược từng biến môi trường theo cấu trúc bên dưới

```shell script
OLD_DATABASE=<source database>
OLD_TABLE_NAME=<source table>
NEW_DATABASE=<destination database>
NEW_TABLE_NAME=<destination table>
WORK_GROUP=<athena workgroup>
OLD_TABLE_LOCATION_PREFIX=<s3 location prefix of source table>
OUTPUT_PREFIX=<destination s3 prefix>
STAGING_OUTPUT_PREFIX=<staging s3 prefix used by athena>
COLUMN_NAMES=<columns of source table excluding partition keys>
```

- Ví dụ mẫu

```shell script
OLD_DATABASE=mydatabase
OLD_TABLE_NAME=retail_trans_json
NEW_DATABASE=mydatabase
NEW_TABLE_NAME=ctas_retail_trans_parquet
WORK_GROUP=primary
OLD_TABLE_LOCATION_PREFIX=s3://xxxxxxxxxxx/json-data
OUTPUT_PREFIX=s3://xxxxxxxxxxx/parquet-retail-trans
STAGING_OUTPUT_PREFIX=s3://xxxxxxxxxxx/tmp
COLUMN_NAMES=invoice,stockcode,description,quantity,invoicedate,price,customer_id,country
```

- Chọn **Save** để lưu thay đổi

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00020.png?featherlight=false&width=70pc)

12. Để thực thi truy cấn với Athena, chúng ta cần IAM Policy.

    Tab **Configuration**,

    - Chọn **Permissions**
    - Tại mục **Rule name**, chọn **MergeSmallFiles-role-xxxxxx** để chỉnh sửa Policy trong Role này

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00012.png?featherlight=false&width=70pc)

13. Chọn **View the MergeSmallFiles-role-xxxxxx role**, sẽ điều hướng sang một tab khác trong trình duyệt của bạn

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00013.png?featherlight=false&width=70pc)

14. Tại tab đó, chọn **Add permissions** và chọn **Attach policies**.

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00014.png?featherlight=false&width=70pc)

15. Trong phần **Other permissions policies**

    - Tại thanh tìm kiếm, nhập **`AmazonAthenaFullAccess`**
    - Chọn **AmazonAthenaFullAccess** vừa tìm được
    - Cuối cùng chọn **Add permissions**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00015.png?featherlight=false&width=70pc)

16. Tiếp tục, chọn **Add permissions** và chọn **Attach policies**.

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00016.png?featherlight=false&width=70pc)

17. Trong phần **Other permissions policies**

    - Tại thanh tìm kiếm, nhập **`AmazonS3FullAccess`**
    - Chọn **AmazonS3FullAccess** vừa tìm được
    - Cuối cùng chọn **Add permissions**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00017.png?featherlight=false&width=70pc)

18. Chúng ta đã thấy 2 Policy mới đã được thêm hành công

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00018.png?featherlight=false&width=70pc)

19. Quay lại tab trước,

    - Tại mục **Time out**, nhập thời gian là **`30s`**
    - Chọn **Save**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00019.png?featherlight=false&width=70pc)

---
title: "Phân tích dữ liệu với Athena"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 4.1 </b> "
---

### Tạo cơ sở dữ liệu

1. Truy cập giao diện **AWS console**:

   - Bắt đầu bằng cách nhấn vào thanh tìm kiếm và nhập **`athena`**
   - Tại mục **Services**, chọn **Athena**

![Query Athena](/ws2-bussiness-intelligence-system-aws/images/4.1-AnalyzeDataAthena/0001-queryathena.png?featherlight=false&width=70pc)

2. Tại giao diện **Amazon Athena**:

   - Chọn **Query your data with Trino SQL**
   - Tiếp theo, chọn **Launch query editor**

![Query Athena](/ws2-bussiness-intelligence-system-aws/images/4.1-AnalyzeDataAthena/0002-queryathena.png?featherlight=false&width=70pc)

{{% notice note %}}
Nếu đây là lần đầu tiên bạn sử dụng Athena, bạn cần thiết lập vị trí của S3 để lưu trữ kết quả truy vấn từ Athena. Trong **Query editor**, chọn **Edit settings**. Sau đó, tạo một thư mục mới trong S3 bucket đã tạo trước đó để lưu trữ kết quả truy vấn. Theo mẫu **`s3://xxxxxxxxxxx/athena-query-results/`**, trong đó **`xxxxxxxxxxx`** là tên S3 bucket. Cuối cùng, chọn **Save** để hoàn tất cấu hình lưu trữ.
{{% /notice %}}

![Query Athena](/ws2-bussiness-intelligence-system-aws/images/4.1-AnalyzeDataAthena/0003.1-queryathena.png?featherlight=false&width=70pc)

![Query Athena](/ws2-bussiness-intelligence-system-aws/images/4.1-AnalyzeDataAthena/0004.1-queryathena.png?featherlight=false&width=70pc)

3. Tạo cơ sở dữ liệu mới:

   - Trong trình soạn thảo truy vấn, nhập câu lệnh sau và chọn **Run again**.
   - Kết quả của câu lệnh sẽ hiển thị. Cuối cùng, trong mục **Database**, chọn **mydatabase** là database vừa tạo

```sql
CREATE DATABASE IF NOT EXISTS mydatabase
```

![Query Athena](/ws2-bussiness-intelligence-system-aws/images/4.1-AnalyzeDataAthena/0005-queryathena.png?featherlight=false&width=70pc)

### Tạo bảng

4. Tiếp theo:

   - Chọn **+** ở trên cửa sổ truy vấn để mở một truy vấn mới.
   - Sao chép câu truy vấn dưới đây vào trình soạn thảo truy vấn, thay thế **`xxxxxxxxxxxxxxx`** ở dòng cuối cùng tại **LOCATION** bằng tên S3 bucket
   - Cuối cùng, chọn **Run again**.

```sql
CREATE EXTERNAL TABLE IF NOT EXISTS `mydatabase.retail_trans_json`(
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
  'org.openx.data.jsonserde.JsonSerDe'
STORED AS INPUTFORMAT
  'org.apache.hadoop.mapred.TextInputFormat'
OUTPUTFORMAT
  'org.apache.hadoop.hive.ql.io.IgnoreKeyTextOutputFormat'
LOCATION
  's3://xxxxxxxxxxxxxxx/json-data'
```

![Query Athena](/ws2-bussiness-intelligence-system-aws/images/4.1-AnalyzeDataAthena/0006-queryathena.png?featherlight=false&width=70pc)

5. Kết quả thực thi câu truy vấn thành công:

   - Bảng **retail_trans_json** sẽ được tạo và hiển thị trên bảng điều khiển bên trái trong phần **Tables**.

![Query Athena](/ws2-bussiness-intelligence-system-aws/images/4.1-AnalyzeDataAthena/0007-queryathena.png?featherlight=false&width=70pc)

{{% notice note %}}
Nếu gặp lỗi, hãy kiểm tra bạn đã cập nhật tên S3 bucket tại **LOCATION** chính xác chưa. Đồng thời đảm bảo rằng bạn đã chọn **mydatabase** trong mục **Database** và chọn **AwsDataCatalog** làm **Data source**.
{{% /notice %}}

6. Tiếp theo:

   - Chọn **+** ở trên cửa sổ truy vấn để mở một truy vấn mới.
   - Chạy truy vấn dưới đây để tải dữ liệu phân vùng.
   - Cuối cùng, chọn **Run again**.

```sql
MSCK REPAIR TABLE mydatabase.retail_trans_json
```

![Query Athena](/ws2-bussiness-intelligence-system-aws/images/4.1-AnalyzeDataAthena/0008-queryathena.png?featherlight=false&width=70pc)

{{% notice note %}}
Chúng ta có thể liệt kê tất cả các phân vùng trong bảng Athena theo thứ tự chưa sắp xếp bằng cách chạy truy vấn bên dưới.
{{% /notice %}}

```sql
SHOW PARTITIONS mydatabase.retail_trans_json
```

![Query Athena](/ws2-bussiness-intelligence-system-aws/images/4.1-AnalyzeDataAthena/0009-queryathena.png?featherlight=false&width=70pc)

### Truy vấn dữ liệu

8. Tiếp theo:

   - Chọn **+** ở trên cửa sổ truy vấn để mở một truy vấn mới.
   - Nhập câu lệnh SQL sau để truy vấn 10 giao dịch từ bảng **retail_trans_json**
   - Cuối cùng, chọn **Run again** và kiểm tra kết quả truy vấn.

```sql
SELECT *
FROM retail_trans_json
LIMIT 10
```

![Query Athena](/ws2-bussiness-intelligence-system-aws/images/4.1-AnalyzeDataAthena/0010-queryathena.png?featherlight=false&width=70pc)

![Query Athena](/ws2-bussiness-intelligence-system-aws/images/4.1-AnalyzeDataAthena/0011-queryathena.png?featherlight=false&width=70pc)

{{% notice info %}}
Bạn có thể thử nghiệm viết các câu lệnh SQL khác nhau để truy vấn, lọc, và sắp xếp dữ liệu dựa trên các điều kiện khác nhau. Hiện tại, Chúng ta đã hiểu được cách Amazon Athena giúp truy vấn dữ liệu trong Amazon S3 một cách thuận tiện mà không cần đến bất kỳ máy chủ cơ sở dữ liệu nào.
{{% /notice %}}

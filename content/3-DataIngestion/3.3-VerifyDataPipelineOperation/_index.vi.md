---
title: "Xác minh hoạt động của đường ống dữ liệu"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 3.3 </b> "
---

### Xác minh hoạt động của đường ống dữ liệu

Trong phần này, chúng ta sẽ tạo dữ liệu mẫu từ EC2 Instance và xác minh dữ liệu đó được xử lý và lưu trữ theo đường ống như sau: **Kinesis Data Streams -> Kinesis Data Firehose -> S3**

1. Kết nối theo giao thức SSH tới phiên bản EC2 Instance mà chúng ta đã tạo trước đó. Đảm bảo rằng bạn đã cấu hình đầy đủ quyền truy cập và SSH key để kết nối.

2. Trên EC2 Instance, thực thi các tập lệnh trong tệp **gen_kinesis_data.py** bằng cách chạy lệnh sau:

```shell script
python3 gen_kinesis_data.py \
  --region-name us-east-1 \
  --service-name kinesis \
  --stream-name retail-trans
```

![Verify Data](/ws2-bussiness-intelligence-system-aws/images/3.3-VerifyDataPipelineOperation/0001-verifydata.png?featherlight=false&width=70pc)

{{% notice note %}}
Sau khi thực thi lệnh trên, đợi khoảng 5 đến 10 phút để dữ liệu được xử lý và phân phối đến S3 Bucket.
{{% /notice %}}

3.  Truy cập vào S3 Bucket đã được tạo trước đó. Chúng ta có thể thấy dữ liệu gốc đã được Kinesis Data Firehose phân phối đến S3 và được lưu trữ theo cấu trúc thư mục là **year=.../ -> month=.../ -> day=.../ -> hour=.../**.

![Verify Data](/ws2-bussiness-intelligence-system-aws/images/3.3-VerifyDataPipelineOperation/0002-verifydata.png?featherlight=false&width=70pc)

4. Ngoài ra, chúng ta có thể điều chỉnh số lượng record được phân phối đến S3 bằng cách sử dụng tùy chọn **--max-count MAX_COUNT**

```shell script
python3 gen_kinesis_data.py \
  --region-name us-east-1 \
  --service-name kinesis \
  --stream-name retail-trans\
  --max-count 100
```

![Verify Data](/ws2-bussiness-intelligence-system-aws/images/3.3-VerifyDataPipelineOperation/0003-verifydata.png?featherlight=false&width=70pc)

5. Kiểm tra dữ liệu vừa được phân phối đến S3 để đảm bảo rằng quy trình hoạt động một cách chính xác và đồng bộ.

![Verify Data](/ws2-bussiness-intelligence-system-aws/images/3.3-VerifyDataPipelineOperation/0004-verifydata.png?featherlight=false&width=70pc)

{{% notice info %}}
Nếu bạn muốn biết thêm về cách sử dụng lệnh này, bạn có thể chạy lệnh **`python3 gen_kinesis_data.py --help`** để xem các tùy chọn và tham số có sẵn.
{{% /notice %}}

![Verify Data](/ws2-bussiness-intelligence-system-aws/images/3.3-VerifyDataPipelineOperation/0005-verifydata.png?featherlight=false&width=70pc)

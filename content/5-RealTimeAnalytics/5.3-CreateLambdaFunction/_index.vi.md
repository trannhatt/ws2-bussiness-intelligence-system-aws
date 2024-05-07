---
title: "Tạo và cấu hình AWS Lambda Function"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

### Tạo và cấu hình AWS Lambda Function

1. Tại giao diện **AWS Lambda**

   - Chọn **Functions**
   - Chọn **Create function**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00014.png?featherlight=false&width=70pc)

2.  Tại giao diện **Create function**

    Trong phần **Basic information**,

    - Tại mục **Function name**, nhập **`UpsertToES`**
    - Tại mục **Runtime**, chọn **Python 3.11**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00015.png?featherlight=false&width=70pc)

3. Các lựa chọn còn lại chúng ta sẽ để giá trị mặc định, cuối cùng chọn **Create function** để hoàn tất việc tạo Lambda Function

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00016.png?featherlight=false&width=70pc)

4. Kết quả việc tạo Lambda Function thành công

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00017.png?featherlight=false&width=70pc)

5. Di chuyển xuống cuối trang hiện tại, trong phần **Layers** chọn **Add a layer**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00018.png?featherlight=false&width=70pc)

### Cấu hình AWS Lambda Function

6. Tại giao diện **Add layer**,

   Trong phần **Choose a layer**,

   - Tại mục **Layer source**, chọn **Custom layers**
   - Tại mục **Custom layers**, chọn **es-lib**
   - Tại mục **Version**, chọn phiên bản mới nhất đã tạo
   - Cuối cùng, chọn **Add** để hoàn tất việc tạo Layer

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00019.png?featherlight=false&width=70pc)

7. Tiếp theo, chúng ta sẽ sao chép và dán mã từ tệp **upsert_to_es.py** vào trình soạn thảo mã của **Code source** và chọn **Deploy**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00021.png?featherlight=false&width=70pc)

8. Sau đó, chọn tab **Configuration**

   - Chọn **Environment variables**
   - Chọn **Edit**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00023.png?featherlight=false&width=70pc)

9. Thêm lần lược từng biến môi trường như cấu trúc bên dưới

```shell script
ES_HOST=<opensearch service domain>
ES_INDEX=<opensearch index name>
ES_TYPE=<opensearch type name>
REQUIRED_FIELDS=<columns to be used as primary key>
REGION_NAME=<region-name>
DATE_TYPE_FIELDS=<columns of which data type is either date or timestamp>
```

- Ví dụ mẫu

```shell script
ES_HOST=vpc-retail-xxxxxxxxxxxxxxxxxxx.es.amazonaws.com
ES_INDEX=retail
ES_TYPE=trans
REQUIRED_FIELDS=Invoice,StockCode,Customer_ID
REGION_NAME=us-east-1
DATE_TYPE_FIELDS=InvoiceDate
```

- chọn **Save** để lưu thay đổi

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00024.png?featherlight=false&width=70pc)

10. Để thực thi Lambda Function trong VPC và đọc dữ liệu từ Kinesis Data Streams, chúng ta cần thêm IAM Policy cần thiết để thực thi Lambda Function.

    Tại tab **Configuration**

    - Chọn **Permissions**
    - Tại mục **Role name**, chọn **UpsertToES-role-xxxxxxx**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00025.png?featherlight=false&width=70pc)

11. Chọn **Add permissions** và chọn **Attach policies**.

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00026.png?featherlight=false&width=70pc)

12. Trong phần **Other permissions policies**

    - Tại thanh tìm kiếm, nhập **`AWSLambdaVPCAccessExecutionRole`**
    - Chọn **AWSLambdaVPCAccessExecutionRole** vừa tìm được
    - Cuối cùng chọn **Add permissions**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00027.png?featherlight=false&width=70pc)

13. Tiếp tục chọn **Add permissions** và chọn **Attach policies**.

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00028.png?featherlight=false&width=70pc)

14. Trong phần **Other permissions policies**

    - Tại thanh tìm kiếm, nhập **`AmazonKinesisReadOnlyAccess`**
    - Chọn **AmazonKinesisReadOnlyAccess** vừa tìm được
    - Cuối cùng chọn **Add permissions**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00029.png?featherlight=false&width=70pc)

15. Chọn **Add permissions** và chọn **Create inline policy**.

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00031.png?featherlight=false&width=70pc)

16. Trong phần **Policy editors**

    - Chọn **JSON**
    - Nhập các tuyên bố chính sách theo cấu trúc bên dưới. IAM Policy này sẽ cho phép Lambda Function thu thập dữ liệu vào chỉ mục **retail** trong OpenSearch Service.

```yaml
{
    "Action": [
        "es:DescribeElasticsearchDomain",
        "es:DescribeElasticsearchDomainConfig",
        "es:DescribeElasticsearchDomains",
        "es:ESHttpPost",
        "es:ESHttpPut"
    ],
    "Resource": [
        "arn:aws:es:region:account-id:domain/retail",
        "arn:aws:es:region:account-id:domain/retail/*"
    ],
    "Effect": "Allow"
},
{
    "Action": "es:ESHttpGet",
    "Resource": [
        "arn:aws:es:region:account-id:domain/retail",
        "arn:aws:es:region:account-id:domain/retail/_all/_settings",
        "arn:aws:es:region:account-id:domain/retail/_cluster/stats",
        "arn:aws:es:region:account-id:domain/retail/_nodes",
        "arn:aws:es:region:account-id:domain/retail/_nodes/*/stats",
        "arn:aws:es:region:account-id:domain/retail/_nodes/stats",
        "arn:aws:es:region:account-id:domain/retail/_stats",
        "arn:aws:es:region:account-id:domain/retail/retail*/_mapping/trans",
        "arn:aws:es:region:account-id:domain/retail/retail*/_stats"
    ],
    "Effect": "Allow"
}
```

{{% notice note %}}
Lưu ý rằng bạn hãy thay thế **region** và **account-id** phù hợp cho dự án
{{% /notice %}}

- Cuối cùng chọn **Next** để qua bước tiếp theo

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00034.png?featherlight=false&width=70pc)

17. Trong phần **Review and create**

    - Tại mục **Policy name**, nhập **`UpsertToESDefaultPolicyWS2`**
    - Chọn **Create policy**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00035.png?featherlight=false&width=70pc)

18. Tại tab **Configuration**

    - Chọn **VPC**
    - Chọn **Edit**

![Configure VPC](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00036.png?featherlight=false&width=70pc)

19. Trong giao diện **Edit VPC**

    - Tại mục **VPC**, chọn **vpc-xxxxxxxxxxxx (10.0.0.0/16)**
    - Tại mục **Subnets**, chọn **project-businesss-intelligence-system-subnet-private2-us-east-1b** và **project-businesss-intelligence-system-subnet-private1-us-east-1a**
    - Tại mục **Security groups**, chọn **use-es-cluster-sg**

![Configure VPC](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00037.png?featherlight=false&width=70pc)

20. Chọn **Save** để hoàn tất việc cấu hình VPC

![Configure VPC](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00038.png?featherlight=false&width=70pc)

![Configure VPC](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00039.png?featherlight=false&width=70pc)

21. chọn **Add trigger**

![Add Trigger](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00040.png?featherlight=false&width=70pc)

22. Trong giao diện **Add trigger**

    Trong phần **Trigger configuration**

    - Chọn **Kinesis**
    - Tại mục **Kinesis stream**, chọn **kinesis/retail-trans**
    - Chọn **Add** để hoàn tất việc thêm trigger

![Add Trigger](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00042.png?featherlight=false&width=70pc)

23. Kiểm tra trigger đã được thêm thành công

![Add Trigger](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00043.png?featherlight=false&width=70pc)

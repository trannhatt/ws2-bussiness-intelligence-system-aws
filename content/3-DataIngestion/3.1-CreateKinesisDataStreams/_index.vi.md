---
title: "Nhận dữ liệu đầu vào với Kinesis Data Streams"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.1 </b> "
---

### Tạo Kinesis Data Streams

1. Tại giao diện AWS console:
   - Nhấn chọn thanh tìm kiếm và nhập **`Kinesis`**
   - Tại mục **Services** chọn **Kinesis**

![Create Kinesis Data Streams](/ws2-bussiness-intelligence-system-aws/images/3.1-CreateKinesisDataStreams/0001-createkinesisdatastreams.png?featherlight=false&width=70pc)

2. Tại giao diện Amazon Kinesis:
   - Chọn **Kinesis Data Streams**
   - Chọn **Create data stream**

![Create Kinesis Data Streams](/ws2-bussiness-intelligence-system-aws/images/3.1-CreateKinesisDataStreams/0002-createkinesisdatastreams.png?featherlight=false&width=70pc)

3. Trong phần Create data stream:
   - Tại mục **Data stream name**, nhập **`retail-trans`**
   - Tại mục **Capacity mode**, nhấn chọn **Provisioned**
   - Tại mục **Provisioned shards**, nhập **`1`**

![Create Kinesis Data Streams](/ws2-bussiness-intelligence-system-aws/images/3.1-CreateKinesisDataStreams/0003-createkinesisdatastreams.png?featherlight=false&width=70pc)

4. Cuối cùng, chọn Create data stream:

![Create Kinesis Data Streams](/ws2-bussiness-intelligence-system-aws/images/3.1-CreateKinesisDataStreams/0004-createkinesisdatastreams.png?featherlight=false&width=70pc)

5. Chúng ta đã tạo Kinesis Data Streams thành công:

![Create Kinesis Data Streams](/ws2-bussiness-intelligence-system-aws/images/3.1-CreateKinesisDataStreams/0005-createkinesisdatastreams.png?featherlight=false&width=70pc)

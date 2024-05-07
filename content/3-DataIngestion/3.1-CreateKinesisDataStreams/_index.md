---
title: "Receive Input Data with Kinesis Data Streams"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.1 </b> "
---

### Create Kinesis Data Streams

1. In the AWS console:
   - Click on the search bar and enter **`Kinesis`**
   - Under **Services**, select **Kinesis**

![Create Kinesis Data Streams](/ws2-bussiness-intelligence-system-aws/images/3.1-CreateKinesisDataStreams/0001-createkinesisdatastreams.png?featherlight=false&width=70pc)

2. In the Amazon Kinesis interface:
   - Choose **Kinesis Data Streams**
   - Select **Create data stream**

![Create Kinesis Data Streams](/ws2-bussiness-intelligence-system-aws/images/3.1-CreateKinesisDataStreams/0002-createkinesisdatastreams.png?featherlight=false&width=70pc)

3. In the Create data stream section:
   - Under **Data stream name**, enter **`retail-trans`**
   - Under **Capacity mode**, select **Provisioned**
   - Under **Provisioned shards**, enter **`1`**

![Create Kinesis Data Streams](/ws2-bussiness-intelligence-system-aws/images/3.1-CreateKinesisDataStreams/0003-createkinesisdatastreams.png?featherlight=false&width=70pc)

4. Finally, select Create data stream:

![Create Kinesis Data Streams](/ws2-bussiness-intelligence-system-aws/images/3.1-CreateKinesisDataStreams/0004-createkinesisdatastreams.png?featherlight=false&width=70pc)

5. We have successfully created Kinesis Data Streams:

![Create Kinesis Data Streams](/ws2-bussiness-intelligence-system-aws/images/3.1-CreateKinesisDataStreams/0005-createkinesisdatastreams.png?featherlight=false&width=70pc)

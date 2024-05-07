---
title: "Verify Data Pipeline Operation"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 3.3 </b> "
---

### Verify Data Pipeline Operation

In this section, we'll generate sample data from an EC2 Instance and verify that the data is processed and stored through the pipeline as follows: **Kinesis Data Streams -> Kinesis Data Firehose -> S3**

1. Connect to the EC2 Instance via SSH using the SSH key and ensure that you have sufficient access permissions.

2. On the EC2 Instance, execute the commands in the **gen_kinesis_data.py** file by running the following command:

```shell script
python3 gen_kinesis_data.py \
  --region-name us-east-1 \
  --service-name kinesis \
  --stream-name retail-trans
```

![Verify Data](/ws2-bussiness-intelligence-system-aws/images/3.3-VerifyDataPipelineOperation/0001-verifydata.png?featherlight=false&width=70pc)

{{% notice note %}}
After executing the above command, wait for approximately 5 to 10 minutes for the data to be processed and delivered to the S3 Bucket.
{{% /notice %}}

3. Access the previously created S3 Bucket. We can observe that the raw data has been distributed to S3 by Kinesis Data Firehose and stored with the directory structure of **year=.../ -> month=.../ -> day=.../ -> hour=.../**.

![Verify Data](/ws2-bussiness-intelligence-system-aws/images/3.3-VerifyDataPipelineOperation/0002-verifydata.png?featherlight=false&width=70pc)

4. Additionally, we can adjust the number of records distributed to S3 using the **--max-count MAX_COUNT** option.

```shell script
python3 gen_kinesis_data.py \
  --region-name us-east-1 \
  --service-name kinesis \
  --stream-name retail-trans\
  --max-count 100
```

![Verify Data](/ws2-bussiness-intelligence-system-aws/images/3.3-VerifyDataPipelineOperation/0003-verifydata.png?featherlight=false&width=70pc)

5. Check the data recently distributed to S3 to ensure that the process is operating correctly and synchronously.

![Verify Data](/ws2-bussiness-intelligence-system-aws/images/3.3-VerifyDataPipelineOperation/0004-verifydata.png?featherlight=false&width=70pc)

{{% notice info %}}
If you want to learn more about using this command, you can run **`python3 gen_kinesis_data.py --help`** to see available options and parameters.
{{% /notice %}}

![Verify Data](/ws2-bussiness-intelligence-system-aws/images/3.3-VerifyDataPipelineOperation/0005-verifydata.png?featherlight=false&width=70pc)

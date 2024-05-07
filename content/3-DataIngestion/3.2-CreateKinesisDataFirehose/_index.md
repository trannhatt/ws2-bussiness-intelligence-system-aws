---
title: "Store Data into S3 with Kinesis Data Firehose"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 3.2 </b> "
---

### Create Kinesis Data Firehose

1. If you're on the Amazon Kinesis Data Stream page from the previous section, select **Amazon Data Firehose** from the left sidebar.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0006-createfirehose.png?featherlight=false&width=70pc)

2. In the **Amazon Data Firehose** interface, select **Create Firehose stream**.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0007-createfirehose.png?featherlight=false&width=70pc)

{{% notice info %}}
If you're starting from the Amazon Kinesis interface, select the Kinesis Data Firehose radio button and choose **Create data stream**.
{{% /notice %}}

3. In the **Create Firehose stream** interface:

   - Under **Source**, search and select **Amazon Kinesis Data Streams**.
   - Under **Destination**, search and select **Amazon S3**.
   - Then, under **Kinesis data stream**, the ARN path of the created Kinesis data stream will be displayed.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0008-createfirehose.png?featherlight=false&width=70pc)

4. In the **Create Firehose stream** section:

   - Under **Firehose stream name**, enter **`retail-trans`**.
   - In the **Transform and convert records** section:
     - **Disable** both options for **Transform source records with AWS Lambda** and **Convert record format**.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0011-createfirehose.png?featherlight=false&width=70pc)

{{% notice note %}}
If you haven't created an S3 Bucket, please refer to this section [Create S3 Bucket](#create-s3-bucket).
{{% /notice %}}

5. In the **Destination settings** section:

   - Under **S3 bucket**, select **Browse** and choose the S3 Bucket created for this project.
   - Under **S3 bucket prefix - optional**, enter **`json-data/year=!{timestamp:yyyy}/month=!{timestamp:MM}/day=!{timestamp:dd}/hour=!{timestamp:HH}/`**.
   - Under **S3 bucket error output prefix - optional**, enter **`error-json/year=!{timestamp:yyyy}/month=!{timestamp:MM}/day=!{timestamp:dd}/hour=!{timestamp:HH}/!{firehose:error-output-type}`**.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0010-createfirehose.png?featherlight=false&width=70pc)

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0012-createfirehose.png?featherlight=false&width=70pc)

6. In the **$3 buffer hints** section:

   - Under **Buffer size**, enter **`1`**.
   - Under **Buffer interval**, enter **`60`**.
   - Leave the remaining information as default.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0013-createfirehose.png?featherlight=false&width=70pc)

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0014-createfirehose.png?featherlight=false&width=70pc)

7. In the **Service access** section:

   - Select **Create or update IAM role KinesisFirehoseServiceRole-** to grant access.
   - Finally, select **Create Firehose stream** to complete the creation of Kinesis Data Firehose.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0017-createfirehose.png?featherlight=false&width=70pc)

8. Verify that the creation of Kinesis Data Firehose was successful.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0016-createfirehose.png?featherlight=false&width=70pc)

### Create S3 Bucket

{{% notice note %}}
You can skip these steps if you've already created a Bucket.
{{% /notice %}}

9. Select **Create** to create a new Bucket.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0009-createfirehose.png?featherlight=false&width=70pc)

10. In the **Create Bucket** section:

    - Under **Bucket type**, select **General purpose**.
    - Under **Bucket name**, enter **`aws-analytics-businesss-intelligence-ws2`**.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0001-createfirehose.png?featherlight=false&width=70pc)

11. Continue:

    - Under **Object Ownership**, select **ACLs disabled (recommended)**.
    - Under **Block Public Access settings for this bucket**, select **Block all public access**.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0002-createfirehose.png?featherlight=false&width=70pc)

12. Under **Bucket Versioning**, select **Disable**.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0003-createfirehose.png?featherlight=false&width=70pc)

13. In the **Default encryption** section:

    - Under **Encryption type**, select **Server-side encryption with Amazon S3 managed keys (SSE-S3)**.
    - Under **Bucket Key**, select **Enable**.
    - Finally, select **Create bucket** to complete the creation of the S3 Bucket.

![Create Kinesis Data Firehose](/ws2-bussiness-intelligence-system-aws/images/3.2-CreateKinesisDataFirehose/0004-createfirehose.png?featherlight=false&width=70pc)

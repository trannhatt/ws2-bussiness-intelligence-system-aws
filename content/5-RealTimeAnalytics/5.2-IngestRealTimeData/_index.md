---
title: "Add Common Libraries to AWS Lambda Layer"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

### Create S3 Bucket to Store Library Files

1. - Under **Bucket type**, select **General purpose**
   - Under **Bucket name**, enter **`xxxxxxxxxxxxxxxxxx`**. Here, **`xxxxxxxxxxxxxxxxxx`** is your S3 bucket name

![Create S3 Bucket](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-0002.png?featherlight=false&width=70pc)

2. In the **Default encryption** section,

   - Under **Encryption type**, select **Server-side encryption with Amazon S3 managed keys (SSE-S3)**
   - Under **Bucket Key**, select **Enable**
   - Finally, select **Create bucket** to create the S3 Bucket

![Create S3 Bucket](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-0003.png?featherlight=false&width=70pc)

### Create Library and Upload Files to S3

3. We will create a Python package on an Amazon Linux EC2 Instance configured from scratch for this project. Run each command below and see the results as
   shown in the images

{{% notice note %}}
Note that **`xxxxxxxxxxxxxxxxxx`** is the S3 bucket name, replace it with the name you set
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
If you are unable to create the Python package on Amazon Linux, create it in a Lambda-like environment simulated with Docker using the commands below.
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
Before proceeding to the next step, let's access the Python package in S3 to copy the **Object URL**
{{% /notice %}}

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-0009.png?featherlight=false&width=70pc)

### Add a Common Library to the Layer for Use with Lambda Function

4. In the **AWS console**

   - Type **`lambda`** in the search bar and select **Lambda** under **Services**

![Create Layer](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-0007.png?featherlight=false&width=70pc)

5. In the **AWS Lambda** interface,

   - Select **Layers**
   - Click on **Create layer**

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-0008.png?featherlight=false&width=70pc)

6. In the **Create layer** interface,

   Under **Layer configuration**,

   - In the **Name** field, enter **`es-lib`**
   - In the **Description - optional** field, enter **`Upload a file from Amazon S3`**
   - Choose **Upload a file from Amazon S3**
   - In the **Amazon S3 link URL** field, paste the URL copied earlier
   - In the **Compatible runtimes - optional** field, select **Python 3.11**

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00010.png?featherlight=false&width=70pc)

7. Finally, click **Create** to complete the creation and configuration of the Layer

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00011.png?featherlight=false&width=70pc)

8. Verify that the Layer has been successfully created

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00012.png?featherlight=false&width=70pc)

![Create Python Package](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00013.png?featherlight=false&width=70pc)

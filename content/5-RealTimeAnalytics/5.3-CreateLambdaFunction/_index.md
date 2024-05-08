---
title: "Create AWS Lambda Function"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

### Create AWS Lambda Function

1. In the **AWS Lambda** interface,

   - Select **Functions**
   - Click **Create function**

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00014.png?featherlight=false&width=70pc)

2. At the **Create function** interface,

   Under **Basic information**,

   - In **Function name**, enter **`UpsertToES`**
   - In **Runtime**, select **Python 3.11**

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00015.png?featherlight=false&width=70pc)

3. Leave the remaining options as default, finally click **Create function** to complete the Lambda Function creation.

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00016.png?featherlight=false&width=70pc)

4. Successful creation of the Lambda Function.

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00017.png?featherlight=false&width=70pc)

5. Scroll down to the bottom of the current page, in the **Layers** section, click **Add a layer**.

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00018.png?featherlight=false&width=70pc)

6. At the **Add layer** interface,

   Under **Choose a layer**,

   - In **Layer source**, select **Custom layers**
   - In **Custom layers**, choose **es-lib**
   - In **Version**, select the latest version created
   - Finally, click **Add** to complete the layer creation.

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00019.png?featherlight=false&width=70pc)

7. Next, we will copy and paste code from the **upsert_to_es.py** file into the code editor of **Code source**, then click **Deploy**.

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00021.png?featherlight=false&width=70pc)

8. Then, select the **Configuration** tab

   - Choose **Environment variables**
   - Select **Edit**

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00023.png?featherlight=false&width=70pc)

9. Add each environment variable according to the structure below.

```shell script
ES_HOST=<opensearch service domain>
ES_INDEX=<opensearch index name>
ES_TYPE=<opensearch type name>
REQUIRED_FIELDS=<columns to be used as primary key>
REGION_NAME=<region-name>
DATE_TYPE_FIELDS=<columns of which data type is either date or timestamp>
```

- Sample Example

```shell script
ES_HOST=vpc-retail-xxxxxxxxxxxxxxxxxxx.es.amazonaws.com
ES_INDEX=retail
ES_TYPE=trans
REQUIRED_FIELDS=Invoice,StockCode,Customer_ID
REGION_NAME=us-east-1
DATE_TYPE_FIELDS=InvoiceDate
```

- Click **Save** to save the changes

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00024.png?featherlight=false&width=70pc)

10. To execute the Lambda Function within a VPC and read data from Kinesis Data Streams, we need to add the necessary IAM Policy to execute the Lambda Function.

    In the **Configuration** tab,

    - Select **Permissions**
    - Under **Role name**, choose **UpsertToES-role-xxxxxxx**

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00025.png?featherlight=false&width=70pc)

11. Click **Add permissions** and then select **Attach policies**.

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00026.png?featherlight=false&width=70pc)

12. In the **Other permissions policies** section,

    - Enter **`AWSLambdaVPCAccessExecutionRole`** in the search bar
    - Select **AWSLambdaVPCAccessExecutionRole**
    - Finally, click **Add permissions**

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00027.png?featherlight=false&width=70pc)

13. Next, click **Add permissions** and then select **Attach policies**.

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00028.png?featherlight=false&width=70pc)

14. In the **Other permissions policies** section,

    - Enter **`AmazonKinesisReadOnlyAccess`** in the search bar
    - Select **AmazonKinesisReadOnlyAccess**
    - Finally, click **Add permissions**

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00029.png?featherlight=false&width=70pc)

15. Click **Add permissions** and then select **Create inline policy**.

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00031.png?featherlight=false&width=70pc)

16. In the **Policy editors** section,

    - Select **JSON**
    - Enter the policy statements according to the structure below. This IAM Policy will allow the Lambda Function to collect data into the **retail** index in OpenSearch Service.

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
Please note that you should replace **region** and **account-id** with the appropriate values for your project.
{{% /notice %}}

- Finally, click **Next** to proceed to the next step.

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00034.png?featherlight=false&width=70pc)

17. In the **Review and create** section,

    - In the **Policy name** field, enter **`UpsertToESDefaultPolicyWS2`**
    - Click **Create policy**

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00035.png?featherlight=false&width=70pc)

18. In the **Configuration** tab,

    - Select **VPC**
    - Click **Edit**

![Configure VPC](/images/5.2-IngestRealTimeData/createlayer-00036.png?featherlight=false&width=70pc)

19. In the **Edit VPC** interface,

    - In the **VPC** field, select **vpc-xxxxxxxxxxxx (10.0.0.0/16)**
    - In the **Subnets** field, select **project-businesss-intelligence-system-subnet-private2-us-east-1b** and **project-businesss-intelligence-system-subnet-private1-us-east-1a**
    - In the **Security groups** field, select **use-es-cluster-sg**

![Configure VPC](/images/5.2-IngestRealTimeData/createlayer-00037.png?featherlight=false&width=70pc)

20. Click **Save** to complete the VPC configuration

![Configure VPC](/images/5.2-IngestRealTimeData/createlayer-00038.png?featherlight=false&width=70pc)

![Configure VPC](/images/5.2-IngestRealTimeData/createlayer-00039.png?featherlight=false&width=70pc)

21. Click **Add trigger**

![Add Trigger](/images/5.2-IngestRealTimeData/createlayer-00040.png?featherlight=false&width=70pc)

22. In the **Add trigger** interface,

    Under **Trigger configuration**,

    - Select **Kinesis**
    - In the **Kinesis stream** field, select **kinesis/retail-trans**
    - Click **Add** to complete adding the trigger

![Add Trigger](/images/5.2-IngestRealTimeData/createlayer-00042.png?featherlight=false&width=70pc)

23. Verify that the trigger has been successfully added

![Add Trigger](/images/5.2-IngestRealTimeData/createlayer-00043.png?featherlight=false&width=70pc)

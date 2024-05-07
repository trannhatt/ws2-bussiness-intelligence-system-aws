---
title: "Create and Configure AWS Lambda Function"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

### Create and Configure AWS Lambda Function

1. On the **AWS Lambda** interface,

   - Select **Functions**
   - Click on **Create function**

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00014.png?featherlight=false&width=70pc)

2. In the **Create function** interface,

   Under **Basic information**,

   - Enter **`UpsertToES`** in the **Function name** field
   - Choose **Python 3.11** for the **Runtime**

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00015.png?featherlight=false&width=70pc)

3. Leave the other options as default, and finally click **Create function** to complete the Lambda Function creation.

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00016.png?featherlight=false&width=70pc)

4. Successful creation of the Lambda Function.

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00017.png?featherlight=false&width=70pc)

5. Scroll down to the bottom of the current page, in the **Layers** section, select **Add a layer**.

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00018.png?featherlight=false&width=70pc)

### Configure AWS Lambda Function

6. In the **Add layer** interface,

   Under **Choose a layer**,

   - Select **Custom layers** for the **Layer source**
   - Choose **es-lib** for the **Custom layers**
   - Select the latest version created for the **Version**
   - Finally, click **Add** to complete the Layer creation.

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00019.png?featherlight=false&width=70pc)

7. Next, copy and paste the code from the **upsert_to_es.py** file into the code editor of **Code source**, and select **Deploy**.

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00021.png?featherlight=false&width=70pc)

8. Then, select the **Configuration** tab

   - Choose **Environment variables**
   - Select **Edit**

![Configure Lambda Function](/images/5.2-IngestRealTimeData/createlayer-00023.png?featherlight=false&width=70pc)

9. Add each environment variable one by one as follows:

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

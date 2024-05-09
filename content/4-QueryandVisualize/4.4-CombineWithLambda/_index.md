---
---

title: "Athena CTAS"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 4.4 </b> "

---

## Combining Small Files Stored in S3 into Large Files with AWS Lambda Function

When data is streamed in real-time by Kinesis Data Firehose and stored in S3, it creates small data files, resulting in overall query performance degradation. When Athena plans a query, it enumerates all partition locations, which takes time, and processing and requesting each file also incurs computational costs. Therefore, loading a larger file from Amazon S3 is faster than loading the same record from multiple smaller files. To improve the query performance of Amazon Athena, we should combine small files into one large file. To execute these tasks periodically, we will create an AWS Lambda Function to execute Athena's Create Table As Select (CTAS) query.

![Architecture Workshop 2 - part 4.4](/ws2-bussiness-intelligence-system-aws/images/4/arch4.4.png?featherlight=false&width=70pc)

### Create a table to store query results

1. Go back to the Athena Query Editor, Create a new query, and enter the following command

   - Select **Run again**

{{% notice note %}}
Replace **`xxxxxxxxxxxxxxx`** at the last line under **LOCATION** with the S3 bucket name
{{% /notice %}}"

```sql
CREATE EXTERNAL TABLE `mydatabase.ctas_retail_trans_parquet`(
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
  'org.apache.hadoop.hive.ql.io.parquet.serde.ParquetHiveSerDe'
STORED AS INPUTFORMAT
  'org.apache.hadoop.hive.ql.io.parquet.MapredParquetInputFormat'
OUTPUTFORMAT
  'org.apache.hadoop.hive.ql.io.parquet.MapredParquetOutputFormat'
LOCATION
  's3://xxxxxxxxxxxxxxx/parquet-retail-trans'
TBLPROPERTIES (
  'has_encrypted_data'='false',
  'parquet.compression'='SNAPPY')
;
```

{{% notice info %}}
The command above will change the data format of the **retail_tran_json** table to **parquet** format and store it in a table named **ctas_retail_trans_parquet**.
Data in the **ctas_retail_trans_parquet** table will be stored at s3://xxxxxxxxxxxxxxx/parquet-retail-trans in the previously created S3 bucket.
{{% /notice %}}

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00023.png?featherlight=false&width=70pc)

### Create Lambda Function

2. On the **AWS console** interface,

   - Click on the search bar and type **`lambda`**
   - Under **Services**, select **Lambda**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0001.png?featherlight=false&width=70pc)

3. On the **AWS Lambda** interface,

   - Choose **Functions**
   - Select **Create a function**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0002.png?featherlight=false&width=70pc)

4. In the **Create function** interface,

   Under **Basic information**,

   - In the **Function name** field, enter **`MergeSmallFiles`**
   - In the **Runtime** field, select **Python 3.11**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0003.png?featherlight=false&width=70pc)

5. Leave the remaining options as default, and finally select **Create function** to complete creating the Lambda Function

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0004.png?featherlight=false&width=70pc)

6. Next, select **Add trigger**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0005.png?featherlight=false&width=70pc)

7. In the **Add trigger** interface,

   Under **Trigger configuration**,

   - Choose **CloudWatch Events/EventBridge**
   - In the **Rule** field, select **Create a new rule**
   - In the **Rule name** field, enter **`MergeSmallFilesEvent`**
   - In the **Rule description** field, enter **`MergeSmallFilesEvent`**
   - In the **Rule type** field, select **Schedule expression**
   - In the **Schedule expression** field, enter **`cron(5 * * * ? *)`** to run the task every 5 minutes
   - Finally, select **Add** to finish adding the trigger

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0006.png?featherlight=false&width=70pc)

8. Check if the trigger has been successfully added

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0007.png?featherlight=false&width=70pc)

9. Copy and paste the code from the **`athena_ctas.py`** file into the code editor of **Code source** and select **Deploy**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0008.png?featherlight=false&width=70pc)

10. Then, select the **Configuration** tab

- Choose **Environment variables**
- Select **Edit**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-0009.png?featherlight=false&width=70pc)

11. Add each environment variable one by one according to the following structure

```shell script
OLD_DATABASE=<source database>
OLD_TABLE_NAME=<source table>
NEW_DATABASE=<destination database>
NEW_TABLE_NAME=<destination table>
WORK_GROUP=<athena workgroup>
OLD_TABLE_LOCATION_PREFIX=<s3 location prefix of source table>
OUTPUT_PREFIX=<destination s3 prefix>
STAGING_OUTPUT_PREFIX=<staging s3 prefix used by athena>
COLUMN_NAMES=<columns of source table excluding partition keys>
```

- Example

```shell script
OLD_DATABASE=mydatabase
OLD_TABLE_NAME=retail_trans_json
NEW_DATABASE=mydatabase
NEW_TABLE_NAME=ctas_retail_trans_parquet
WORK_GROUP=primary
OLD_TABLE_LOCATION_PREFIX=s3://xxxxxxxxxxx/json-data
OUTPUT_PREFIX=s3://xxxxxxxxxxx/parquet-retail-trans
STAGING_OUTPUT_PREFIX=s3://xxxxxxxxxxx/tmp
COLUMN_NAMES=invoice,stockcode,description,quantity,invoicedate,price,customer_id,country
```

- Select **Save** to save the changes

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00020.png?featherlight=false&width=70pc)

12. To execute queries with Athena, we need an IAM Policy.

    On the **Configuration** tab,

    - Choose **Permissions**
    - Under **Execution role**, select **MergeSmallFiles-role-xxxxxx** to edit the Policy in this Role

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00012.png?featherlight=false&width=70pc)

13. Select **View the MergeSmallFiles-role-xxxxxx role**, which will navigate to another tab in your browser

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00013.png?featherlight=false&width=70pc)

14. In that tab, select **Add permissions** and choose **Attach policies**.

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00014.png?featherlight=false&width=70pc)

15. Under **Other permissions policies**,

    - In the search bar, type **`AmazonAthenaFullAccess`**
    - Select **AmazonAthenaFullAccess** from the search results
    - Finally, select **Add permissions**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00015.png?featherlight=false&width=70pc)

16. Next, select **Add permissions** and choose **Attach policies**.

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00016.png?featherlight=false&width=70pc)

17. Under **Other permissions policies**,

    - In the search bar, type **`AmazonS3FullAccess`**
    - Select **AmazonS3FullAccess** from the search results
    - Finally, select **Add permissions**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00017.png?featherlight=false&width=70pc)

18. We have successfully added 2 new Policies

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00018.png?featherlight=false&width=70pc)

19. Go back to the previous tab,

    - In the **Time out** field, enter the time as **`30s`**
    - Select **Save**

![Athena CTAS](/ws2-bussiness-intelligence-system-aws/images/4.4-CombineWithLambda/athenactas-00019.png?featherlight=false&width=70pc)

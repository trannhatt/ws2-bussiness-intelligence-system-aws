---
title: "Analyzing Data with Athena"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 4.1 </b> "
---

### Creating a Database

1. In the **AWS console**:

   - Click on the search bar and type **`athena`**
   - Under **Services**, select **Athena**

![Query Athena](/images/4.1-AnalyzeDataAthena/0001-queryathena.png?featherlight=false&width=70pc)

2. In the **Amazon Athena** interface:

   - Choose **Query your data with Trino SQL**
   - Select **Launch query editor**

![Query Athena](/images/4.1-AnalyzeDataAthena/0002-queryathena.png?featherlight=false&width=70pc)

{{% notice note %}}
If this is your first time using Athena, you need to set the location of S3 to store query results. In the **Query editor**, select **Edit settings**. Next, create a new folder in the previously created S3 bucket to store query results. Following the pattern **`s3://xxxxxxxxxxx/athena-query-results/`**, where **`xxxxxxxxxxx`** is the name of the S3 bucket. Select **Save** to complete the storage configuration.
{{% /notice %}}

![Query Athena](/images/4.1-AnalyzeDataAthena/0003.1-queryathena.png?featherlight=false&width=70pc)

![Query Athena](/images/4.1-AnalyzeDataAthena/0004.1-queryathena.png?featherlight=false&width=70pc)

3. Now, let's query data with Athena. First, create a new database named **mydatabase**.

   - Enter the command below into the query editor window and select **Run again**.
   - We can see the command execution result. Finally, under **Database**, select **mydatabase** as the created database.

```sql
CREATE DATABASE IF NOT EXISTS mydatabase
```

![Query Athena](/images/4.1-AnalyzeDataAthena/0005-queryathena.png?featherlight=false&width=70pc)

### Creating a Table

4. Next,
   - Click **+** above the query window to open a new query.
   - Copy the query below into the query editor window, replacing **xxxxxxxxxxxxxxx** at the last line in **LOCATION** with the S3 bucket name
   - Finally, select **Run again**.

```sql
CREATE EXTERNAL TABLE IF NOT EXISTS `mydatabase.retail_trans_json`(
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
  'org.openx.data.jsonserde.JsonSerDe'
STORED AS INPUTFORMAT
  'org.apache.hadoop.mapred.TextInputFormat'
OUTPUTFORMAT
  'org.apache.hadoop.hive.ql.io.IgnoreKeyTextOutputFormat'
LOCATION
  's3://xxxxxxxxxxxxxxx/json-data'
```

![Query Athena](/images/4.1-AnalyzeDataAthena/0006-queryathena.png?featherlight=false&width=70pc)

5. The query executes successfully as shown in the image

   - The table named **retail_trans_json** will be created and displayed on the left control panel under **Tables**.

![Query Athena](/images/4.1-AnalyzeDataAthena/0007-queryathena.png?featherlight=false&width=70pc)

{{% notice note %}}
If encountering an error, check if you have updated the S3 bucket name under **LOCATION** correctly, and make sure you have selected **mydatabase** under **Database** and **AwsDataCatalog** as **Data source**.
{{% /notice %}}

6. Next,
   - Click **+** above the query window to open a new query.
   - Run the query below to load partitioned data.
   - Finally, select **Run again**.

```sql
MSCK REPAIR TABLE mydatabase.retail_trans_json
```

![Query Athena](/images/4.1-AnalyzeDataAthena/0008-queryathena.png?featherlight=false&width=70pc)

{{% notice note %}}
We can list all partitions in the Athena table in unsorted order by running the query below.
{{% /notice %}}

```sql
SHOW PARTITIONS mydatabase.retail_trans_json
```

![Query Athena](/images/4.1-AnalyzeDataAthena/0009-queryathena.png?featherlight=false&width=70pc)

### Querying Data

8. Next,
   - Click **+** above the query window to open a new query.
   - Enter the SQL command below to query 10 transactions from the **retail_trans_json** table.
   - Finally, select **Run again** and check the query result.

```sql
SELECT *
FROM retail_trans_json
LIMIT 10
```

![Query Athena](/images/4.1-AnalyzeDataAthena/0010-queryathena.png?featherlight=false&width=70pc)

![Query Athena](/images/4.1-AnalyzeDataAthena/0011-queryathena.png?featherlight=false&width=70pc)

{{% notice info %}}
We can experiment with writing different SQL commands to query, filter, and sort data based on various conditions. At this point, we have understood how Amazon Athena helps query data in Amazon S3 conveniently without the need for any database servers.
{{% /notice %}}

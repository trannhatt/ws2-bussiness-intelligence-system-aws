---
title: "Applying Machine Learning Models with SageMaker"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 4.3 </b> "
---

### Create an Amazon SageMaker Notebook Instance

1. In the **AWS console**

   - Click on the search bar and type **`sagemaker`**
   - Under **Services**, select **Amazon SageMaker**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0001.png?featherlight=false&width=70pc)

2. In the **Amazon SageMaker** interface,

   - Choose **Notebook instances**
   - Click **Create notebook instance**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0003.png?featherlight=false&width=70pc)

3. In the **Create notebook instance** interface,

   Under **Notebook instance settings**,

   - Enter **`bi-system-sagemaker`** for **Notebook instance name**
   - Choose **ml.t3.medium** for **Notebook instance type**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0002.png?featherlight=false&width=70pc)

4. Next, in the **Permissions and encryption** section, we need to select a role for the notebook instance in Amazon SageMaker to interact with Amazon S3. If not already available, under **IAM role**, select **Create a new role**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0004.png?featherlight=false&width=70pc)

5. In the **Create an IAM role** section, choose **Any S3 bucket** and click **Create role**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0005.png?featherlight=false&width=70pc)

6. Once the IAM role is created, click on the blue hyperlink to go to the IAM role page in a new window. Here, we will add IAM permissions to allow SageMaker access to Athena.

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0006.png?featherlight=false&width=70pc)

7. Click **Add permissions** and then **Attach policies**.

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0007.png?featherlight=false&width=70pc)

8. In the **Other permissions policies** section,

   - In the search bar, type **`AmazonAthenaFullAccess`**
   - Select **AmazonAthenaFullAccess**
   - Finally, click **Add permissions**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0008.png?featherlight=false&width=70pc)

9. You will see a policy successfully added to this IAM role.

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0009.png?featherlight=false&width=70pc)

10. Return to the **Create notebook instance** interface, leave all other options as default values, and click **Create notebook instance**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-00010.png?featherlight=false&width=70pc)

11. Wait for the notebook instance to be created successfully. Once the status changes to **InService**, click **Open Jupyter**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-00011.png?featherlight=false&width=70pc)

### Connect SageMaker Jupyter Notebook to Athena

12. In the **Jupyter notebook**,

    - Click **New**
    - Then select **conda_python3** for the kernel.
    - This action will open the notebook in a new tab.

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-00012.png?featherlight=false&width=70pc)

13. In the **notebook**,

    - Enter the command below in a cell
    - Click **Run** to install the Athena JDBC driver.
    - Check that PyAthena has been successfully installed.

```shell script
!pip install PyAthena[SQLAlchemy]
```

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-00013.png?featherlight=false&width=70pc)

### Working with Pandas

14. We can load data from Athena table in S3 into a structured DataFrame and apply machine learning.

```python
from pyathena import connect
import pandas as pd
conn = connect(s3_staging_dir='s3://xxxxxxxxxxxxxxxxxx/athena-query-results/',
               region_name='us-east-1')
df = pd.read_sql("SELECT * FROM mydatabase.retail_trans_json LIMIT 10;", conn)
df
```

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-00014.png?featherlight=false&width=70pc)

{{% notice info %}}
Your region: Enter the command below to view the current AWS region, make sure the region matches the S3 bucket and database.
{{% /notice %}}

```shell script
!aws configure get region
```

15. We can further explore the data. For example, plotting a bar chart to display the quantity of **products** sold for each **item** by code below (assuming we take the top 10 rows of the DataFrame to be used for plotting).

```python
import seaborn as sns

plt.figure(figsize=(10, 6))
sns.barplot(x='stockcode', y='quantity', data=df.head(10))
plt.title('Số lượng sản phẩm bán ra cho mỗi mặt hàng')
plt.xlabel('Mã mặt hàng')
plt.ylabel('Số lượng')
plt.xticks(rotation=45)
plt.show()
```

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-00019.png?featherlight=false&width=70pc)

16. We can use a Linear Regression model to predict the quantity of items sold based on price. This allows us to examine the relationship between price and quantity sold, an important part of business and marketing data analysis, as shown in the example below where you'll plot the data using the matplotlib library.

```python
from sklearn.linear_model import LinearRegression
import matplotlib.pyplot as plt

X = df[['price']]
y = df['quantity']

model = LinearRegression()
model.fit(X, y)

predicted_quantity = model.predict(X)

plt.figure(figsize=(10, 6))
plt.scatter(X, y, color='blue', label='Actual Data')
plt.plot(X, predicted_quantity, color='red', label='Linear Regression')
plt.xlabel('Price')
plt.ylabel('Quantity')
plt.legend()
plt.grid(True)
plt.show()
```

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-00015.png?featherlight=false&width=70pc)

---
title: "Áp dụng các mô hình học máy với SageMaker"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 4.3 </b> "
---

### Tạo Amazon SageMaker Notebook Instance

1. Tại giao diện **AWS console**

   - Nhấn chọn thanh tìm kiếm và nhập **`sagemaker`**
   - Tại mục **Services** chọn **Amazon SageMaker**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0001.png?featherlight=false&width=70pc)

2. Tại giao diện **Amazon SageMaker**

   - Chọn **Notebook instances**
   - Chọn **Create notebook instance**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0003.png?featherlight=false&width=70pc)

3. Tại giao diện **Create notebook instance**

   Trong phần **Notebook instance settings**,

   - Tại mục **Notebook instance name**, nhập **`bi-system-sagemaker`**
   - Tại mục **Notebook instance tvpe**, chọn **ml.t3.medium**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0002.png?featherlight=false&width=70pc)

4. Tiếp tục, trong phần **Permissions and encryption**, chúng ta cần chọn role cho notebook instance trong Amazon SageMaker để tương tác với Amazon S3. Nếu chưa có, tại mục **IAM role** chọn **Create a new role**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0004.png?featherlight=false&width=70pc)

5. Trong phần **Create an IAM role**, chọn **Any S3 bucket** và chọn **Create role**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0005.png?featherlight=false&width=70pc)

6. Sau khi IAM role được tạo, hãy nhấp vào đường dẫn màu xanh để đến trang IAM role trong một cửa sổ mới. Ở đây, chúng ta sẽ thêm quyền IAM để cho phép SageMaker truy cập vào Athena.

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0006.png?featherlight=false&width=70pc)

7. Chọn **Add permissions** và chọn **Attach policies**.

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0007.png?featherlight=false&width=70pc)

8. Trong phần **Other permissions policies**

   - Tại thanh tìm kiếm, nhập **`AmazonAthenaFullAccess`**
   - Chọn **AmazonAthenaFullAccess** vừa tìm được
   - Cuối cùng chọn **Add permissions**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0008.png?featherlight=false&width=70pc)

9. Chúng ta sẽ thấy một police đã được thêm vào IAM role này thành công

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-0009.png?featherlight=false&width=70pc)

10. Quay lại giao diện **Create notebook instance**, tất cả các tùy chọn khác chúng ta để giá trị mặc định và chọn **Create notebook instance**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-00010.png?featherlight=false&width=70pc)

11. Đợi notebook instance tạo thành công, trạng thái sẽ được đổi thành **InService**. Khi đó chọn **Open Jupyter**

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-00011.png?featherlight=false&width=70pc)

### Kết nối SageMaker Jupyter notebook với Athena

12. Trong **Jupyter notebook**,

    - Chọn **New**
    - Sau đó chọn **conda_python3** cho kernel.
    - Thao tác này sẽ mở notebook trong tab mới.

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-00012.png?featherlight=false&width=70pc)

13. Trong **notebook**,

    - Nhập lệnh bên dưới vào một ô
    - Chọn **Run** để cài đặt Athena JDBC driver.
    - Kiểm tra kết quả PyAthena đã được cài đặt thành công.

```shell script
!pip install PyAthena[SQLAlchemy]
```

![SageMaker](/ws2-bussiness-intelligence-system-aws/images/4.3-AthenaAndSageMaker/sagemaker-00013.png?featherlight=false&width=70pc)

### Thao tác với Pandas

14. Chúng ta có thể tải dữ liệu trong bảng Athena từ S3 vào khung dữ liệu có cấu trúc và áp dụng học máy.

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
Region của bạn: nhập lệnh bên dưới để xem region AWS hiện tại, đãm bảo region trùng với S3 bucket và database.
{{% /notice %}}

```shell script
!aws configure get region
```

15. Chúng ta có thể khám phá thêm về dữ liệu. ví dụ như vẽ biểu đồ cột để hiển thị số lượng **sản phẩm (quantity)** bán ra cho mỗi **mặt hàng (stockcode)** theo mã bên dưới (giả sử chúng ta lấy 10 hàng đầu tiên của DataFrame sẽ được sử dụng để vẽ biểu đồ).

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

1.  Chúng ta có thể sử dụng mô hình Linear Regression để dự đoán số lượng hàng bán ra dựa trên giá. Bằng cách này, chúng ta có thể xem xét mối quan hệ giữa giá và số lượng hàng bán ra, một phần quan trọng của phân tích dữ liệu kinh doanh và tiếp thị, như ví dụ bên dưới chúng ta bạn sẽ vẽ biểu đồ dữ liệu bằng thư viện matplotlib.

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

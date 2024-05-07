---
title: "Trực quan hóa dữ liệu với QuickSight"
date: "2024-05-04"
weight: 2
chapter: false
pre: " <b> 4.2 </b> "
---

## Trực quan hóa dữ liệu với QuickSight

1. Truy cập giao diện **AWS console**:

   - Nhấn vào thanh tìm kiếm và nhập **`quicksight`**
   - Tại mục **Services**, chọn **QuickSight**

![Visualization QuickSight](/ws2-bussiness-intelligence-system-aws/images/4.2-DataVisualizationQuickSight/0001-quicksight.png?featherlight=false&width=70pc)

2. Để sử dụng phiên bản **Standard Edition**, chọn **here**

![Visualization QuickSight](/ws2-bussiness-intelligence-system-aws/images/4.2-DataVisualizationQuickSight/0002-quicksight.png?featherlight=false&width=70pc)

![Visualization QuickSight](/ws2-bussiness-intelligence-system-aws/images/4.2-DataVisualizationQuickSight/0003-quicksight.png?featherlight=false&width=70pc)

3. Hoàn tất đăng ký tài khoản và chọn **Go to Amazon QuickSight**

![Visualization QuickSight](/ws2-bussiness-intelligence-system-aws/images/4.2-DataVisualizationQuickSight/0004-quicksight.png?featherlight=false&width=70pc)

4. Chọn **New analysis**

![Visualization QuickSight](/ws2-bussiness-intelligence-system-aws/images/4.2-DataVisualizationQuickSight/0005-quicksight.png?featherlight=false&width=70pc)

5. Chọn **New dataset**

![Visualization QuickSight](/ws2-bussiness-intelligence-system-aws/images/4.2-DataVisualizationQuickSight/0006-quicksight.png?featherlight=false&width=70pc)

6. Chọn **Athena**

![Visualization QuickSight](/ws2-bussiness-intelligence-system-aws/images/4.2-DataVisualizationQuickSight/0007-quicksight.png?featherlight=false&width=70pc)

7. Trong phần **New Athena data source**:

   - Tại mục **Data source name**, nhập **`retail-quicksight`**
   - Tại mục **Athena workgroup**, chọn **[ primary ]**
   - Chọn **Validate connection** để kết nối thành **Validated**
   - Cuối cùng, chọn **Create data source**

![Visualization QuickSight](/ws2-bussiness-intelligence-system-aws/images/4.2-DataVisualizationQuickSight/0008-quicksight.png?featherlight=false&width=50pc)

8. Tiếp tục, trong phần **Choose your table**:

   - Tại mục **Catalog: contain sets of databases.**, chọn **AwsDataCatalog**
   - Tại mục **Database: contain sets of tables.**, chọn **mydatabase**
   - Tại mục **Tables: contain the data you can visualize.**, chọn **retail_trans_json**
   - Cuối cùng, chọn **Select**

![Visualization QuickSight](/ws2-bussiness-intelligence-system-aws/images/4.2-DataVisualizationQuickSight/0009-quicksight.png?featherlight=false&width=50pc)

9. Trong phần **Finish dataset creation**, chọn **Directly query your data** và chọn **Visualize**

![Visualization QuickSight](/ws2-bussiness-intelligence-system-aws/images/4.2-DataVisualizationQuickSight/0010-quicksight.png?featherlight=false&width=50pc)

10. Trực quan hoá dữ liệu:

    - Tại mục **CHANGE VISUAL TYPE**, chọn loại biểu đồ ví dụ như **Vertical bar chart**
    - Kéo **invoice** từ phần **Data** bên trái vào **X AXIS** và kéo **price** và **quanity** vào **VALUE**
    - Một biểu đồ sẽ hiển thị như ảnh

![Visualization QuickSight](/ws2-bussiness-intelligence-system-aws/images/4.2-DataVisualizationQuickSight/0012-quicksight.png?featherlight=false&width=70pc)

### Chia sẻ Dashboard với người dùng khác

11. Chia sẻ Dashboard:

    - Chọn tên tài khoản ở góc trên bên phải và chọn **Manage QuickSight**

![Visualization QuickSight](/ws2-bussiness-intelligence-system-aws/images/4.2-DataVisualizationQuickSight/0014-quicksight.png?featherlight=false&width=30pc)

12. Chọn **Invite users**

![Visualization QuickSight](/ws2-bussiness-intelligence-system-aws/images/4.2-DataVisualizationQuickSight/0015-quicksight.png?featherlight=false&width=70pc)

13. Nhập địa chỉ email của người mà bạn muốn chia sẻ hình ảnh trực quan. Cuối cùng chọn **Invite**

![Visualization QuickSight](/ws2-bussiness-intelligence-system-aws/images/4.2-DataVisualizationQuickSight/0016-quicksight.png?featherlight=false&width=50pc)

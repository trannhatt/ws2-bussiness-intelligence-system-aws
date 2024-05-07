---
title: "Data Visualization with QuickSight"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 4.2 </b> "
---

### Data Visualization with QuickSight

1. In the **AWS console**

   - Click on the search bar and type **`quicksight`**
   - Under **Services**, select **QuickSight**

![Visualization QuickSight](/images/4.2-DataVisualizationQuickSight/0001-quicksight.png?featherlight=false&width=70pc)

2. To use the **Standard Edition**, select **here**

![Visualization QuickSight](/images/4.2-DataVisualizationQuickSight/0002-quicksight.png?featherlight=false&width=70pc)

![Visualization QuickSight](/images/4.2-DataVisualizationQuickSight/0003-quicksight.png?featherlight=false&width=70pc)

3. Sign up for an account, then select **Go to Amazon QuickSight**

![Visualization QuickSight](/images/4.2-DataVisualizationQuickSight/0004-quicksight.png?featherlight=false&width=70pc)

4. Click **New analysis**

![Visualization QuickSight](/images/4.2-DataVisualizationQuickSight/0005-quicksight.png?featherlight=false&width=70pc)

5. Choose **New dataset**

![Visualization QuickSight](/images/4.2-DataVisualizationQuickSight/0006-quicksight.png?featherlight=false&width=70pc)

6. Select **Athena**

![Visualization QuickSight](/images/4.2-DataVisualizationQuickSight/0007-quicksight.png?featherlight=false&width=70pc)

7. In the **New Athena data source** section,

   - Enter **`retail-quicksight`** for **Data source name**
   - Choose **[ primary ]** for **Athena workgroup**
   - Select **Validate connection** to ensure it shows **Validated**
   - Finally, click **Create data source**

![Visualization QuickSight](/images/4.2-DataVisualizationQuickSight/0008-quicksight.png?featherlight=false&width=50pc)

8. Next, in the **Choose your table** section,

   - Under **Catalog: contain sets of databases**, choose **AwsDataCatalog**
   - Under **Database: contain sets of tables**, choose **mydatabase**
   - Under **Tables: contain the data you can visualize**, select **retail_trans_json**
   - Finally, click **Select**

![Visualization QuickSight](/images/4.2-DataVisualizationQuickSight/0009-quicksight.png?featherlight=false&width=50pc)

9. In the **Finish dataset creation** section, select **Directly query your data** and then click **Visualize**

![Visualization QuickSight](/images/4.2-DataVisualizationQuickSight/0010-quicksight.png?featherlight=false&width=50pc)

10. Suppose we want to visualize **price** and **quantity** by **invoice**.

    - Under **CHANGE VISUAL TYPE**, choose a chart type like **Vertical bar chart**
    - Then drag **invoice** from the **Data** pane on the left to **X AXIS**, and drag **price** and **quantity** to **VALUE**.
    - You will see a chart as shown in the image

![Visualization QuickSight](/images/4.2-DataVisualizationQuickSight/0012-quicksight.png?featherlight=false&width=70pc)

### Share Dashboard with Other

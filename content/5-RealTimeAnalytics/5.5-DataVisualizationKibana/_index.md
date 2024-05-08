---
title: "Visualize Data with OpenSearch Dashboards"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: " <b> 5.5 </b> "
---

### Visualize Data with OpenSearch Dashboards

1. Accessing the main screen of OpenSearch Dashboards:

   - Start by clicking on the toolbar icon at the top left corner of the screen, then select **Home**.
   - Next, choose **Dashboards Management** to proceed with managing the dashboards.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00060.png?featherlight=false&width=70pc)

2. Creating an Index Pattern:

   - In the **Dashboards Management** interface, select **Index patterns**.
   - Click on **Create an index pattern** to start creating a new index pattern.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00061.png?featherlight=false&width=70pc)

3. Setting up Index Patterns:

   In the **Create index pattern** section:

   - Enter the index pattern name in the **Index pattern name** field, for example: **`retail*`**.
   - Then, click **Next step** to continue.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00064.png?featherlight=false&width=70pc)

4. Selecting the Time Field:

   - Under **Time field**, choose the field containing time information, for example: **InvoiceDate**.
   - Once done, click **Create index pattern** to create the index pattern.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00065.png?featherlight=false&width=70pc)

5. Advanced Customizations:

   - Select **Advanced settings** to access additional advanced settings.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00066.png?featherlight=false&width=70pc)

6. Setting Timezone for Date Formatting:

   - In the **Timezone for date formatting** section, select the desired timezone, for example: **Etc/UTC**.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00067.png?featherlight=false&width=70pc)

7. Opening OpenSearch Dashboards:

   - Once the setup is completed, select **OpenSearch Dashboards** to access the dashboard.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00068.png?featherlight=false&width=70pc)

8. Exploring Data:

   - In the **Overview** interface of OpenSearch Dashboards, select **Discover** to explore the data.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00069.png?featherlight=false&width=70pc)

9. Checking Data:

   - Ensure that the data is being collected and displayed accurately in OpenSearch.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00073.png?featherlight=false&width=70pc)
   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00075.png?featherlight=false&width=70pc)

10. Visualizing Data:

    - Use the visualization feature to display data on charts. You can select any field to visualize data over time.

    ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00075.png?featherlight=false&width=70pc)
    ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00076.png?featherlight=false&width=70pc)

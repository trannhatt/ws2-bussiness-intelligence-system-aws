---
title: "Trực quan hóa dữ liệu với Kibana"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: " <b> 5.5 </b> "
---

### Trực quan hóa dữ liệu với Kibana

1. Tại màn hình chính

   - Chọn vào biểu tượng thanh công cụ ở bên trái nút **Home**
   - Chọn **Dashboards Management**.

![Kibana](/images/5.2-IngestRealTimeData/createlayer-00060.png?featherlight=false&width=70pc)

2. Trong giao diện **Dashboards Management**

   - Chọn **Index patterns**
   - Chọn **create an index pattern**

![Kibana](/images/5.2-IngestRealTimeData/createlayer-00061.png?featherlight=false&width=70pc)

3. Tiếp tục, trong phần **Create index pattern**

   - Tại mục **Index pattern name**, nhập **`retail*`**
   - Chọn **Next step**

![Kibana](/images/5.2-IngestRealTimeData/createlayer-00064.png?featherlight=false&width=70pc)

4. - Tại mục **Time field**, chọn **InvoiceDate**
   - Chọn **Create index pattern** để hoàn tất việc tạo index

![Kibana](/images/5.2-IngestRealTimeData/createlayer-00065.png?featherlight=false&width=70pc)

5. Chọn **Advanced settings**

![Kibana](/images/5.2-IngestRealTimeData/createlayer-00066.png?featherlight=false&width=70pc)

6. Tại mục **Timezone for date formatting**, chọn **Etc/UTC**

![Kibana](/images/5.2-IngestRealTimeData/createlayer-00067.png?featherlight=false&width=70pc)

7. Chọn **OpenSearch Dashboards**

![Kibana](/images/5.2-IngestRealTimeData/createlayer-00068.png?featherlight=false&width=70pc)

8. Tại giao diện **Overview**, chọn **Discover**

![Kibana](/images/5.2-IngestRealTimeData/createlayer-00069.png?featherlight=false&width=70pc)

9. Kiểm tra dữ liệu đang được thu thập vào Amazon OpenSearch

![Kibana](/images/5.2-IngestRealTimeData/createlayer-00073.png?featherlight=false&width=70pc)

![Kibana](/images/5.2-IngestRealTimeData/createlayer-00075.png?featherlight=false&width=70pc)

10. Chúng ta có thể trực quan hoá một trường bất kỳ theo **InvoiceDate**

![Kibana](/images/5.2-IngestRealTimeData/createlayer-00075.png?featherlight=false&width=70pc)

![Kibana](/images/5.2-IngestRealTimeData/createlayer-00076.png?featherlight=false&width=70pc)

---
title: "Trực quan hóa dữ liệu với OpenSearch Dashboardsa"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: " <b> 5.5 </b> "
---

### Trực quan hóa dữ liệu với OpenSearch Dashboards

1. Truy cập vào màn hình chính của OpenSearch Dashboards:

   - Bắt đầu bằng cách nhấp vào biểu tượng thanh công cụ ở góc trái màn hình, sau đó chọn **Home**.
   - Tiếp theo, chọn **Dashboards Management** để tiếp tục quản lý bảng điều khiển.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00060.png?featherlight=false&width=70pc)

2. Tạo một Index patterns:

   - Trong giao diện **Dashboards Management**, chọn **Index patterns**.
   - Nhấn vào **Create an index pattern** để bắt đầu quá trình tạo một mẫu chỉ mục mới.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00061.png?featherlight=false&width=70pc)

3. Thiết lập Index patterns:

   Trong phần **Create index pattern**:

   - Nhập tên mẫu chỉ mục vào mục **Index pattern name**, ví dụ: **`retail*`**.
   - Sau đó, nhấn **Next step** để tiếp tục.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00064.png?featherlight=false&width=70pc)

4. Chọn trường thời gian:

   - Tại mục **Time field**, chọn trường dữ liệu chứa thông tin về thời gian, ví dụ: **InvoiceDate**.
   - Khi đã hoàn thành, nhấn **Create index pattern** để tạo mẫu chỉ mục.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00065.png?featherlight=false&width=70pc)

5. Tùy chỉnh nâng cao:

   - Chọn **Advanced settings** để truy cập các tùy chỉnh nâng cao khác.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00066.png?featherlight=false&width=70pc)

6. Thiết lập múi giờ cho định dạng ngày tháng:

   - Trong mục **Timezone for date formatting**, chọn múi giờ mong muốn, ví dụ: **Etc/UTC**.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00067.png?featherlight=false&width=70pc)

7. Mở OpenSearch Dashboards:

   - Sau khi hoàn tất cài đặt, chọn **OpenSearch Dashboards** để truy cập vào bảng điều khiển.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00068.png?featherlight=false&width=70pc)

8. Khám phá dữ liệu:

   - Tại giao diện **Overview** của OpenSearch Dashboards, chọn **Discover** để khám phá dữ liệu.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00069.png?featherlight=false&width=70pc)

9. Kiểm tra dữ liệu:

   - Đảm bảo rằng dữ liệu đang được thu thập và hiển thị chính xác trong OpenSearch.

   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00073.png?featherlight=false&width=70pc)
   ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00075.png?featherlight=false&width=70pc)

10. Trực quan hoá dữ liệu:

    - Sử dụng tính năng trực quan hoá để hiển thị dữ liệu trên biểu đồ. Bạn có thể chọn một trường bất kỳ để trực quan hoá dữ liệu theo thời gian.

    ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00075.png?featherlight=false&width=70pc)
    ![OpenSearch Dashboards](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00076.png?featherlight=false&width=70pc)

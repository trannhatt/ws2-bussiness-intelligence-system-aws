---
title: "Giới thiệu"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

### Tổng quan

**Trí Tuệ Kinh Doanh** bao gồm một bộ các phần mềm có khả năng cho phép doanh nghiệp truy cập, phân tích và rút ra những hiểu biết sâu sắc có thể hành động từ dữ liệu để đưa ra quyết định sáng suốt. Thông thường, các công cụ này trình bày dữ liệu thông qua bảng điều khiển và trực quan hóa giúp thân thiện với người dùng, tạo điều kiện thuận lợi cho việc nắm bắt các số liệu chính. Mặc dù theo truyền thống được quản lý bởi các nhóm CNTT có chuyên môn chuyên sâu, các công cụ BI hiện đại trao quyền cho người ra quyết định bằng cách tích hợp dữ liệu và khả năng phân tích dự đoán, cho phép họ tạo báo cáo và trích xuất thông tin chi tiết về doanh nghiệp cụ thể. Trong lịch sử, BI chủ yếu tập trung vào báo cáo mô tả và chẩn đoán về các hoạt động kinh doanh trong quá khứ và hiện tại.

![Architecture Workshop 2](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/archmain.png?featherlight=false&width=70pc)

**Amazon Athena** là dịch vụ truy vấn tương tác được thiết kế để phân tích dữ liệu được lưu trữ trong Amazon S3 bằng các câu lệnh SQL. Nó hoạt động trên mô hình không có máy chủ, loại bỏ nhu cầu quản lý cơ sở hạ tầng và người dùng chỉ bị tính phí cho các truy vấn họ thực hiện.

Amazon Athena cung cấp sự đơn giản và dễ sử dụng cho nguòi dùng. Người dùng có thể dễ dàng truy cập dữ liệu được lưu trữ trong Amazon S3, xác định lược đồ và bắt đầu truy vấn thông qua các câu lệnh SQL. Hầu hết các kết quả truy vấn được trả về trong vòng vài giây, loại bỏ nhu cầu về quy trình ETL phức tạp để chuẩn bị dữ liệu cho phân tích. Khả năng truy cập này trao quyền cho các cá nhân có kỹ năng SQL để phân tích hiệu quả các tập dữ liệu quy mô lớn mà không cần chuẩn bị dữ liệu rộng rãi.

![Amazon Athena Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/athenaicon.png?featherlight=false&width=8pc)

**Amazon Data Firehose** cung cấp giải pháp đơn giản và đáng tin cậy để tải dữ liệu phát trực tiếp vào nhiều kho dữ liệu và công cụ phân tích khác nhau. Nó hỗ trợ thu thập, chuyển đổi và tải dữ liệu phát trực tiếp tới các điểm đến như Amazon S3, Amazon Redshift, Amazon OpenSearch Service và Splunk, cho phép phân tích gần như thời gian thực với các công cụ và bảng thông tin nghiệp vụ hiện có.

Là một dịch vụ được quản lý toàn phần, Amazon Data Firehose có thể tự động thay đổi quy mô để đáp ứng thông lượng dữ liệu mà không cần quản trị liên tục. Nó cung cấp các tính năng như phân khối, nén, chuyển đổi và mã hóa dữ liệu trước khi tải, giảm mức sử dụng bộ nhớ tại điểm đích và tăng cường bảo mật.

![Amazon Data Firehose Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/datafirehoseicon.png?featherlight=false&width=12pc)

**Amazon Kinesis Data Streams** là dịch vụ phát trực tuyến dữ liệu theo thời gian thực có khả năng mở rộng cao và linh hoạt, có khả năng thu thập hàng gigabyte dữ liệu mỗi giây từ nhiều nguồn khác nhau. Các nguồn này bao gồm luồng nhấp chuột trên trang web, luồng sự kiện cơ sở dữ liệu, giao dịch tài chính, nguồn cấp dữ liệu truyền thông xã hội, nhật ký CNTT và sự kiện theo dõi vị trí. Dữ liệu thu thập được cung cấp trong vòng một phần nghìn giây, tạo điều kiện thuận lợi cho các ứng dụng phân tích thời gian thực như bảng thông tin trực tiếp, phát hiện bất thường, định giá linh hoạt và các trường hợp sử dụng khác yêu cầu thông tin chi tiết ngay lập tức.

![Amazon Kinesis Data Streams Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/datastreamicon.png?featherlight=false&width=12pc)

**Amazon OpenSearch Service** (OpenSearch) giúp đơn giản hóa việc triển khai, bảo mật, vận hành và mở rộng quy mô OpenSearch để tìm kiếm, phân tích và trực quan hóa dữ liệu theo thời gian thực. Nó cung cấp các API dễ sử dụng và khả năng phân tích thời gian thực để hỗ trợ nhiều trường hợp sử dụng khác nhau như phân tích nhật ký, tìm kiếm toàn văn bản, giám sát ứng dụng và phân tích dòng nhấp chuột. Cung cấp tính khả dụng, khả năng mở rộng và bảo mật ở cấp doanh nghiệp, dịch vụ này tích hợp với các công cụ nguồn mở như OpenSearch Dashboards và Logstash để nhập và trực quan hóa dữ liệu.

![Amazon OpenSearch Service Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/opensearchicon.png?featherlight=false&width=12pc)

**Amazon QuickSight** là một dịch vụ nghiệp vụ thông minh phi máy chủ hoạt động trên đám mây, cung cấp các phương tiện trực quan hóa dữ liệu, bảng điều khiển tương tác và phân tích dữ liệu được ML hỗ trợ. Bạn có thể sử dụng dịch vụ này để khám phá thông tin chuyên sâu ẩn từ dữ liệu của mình, thực hiện dự báo chính xác và mở ra các cơ hội kiếm tiền mới. QuickSight sử dụng ML để tạo các phản hồi chính xác cho những câu hỏi về dữ liệu bằng ngôn ngữ tự nhiên.

![Amazon QuickSight Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/quicksighticon.png?featherlight=false&width=8pc)

**Amazon SageMaker** bạn có thể xây dựng, huấn luyện và triển khai các mô hình ML cho mọi trường hợp sử dụng với cơ sở hạ tầng, công cụ và quy trình làm việc được quản lý hoàn toàn. SageMaker loại bỏ gánh nặng khỏi mỗi bước của quy trình ML để giúp phát triển các mô hình chất lượng cao dễ dàng hơn. SageMaker cung cấp tất cả các thành phần được sử dụng cho ML trong một bộ công cụ duy nhất để các mô hình được đưa vào sản xuất nhanh hơn với ít nỗ lực hơn và với chi phí thấp hơn.

![Amazon SageMaker Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/sagemakericon.png?featherlight=false&width=8pc)

**AWS Lambda** cho phép thực thi mã không cần máy chủ, loại bỏ nhu cầu cung cấp và quản lý máy chủ. Người dùng chỉ bị tính phí cho thời gian tính toán đã sử dụng và không bị tính phí khi mã không hoạt động.

Lambda hỗ trợ nhiều loại ứng dụng và dịch vụ phụ trợ khác nhau, không cần quản trị. Người dùng chỉ cần tải mã của họ lên và Lambda xử lý tất cả các khía cạnh của việc chạy và mở rộng quy mô mã với tính sẵn sàng cao. Ngoài ra, mã có thể được cấu hình để tự động kích hoạt từ các dịch vụ AWS khác hoặc được gọi trực tiếp từ ứng dụng web hoặc thiết bị di động.

![AWS Lambda Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/lambdaicon.png?featherlight=false&width=8pc)

**Amazon Simple Storage Service** (Amazon S3) là một giải pháp lưu trữ đối tượng có khả năng mở rộng cao, cung cấp khả năng mở rộng, tính khả dụng của dữ liệu, tính bảo mật và hiệu suất vượt trội. Nó phục vụ cho các tổ chức thuộc mọi quy mô và thuộc nhiều ngành khác nhau, cung cấp nền tảng đáng tin cậy để lưu trữ và bảo vệ mọi khối lượng dữ liệu cho các trường hợp sử dụng khác nhau như: các trang web, ứng dụng di động, hoạt động sao lưu và khôi phục, mục đích lưu trữ, ứng dụng doanh nghiệp, thiết bị IoT và phân tích dữ liệu lớn.

![Amazon Simple Storage Service Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/s3icon.png?featherlight=false&width=7pc)

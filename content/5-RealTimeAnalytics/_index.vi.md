---
title: "Phân tích dữ liệu theo thời gian thực"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

### Giới thiệu

Phần này đi sâu vào phân tích dữ liệu thời gian thực, chúng ta sẽ tạo Amazon OpenSearch Service, thêm các thư viện phổ biến vào AWS Lambda Layer, tạo và cấu hình AWS Lambda Function, kích hoạt AWS Lambda Function để nhập bản ghi vào Amazon OpenSearch và trực quan hóa dữ liệu bằng OpenSearch Dashboards. Chúng ta sẽ học được cách phân tích dữ liệu thời gian thực một cách hiệu quả và trực quan hóa thông tin chi tiết phục vụ cho mục đích ra quyết định.

![Architecture Workshop 2 - part 5](/images/5/arch5.png?featherlight=false&width=70pc)

### Nội dung

- [5.1 Tạo Amazon OpenSearch Service](5.1-CreateOpenSearch/)
- [5.2 Thêm thư viện dùng chung vào AWS Lambda Layer](5.2-IngestRealTimeData/)
- [5.3 Tạo AWS Lambda Function](5.3-CreateLambdaFunction/)
- [5.4 Kích hoạt AWS Lambda Function để nhập bản ghi vào Amazon OpenSearch](5.4-EnableLambdaFunction/)
- [5.5 Trực quan hóa dữ liệu với OpenSearch Dashboards](5.5-DataVisualizationKibana/)

---
title: "Introduction"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

### Overview

**Business Intelligence (BI)** encompasses a suite of software capabilities enabling businesses to access, analyze, and derive actionable insights from data for informed decision-making. Typically, BI tools present data through user-friendly dashboards and visualizations, facilitating the interpretation of key metrics. While traditionally managed by tech or IT teams with specialized expertise, modern BI tools empower decision-makers by integrating data and predictive analytics capabilities, allowing them to generate reports and extract specific business insights. Historically, BI has primarily focused on descriptive and diagnostic reporting of past and present business activities.

![Architecture Workshop 2](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/archmain.png?featherlight=false&width=70pc)

**Amazon Athena** is an interactive query service designed for analyzing data stored in Amazon S3 using standard SQL. It operates on a serverless model, eliminating the need for infrastructure management, and users are only charged for the queries they execute.

Amazon Athena offers simplicity and ease of use. Users can effortlessly access their data stored in Amazon S3, define the schema, and begin querying with standard SQL. Most query results are returned within seconds, eliminating the need for complex ETL processes to prepare data for analysis. This accessibility empowers individuals with SQL skills to efficiently analyze large-scale datasets without extensive data preparation.

![Amazon Athena Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/athenaicon.png?featherlight=false&width=8pc)

**Amazon Data Firehose** provides a simple and reliable solution for loading streaming data into various data stores and analytics tools. It supports capturing, transforming, and loading streaming data into destinations such as Amazon S3, Amazon Redshift, Amazon OpenSearch Service, and Splunk, enabling near real-time analytics with existing business intelligence tools and dashboards.

As a fully managed service, Amazon Data Firehose automatically scales to accommodate data throughput without requiring ongoing administration. It offers features like batching, compression, transformation, and encryption of data before loading, reducing storage usage at the destination and enhancing security.

![Amazon Data Firehose Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/datafirehoseicon.png?featherlight=false&width=12pc)

**Amazon Kinesis Data Streams** is a highly scalable and resilient real-time data streaming service capable of capturing gigabytes of data per second from a wide array of sources. These sources include website clickstreams, database event streams, financial transactions, social media feeds, IT logs, and location-tracking events. The collected data is made available within milliseconds, facilitating real-time analytics applications like live dashboards, anomaly detection, dynamic pricing, and other use cases requiring immediate insights.

![Amazon Kinesis Data Streams Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/datastreamicon.png?featherlight=false&width=12pc)

**Amazon OpenSearch Service** (OpenSearch Service) simplifies the deployment, security, operation, and scaling of OpenSearch for real-time data search, analysis, and visualization. It provides easy-to-use APIs and real-time analytics capabilities to support various use cases such as log analytics, full-text search, application monitoring, and clickstream analytics. Offering enterprise-grade availability, scalability, and security, the service integrates with open-source tools like OpenSearch Dashboards and Logstash for data ingestion and visualization.

![Amazon OpenSearch Service Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/opensearchicon.png?featherlight=false&width=12pc)

**Amazon QuickSight** is a rapid, cloud-based business intelligence (BI) service designed to facilitate the dissemination of insights across an organization. With QuickSight, users can effortlessly create and distribute interactive dashboards accessible via web browsers or mobile devices. These dashboards can also be embedded into applications, empowering customers with robust self-service analytics capabilities.

![Amazon QuickSight Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/quicksighticon.png?featherlight=false&width=8pc)

**Amazon SageMaker** you can build, train, and deploy ML models for any use case with fully managed infrastructure, tools, and workflows. SageMaker removes the heavy lifting from each step of the ML process to make it easier to develop high-quality models. SageMaker provides all of the components used for ML in a single toolset so models get to production faster with much less effort and at lower cost.

![Amazon SageMaker Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/sagemakericon.png?featherlight=false&width=8pc)

**AWS Lambda** enables serverless execution of code, eliminating the need for server provisioning and management. Users are billed solely for the compute time consumed, with no charges when the code is inactive.

Lambda supports various application and backend service types, requiring zero administration. Users simply upload their code, and Lambda handles all aspects of running and scaling it with high availability. Additionally, code can be configured to automatically trigger from other AWS services or be directly invoked from web or mobile applications.

![AWS Lambda Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/lambdaicon.png?featherlight=false&width=8pc)

**Amazon Simple Storage Service** (Amazon S3) is a highly scalable object storage solution offering unparalleled scalability, data availability, security, and performance. It caters to organizations of all sizes and across various industries, providing a reliable platform to store and safeguard any volume of data for diverse use cases. These include websites, mobile applications, backup and restore operations, archival purposes, enterprise applications, IoT devices, and big data analytics.

![Amazon Simple Storage Service Icon](/ws2-bussiness-intelligence-system-aws/images/1-Introduce/s3icon.png?featherlight=false&width=7pc)

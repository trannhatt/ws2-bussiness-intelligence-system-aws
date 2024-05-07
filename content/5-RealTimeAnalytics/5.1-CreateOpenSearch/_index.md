---
title: "Real-time Data Analysis with Amazon OpenSearch Service"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---

### Create Amazon OpenSearch Service

1. In the **AWS Management Console**,

   - Click on the search bar and type **`opensearch`**
   - Under **Services**, select **Amazon OpenSearch Service**

![Create OpenSearch](/images/5.1-CreateOpenSearch/createopensearch-0001.png?featherlight=false&width=70pc)

2. From the **Amazon OpenSearch Service** interface,

   - Click on **Domains** and then select **Create domain**

![Create OpenSearch](/images/5.1-CreateOpenSearch/createopensearch-00013.png?featherlight=false&width=70pc)

3. In the **Create domain** interface,

   - In the **Domain name** field, enter **`retail`**
   - In the **Domain creation method** section, select **Standard create**
   - In the **Templates** section, select **Dev/test**

![Create OpenSearch](/images/5.1-CreateOpenSearch/createopensearch-0002.png?featherlight=false&width=70pc)

4. In the **Deployment options** section,

   - In the **Deployment option** field, select **Domain without standby**
   - In the **Availability Zone** field, select **2-AZ**

![Create OpenSearch](/images/5.1-CreateOpenSearch/createopensearch-0003.png?featherlight=false&width=70pc)

5. Continue,

   - In the **Version** field, select **2.11 (latest)** as the latest version
   - In the **Instance family** field, select **General purpose**
   - In the **Instance type** field, select **t3.small.search**

![Create OpenSearch](/images/5.1-CreateOpenSearch/createopensearch-0004.png?featherlight=false&width=70pc)

6. In the **Number of nodes** field, enter **`6`**, leave the other options as default

![Create OpenSearch](/images/5.1-CreateOpenSearch/createopensearch-0005.png?featherlight=false&width=70pc)

![Create OpenSearch](/images/5.1-CreateOpenSearch/createopensearch-0006.png?featherlight=false&width=70pc)

7. In the **Network** section,

   - In the **Network** field, select **VPC access - recommended**
   - In the **IP address type** field, select **Dual-stack mode - recommended**
   - In the **VPC** field, select **vpc-xxxxxxxxx (10.0.0.0/16)**
   - In the **Subnets** field, select **project-businesss-intelligence-system-subnet-private2-us-east-1b** and **project-businesss-intelligence-system-subnet-private1-us-east-1a**
   - In the **Security groups** field, select **es-cluster-sg**

![Create OpenSearch](/images/5.1-CreateOpenSearch/createopensearch-0007.png?featherlight=false&width=70pc)

8. In the **Fine-grained access control** section, first enable **Enable fine-grained access control**

   - In the **Master user** field, select **Create master user**
   - In the **Master username** field, enter **`admin`**
   - In the **Master password** field, enter **`xxxxxxxxxxxxxx`**
   - In the **Confirm master password** field, enter **`xxxxxxxxxxxxxx`**

![Create OpenSearch](/images/5.1-CreateOpenSearch/createopensearch-0008.png?featherlight=false&width=70pc)

9. In the **Access policy** section,

   - In the **Domain access policy** field, select **Only use fine-grained access control**

![Create OpenSearch](/images/5.1-CreateOpenSearch/createopensearch-0009.png?featherlight=false&width=70pc)

10. In the **Encryption** section,

- In the **Choose an AWS KMS key** field, select **Use AWS owned key**

![Create OpenSearch](/images/5.1-CreateOpenSearch/createopensearch-00010.png?featherlight=false&width=70pc)

11. Leave the remaining options as default, and finally click **Create** to complete the OpenSearch creation process

![Create OpenSearch](/images/5.1-CreateOpenSearch/createopensearch-00011.png?featherlight=false&width=70pc)

12. New domains typically take 15–30 minutes to initialize and may take longer depending on the configuration.

![Create OpenSearch](/images/5.1-CreateOpenSearch/createopensearch-00012.png?featherlight=false&width=70pc)

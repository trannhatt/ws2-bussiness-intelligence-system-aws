---
title: "Create VPC"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2.2 </b> "
---

### Create VPC

{{% notice info %}}
In this project, we will perform actions in the **US East (N. Virginia) us-east-1** Region.
{{% /notice %}}

1. Log in to IAM User and select Region:
   - Log in to the previously created IAM User.
   - Choose the Region **US East (N. Virginia) us-east-1**.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0001-createvpc.png?featherlight=false&width=20pc)

2. Access AWS Console and select VPC:
   - Click on the search bar and type **`vpc`**.
   - Under **Services**, select **VPC**.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0002-createvpc.png?featherlight=false&width=70pc)

3. Create a new VPC:
   - In the **VPC** interface, choose **Your VPCs**.
   - Select **Create VPC**.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0003-createvpc.png?featherlight=false&width=70pc)

4. Set up information for the VPC:
   - In the **Create VPC** section, enter the following details:
     - Under **Resources to create**, select **VPC and more**.
     - Under **Name tag auto-generation**, select **Auto-generate** and enter **`project-businesss-intelligence-system`**.
     - For **IPv4 CIDR block**, enter **`10.0.0.0/16`**.
     - For **IPv6 CIDR block**, select **Amazon-provided IPv6 CIDR block**.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0004-createvpc.png?featherlight=false&width=70pc)

5. Continue setup:
   - In the **Create VPC** section, enter the following details:
     - For **Number of Availability Zones (AZs)**, select **2**.
     - For **First availability zone**, choose **us-east-1a**.
     - For **Second availability zone**, choose **us-east-1b**.
     - For **Number of public subnets**, select **2**.
     - For **Number of private subnets**, select **2**.
     - For **Customize subnets CIDR blocks**, enter the CIDR ranges for 4 Subnets: **`10.0.1.0/24`**, **`10.0.2.0/24`**, **`10.0.3.0/24`**, **`10.0.4.0/24`**.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0005-createvpc.png?featherlight=false&width=70pc)

6. Continue setup:
   - In the **Create VPC** section, enter the following details:
     - For **NAT gateways ($)**, select **In 1 AZ**.
     - For **Egress only internet gateway**, select **No**.
     - For **VPC endpoints**, select **None**.
     - For **DNS options**, select **Enable DNS hostnames** and **Enable DNS resolution**.
     - Finally, click **Create VPC**.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0006-createvpc.png?featherlight=false&width=70pc)

7. Complete VPC creation:
   - The VPC has been successfully created.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0007-createvpc.png?featherlight=false&width=70pc)

8. View detailed information of the VPC:
   - Click on **View VPC**.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0008-createvpc.png?featherlight=false&width=70pc)

9. Overview of resources within the VPC:
   - We can view an overview of the current resources within the VPC under the **Resource map** section.

![Create VPC](/ws2-bussiness-intelligence-system-aws/images/2.2-createVPC/0009-createvpc.png?featherlight=false&width=70pc)

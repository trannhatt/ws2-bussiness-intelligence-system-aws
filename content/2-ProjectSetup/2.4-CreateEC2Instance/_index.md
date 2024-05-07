---
title: "Launch EC2 Instance"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 2.4 </b> "
---

### Launch EC2 Instance

1. Access the EC2 interface and select Launch instances:
   - Choose **Instances**.
   - Then select **Launch instances**.

![Create EC2 Instance](/ws2-bussiness-intelligence-system-aws/images/2.4-createEC2Instance/0001-createec2instance.png?featherlight=false&width=70pc)

2. Configure EC2 Instance:
   - In the **Launch an instance** interface:
     - Under **Name and tags**, enter **`bastion-host-bi-system`**.
     - Under **Application and OS Images (Amazon Machine Image)**, select **AmazonLinux**.

![Create EC2 Instance](/ws2-bussiness-intelligence-system-aws/images/2.4-createEC2Instance/0002-createec2instance.png?featherlight=false&width=70pc)

3. Continue configuration:
   - Under **Instance type**, select **t2.micro**.
   - Under **Key pair (login)**, select **analytics-hol-ws2**.

![Create EC2 Instance](/ws2-bussiness-intelligence-system-aws/images/2.4-createEC2Instance/0003-createec2instance.png?featherlight=false&width=70pc)

{{% notice note %}}
Note: If you don't have a Key pair, select **Create new key pair**.
{{% /notice %}}

![Create EC2 Instance](/ws2-bussiness-intelligence-system-aws/images/2.4-createEC2Instance/0004-createec2instance.png?featherlight=false&width=70pc)

4. Configure Network settings:
   - Under **VPC - required**, select **vpc-02e213a24e410c89 (project-businesss-intelligence-system-vpc)**.
   - Under **Subnet**, select **subnet-Ofa8fc52157d75fba**.
   - Under **Auto-assign public IP**, select **Enable**.
   - Under **Firewall (security groups)**, select **Select existing security group** and choose **bastion-sg** and **use-es-cluster-sg**.

![Create EC2 Instance](/ws2-bussiness-intelligence-system-aws/images/2.4-createEC2Instance/0005-createec2instance.png?featherlight=false&width=70pc)

5. Launch instance:
   - Leave the remaining fields as default, and finally select **Launch instance** to complete the creation of the Bastion Host server.

![Create EC2 Instance](/ws2-bussiness-intelligence-system-aws/images/2.4-createEC2Instance/0006-createec2instance.png?featherlight=false&width=70pc)

6. EC2 Instance is successfully launched:

![Create EC2 Instance](/ws2-bussiness-intelligence-system-aws/images/2.4-createEC2Instance/0007-createec2instance.png?featherlight=false&width=70pc)
![Create EC2 Instance](/ws2-bussiness-intelligence-system-aws/images/2.4-createEC2Instance/0008-createec2instance.png?featherlight=false&width=70pc)

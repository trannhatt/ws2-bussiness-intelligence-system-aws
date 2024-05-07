---
title: "Create Security Groups"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 2.3 </b> "
---

### Create Security Groups

1. Access AWS Console and select EC2:
   - Click on the search bar.
   - Type **`ec2`**.
   - Under **Services**, select **EC2**.

![Create Security Groups](/ws2-bussiness-intelligence-system-aws/images/2.3-createSecurityGroup/0001-createsg.png?featherlight=false&width=70pc)

2. Create Security Group for the EC2 instance acting as a bastion host:
   - In the **EC2** interface, select **Security Group**.
   - Choose **Create security group**.

![Create Security Groups](/ws2-bussiness-intelligence-system-aws/images/2.3-createSecurityGroup/0002-createsg.png?featherlight=false&width=70pc)

3. Configure Security Group:
   - In the **Create security group** section, enter the following details:
     - **Security Group name**: `bastion-sg`.
     - **Description**: `Security group for bastion`.
     - **VPC**: `vpc-02e213a24e410c89 (project-businesss-intelligence-system-vpc)`.
     - Click **Add rule**, under **Type**: select **SSH** and **Source**: select **Anywhere IPv4 (0.0.0.0/0)**.

![Create Security Groups](/ws2-bussiness-intelligence-system-aws/images/2.3-createSecurityGroup/0003-createsg.png?featherlight=false&width=70pc)

4. Add tags to the Security Group:
   - Under **Tags - optional**, click **Add new tag**:
     - **Key**: `Name`.
     - **Value - optional**: `bastion-sg`.
   - Finally, click **Create security group**.

![Create Security Groups](/ws2-bussiness-intelligence-system-aws/images/2.3-createSecurityGroup/0004-createsg.png?featherlight=false&width=70pc)

5. Security Group for the EC2 instance is successfully created:

![Create Security Groups](/ws2-bussiness-intelligence-system-aws/images/2.3-createSecurityGroup/0005-createsg.png?featherlight=false&width=70pc)
![Create Security Groups](/ws2-bussiness-intelligence-system-aws/images/2.3-createSecurityGroup/0006-createsg.png?featherlight=false&width=70pc)

We will now continue to create 2 Security Groups to use for OpenSearch Service.

6. Configure Security Group for OpenSearch Service:
   - In the **Create security group** section, enter the following details:
     - **Security Group name**: `use-es-cluster-sg`.
     - **Description**: `Security group for an es client`.
     - **VPC**: `vpc-02e213a24e410c89 (project-businesss-intelligence-system-vpc)`.
     - Skip the **Inbound rules** section.

![Create Security Groups](/ws2-bussiness-intelligence-system-aws/images/2.3-createSecurityGroup/0007-createsg.png?featherlight=false&width=70pc)

7. Add tags to the Security Group:
   - Under **Tags - optional**, click **Add new tag**:
     - **Key**: `Name`.
     - **Value - optional**: `use-es-cluster-sg`.
   - Finally, click **Create security group**.

![Create Security Groups](/ws2-bussiness-intelligence-system-aws/images/2.3-createSecurityGroup/0008-createsg.png?featherlight=false&width=70pc)

8. Security Group is successfully created:

![Create Security Groups](/ws2-bussiness-intelligence-system-aws/images/2.3-createSecurityGroup/0009-createsg.png?featherlight=false&width=70pc)
![Create Security Groups](/ws2-bussiness-intelligence-system-aws/images/2.3-createSecurityGroup/0010-createsg.png?featherlight=false&width=70pc)

9. Continue configuring Security Group for OpenSearch Service:
   - In the **Create security group** section, enter the following details:
     - **Security Group name**: `es-cluster-sg`.
     - **Description**: `Security group for an es cluster`.
     - **VPC**: `vpc-02e213a24e410c89 (project-businesss-intelligence-system-vpc)`.
     - Click **Add rule**, under **Type**: select **All TCP** and **Source**: select **Custom (use-es-cluster-sg)**.

![Create Security Groups](/ws2-bussiness-intelligence-system-aws/images/2.3-createSecurityGroup/0011-createsg.png?featherlight=false&width=70pc)

10. Add tags to the Security Group:
    - Under **Tags - optional**, click **Add new tag**:
      - **Key**: `Name`.
      - **Value - optional**: `es-cluster-sg`.
    - Finally, click **Create security group**.

![Create Security Groups](/ws2-bussiness-intelligence-system-aws/images/2.3-createSecurityGroup/0012-createsg.png?featherlight=false&width=70pc)

11. Security Group is successfully created:

![Create Security Groups](/ws2-bussiness-intelligence-system-aws/images/2.3-createSecurityGroup/0013-createsg.png?featherlight=false&width=70pc)
![Create Security Groups](/ws2-bussiness-intelligence-system-aws/images/2.3-createSecurityGroup/0014-createsg.png?featherlight=false&width=70pc)

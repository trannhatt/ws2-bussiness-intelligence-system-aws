---
title: " Activate AWS Lambda Function"
date: "2024-05-08"
weight: 4
chapter: false
pre: "<b>5.4</b>"
---

### Activate AWS Lambda Function to Ingest Records into Amazon OpenSearch

{{% notice info %}}
Initially, we created an Amazon OpenSearch cluster within a Virtual Private Cloud (VPC). Therefore, the Amazon OpenSearch endpoint and Kibana endpoint cannot be accessed directly over the internet. Hence, to access these endpoints, we need to set up an SSH tunnel and forward a local port.
{{% /notice %}}

1. Using SSH Tunneling, first, we'll configure SSH

   - For Mac/Linux operating systems to access the OpenSearch cluster, add SSH tunnel configuration to your personal computer's SSH configuration file as follows:

```shell script
# OpenSearch Tunnel
Host estunnel
  HostName <EC2 Public IP of Bastion Host>
  User ec2-user
  IdentitiesOnly yes
  IdentityFile ~/.ssh/analytics-hol.pem
  LocalForward 9200 <OpenSearch Endpoint>:443
```

{{% notice note %}}
**EC2 Public IP of the Bastion Host** is the Public IP address of the EC2 instance we created in the **Preparation Steps** section.
{{% /notice %}}

- Example

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00044.png?featherlight=false&width=50pc)

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00045.png?featherlight=false&width=50pc)

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00046.png?featherlight=false&width=50pc)

2. Finally, run the command **`ssh -N estunnel`** in the Terminal

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00048.png?featherlight=false&width=50pc)

3. Access the following URL in your browser:

   - **`https://localhost:9200/_dashboards/app/login?`**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00047.png?featherlight=false&width=70pc)

4. Enter the username and password that we set up when creating the Amazon OpenSearch Service. The username and password are stored in **AWS Secrets Manager** with the name `OpenSearchMasterUserSecret1-xxxxxxxxxxxx`.

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00049.png?featherlight=false&width=70pc)

5. We have successfully accessed the Amazon OpenSearch Service. This is the main screen interface.

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00050.png?featherlight=false&width=70pc)

6. Next, on the main screen:

   - Select the toolbar icon on the left side of the **Home** button
   - Choose **Security**.

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00051.png?featherlight=false&width=70pc)

7. In the **Get started** interface, select **Create new role**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00052.png?featherlight=false&width=70pc)

8. In the **Create Role** section,
   - At the **Name** field, enter **`firehose_role`**
   - Under **Cluster permissions**, add 2 permissions: **cluster_composite_ops** and **cluster_monitor**
   - Under **Index**, add the index **retail\***

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00053.png?featherlight=false&width=70pc)

9. Under **Index permissions**, add 3 actions: **crud**, **create_index**, and **manage**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00054.png?featherlight=false&width=70pc)

10. Finally, select **Create** to complete the role creation

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00055.png?featherlight=false&width=70pc)

11. The role has been created with the configurations as shown in the image

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00056.png?featherlight=false&width=70pc)

12. Next, select the **Mapped users** tab

    - Choose **Map users**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00057.png?featherlight=false&width=70pc)

13. In the **Map user** section,

    - In the **Backend roles** field, enter the IAM ARN that the Lambda Function is using
    - Select **Map**

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00058.png?featherlight=false&width=70pc)

14. Verify the successful mapping

![Configure Lambda Function](/ws2-bussiness-intelligence-system-aws/images/5.2-IngestRealTimeData/createlayer-00059.png?featherlight=false&width=70pc)

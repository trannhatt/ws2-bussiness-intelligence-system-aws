---
title: "Configure EC2 Instance"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: " <b> 2.5 </b> "
---

### Configure EC2 Instance

We will configure the EC2 instances to access and manage other AWS resources as follows:

1. Log in to the newly created EC2 instance via SSH protocol:

```shell script
ssh -i "<Key pair name>" ec2-user@<Public IP>
```

![Configure EC2 Instance](/images/2.5-configureEC2Instance/0001-configureec2instance.png?featherlight=false&width=70pc)

2. Download the project source code:

```shell script
wget 'https://github.com/trannhatt/Analytics-on-AWS-Build-BI-System/archive/refs/heads/main.zip'
```

3. Unzip the downloaded source code:

```shell script
unzip -u main.zip
```

![Configure EC2 Instance](/images/2.5-configureEC2Instance/0002-configureec2instance.png?featherlight=false&width=70pc)

4. List the files and directories currently available in list format:

```shell script
ls -l
```

5. Grant execute permission to the script:

```shell script
chmod +x ./Analytics-on-AWS-Build-BI-System-main/set-up-hands-on-lab.sh
```

![Configure EC2 Instance](/images/2.5-configureEC2Instance/0003-configureec2instance.png?featherlight=false&width=70pc)

6. Execute the setup script to install the environment:

```shell script
./Analytics-on-AWS-Build-BI-System-main/set-up-hands-on-lab.sh
```

7. Ensure that the necessary files for the project are created successfully after executing the setup script: By checking if the source code and required files exist using the command.

```shell script
ls -l
```

![Configure EC2 Instance](/images/2.5-configureEC2Instance/0004-configureec2instance.png?featherlight=false&width=70pc)

8. Execute the command to enable us to access AWS resources: From the previously created IAM User, we will retrieve the **Access key ID** and **Secret access key**, and input them as requested.

```shell script
aws configure
```

![Configure EC2 Instance](/images/2.5-configureEC2Instance/0005-configureec2instance.png?featherlight=false&width=70pc)

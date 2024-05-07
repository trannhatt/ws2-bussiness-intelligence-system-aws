---
title: "Create an IAM User"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 2.1 </b> "
---

### Create an IAM User

In this section, we will create an IAM User on the AWS Console to use in the project.

1. Access the AWS Console:
   - Sign in to the AWS Console at [https://console.aws.amazon.com/](https://console.aws.amazon.com/).
   - Click on the search bar and type `iam`.
   - Under **Services**, select **IAM**.

![Create IAM User](/ws2-bussiness-intelligence-system-aws/images/2.1-createIAMUser/0001-createiamuser.png?featherlight=false&width=70pc)

2. Create an IAM User:
   - In the IAM dashboard, choose **Users**.
   - Select **Create User**.

![Create IAM User](/ws2-bussiness-intelligence-system-aws/images/2.1-createIAMUser/0002-createiamuser.png?featherlight=false&width=70pc)

3. Specify User details:
   - Under **Specify user details**:
     - Enter a name for the User in the **User name** field (e.g., `workshop2-user`).
     - Check **Provide user access to the AWS Management Console - optional**.
     - Continue by selecting **I want to create an IAM user**.
     - Choose **Custom password** and enter a password for your IAM User in the **Console password** field.
   - Then, click **Next** to proceed.

![Create IAM User](/ws2-bussiness-intelligence-system-aws/images/2.1-createIAMUser/0003-createiamuser.png?featherlight=false&width=70pc)

4. Set permissions for the User:
   - Under **Set permissions**:
     - Choose **Attach policies directly** in the **Permissions options** section.
     - Search for and select the **AdministratorAccess** policy under **Permissions policies**.
   - Click **Next** to continue.

![Create IAM User](/ws2-bussiness-intelligence-system-aws/images/2.1-createIAMUser/0004-createiamuser.png?featherlight=false&width=70pc)

5. Review and create the User:
   - Under **Review and create**:
     - Click **Add new tag** to add a new Tag.
     - In the **Tags - optional** section:
       - Enter **`name`** in the **Key** field.
       - Enter **`workshop2-user`** in the **Value - optional** field.
     - Finally, click **Create user** to create the User.

![Create IAM User](/ws2-bussiness-intelligence-system-aws/images/2.1-createIAMUser/0005-createiamuser.png?featherlight=false&width=70pc)

6. Complete IAM User creation:
   - You have successfully created an IAM User for the project.
   - You can choose **Download .csv file** to download the User's login information to your device.
   - Select **Return to users list** to go back to the users' page.

![Create IAM User](/ws2-bussiness-intelligence-system-aws/images/2.1-createIAMUser/0006-createiamuser.png?featherlight=false&width=70pc)

7. Activate MFA and log in again:
   - Sign out of the Root User account and log back in to the newly created IAM User account.
   - Before using the IAM User account, activate **MFA** to secure your account.

![Create IAM User](/ws2-bussiness-intelligence-system-aws/images/2.1-createIAMUser/0007-createiamuser.png?featherlight=false&width=70pc)

{{% notice note %}}
**MFA** (Multi-Factor Authentication) is an important security mechanism that helps protect accounts by requiring users to provide two or more types of authentication information to log in.
{{% /notice %}}

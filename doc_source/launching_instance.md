# Seamlessly Join a Windows EC2 Instance<a name="launching_instance"></a>

This procedure will seamlessly join a Windows EC2 instance to your directory\.

**To seamlessly join a Windows EC2 instance**

1. Sign in to the AWS Management Console and open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. From the region selector in the navigation bar, select the same region as the existing directory\.

1. From the Amazon EC2 console dashboard, choose **Launch Instance**\.

1. On the **Step 1** page, select the appropriate AMI\.

1. On the **Step 2** page, select the appropriate instance type, and then choose **Next**\.

1. On the **Step 3** page, do the following, and then choose **Next** :

   1. For **Network**, choose the VPC that your directory was created in\.

   1. For **Subnet**, select one of the public subnets in your VPC\. The subnet you select must have all external traffic routed to an Internet gateway\. 

   1. For **Auto\-assign Public IP**, choose **Enable** \(if the subnet setting is not set to enable by default\)\. For more information about public and private IP addressing, see [Amazon EC2 Instance IP Addressing](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-instance-addressing.html) in the *Amazon EC2 User Guide for Linux Instances*\.

   1. For **Domain join directory**, select your domain from the **Domain join directory** list\. To seamlessly join the instance, you also need an IAM role that has the **AmazonEC2RoleforSSM** managed policy attached to it\. Select the IAM role that has permission from the IAM role list\. If you choose this option, you will not have to manually join the instance to the domain as that will be done for you when the instance is launched\.
**Note**  
This option is only available for Windows instances\. Linux instances must be manually joined to the directory as explained in [Manually Join a Linux Instance](join_linux_instance.md)\.

   1. For **IAM role**, optionally choose the **Create new IAM role** link to create a new IAM role and attach the AmazonEC2RoleforSSM policy, and then on the **Roles** page, do the following:

      1. Select the **Create role** button\.

      1. Under **AWS service**, select the **EC2** link, and then click **Next**\.

      1. Under **Select your use case**, select **EC2**, and then select **Next**\.

      1. In the list of polices, select the **AmazonEC2RoleforSSM** policy, and then select **Next**\.

      1. In **Role name**, type a name for your new role \(For example, EC2DomainJoin\), in **Role description** type a description \(optional\), and then select the **Create role** button\.

1. Go back to the **Step 3** page, for **IAM role**, choose the refresh icon next to the **IAM role** field\. Your new role should be visible in the drop down menu\. Select it, and leave the rest of the settings on this page with their default values, and then select **Next**\.

1. Continue through the remaining pages in the wizard using your preferred settings\.
**Note**  
The security group you select for the instance \(on the **Step 6** page\) must allow remote access to the instance from your network\.

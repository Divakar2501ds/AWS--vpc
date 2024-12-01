# VPC with servers in private subnets and NAT
## Overview :
In this project, a Virtual Private Cloud (VPC) is designed and implemented on AWS to create a secure and scalable environment for hosting web applications and services. The VPC is segmented into public and private subnets, with specific routing configurations that allow secure communication between the components and the internet.



![vpc image](images/vpc.png)

## step 1: Create a VPC:
•	Log in to the AWS Management Console and navigate to the VPC Dashboard.  

•	Click on Create VPC and More to begin the VPC creation process.

•	Name your VPC, define an IPv4 CIDR block (for example, 10.0.0.0/16), and select the Default Tenancy option.

![alter text](images/p1.png)

•	For high availability, ensure that you select at least two Availability Zones in which to deploy your subnets.

•	Create subnets

•	Configure the subnets

        a. Set the "Number of Availability Zones" to 2 for increased resiliency across multiple Availability Zones.
        b. Specify the "Number of public subnets" as 2.
        c. Specify the "Number of private subnets" as 2.
        d. For NAT gateways, choose "1 per AZ" to enhance resiliency
•	If necessary, configure a NAT Gateway in each Availability Zone to enable internet access for your private subnets. This allows instances in the private subnets to access the internet.

•	Leave the VPC Endpoints as "None" unless specific services require endpoint configuration.

![alter text](images/p2.png)

•	Click Create VPC to finalize the setup.

•   Successfully created VPC

![alter text](images/p3.png)

## Step 2: Create an Auto Scaling Group
1.	Navigate to Auto Scaling Groups:

•	In the EC2 Dashboard, under Auto Scaling in the left-hand menu, select Auto Scaling Groups.
2.	Create an Auto Scaling Group:

•	Click on the Create Auto Scaling group button.

3.	Configure the Auto Scaling Group:

•	Auto Scaling group name: Provide a name for the Auto Scaling group

![alter text](images/p5.png)

•	Create a Launch Template:

    o	In the left-hand navigation pane, select Launch Templates under Instances.
    o	Click Create launch template.

•	Configure Launch Template:

    o	Template Name: Give your template a name .
    o	AMI: Select the AMI (e.g., Amazon Linux 2, Ubuntu).
    o	Instance Type: Select an instance type (e.g., t2.micro).
    o	Key Pair: Select the existing or create a new key pair.
    o	Network: Choose the VPC you created earlier (e.g., MyVPC).
    o	Subnet: Choose the private subnet where the instances will be launched.
    o	Security Group: Choose or create a security group that allows traffic between instances in the private subnet (and from the NAT Gateway for outbound internet access).
    o	Click Create launch template to finalize the template.

•	Launch Template: Select the launch template you created earlier.



•	Configure Group Size:

    o	Desired capacity: Enter the initial number of instances you want in your Auto Scaling group (e.g., 2 instances).
    o	Minimum size: Set the minimum number of instances (e.g., 1).
    o	Maximum size: Set the maximum number of instances (e.g., 4).

•	Configure VPC and Subnets:

    o	VPC: Choose the VPC where your private subnets are located (e.g., MyVPC).
    o	Subnets: Select the private subnets where the instances will be launched. If you have multiple private subnets across different availability zones, select both.

 •  Configure any additional settings as needed and click Create AutoScalinggroup

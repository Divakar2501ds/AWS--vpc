# VPC with servers in private subnets and NAT
## Overview :
In this project, a Virtual Private Cloud (VPC) is designed and implemented on AWS to create a secure and scalable environment for hosting web applications and services. The VPC is segmented into public and private subnets, with specific routing configurations that allow secure communication between the components and the internet.



![vpc image](images/vpc.png)

## step 1: Create a VPC:
1.	Log in to the AWS Management Console and navigate to the VPC Dashboard.  

2.	Click on Create VPC and More to begin the VPC creation process.

3.	Name your VPC, define an IPv4 CIDR block (for example, 10.0.0.0/16), and select the Default Tenancy option.

4.	![alter text](images/p1.png)

5.	For high availability, ensure that you select at least two Availability Zones in which to deploy your subnets.

6.	Create subnets

7.	Configure the subnets

8.	Set the "Number of Availability Zones" to 2 for increased resiliency across multiple Availability Zones.

9.	Specify the "Number of public subnets" as 2.

10.	Specify the "Number of private subnets" as 2.

11.	For NAT gateways, choose "1 per AZ" to enhance resiliency

12.	If necessary, configure a NAT Gateway in each Availability Zone to enable internet access for your private subnets. This allows instances in the private subnets to access the internet.

13.	Leave the VPC Endpoints as "None" unless specific services require endpoint configuration.

14.	![alter text](images/p2.png)

15.	Click Create VPC to finalize the setup.

16.	Successfully created VPC

![alter text](images/p3.png)


## Step 2: Create an Auto Scaling Group
1.	Navigate to Auto Scaling Groups:

2.	In the EC2 Dashboard, under Auto Scaling in the left-hand menu, select Auto Scaling Groups.
3.	Create an Auto Scaling Group:

4.	Click on the Create Auto Scaling group button.

5.	Configure the Auto Scaling Group:

6.	Auto Scaling group name: Provide a name for the Auto Scaling group

7.	![alter text](images/p5.png)

8.	Create a Launch Template:

9.	In the left-hand navigation pane, select Launch Templates under Instances.
10.	Click Create launch template.

11.	Configure Launch Template:

12.	Template Name: Give your template a name .

13.	AMI: Select the AMI (e.g., Amazon Linux 2, Ubuntu).

14.	Instance Type: Select an instance type (e.g., t2.micro).

15.	Key Pair: Select the existing or create a new key pair.

16.	Network: Choose the VPC you created earlier (e.g., MyVPC).

17.	Subnet: Choose the private subnet where the instances will be launched.

18.	Security Group: Choose or create a security group that allows traffic between instances in the private subnet (and from the NAT Gateway for outbound internet access).

19.	Click Create launch template to finalize the template.

20.	Launch Template:Select the launch template you created earlier.

21.	Configure Group Size:

22.	Desired capacity: Enter the initial number of instances you want in your Auto Scaling group (e.g., 2 instances).

23.	Minimum size: Set the minimum number of instances (e.g., 1).

24.	Maximum size: Set the maximum number of instances (e.g., 4).

25.	Configure VPC and Subnets:

26.	VPC: Choose the VPC where your private subnets are located (e.g., MyVPC).

27.	Subnets: Select the private subnets where the instances will be launched. If you have multiple private subnets across different availability zones, select both.

28.	Configure any additional settings as needed and click Create AutoScalinggroup

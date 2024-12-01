# VPC with servers in private subnets and NAT
## Overview :
In this project, a Virtual Private Cloud (VPC) is designed and implemented on AWS to create a secure and scalable environment for hosting web applications and services. The VPC is segmented into public and private subnets, with specific routing configurations that allow secure communication between the components and the internet.


## Step 1: Create the VPC
1.	Open the Amazon VPC Console:<br>
    a.	Visit Amazon VPC Console.<br>
2.	Create a New VPC:<br>
    a.	On the dashboard, click Create VPC.<br>
    b.	Under Resources to create, select VPC and more.<br>

    ![Alter text](images/p1.png)
3.	Configure the VPC:<br>
    a.	Provide a name for the VPC in the Name tag auto-generation field.<br>
    b.	For the IPv4 CIDR block, leave it as the default suggestion (e.g., 10.0.0.0/16).<br>
4.	Configure Subnets:<br>
    a.	Set the Number of Availability Zones to 2 for higher availability.<br>
    b.	Specify the Number of public subnets as 2.<br>
    c.	Specify the Number of private subnets as 2.<br>
    d.	For NAT gateways, choose 1 per AZ to ensure high resiliency.<br>
    e.	Leave VPC endpoints as None unless required.<br>
    ![Alter text](images/p2.png)
    f.	For DNS options, ensure the checkbox for Enable DNS hostnames is unchecked.<br>
5.	Create the VPC:<br>
    a.	Once you’ve configured all the settings, click Create VPC.<br>
    ![Alter text](images/p3.png)
## Step2 : Create an Auto Scaling Group
1.	Navigate to the EC2 Console:<br>
    a.	Log in to the AWS Management Console.<br>
    b.	Navigate to Services > EC2 under the Compute section.<br>
2.	Access Auto Scaling Groups:<br>
    a.	From the left-hand menu, choose Auto Scaling Groups under the Auto Scaling section.<br>
    b.	Click on the Create Auto Scaling Group button.<br>
3.	Create a Launch Template:<br>
    a.	Click the Create Launch Template button.<br>
    b.	Provide a Name and Description for your launch template.<br>
    c.	Select a Linux AMI (Amazon Machine Image).<br>
    d.	Choose a free-tier eligible instance type (e.g., t2.micro).<br>
    e.	Select an existing Key Pair or create a new one (ensure you have access to this key).<br>
4.	Create a Security Group:<br>
    a.	Go to the Security Groups section from the left-hand menu in the EC2 dashboard under Network & Security.<br>
    b.	Click on Create Security Group and provide a Name and Description for it.
5.	Configure Security Group Rules:<br>
    o	Inbound Rules:<br>
        	Type: SSH, Protocol: TCP, Port Range: 22, Source: Anywhere (IPv4).<br>
        	Type: All TCP, Protocol: TCP, Port Range: All, Source: Anywhere (IPv4).<br>
    o	Outbound Rules:<br>
        	Type: All Traffic, Protocol: All, Port Range: All, Destination: Anywhere (IPv4).<br>
    o	Click Create Security Group to finalize.<br>
6.	Save the Launch Template:<br>
    a.	Once all the configurations (AMI, instance type, key pair, and security group) are complete, click Create Launch Template to save your settings.<br>
7.	Configure Auto Scaling Group Settings:<br>
    a.	Back in the Auto Scaling Group creation page, select the pre-created Launch Template.<br>
    b.	Choose the VPC where your instances will run.<br>
    c.	Select private subnets in the VPC (preferably across multiple Availability Zones for high availability).<br>
8.	Define Scaling Parameters:<br>
    a.	Minimum Capacity: Set the minimum number of instances (e.g., 2).<br>
    b.	Maximum Capacity: Set the maximum number of instances (e.g., 4).<br>
    c.	Desired Capacity: Set the initial number of instances (e.g., 2).<br>
9.	Finalize the Auto Scaling Group:<br>
    a.	Review your configuration and make any necessary adjustments.<br>
    b.	Click Create Auto Scaling Group to complete the setup.<br>

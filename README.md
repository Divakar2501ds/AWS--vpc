# VPC with servers in private subnets and NAT
## Overview :
In this project, a Virtual Private Cloud (VPC) is designed and implemented on AWS to create a secure and scalable environment for hosting web applications and services. The VPC is segmented into public and private subnets, with specific routing configurations that allow secure communication between the components and the internet.


Step 1: Create the VPC
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

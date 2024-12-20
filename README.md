﻿# VPC with servers in private subnets and NAT
## Overview :
In this project, a Virtual Private Cloud (VPC) is designed and implemented on AWS to create a secure and scalable environment for hosting web applications and services. The VPC is segmented into public and private subnets, with specific routing configurations that allow secure communication between the components and the internet.
![alter text](images/vpc.png)

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
    a.	Navigate to Services > EC2 under the Compute section.<br>
2.	Access Auto Scaling Groups:<br>
    a.	From the left-hand menu, choose Auto Scaling Groups under the Auto Scaling section.<br>
    b.	Click on the Create Auto Scaling Group button.<br>
    ![alter text](images/p4.png)
3.	Create a Launch Template:<br>
    a.	Click the Create Launch Template button.<br>
    b.	Provide a Name and Description for your launch template.<br>
    ![alter text](images/p6.png)
    c.	Select a Amazon Machine Image AMI (Ubuntu Image).<br>
    d.	Choose a free-tier eligible instance type (e.g., t2.micro).<br>
    e.	Select an existing Key Pair or create a new one (ensure you have access to this key).<br>
4.	Create a Security Group:<br>
    a.	Click on Create Security Group and provide a Name and Description for it.<br>
    ![alter text](images/p9.png)
5.	Configure Security Group Rules:<br>
    o	Inbound Rules:<br>
        	Type: SSH, Protocol: TCP, Port Range: 22, Source: Anywhere (IPv4).<br>
        	Type: All TCP, Protocol: TCP, Port Range: All, Source: Anywhere (IPv4).<br>
    ![alter text](images/p10.png)
    o	Outbound Rules:<br>
        	Type: All Traffic, Protocol: All, Port Range: All, Destination: Anywhere (IPv4).<br>
    o	Click Create Security Group to finalize.<br>
6.	Save the Launch Template:<br>
    a.	Once all the configurations (AMI, instance type, key pair, and security group) are complete, click Create Launch Template to save your settings.<br>
7.	Configure Auto Scaling Group Settings:<br>
    a.	Back in the Auto Scaling Group creation page, select the pre-created Launch Template.<br>
    ![alter text](images/p11.png)
    b.	Choose the VPC where your instances will run.<br>
    c.	Select private subnets in the VPC (preferably across multiple Availability Zones for high availability).<br>
    ![alter text](images/p12.png)
8.	Define Scaling Parameters:<br>
    a.	Minimum Capacity: Set the minimum number of instances (e.g., 2).<br>
    b.	Maximum Capacity: Set the maximum number of instances (e.g., 4).<br>
    c.	Desired Capacity: Set the initial number of instances (e.g., 2).<br>
9.	Finalize the Auto Scaling Group:<br>
    a.	Review your configuration and make any necessary adjustments.<br>
    b.	Click Create Auto Scaling Group to complete the setup.<br>
    ![alter text](images/p16.png)
## step 3: Create an instance
1.	Navigate to Services > EC2 from the top menu.<br>
2.	Click on Instances from the left-hand menu, then click on the Launch Instances button to start creating a new instance.<br>
3.	Choose an Amazon Machine Image (AMI):<br>

4.	Select an AMI based on your requirements. For example:<br>
    a.	Use Ubuntu AMI for general-purpose workloads.<br>
    b.	Pick a pre-configured AMI if your application requires specific software.<br>
    ![alter text](images/p17.png)
5.	Select an Instance Type:<br>
6.	Choose an instance type that matches your performance and cost requirements. For example:<br>
    a.	t2.micro is suitable for lightweight workloads and is free-tier eligible.<br>
    b.	For larger workloads, select an instance type with more CPU or memory.<br>
7.	Configure the Network Settings:<br>
8.	Under Network settings, choose the VPC you want the instance to be part of.<br>
9.	Select a public subnet within your VPC.<br>
10.	Enable Auto-assign Public IP to ensure your instance can be accessed from the internet.<br>
    ![alt text](images/p19.png)
11.	Assign a Security Group:<br>
12.	Select an existing Security Group or create a new one.<br>
13.	Ensure the following rules are added:<br>
    a.	Inbound Rules:<br>
        i.	SSH (Protocol: TCP, Port: 22, Source: Anywhere or your IP address).<br>
        ii.	HTTP (Protocol: TCP, Port: 80, Source: Anywhere) if you're hosting a website.<br>
14.	Review and Launch the Instance:<br>
15.	Carefully review all configurations, including the AMI, instance type, storage, and network.<br>
16.	Click Launch and select a Key Pair for SSH access. If you don’t have one, create a new key pair and download it.<br>
17.	Verify the Instance:<br>
18.	Once the instance is launched, go to the Instances section in the EC2 dashboard.<br>
19.	Check that the instance state is Running and verify the Public IP Address.<br>
20.	Use this IP address to connect to your instance via SSH or test accessibility<br>

## Step 4: Create a load balancer

1.	Access the EC2 Dashboard:<br>
    a.	Log in to the AWS Management Console.<br>
    b.	Navigate to Services > EC2.<br>
    c.	In the left-hand menu, select Load Balancers under the Load Balancing section.<br>
2.	Create a Load Balancer:<br>
    a.	Click on the Create Load Balancer button.<br>
    b.	Choose Application Load Balancer (ALB) for HTTP/HTTPS traffic distribution.<br>
3.	Configure the Load Balancer Settings:<br>
    a.	Provide a name for your Load Balancer in the Name field.<br>
    b.	Set the Scheme to Internet-facing to allow external traffic.<br>
    ![alter text](images/p28.png)
    c.	Choose IP Address Type as IPv4.<br>
    d.	Under Network mapping, select the VPC you created earlier.<br>
4.	Enable Availability Zones:<br>
    a.	Activate at least 2 Availability Zones for high availability.<br>
    b.	Select Public Subnets for each Availability Zone where your instances are deployed.<br>
     ![alter text](images/p29.png)
5.	Configure the Security Group:<br>
    a.	Assign a Security Group that allows traffic to your Load Balancer.<br>
    b.	For example, ensure the following rules are added to the Security Group:<br>
        i.	HTTP (TCP, Port 80, Source: Anywhere).<br>
        ii.	HTTPS (TCP, Port 443, Source: Anywhere), if using SSL.<br>
6.	Security Settings (Optional):<br>
    a.	If you're using HTTPS, configure the SSL Certificate here. Otherwise, skip this step.<br>
7.	Configure Routing Settings:<br>
    a.	Under Routing, create a new Target Group by clicking Create a new target group.<br>
8.	Create a Target Group:<br>
    a.	Enter a name for your Target Group.<br>
    b.	Set the Target Type to Instances to distribute traffic among EC2 instances.<br>
    ![alter text](images/p30.png)
    c.	Select the VPC where your instances are deployed.<br>
    ![alter text](images/p31.png)
    d.	Configure Health Check Settings:<br>
        i.	Protocol: Choose HTTP or HTTPS.<br>
        ii.	Path: Specify the health check path (e.g., /index.html).<br>
9.	Register Targets:<br>
    a.	Add the EC2 instances to the Target Group by selecting them.<br>
    b.	Click Include as targets to associate the instances.<br>
     ![alter text](images/p32.png)
    c.	Proceed by clicking Next: Review.<br>
10.	Review and Create the Target Group:<br>
    a.	Verify the settings and click Create target group to finalize.<br>
11.	Add the Target Group to the Load Balancer:<br>
    a.	After creating the Target Group, go back to the Load Balancer configuration.<br>
    b.	Select the Target Group you created and associate it with the Load Balancer.<br>
12.	Review and Create the Load Balancer:<br>
    a.	Double-check all the settings, including availability zones, security groups, and the associated Target Group.<br>
    b.	Click Create Load Balancer to complete the setup.<br>

## Step 5: SSH into Private Instance via Bastion Host and Deploy Application

Step 1: SSH into the Bastion Host<br>
1.	Ensure the PEM file is accessible:<br>
    a.	Verify that your .pem file (key pair) is present on your local machine.<br>
    b.	Rename the file if necessary to avoid spaces in the name (e.g., aws_vpc.pem instead of aws vpc.pem).<br>
2.	Copy the PEM file to the Bastion Host:<br>
    a.	Use the scp command to transfer the .pem file to the Bastion host.<br>
    b.	Replace <local file path> with the location of the PEM file on your local machine, and <bastion public IP> with your Bastion Host's public IP.<br>
        scp -i C:\Users\Lenovo_Admin\Downloads\aws-vpc.pem C:\Users\Lenovo_Admin\Downloads\aws-vpc.pem ubuntu@13.233.106.134:/home/ubuntu
        <br>
        ![alter text](images/p21.png)<br>
3.	SSH into the Bastion Host:<br>
    a.	Use the ssh command with the Bastion Host's public IP to log in.<br>
    ssh -i aws-vpc.pem ubuntu@13.233.106.134
    <br>
    ![alt text](images/p22.png)<br>
4.	Set permissions for the PEM file:<br>
    a.	On the Bastion Host, ensure the .pem file has proper permissions. Use:<br>
    chmod 400 aws-vpc.pem
________________________________________
Step 2: SSH into the Private Instance<br>
1.	Log into the Private Instance from the Bastion Host:<br>
    a.	Use the Private Instance's private IP address to SSH into it:<br>
    ssh -i aws-vpc.pem ubuntu@10.0.133.85
2.	Verify Connectivity:<br>
    a.	Run ls on the Bastion Host to confirm the presence of the PEM file before attempting to SSH into the private instance.<br>
     <br>
    ![alt text](images/p23.png)<br>
________________________________________
Step 3: Deploy the Application on the Private Instance<br>
1.	Create an HTML File:<br>
    a.	Use the Vim editor to create a simple HTML file:<br>
    vim index.html
2.	Add the Following HTML Content:<br>
    a.	Insert the content below into the file:<br>
        html
       ![alter text](images/p36.png)
3.	Save the HTML File:<br>
    a.	Press Esc, type :wq, and hit Enter to save and exit Vim.<br>
4.	Start a Python HTTP Server:<br>
    a.	Use the following command to start a simple HTTP server on port 8000:<br>
    python3 -m http.server 8000
     <br>
    ![alt text](images/p37.png)<br>
5.	Verify Deployment:<br>
a.	The application will now be available on the private instance at port 8000.<br>
 
6.  Go to load balancer,copy the DNS of the load balancer you created and run it on the browser<br>
  <br>  copy the DNS name of load balancer
    ![alt text](images/p40.png)<br>

## Step 6: RESULT
img result 
    ![alter text](images/p39.png)<br>

Now we have successfully deployed the application securely on the private instance. The application can be accessed over the internet using the Load Balancer, ensuring secure and efficient traffic distribution.

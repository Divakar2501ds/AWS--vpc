# VPC with servers in private subnets and NAT
## Overview :
In this project, a Virtual Private Cloud (VPC) is designed and implemented on AWS to create a secure and scalable environment for hosting web applications and services. The VPC is segmented into public and private subnets, with specific routing configurations that allow secure communication between the components and the internet.



![vpc image](images/vpc.png)

## step 1: Create a VPC:
•	Log in to the AWS Management Console and navigate to the VPC Dashboard.   
 
•	Click on Create VPC and More to begin the VPC creation process. 

•	Name your VPC, define an IPv4 CIDR block (for example, 10.0.0.0/16), and select the Default Tenancy option.  

•	For high availability, ensure that you select at least two Availability Zones in which to deploy your subnets.

•	Create subnets:

•	Configure the subnets:

        a. Set the "Number of Availability Zones" to 2 for increased resiliency across multiple Availability Zones.

        b. Specify the "Number of public subnets" as 2.

        c. Specify the "Number of private subnets" as 2.

        d. For NAT gateways, choose "1 per AZ" to enhance resiliency

•	If necessary, configure a NAT Gateway in each Availability Zone to enable internet access for your private subnets. This allows instances in the private subnets to access the internet.

•	Leave the VPC Endpoints as "None" unless specific services require endpoint configuration.

•	Click Create VPC to finalize the setup.

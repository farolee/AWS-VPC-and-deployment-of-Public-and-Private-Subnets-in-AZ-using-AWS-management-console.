A Virtual Private Cloud (VPC) is a logically isolated network in Amazon Web Services
where you can launch AWS resources such as EC2 instances, databases, and load balancers.
A VPC allows you to:

•	Control IP addressing 
•	Create public and private subnets 
•	Configure routing 
•	Improve security and network isolation




Example setup:

1 VPC
2 Public Subnets
2 Private Subnets
Internet Gateway
Route Tables
NAT Gateway (optional for private subnet internet access)


A Virtual Private Cloud (VPC) is a logically isolated network in Amazon Web Services where you can launch AWS resources such as EC2 instances, databases, and load balancers.
A VPC allows you to:
•	Control IP addressing 
•	Create public and private subnets 
•	Configure routing 
•	Improve security and network isolation
Step 1: Log in to AWS Console
Go to: AWS Management Console
Then:
1.	Sign in to your AWS account 
2.	Search for VPC 
3.	Open the VPC Dashboard 
________________________________________
BeeQ LLC Final Reference Architecture.
 







Step 2: Create a VPC.
1.	In the VPC Dashboard, click Create VPC 
2.	Select VPC only 
3.	Enter the following:
Setting	         Value
Name tag                   	        Production-VPC
IPv4 CIDR block	10.0.0.0/16
Tenancy	Default
4.	Click Create VPC 
________________________________________
Step 3: Create Public Subnets
Public subnets allow resources to communicate with the internet.
Public Subnet 1
Setting	Value
Name	Public-Subnet-1
Availability Zone	us-east-1a
CIDR	10.0.1.0/24
Public Subnet 2
Setting	Value
Name	Public-Subnet-2
Availability Zone	us-east-1b
CIDR	10.0.2.0/24
Steps
1.	Click Subnets 
2.	Click Create subnet 
3.	Select your VPC 
4.	Create both public subnets 
________________________________________
Step 4: Create Private Subnets
Private subnets do not allow direct internet access.
Private Subnet 1
Setting                     	Value
Name	Private-Subnet-1
Availability Zone	us-east-1a
CIDR	10.0.0.0/16
Private Subnet 2
Setting	Value
Name	Private-Subnet-2
Availability Zone	us-east-1b
CIDR	10.0.4.0/24
Repeat the subnet creation steps.
________________________________________
Step 5: Create and Attach an Internet Gateway
An Internet Gateway allows communication between the VPC and the internet.
Steps
1.	Click Internet Gateways 
2.	Click Create internet gateway 
3.	Name it: 
o	Production-IGW 
4.	Click Create 
5.	Select the gateway 
6.	Click Attach to VPC 
7.	Choose your VPC 
________________________________________
Step 6: Create Route Table for Public Subnets
Create Public Route Table
1.	Go to Route Tables 
2.	Click Create route table 
3.	Name: 
o	Public-RT 
4.	Select your VPC 
Add Internet Route
1.	Open the route table 
2.	Click Routes → Edit routes 
3.	Add: 
Destination	Target
0.0.0.0/0	Internet Gateway
Associate Public Subnets
1.	Click Subnet Associations 
2.	Select: 
o	Public-Subnet-1 
o	Public-Subnet-2 
________________________________________
Step 7: Create Route Table for Private Subnets
Create Private Route Table
1.	Create another route table 
2.	Name: 
o	Private-RT 
Associate Private Subnets
Associate:
•	Private-Subnet-1 
•	Private-Subnet-2 
At this stage, private subnets have no internet access.
________________________________________
Step 8: (Optional) Create NAT Gateway
A NAT Gateway allows private subnet resources to access the internet securely.
Steps
1.	Go to NAT Gateways 
2.	Click Create NAT Gateway 
3.	Select: 
o	Public subnet 
4.	Allocate Elastic IP 
5.	Click Create 
________________________________________
Step 9: Update Private Route Table
Add route:
Destination	Target
0.0.0.0/0	NAT Gateway
Now private subnet instances can access the internet for updates and downloads.
________________________________________



6
Public Subnets
Used for:
•	Load Balancers 
•	Bastion Hosts 
•	Web Servers 
Private Subnets
Used for:
•	Databases 
•	Application Servers 
•	Internal Services 
________________________________________
Best Practices
•	Use multiple Availability Zones for high availability 
•	Keep databases in private subnets 
•	Enable VPC Flow Logs for monitoring 
•	Use Security Groups and NACLs 
•	Tag all AWS resources properly 
•	Use least privilege IAM policies 
________________________________________
AWS Services Used
•	Amazon Web Services VPC 
•	Amazon EC2 
•	Internet Gateway 
•	NAT Gateway 
•	Route Tables 
•	Subnets 
•	Elastic IP



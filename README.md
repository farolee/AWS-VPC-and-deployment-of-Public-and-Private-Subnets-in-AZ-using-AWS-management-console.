A Virtual Private Cloud (VPC) is a logically isolated network in Amazon Web Services where you can launch AWS resources such as EC2 instances, databases, and load balancers.
A VPC allows you to:
1.	Control IP addressing 
2.	Create public and private subnets 
3.	Configure routing 
4.	Improve security and network isolation
5.	Deploy in us-east-2
________________________________________

BeeQ LLC Final Reference Architecture.
<img width="1030" height="516" alt="BeeQ Ref Achitecture" src="https://github.com/user-attachments/assets/a0414d8b-bbd9-4b2b-8942-7a57d4892a60" />

________________________________________
Step 1: Log in to AWS Console
Go to the:  AWS Management Console
Then:
1.	Sign in to BeeQ LLC AWS account 
2.	Search for VPC 
3.	Open the VPC dashboard 
________________________________________
Step 2: Create a VPC.
1.	In the VPC Dashboard, click Create VPC 
2.	Select VPC only 
3.	Enter the following:
Setting	         Value
Name tag                   	         BeeQVPC
IPv4 CIDR block	         10.0.0.0/16
Tenancy	          Default
________________________________________

Step 3:  Create Subnets

a. Create Private Subnet (Private subnets do not allow direct internet access)
b.	Configuration	Value
c.	Name	BeeQ_Pri_Subnet
d.	Availability Zone	us-east-2b
e.	CIDR Block	10.0.3.0/24
________________________________________

Create Public Subnet (Public subnets allow direct internet access)
a. Configuration	Value
b. Name	BeeQ_Public_Subnet
c. Availability Zone	us-east-2a
d. CIDR Block	10.0.4.0/24

Public and Private Subnets
<img width="1896" height="637" alt="image" src="https://github.com/user-attachments/assets/8599023a-c244-4a96-a6cf-80f412155689" />

________________________________________

Step 4: Create an Internet Gateway and attach it to the VPC.
An Internet Gateway allows communication between the VPC and the internet.
1.	Click Create Internet Gateway. 
2.	Name: IGW_BeeQ 
3.	Click Attach to VPC.
   
   Internet Gateway Attached to the VPC(BeeQVPC)
<img width="1895" height="592" alt="IGW_BeeQ" src="https://github.com/user-attachments/assets/71df25f4-48f7-4291-b78f-f3bed610e19b" />

________________________________________

Step:5 Create a Route Table for Public Subnets and Private Subnets
Create Public Route Table
1.	Go to Route Tables 
2.	Click Create route table. 
3.	Name: BeeQ_Public-RT 
4.	Select your BeeQVPC 
Add Internet Route
1.	Open the route table. 
2.	Edit routes. Add a destination target (0.0.0.0/0) route to the internet. Associating with the subnet enables the resource in the subnet to communicate with the public Internet.
3.	Create another route table without a destination target to the internet. Associate with the private subnet (BeeQ_Pri_Subnet). At this stage, private subnets have no internet access.


Creat Route tables
Public Route Table
<img width="1908" height="561" alt="Public Rout Table BeeQ_Pub Rt" src="https://github.com/user-attachments/assets/1d580419-2389-48eb-a245-9d935dabce3d" />

 Associate with Public Subnet
<img width="1898" height="655" alt="RT associte with Public Subnet" src="https://github.com/user-attachments/assets/5cc7ecf4-3ee9-40e2-b3bb-f7b7c36f7fcf" />

Private Route Table
<img width="1916" height="748" alt="image" src="https://github.com/user-attachments/assets/08e17b96-69d3-42aa-9f89-be9e56fbf2f7" />

________________________________________

Step 6: (Optional) Create NAT Gateway
A NAT Gateway allows private subnet resources to access the internet securely. Deploy the NAT Gateway in the public subnet (BeeQ_Public_Subnet).
Steps
1.	Go to NAT Gateways :  BeeQ_NAT_GateWay
2.	Click Create NAT Gateway. 
3.	Select: Public subnet 
4.	Allocate Elastic IP

<img width="1809" height="773" alt="image" src="https://github.com/user-attachments/assets/cf8f39b2-a8de-42ac-97cb-d03b6a09273f" />

NAT Gateway

<img width="1901" height="754" alt="image" src="https://github.com/user-attachments/assets/91067594-9d79-44d7-b7b6-36cd8a2c5d80" />

________________________________________
Step 7: Update Private Route Table
Add route: 
Destination	Target
0.0.0.0/0	NAT Gateway
Now private subnet instances can access the internet for updates and downloads.
________________________________________

# AWS VPC Resources Table

| S/N | Resources    |    Names            |     AWS ARN    |
|-----|--------------|---------------------|----------------|
| 1 | VPC            | BeeQVPC             | arn:aws:ec2:us-east-1:123456789012:vpc/vpc-0abc123def4567890
| 2 | Private Subnet | BeeQ_Pri_Subnet     | arn:aws:ec2:us-east-2:954976289682:subnet/subnet-0e36577c61330fc3e |
| 3 | Public Subnet  | BeeQ_Public_Subnet  | arn:aws:ec2:us-east-2:954976289682:subnet/subnet-0ab40db5721b96cc9 |
| 4 | Internet Gateway | IGW_BeeQ          |arn:aws:ec2:us-east-1:123456789012:internet-gateway/igw-xxxxxxxx    |
| 5 | NAT Gateway    | BeeQ_NAT_GateWay    |arn:aws:ec2:us-east-2:954976289682:natgateway/nat-1e4959212403f64c3|
| 6 | Public Route Table | BeeQ_Public_RT  |    |
| 7 | Private Route Table | BeeQ_Private_RT|     |



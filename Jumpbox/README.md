# AWS_Jumpbox

## Goal: We have to charge

## Build Up Your Architecture

### 1. VPC

Create a VPC, named *VPC_JumpBox*, with 10.0.0.0/16 IPv4 CIDR block

### 2. Subnets

Create 2 subnets, named *Public_Jump* and *Private_Jump* in the VPC and same availability zone (AZ) with /24 IPv4 CIDR block

* Public_Jump: 10.0.1.0/24

* Private_Jump: 10.0.2.0/24

### 3. Internet Gateways (IGW)

Create an internet gateway, named *IGW_Jump*. Attaching it to the VPC

### 4. Instances

Launch 3 instances

#### 2 in Public:

- **NAT Instance**, named *Ins_NAT*

Community AMIs amzn-ami-vpc-nat-hvm → Enable Auto-assign Public IP → SG_NAT → NATKey.pem

![](https://github.com/wulinghsuan/AWS/blob/master/Jumpbox/JumpBox_1.png)

![](https://github.com/wulinghsuan/AWS/blob/master/Jumpbox/JumpBox_8.png)

- **Jumpbox Instance**, named *Ins_JB*

Amazon Linux 2 AMI (HVM) → Enable Auto-assign Public IP → SG_JB → JBKey.pem

![](https://github.com/wulinghsuan/AWS/blob/master/Jumpbox/JumpBox_6.png)

#### 1 in Private:

- **Final Instance**, named *Ins_FI*

Amazon Linux 2 AMI (HVM) → Enable Auto-assign Public IP → SG_FI → JBKey.pem

![](https://github.com/wulinghsuan/AWS/blob/master/Jumpbox/JumpBox_7.png)

### 5. Route Tables

Select the private subnet, Private_Jump → Click on the Route Tables tag down below → Enter **Route Table ID** NOT Edit route table association

Edit routes → Add route: Target IGW, choose IGW_Jump


### 6. Security Groups

Edit inbound rules of 3 security group corresponding to the instances.

- **SG_NAT**

|Type|Protocol|Port Range|Source|
| --- | --- | --- | --- |
|All traffic|All|All|SG_FI|

- **SG_JB**

|Type|Protocol|Port Range|Source|
| --- | --- | --- | --- |
|SSH|TCP|22|0.0.0.0/0|

- **SG_FI**

|Type|Protocol|Port Range|Source|
| --- | --- | --- | --- |
|SSH|TCP|22|SG_JB|

## Connect With Local Command Prompt and PuTTY

Transform key pair, JBKey.pem, to ppk file, named *JBKey.pem* with Puttygem

### 7. PuTTY

- Session → Host Name (or IP address): *ec2-user@3.230.2.11*

> ec2-user@**JumpBox IPv4 Public IP**

![](https://github.com/wulinghsuan/AWS/blob/master/Jumpbox/JumpBox_2.png)

- Connection → SSH → Auth → Browse: choose JBKey.pem location

- Open

### 8. Local Command Prompt

- Find the location of Key Pair 

cd **location**

> cd Downloads (I save it in Downloads)

![](https://github.com/wulinghsuan/AWS/blob/master/Jumpbox/JumpBox_5.png)

- Copy Key Pair to Jumpbox 

scp -i **Key Pair Name** **Key Pair Name** ec2-user@"**JumpBox IPv4 Public IP**:**Key Pair Name**

> scp -i JBKey.pem JBKey.pem ec2-user@"3.230.2.11":JBKey.pem

![](https://github.com/wulinghsuan/AWS/blob/master/Jumpbox/JumpBox_3.png)

### 9. Back To PuTTY

- Follow the step on AWS

> chmod 400 JBKey.pem

> ssh -i "JBKey.pem" ec2-user@10.0.2.124

![](https://github.com/wulinghsuan/AWS/blob/master/Jumpbox/JumpBox_4.png)

# AWS
# Run RStudio on AWS 

## Lanch a instance

[Step 1: Choose an Amazon Machine Image (AMI)]
Amazon Linux 2 AMI (HVM), SSD Volume Type

[Step 2: Choose an Instance Type]

[Step 3: Configure Instance Details]
Network* your own VPC
Subnet* your own Subnet 
Auto-assign Public IP* Enable

同頁拉到下面

Advanced Details*

User data* As text

#!/bin/bash
sudo yum -y update
sudo amazon-linux-extras install R3.4 -y
wget https://download2.rstudio.org/server/centos6/x86_64/rstudio-server-rhel-1.2.5019-x86_64.rpm
sudo yum install rstudio-server-rhel-1.2.5019-x86_64.rpm -y
sudo useradd wulinghsuan
echo wulinghsuan:000000 | sudo chpasswd

[Step 4,5]
Do not need to change

[Step 6: Configure Security Group]
Assign a security group* Create a new security group
Security group name* MySG_For_RStudio
Description* Same as the upper one

Click--->Add Rule
Type* Custom TPC Rule
Protocol* Do not need to change
Port Range* 8787  //Port of RStuio
Source* Anywhere

Create a new key pair
Download

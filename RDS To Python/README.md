# AWS_RDS-To-Python

## Build Up Your Architecture

### 1. VPC

Create a VPC, named *VPC_RDS*, with 10.0.0.0/16 IPv4 CIDR block

### 2. Subnets

Create 2 subnets, named *RDSSub_1* and *RDSSub_2* in the VPC and same availability zone (AZ) with 10.0.0.0/24 IPv4 CIDR block

* Public_Jump: 

* Private_Jump:

### 3. Internet Gateways (IGW)

Create an internet gateway, named *IGW_Jump*. Attaching it to the VPC

### 4. Instances

Launch 3 instances

#### 2 in Public:

- **NAT Instance**, named *Ins_NAT*

Community AMIs amzn-ami-vpc-nat-hvm → Enable Auto-assign Public IP → SG_NAT → NATKey.pem

- **Jumpbox Instance**, named *Ins_JB*

Amazon Linux 2 AMI (HVM) → Enable Auto-assign Public IP → SG_JB → JBKey.pem

#### 1 in Private:

- **Final Instance**, named *Ins_FI*

Amazon Linux 2 AMI (HVM) → Enable Auto-assign Public IP → SG_FI → JBKey.pem

### 5. Route Tables

Select the private subnet, Private_Jump → Click on the Route Tables tag down below → Enter **Route Table ID** NOT Edit route table association

Edit routes → Add route: Target IGW, choose IGW_Jump


### 6. Security Groups



VPC

VPC_RDS
10.0.0.0/16

RDSSub_2

IGW_RDS

## Launching an AWS Database (DB) instance

mydatabase

Publicly accessible
Yes


SG_RDS

Initial database name
mydatabase


## Jupyter

import pymysql
connection = pymysql.connect(
    host = 'your_RDB_AWS_instance_Endpoint',
    port = 5432,
    user = 'YOUR_USER_NAME',
    password = 'YOUR_PASSWORD',
    database='YOUR_DATABASE_NAME'
    )
cursor=connection.cursor()



pip install psycopg2

import psycopg2
connection = psycopg2.connect(
    host = 'mydatabase.c9vzraox7dca.us-east-1.rds.amazonaws.com',
    port = 3306,
    user = 'admin',
    password = 'adminadmin',
    database='mydatabase'
    )
cursor=connection.cursor()







mysql -h mydatabase.c9vzraox7dca.us-east-1.rds.amazonaws.com -u admin -p
adminadmin
connect mydatabase


https://towardsdatascience.com/amazon-rds-step-by-step-guide-14f9f3087d28
https://datascience-enthusiast.com/R/AWS_RDS_R_Python.html#Connect-to-database

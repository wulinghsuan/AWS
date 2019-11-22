# AWS




#!/bin/bash
sudo yum -y update
sudo amazon-linux-extras install R3.4 -y
wget https://download2.rstudio.org/server/centos6/x86_64/rstudio-server-rhel-1.2.5019-x86_64.rpm
sudo yum install rstudio-server-rhel-1.2.5019-x86_64.rpm -y
sudo useradd wulinghsuan
echo wulinghsuan:000000 | sudo chpasswd

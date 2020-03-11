# AWS_Jupyter

##

* Launch Instance

* Check for Python

* Execute small script

### 1. Instance

Ubuntu Instance, named *Ins_Ubuntu*

Ubuntu Server 18.04 LTS (HVM) → Enable Auto-assign Public IP → Size (GiB): 15 → SG_Ubuntu → Key.pem

SG_Ubuntu:

|Type|Protocol|Port Range|Source|
| --- | --- | --- | --- |
|Custom TCP Rule|TCP|8888|0.0.0.0/0|
|SSH|TCP|22|0.0.0.0/0|

![](https://github.com/wulinghsuan/AWS/blob/master/Jupyter/Jupyter_1.png)

### 2. PuTTY

Transform key pair, Key.pem, to ppk file, named Key.ppk with Puttygem

Session → Host Name (or IP address): ubuntu@18.212.77.101

> ubuntu@Ubuntu IPv4 Public IP (**NOT** ec2-user@ this time)

Save sessions: Key → click on the botton "Save"

![](https://github.com/wulinghsuan/AWS/blob/master/Jupyter/Jupyter_2.png)

### 3. WinSCP

Copy Key.pem to ubuntu instance

Chick on tools → Import Sites → check on Key, which you just created on step 2

![](https://github.com/wulinghsuan/AWS/blob/master/Jupyter/Jupyter_3.png)

Copy Hello.py as you always do

![](https://github.com/wulinghsuan/AWS/blob/master/Jupyter/Jupyter_4.png)

### 4. Back To PuTTY

Everytime you want to install, make sure update first

> sudo apt-get update -y

Install Python3

> sudo apt-get install python3-pip -y

You can check if it succeed by find out the version

> pip3 --version

![](https://github.com/wulinghsuan/AWS/blob/master/Jupyter/Jupyter_5.png)

Or by running a simple Python script we have copied in Step 3, Hello.py

> python3 filename.py

![](https://github.com/wulinghsuan/AWS/blob/master/Jupyter/Jupyter_6.png)

Install Jupyter

> sudo pip3 install jupyter

Binding to an IP

> jupyter notebook --ip=0.0.0.0

![](https://github.com/wulinghsuan/AWS/blob/master/Jupyter/Jupyter_7.png)

POINT: use the code **nohup jupyter notebook --ip=0.0.0.0 &**, if you want to stay connect to virtual environment after shutting down the computer.

![](https://github.com/wulinghsuan/AWS/blob/master/Jupyter/Jupyter_8.png)

![](https://github.com/wulinghsuan/AWS/blob/master/Jupyter/Jupyter_11.png)

You will get an URL started with ip, such as http://ip-10-0-1-69:8888/?token=59b13d15165080f91f86151c4d528bf8b53d2165dc019d2c.

Replace ip-10-0-1-69 by IPv4 Public IP of Ubuntu Instance, 18.212.77.101, and open it on your browser.

![](https://github.com/wulinghsuan/AWS/blob/master/Jupyter/Jupyter_9.png)

### 5. Virtual Environment

Go to Jupyter page you just linked. Click NEW → Terminal

![](https://github.com/wulinghsuan/AWS/blob/master/Jupyter/Jupyter_10.png)

Here are two ways:

- Anaconda

Advantage of Conda: it allows the setup of virtual environments with different Python versions.

In the newly opened terminal create a tmp folder

> mkdir tmp

Get into the folder

> cd tmp/

Download Anaconda

> curl -O https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh

> bash Anaconda3-2019.10-Linux-x86_64.sh

Follow the steps, or just keep pressing ENTER then type **yes**

It will take a while...

- Pew

Open a new Terminal, install pew

> pip3 install pew

Create a new environment in Pew, called *NEW*

> pew new NEW

![](https://github.com/wulinghsuan/AWS/blob/master/Jupyter/Jupyter_12.png)

POINT: 

**ls**: find out what the packages/ files are there in side

**exit**: leave pew and go back to Ubuntu

**pew ls**: check which pew are there

**pew workon NEW**: enter the pew, NEW

Keep all packages you have already installed

> pip3 freeze

- ipykernel

In order to link virtual environment to Jupyter, we can do it with ipykernel

Install ipykernel

> pip3 install --user virtualenv

Create a new environment

> python3 -m ipykernel install --user --name=myENV

![](https://github.com/wulinghsuan/AWS/blob/master/Jupyter/Jupyter_13.png)

Download the display on a python script in *nohup.out.txt* file

> cat nohup.out

Disconnect to Jupyter Notebook

> jupyter notebook stop

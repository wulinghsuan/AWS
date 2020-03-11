# AWS_MNIST

## 1. TRAINMACHINE

### (1) Lunch an instance

You choose Amazon Linux 2 AMI (HVM) or Ubuntu.

Type: m5.xlarge → Public Subnet → Enable Auto-assign Public IP → Size (GiB): 15 → SG_Ubuntu → Key.pem

![](https://github.com/wulinghsuan/AWS/blob/master/MNIST/MNIST_5.png)

### (2) Set up machine through PuTTY

Save sessions: MNIST → click on the botton "Save"

![](https://github.com/wulinghsuan/AWS/blob/master/MNIST/MNIST_1.png)

Install [Anaconda](https://www.anaconda.com/distribution/) by copy the download URL for Linux

    wget https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh

    sudo bash Anaconda3-2019.10-Linux-x86_64.sh 

Answer yes to all questions, or just keep pressing SPACE then type yes.

Check if conda works. When getting command is not found after installation, try the following code.

    export PATH=~/anaconda3/bin:$PATH

![](https://github.com/wulinghsuan/AWS/blob/master/MNIST/MNIST_2.png)

Install jupyter notebook

    jupyter notebook --ip=0.0.0.0 --no-browser

Go to Jupyter page you just linked. Click NEW → Terminal

Creat a new virtual environment

    conda install nb_conda                        #This needs to be done outside your virtual env
    
    conda create -n MNIST python=3.6              #MNIST can replace by any name of env you like
    conda activate MNIST
    
    conda install ipykernel
    ipython kernel install --user --name=MNIST    #MNIST can replace by any name you want to display
    
Train MNIST model

    conda install keras
    conda install opencv
    
If you get the following command, try the following code and do it again.

    sudo chown -R $USER:$USER anaconda3

![](https://github.com/wulinghsuan/AWS/blob/master/MNIST/MNIST_3.png)

![](https://github.com/wulinghsuan/AWS/blob/master/MNIST/MNIST_4.png)

Copy [TRAINMACHINE](https://github.com/wulinghsuan/AWS_MNIST/tree/master/TRAINMACHINE) folder to the env

    sudo apt-get install git
    sudo git clone https://github.com/wulinghsuan/AWS_MNIST.git

## 2. Web - FRONTEND Server

You choose Amazon Linux 2 AMI (HVM) or Ubuntu.

Public Subnet → Enable Auto-assign Public IP → SG_FE → Key.pem

SG_FE:

|Type|Protocol|Port Range|Source|
| --- | --- | --- | --- |
|HTTP|TCP|80|0.0.0.0/0|
|SSH|TCP|22|0.0.0.0/0|

In Amazon Linux 2 AMI (HVM):

    sudo yum update -y	                    	#Update the list of the available software
    sudo yum -y install httpd    	        	#httpd: the package that runs Apache
    
    sudo yum install git
    sudo git clone https://github.com/wulinghsuan/AWS_MNIST.git
    
    sudo service httpd start       	        	#Start the servcie
    sudo service httpd status     	        	#Check if it works
    
    sudo mv AWS_MNIST/FRONTEND/index.html /var/www/html/
    sudo mv AWS_MNIST/FRONTEND/static /var/www/html/
    
In Ubuntu:

    sudo apt-get update -y
    sudo apt-get install apache2

    sudo apt-get install git
    sudo git clone https://github.com/wulinghsuan/AWS_MNIST.git
    
    sudo mv AWS_MNIST/FRONTEND/index.html /var/www/html/
    sudo mv AWS_MNIST/FRONTEND/static /var/www/html/
    
    
**Result**

Link IPv4 Public IP on brower.

![](https://github.com/wulinghsuan/AWS/blob/master/MNIST/MNIST_6.png)


## 3. APP - BACKEND Server

Ubuntu Server 18.04 LTS (HVM) → Public Subnet → Enable Auto-assign Public IP → SG_BE → Key.pem

SG_BE:

|Type|Protocol|Port Range|Source|
| --- | --- | --- | --- |
|Custom TCP Rule|TCP|5000|0.0.0.0/0|
|SSH|TCP|22|0.0.0.0/0|

    sudo apt-get update
    sudo apt install python3-pip

    sudo apt-get install git
    sudo git clone https://github.com/wulinghsuan/AWS_MNIST.git
    
    #Download packages
    pip3 install scipy==1.1.0
    sudo pip3 install flask
    sudo pip3 install imageio
    sudo pip3 install keras
    sudo pip3 install tensorflow
    sudo pip3 install flask_cors
    sudo pip3 install opencv-python
    
    sudo mv AWS_MNIST/BACKEND/cnn-minst
    
    sudo python3 keras_flask.py

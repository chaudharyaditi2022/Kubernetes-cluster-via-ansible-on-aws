# Kubernetes-cluster-on-AWS-via-Ansible

This project launches Kubernetes cluster on AWS Cloud with `3 nodes (one master node and two worker nodes)`. It launches three EC2 instances, configures docker and
configures kubernetes master and slave node in the launched instances.


## Prerequisites

Before you begin, ensure you have met the following requirements:

* Make sure your system has following softwares and libraries installed.

To install awscli use following commands:
```
$sudo apt update
$sudo apt install python3-pip
$pip3 install awscli
```
or
```
$sudo yum update
$sudo yum install python3-pip
$pip3 install awscli
```

Once the CLI is installed, run aws configure and enter your AWS access key ID and secret access key.
```
aws configure
cat .aws/credentials
```
You can get keys from the Your Security Credentials page in the AWS Management Console. Here's how those keys will look
```
AccessKeyId: AKIALNZTQW6H3EFBRLHQ
SecretAccessKey: f26B8touguUBELGpdyCyc9o0ZDzP2MEUWNC0JNwA
```

To install Ansible use following command
```
$pip install ansible
$ansible --version

$pip3 install boto boto3
```

## Usage

Follow these steps:
* Create a working directory for properly managing the files and clone the repository or download the code inside the working directory.
```
$mkdir <working_directory_path>
$cd <working_directory_path>
$wget https://github.com/chaudharyaditi2022/Kubernetes-cluster-via-ansible-on-aws.git
```
### Files Description
* aws_ec2.yml :- Launches three ec2 instances on aws
* inventory_aws_ec2.yml :- Inventory file which dynamically fetches infomation about launched instances.
* docker-configure.yml :- Installs and configures docker 
* kubernetes-configure-master.yml :- Configures kubernetes master node
* kubernetes-configure-worker.yml :- Configures kubernetes worker node

To launch instances follow the following steps
* Configure ansible.cfg file by adding following under `[defaults]` block
```
private_key_file= <working_directory_path>/Kubernetes-cluster-key.pem
remote_user= ec2-user
```
* Run the following commands to launch kubernetes cluster
```
$ansible-playbook aws_ec2.yml
$ansible -i inventory_aws_ec2.yml --list-hosts
$ansible-playbook -i inventory_aws_ec2.yml docker-configure.yml
$ansible-playbook -i inventory_aws_ec2.yml kubernetes-configure-master.yml
$ansible-playbook -i inventory_aws_ec2.yml kubernetes-configure-worker.yml

```




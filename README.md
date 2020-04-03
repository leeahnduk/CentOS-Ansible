# Ansible CentOS Apps
This application helps to quickly deploy a multi Tier apps with CentOS VMs and deploy Tetration sensors automatically.

## Table of contents
* [Installation](#Installation)
* [Screenshots](#screenshots)
* [How to Use](#UserGuide)
* [Steps to run](#Steps)
* [Feedback and Author](#Feedback)

## Installation

From sources

Download the sources from [Github](https://github.com/leeahnduk/CentOS-Ansible.git), extract and execute the following commands

```
$ git clone https://github.com/leeahnduk/CentOS-Ansible.git

```

## Screenshots
![Run screenshot](https://github.com/leeahnduk/CentOS-Ansible/blob/master/Ansible-CentOS.jpg)
![Result screenshot](https://github.com/leeahnduk/CentOS-Ansible/blob/master/Result.jpg)
![vCenter screenshot](https://github.com/leeahnduk/CentOS-Ansible/blob/master/vCenter.jpg)
![Tetration screenshot](https://github.com/leeahnduk/CentOS-Ansible/blob/master/Tetration.jpg)

## UserGuide
How to use this application:
* You need to have an ansible VM to run Ansible Playbook. It can run on CentOS or Ubuntu VM. How to setup, please use this link: https://www.ansible.com/resources/videos/quick-start-video?extIdCarryOver=true&sc_cid=701f2000001OH7YAAW
* Copy ssh/ansible-ssh private key and ssh/ansible-ssh.pub key into ~/.ssh folder of ansible VM and change name to ansible and ansible.pub
* Run in ansible VM: eval `ssh-agent -s`, ssh-add ~/.ssh/ansible, ssh-keygen -R Remote_VMs_IP
* export ANSIBLE_HOST_KEY_CHECKING=False in ansible VM
* Edit to match with the destination environment (vCenter, Portgroups, VM Folder, DC, …) in Group_vars, Hosts folders AND VM_DEPLOY.YML.
* can ssh to the remote VM to test: ssh ansible@…, sudo -i, yum install -y ...
* add your ansible VM public key into roles/ssh/files/public_keys,
* edit file main.yml in folder roles/ssh/tasks for ssh public key
* Add Tetration agents sh scripts into folder roles/tetration/files
* cp roles/tetration/files/asean_enforcer_linux.sh /tmp/asean_enforcer_linux.sh
* Change Tetration sh filename accordingly.
* Create Folder in vCenter: Ansible in this example
* Portgroup in vCenter - For Example Shared: 192.168.33.128/28. in ACI, create EPG for Shared Service portgroup in the same subnet
    * Core|Tetration|Tet-Shared
    * myvm_folder="Ansible"

* to run ansible playbook, use command:  `ansible-playbook -i hosts/test deploy.yml`
* It will automatically deploy Multi Tier Apps: Wordpress, OpenCart, with FrontEnd Proxy, BackEnd Proxy and Percona DB cluster with NFS server. 


## Steps

Step 1: Issue `git clone https://github.com/leeahnduk/CentOS-Ansible.git` to install.

Step 2: Modify all the above parameters to match with your environment.

Step 3: Run the apps: `ansible-playbook -i hosts/test deploy.yml`

Step 4: Run the apps: `ansible-playbook -i hosts/test clean.yml` to clean all the VMs.

## Feedback
Any feedback can send to me: Le Anh Duc (leeahnduk@yahoo.com or anhdle@cisco.com)

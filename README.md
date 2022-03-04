# Ansible-Documentation
# Ansible Notes
Ansible is a open-source IT Congfiguration Management,Development and Orchestration Tool.
It aims to provided large productivity gains to wide varicty of automation challengers.

## How to Establish ssh connection between Server and Node
Take acces of all machines Windows (vi putty) and linux terminal

Now go inside ansible server and download ansible package
```sh
weget http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```
Now do "ls"
```sh
yum install epel-release-latest-7.noarch.rpm -y
```
```sh
yum update -y
```
Now we have to install all packages are by one
```sh
yum install git python python-level python-pip openssl ansible -y
```
Now got to hosts file inside ansible server and paste privet ip of nodes1 & node2
```sh
vi /etc/ansible/hosts
```
Now this hosts file is any working after updating ansible cfg file
```sh
vi /etc/ansible/ansible.cfg
```
## uncommented
#inventory  = /etc/ansible/hosts
#sudo-user  = root

Now create one user ,in all the these instances
```sh
adduser ansible
```
Now set password for this user

```sh
passwd ansible
````

Now Switch as ansible user
```sh
su -ansible
```
Sudo priviledges to ansible User
```sh
visudo
```
Now go to inside this file
visudo file write....

root ALL = (ALL)    ALL
ansible ALL=(ALL)   NOPASSWD: ALL

Now go to ansible server and they to install httpd package as a ansible user
```sh
sudo yum install httpd -y
```

Now estabilish connection betwwen server node and go to ansible server
[ansible@ip]#
```sh
ssh  <node privet ip>
``` 
OUTPUT : permission denied

Now we have to do some changes in sshd_config file go to ansible server
[roo@ip]#
```sh
vi /etc/ssh/ssh_config
```
```sh
service sshd restart
```
## uncomment and comment
PermitRootLogin yes
PasswordAuthentication yes
#PasswordAuthentication no

Do this work in Node1 & Node2 also Now verify in ansible server
[ansible@ip]#
```sh
sudo -ansible
ssh  <node privet ip>
``` 

Now go to ansible server and create keys Rule this command as ansible user.
[ansible@ip]#
```sh
ssh-keygen
```
hidden file show 
```sh
ls -a
```
```sh
cd .ssh/
ls
```
O/P -----> id_rsa_pub
Now I need to copy public key in bot nodes 
[ansible@ip]# 
```sh
ssh-copy-id ansible@<node1 privet ip>
ssh-copy-id ansible@<node2 privet ip>
```
## Host Pattern
"all" pattern refers to all the machine in an inventary

```sh
ansible all --list-hosts
ansible demo --list-hosts
ansible demo[0] --list-hosts
ansible demo[0:1] --list-hosts
ansible demo[2] --list-hosts
```
Group sepralid by a colon can be used to use hosts from multiple groups

demo[1:3]:devops[2:8]


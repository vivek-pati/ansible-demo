# Ansible

This docmument covers the basis of Ansible. Includes topics like how to setup ansible enviornment using Docker, Oracle Virtual box. 
Walks you through a sample project using Ansible. 

## Installation

Downwload Oracle Virtual box and CENTOS image. Spin up a VM using the same CENTOS image. 

Once your VM is running , shh into the machine to Install docker and Ansible. 

Run 2-3 docker containers that will act as target server. I am downloading ssh enable docker container from one of the open docker hub repo. 

```bash
  #download the docker image
  docker run -it -d mmumshad/ubuntu-ssh-enabled 
  #check the container is running or not. 
  docker ps
  # Inspect the container to get the IP.
  docker inspect <containerID-1sttwoletters will work>
```
Once your contianer are up and running , ssh into the the each of the cotainers at least once. 

Now create inventory.txt file
```bash
  target1 ansible_host=172.17.0.2 ansible_ssh_pass=Passw0rd
  target2 ansible_host=172.17.0.3 ansible_ssh_pass=Passw0rd
  target3 ansible_host=172.17.0.4 ansible_ssh_pass=Passw0rd
```
ping into the mashines using ansible
```bash
  ansible target1 -m ping -i inventory.txt
```

## Application 
[Simple Web App](APPSETUP_README.md)

https://github.com/mmumshad/ansible-training-answer-keys-2/blob/master/Section_3_HostVars_Include/Exercise_4/playbook.yml
galaxy.ansibl.com

docs.ansible.com
## Strategy 

### Liner Strategy 
All the tasks are executed in the same time in all servers- eg : Dependency, Install DB, Python Flask, Run server. It waits for the 1st task to complete in all servers before it moves to next. This is the default strategy 

### Free Strategy 

Tasks in each servers executed in the same time but doesnt wait for the task on other server to complete unlike linear. As soon a task is completed in one server it moves to other. 

### Batch Strategy 
This is based on linear strategy , instead of executing task in all the servers, it triggers on batch based on the field ( serial : 3)
can talk to 30 % as well. 

Note** : ansible.cfg has property called forks , default =5 . This is the number of servers that ansible can communicate in a single point of time. This can be increased to any desired number but you controller should have the CPU and network bandwidth to do this operation. 
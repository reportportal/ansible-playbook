

# Kubernetes and Report Portal

This Ansible playbook to help deploying and configuring a Kubernetes cluster with Report Portal

# Requirements

You will need a driver machine with ansible installed and a clone of the current repository:

* If you are running on cloud (public/private network)
  * Install ansible on the edge node (with public ip)
* if you are running on private cloud (public network access to all nodes)
  * Install ansible on your laptop and drive the deployment from it

### Installing Ansible on RHEL

```
curl -O https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
sudo rpm -i epel-release-latest-7.noarch.rpm
sudo yum update -y
sudo yum install -y  ansible
```

### Installing Ansible on Mac

* Install Annaconda
* Use pip install ansible

```
pip install --upgrade ansible
```

### Updating Ansible configuration

In order to have variable overriding from host inventory, please add the following configuration into your ~/.ansible.cfg file

```
[defaults]
host_key_checking = False
hash_behaviour = merge
command_warnings = False
```

### Supported/Tested Platform

* RHEL 7.x
* Ansible 2.6


# Defining your cluster deployment metadata (host inventory)

Ansible uses 'host inventory' files to define the cluster configuration, nodes, and groups of nodes
that serves a given purpose (e.g. master node).

Below is a host inventory sample definition for example:

```
[all:vars]

[master]
master-1   ansible_host=10.10.0.10  ansible_ssh_private_key_file=/home/user/.ssh/key_rsa.pem

[nodes]
node-1   ansible_host=10.10.0.11  ansible_ssh_private_key_file=/home/user/.ssh/key_rsa.pem
node-2   ansible_host=10.10.0.12  ansible_ssh_private_key_file=/home/user/.ssh/key_rsa.pem
```

# Deploying Kubernetes

### Deployment playbook

The sample playbook below can be used to deploy an Report Portal

```
- name: setup kubernetes
  hosts: all
  remote_user: root
  roles:
    - role: common
    - role: k8s

```




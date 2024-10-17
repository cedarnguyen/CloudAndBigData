# Step-by-Step Instructions for Setting Up a Hadoop-Spark Cluster with Ansible

## 1. Install SSH on 3 Servers

### On Master Server:
1. **Install Ansible:**
   ```bash
   sudo apt-get install ansible -y
Update /etc/hosts
   ```
   ```bash
sudo vim /etc/hosts
   ```
Verify Connectivity:

   ```bash
ping ...
```
Create Ubuntu User:
   
   ```bash
sudo adduser ubuntu
```
Install SSH:
   
   ```bash
sudo apt-get install openssh-server
```
Update SSH Configuration:

   ```bash
sudo nano /etc/ssh/ssh_config
```
Add modified the following lines:
```
Host *
    StrictHostKeyChecking no
```
Generate SSH Key:
   ```bash
ssh-keygen -t rsa
```
Copy Key to Slave Servers:

   ```bash
ssh-copy-id ubuntu@slave1
ssh-copy-id ubuntu@slave2
```
Update SSH Configuration Again:

```bash
sudo nano /etc/ssh/ssh_config
```
2. Install Ansible:

   ```bash
sudo apt install ansible
```
3. Create Directory Structure:

   ```bash
mkdir ansible
mkdir inventory
```
Create Inventory File:

   ```bash
vim ~/ansible/inventory/hosts.ini
```
Test Ansible Connectivity:

   ```bash
ansible all -m ping
```
4. Create Playbooks Directory:

   ```bash
mkdir playbooks
```
Create passwdless_su.yaml Playbook

Run the playbook with:

   ```bash
ansible-playbook passwdless_su.yaml --ask-become-pass
```
Then specify sudo password (same).

Create install_java.yaml Playbook

Run the playbook to install Java:

   ```bash
ansible-playbook playbook/install_java.yaml
```
Install Hadoop & Spark
Run the playbook to install:

   ```bash
ansible-playbook playbook/hadoop_spark_install.yaml
```
Change Permission of Install Folder:
Run the playbook:

   ```bash
ansible-playbook playbook/change_permission.yaml
```
Update .bashrc

Run the playbook:

   ```bash
ansible-playbook playbook/update_bashrc.yaml
```
Configure Hadoop & Spark:
Run the playbooks:

   ```bash
ansible-playbook playbook/config_hadoop.yaml
ansible-playbook playbook/config_sparks.yaml
```
Create Start and Stop Scripts
Create start.sh and stop.sh:

   ```bash
./start.sh
./stop.sh
```
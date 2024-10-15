Here's a sample README file you can use for your GitHub repository:

---

# Jenkins Deployment Guide

## Setup Instructions

### 1. Copy SSH Public Key

To enable Ansible to connect to your Jenkins server, you need to copy your SSH public key from the control plane or workstation to the Jenkins server.

Run the following command on your control plane or workstation to copy the public key:

```bash
ssh-copy-id vagrant@192.168.201.23
```

Replace `vagrant@192.168.201.23` with your actual Jenkins server SSH credentials.

### 2. Update Inventory File

Edit your Ansible inventory file to include your Jenkins server. Here is an example of how to update your `inventory` file:

```ini
[jenkins]
192.168.201.23 ansible_user=vagrant
```

Ensure the IP address and username match your Jenkins server setup.

### 3. Update `tests/test.yml` File

You need to configure your `tests/test.yml` file to use the Jenkins role. Here is an example of how to update it:

```yaml
---
- hosts: jenkins
  remote_user: vagrant
  become: true

  roles:
    - ./roles/jenkins
```

### Then run the ansible role using ansible-playbook commands

```
ansible-playbook -i roles/jenkins/tests/inventory.ini roles/jenkins/tests/test.yml


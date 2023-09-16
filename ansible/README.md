# Provisioning VMS using Ansible Playbooks

- Make sure you have Vagrant installed on your host machine. You can follow instructions on how to do this [here](https://developer.hashicorp.com/vagrant/downloads).
- In this folder we have 2 playbook examples in the folder `playbooks`. One is for `Docker` installation, the other is for `Kubectl` for Kubernetes.

### Update Ansible inventory

- Create an `inventory.ini` file using the example (`inventory.ini.example`) provided and change the VMs' IP addresses to your own.

```
cp inventory.ini.example inventory.ini
```

- If using passwords for SSH, install `sshpass`

```
sudo apt-get install sshpass
```

### Installing Docker on VMs using Ansible playbook

Use the command below:

```
SSH_CONFIG=./ssh_config ansible-playbook -i inventory.ini -u vagrant -k playbooks/install_docker.yml
```

### Installing Kubectl on VMs using Ansible playbook

Use the command below:

```
SSH_CONFIG=./ssh_config ansible-playbook -i inventory.ini -u vagrant -k playbooks/install_kubectl.yml
```

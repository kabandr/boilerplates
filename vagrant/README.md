# Deploying VMs using Vagrant

## 1. Install Vagrant

Make sure you have Vagrant installed on your host machine.

## 2. Single vs Multiple VMs

Change to the directory `single-vm` or `multiple-vms` depending on whether you want to deploy a single vm or multiple.

In this exercise we are testing our deployment on our local machine (Linux) using KVM (Kernel-based Virtual Machine) using the open source virtualization management API libvirt. You can learn more about Libvirt [here](https://libvirt.org/docs.html).

## 3. Update Vagrantfile

Once you are in the your folder of choice, change the configuration details to add your preferred image types and versions, CPU number, Memory size and any shell commands you want to run on your deployed machines.

You can all the Vagrant boxes you can use [here](https://app.vagrantup.com/boxes/search). Adjust the filter to match your interest and speed up the search or simply enter some keywords in the search box.

## 4. Run Vagrantfile

Once you've configured the Vagrantfile to match your preferences, run this command to deploy your VMs:

```
vagrant up
```

You might need to run this command with sudo depending on how your user groups are set up. Be careful if you are running this in a production environment and make sure you understand the implications.

## 5. Check VMs' state

To check that your VMs are up and running, you can use a tool like virsh by running this command:

```
sudo virsh list
```

This command shows your VMs names and their state. The output will look like this:

```
 Id   Name                   State
--------------------------------------
 1    multiple-vms_ubuntu3   running
 2    multiple-vms_ubuntu5   running
 3    multiple-vms_ubuntu2   running
 4    multiple-vms_ubuntu4   running
 5    multiple-vms_ubuntu1   running
```

## 6. Accessing our VMs

We are using SSH to access our VMs. For a single VM, you can simply run this command:

```
ssh vagrant
```

But if we are running multiple VMs, we can use the same virsh tool to view our VMs ip addresses. Let's use the VM with Id 1 for example.

```
sudo virsh domifaddr multiple-vms_ubuntu3
```

The command above then outputs the VM's ip address, the network it's running on, the VM's MAC adrress and the network protocol the ip is using.

```
Name       MAC address          Protocol     Address
-------------------------------------------------------------------------------
 vnet0      52:54:00:71:90:97    ipv4         192.168.121.237/24
```

To access our VM, we run this command:

```
ssh vagrant@192.168.121.237
```

If you used a default vagrant box, here the VM login credentials:

- user: `vagrant`
- password: `vagrant`

## 6. Terminating our VMs

To stop our VMs, we use a simple command:

```
vagrant destroy

or

sudo vagrant destroy
```

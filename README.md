# kube-deploy-vagrant


## What's This About?
The purpose of this project is to easily fire up a VMs with a running Docker.
This project clones kubernetes/kube-deploy and creates docker mutinode k8s cluster. 

## Preparation of *Ubuntu* Host

### `libvirt`
```bash
sudo apt-get install libvirt-bin qemu qemu-system-x86
```

### *Vagrant* 1.8.1+
Download from [website](http://www.vagrantup.com/downloads.html), then:
```bash
sudo dpkg -i vagrant_1.8.1_x86_64.deb
sudo apt-get install libvirt-dev
vagrant plugin install vagrant-libvirt
```

### *Ansible* 1.9+

```
sudo apt-get remove pip
sudo apt-get install python-setuptools python-dev build-essential
sudo easy_install pip
sudo pip install ansible
```

Reboot system.


## Preparation of *CentOS 7* Host

Add *epel* repository:
```
sudo yum install epel-release
```

### `libvirt`
```bash
sudo yum install libvirt qemu qemu-system-x86
```

### Install Vagrant 1.8.1+
Download from [website](http://www.vagrantup.com/downloads.html), then:
```
sudo yum install vagrant_1.8.1_x86_64.rpm
sudo yum install gcc libvirt-devel
vagrant plugin install vagrant-libvirt
```

### Ansible 1.9+
```
sudo yum install ansible
```

Reboot the system

## Start instances

```
vagrant up master --provider libvirt
```

When master is ready you can start node:

```
vagrant up node --provider libvirt
```

## Destroy cluster

```
vagrant destroy master
vagrant destroy node
```

##License
Apache

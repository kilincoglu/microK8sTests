# mircoK8sTests
Some Vagrant setups to play around with mircoK8s

To install provision the used virtual machines is ansible used

# Requirements
* installed VirtualBox or HyperV
* installed vagrant
* installed Ansible
* installed sshpass

Tested under Ubuntu 20.04 with virtualBox

# Usage
## General
```bash
# configuration of ssh key usage to login into the virtual machines
./bin/configure_ssh.sh
```

In the virtual machines is tmux used to run background processes. See also here: https://wiki.ubuntuusers.de/tmux/

```bash
# tmux basics
## list open session
tmux ls

## create a new session 
tmux new -s new_session_name

## attach a session
tmux attach -s new_session_name

# detach a tmux session
CTRL-B d 
```

## Setup a single machine microK8s instance
```bash
# start/create the VM for the installation
cd REPO_ROOT/vagrant/single
vagrant up

# optional - is also called by the install script 
# configuration of ssh key authentication for user 'admin'
#REPO_ROOT/bin/configure_ssh.sh IP_OF_THE_NEW_VM admin single demo123

# optional - connect to the virtua machine
#REPO_ROOT/bin/connect.sh IP_OF_THE_NEW_VM admin single

# optional - install microK8s
# REPO_ROOT/bin/install_single.sh 172.28.128.7 admin single demo123

# install microK8s, with autodiscovery if the VM IP
REPO_ROOT/bin/install_single.sh

# connect to the single instance installation
REPO_ROOT/bin/connect_single.sh

# test the state of microk8s
microk8s status --wait-ready

# query existing nodes
microk8s kubectl get nodes

# query existing services
microk8s kubectl get services


# for completeness - destroy/remove the VM
cd REPO_ROOT/vagrant/single
vagrant destroy
```


# Folder Project Structure
* ansible - Ansible scripts to prepare the virtual machines
* bin - contains helper scripts to simplify usage
* vagrant - base for the vagrant machines
* vagrant/single - single machine Kubernetes
* vagrant/cluster - a Kubernetes cluster that constists of one master and three worker nodes

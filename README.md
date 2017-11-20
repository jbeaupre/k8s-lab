# k8s-lab
Ansible pre-setup tasks for a k8s cluster on ubuntu 16.04


# Pre-reqs
Need to have ansible installed. You can easily run it in a virtual env on the development machines.

```
sudo apt-get install virtualenv python-pip
mkdir ansible-env
virtualenv ansible-env
source ansible-env/bin/activate
pip install --upgrade pip
pip install ansible
```

The virtual env is activated by `source ansible-env/bin/activate`. If you exit the virtual env or start a new shell be sure to activate the virtual env. 


# Inventory
Update the ansible/inventory file for your setup. 

## Key Variables:
1. Per Host Variables
* `clusternet_ip` IP address used for cluster interface 
* `podnet_cider` CIDR for the pod network on this host 
* `ansible_host` IP address for ansible to use to connect to server (most likely same as cluster IP)
* `ansible_ssh_user` Username for ansible to log in with (ubuntu for Vagrant)
* `ansible_ssh_pass` Password for ansible to log in with (See box Vagrantfile for Vagrant)
* `ansible_sudo_pass` Password for sudo once logged into box
* `clusternet_interface` Inteface to use for cluster (enp0s8 for Vagrant)
* `clusternet_netmask` Netmask for cluster

2. Per Setup Variables
* `bridge_interface` true/false - flag to determine whether to use bridge CNI plugin for cluster


# Setup
After editing inventory, test connectivity:
```
ansible -i inventory -m ping all
```

If all pass, then apply the setup:
```
ansible-playbook -i inventory site.yml all
```

# Cluster
On the master initialize the cluster with the following:
```
sudo kubeadm init --apiserver-advertise-address=172.42.42.1 --pod-network-cidr=192.168.0.0/16 --service-cidr 10.96.0.0/12

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

```
When the command completes run the join command on the nodes (see output from kubeadmin init for the join command to run):
```
ansible -i inventory -a "kubeadm join --token <INSERT TOKEN> 172.42.42.1:6443 --discovery-token-ca-cert-hash <INSERT DISCOVERY TOKEN>" --become kube_nodes

```




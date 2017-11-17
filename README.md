# k8s-lab
Ansible pre-setup tasks for a k8s cluster on ubuntu 16.04


# Pre-reqs
Need to have ansible installed. You can easily run it in a virtual env on the development machines.

```
mkdir dinet-env
virtualenv dinet-env
source dinet-env/bin/activate
pip install --upgrade pip
pip install ansible
```

The virtual env is activated by `source dinet-env/bin/activate`. If you exit the virtual env or start a new shell be sure to activate the virtual env. 


# Inventory
Update the ansible/inventory file for your setup. 


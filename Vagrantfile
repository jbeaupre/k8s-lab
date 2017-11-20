# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

Vagrant.configure("2") do |config|

  config.vm.define "master" do |master|
    master.vm.box = "ubuntu/xenial64"
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: "172.42.42.1",
      auto_config: false
    master.vm.network "private_network", ip: "192.168.254.1"
    master.vm.provision "shell", path: "master_install.sh"
  end

  config.vm.define "node1" do |node1|
    node1.vm.box = "ubuntu/xenial64"
    node1.vm.hostname = "node1"
    node1.vm.network "private_network", ip: "172.42.42.2",
      auto_config: false
    node1.vm.network "private_network", ip: "192.168.254.2"
    node1.vm.provision "shell", path: "install.sh"
  end

  config.vm.define "node2" do |node2|
    node2.vm.box = "ubuntu/xenial64"
    node2.vm.hostname = "node2"
    node2.vm.network "private_network", ip: "172.42.42.3",
      auto_config: false
    node2.vm.network "private_network", ip: "192.168.254.3"
    node2.vm.provision "shell", path: "install.sh"
  end
  
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
  end
  
end


# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
config.vm.box = "bertvv/centos72"

config.vm.provider "virtualbox" do |vb|
     vb.gui = true
     vb.memory = 1024
     vb.cpus = 1
end

config.vm.define "server1" do |server1|
    server1.vm.hostname = "srv1"
    server1.vm.network "private_network", ip: "192.168.56.111"
    server1.vm.provision "shell", inline: <<-SHELL
       echo "192.168.56.112 srv2" >> /etc/hosts
       #yum update -y
       yum install git -y
       git clone https://github.com/evgenyte/vagrant.git
       cd vagrant
       git checkout task2
       cat task2.txt
    SHELL
end

config.vm.define "server2" do |server2|
    server2.vm.hostname = "srv2"
    server2.vm.network "private_network", ip: "192.168.56.112"
    server2.vm.provision "shell", inline: <<-SHELL
      echo "192.168.56.111 srv1" >> /etc/hosts
      #yum update -y
    SHELL
end
end

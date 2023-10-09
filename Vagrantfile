# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |vb|
    vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
  end
  config.ssh.insert_key = false
  config.vm.define "load_balancer" do |lb|
    lb.vm.box = "ubuntu/focal64"
    lb.vm.network "forwarded_port", 
      id: 'http', guest: 80, host: 8080, host_ip: "127.0.0.1"
    lb.vm.network "forwarded_port",
     id: 'https', guest: 443, host: 8443, host_ip: "127.0.0.1"
    lb.vm.network "private_network", ip: "192.168.0.254", virtualbox__intnet: "backend"
  end

  config.vm.define "backend1" do |b1|
    b1.vm.box = "ubuntu/focal64"
    b1.vm.network "private_network", ip: "192.168.0.1", virtualbox__intnet: "backend"
  end

  config.vm.define "backend2" do |b2|
    b2.vm.box = "ubuntu/focal64"
    b2.vm.network "private_network", ip: "192.168.0.2", virtualbox__intnet: "backend"
  end

  config.vm.define "backend3" do |b3|
    b3.vm.box = "ubuntu/focal64"
    b3.vm.network "private_network", ip: "192.168.0.3", virtualbox__intnet: "backend"
  end
end

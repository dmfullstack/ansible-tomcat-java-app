#!/usr/bin/env ruby
# Creates an Ubuntu 16.04 VM
#   * Run using 'vagrant up'
#   * SSH using vagrant@192.168.10.10, password 'vagrant'

Vagrant.configure("2") do |config|
    config.vm.box = "bento/ubuntu-16.04"
  config.vm.network "private_network", ip: "192.168.10.10"

    config.vm.provider "virtualbox" do |vb|
   	 vb.memory = "1024"
   	 vb.customize ["modifyvm", :id, "--cableconnected1", "on"]
    end
end


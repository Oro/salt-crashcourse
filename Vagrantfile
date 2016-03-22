# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "master" do |box|
    box.vm.box = "ubuntu/trusty64"
    box.vm.hostname = "master"
    box.vm.network :private_network, ip: "172.17.0.200", :netmask => "255.255.0.0"
    box.vm.synced_folder "salt/roots/", "/srv/salt/"
    box.vm.provision :salt do |salt|
      #-F overwrite files
      #-c set temp config directory
      #-P allow pip based installations
      #-D enable debug logging
      #-A set master url
      #-M install master
      salt.bootstrap_options = "-A 172.17.0.200 -M"
      salt.master_config = "master.conf"
      salt.colorize = true
    end
  end

  config.vm.define "minion-01" do |box|
    box.vm.box = "ubuntu/trusty64"
    box.vm.hostname = "minion1"
    box.vm.network :private_network, ip: "172.17.0.202", :netmask => "255.255.0.0"
    box.vm.provision :salt do |salt|
      salt.bootstrap_options = "-A 172.17.0.200"
      salt.minion_config = "minion.conf"
      salt.colorize = true
    end
  end

  config.vm.define "minion-02" do |box|
    box.vm.box = "ubuntu/trusty64"
    box.vm.hostname = "minion2"
    box.vm.network :private_network, ip: "172.17.0.203", :netmask => "255.255.0.0"
    box.vm.provision :salt do |salt|
      salt.bootstrap_options = "-A 172.17.0.200"
      salt.minion_config = "minion.conf"
      salt.colorize = true
    end
  end
end

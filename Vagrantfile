# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "bento/ubuntu-18.04"

  # Private network static IP
  config.vm.network "private_network", ip: "192.168.50.50"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Customize the amount of CPU and memory on the VM:
    vb.cpus = 2
    vb.memory = "4096"
  end

  # Enable USB Controller on VirtualBox
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--usb", "on"]
    vb.customize ["modifyvm", :id, "--usbehci", "on"]
  end

  # Implement determined configuration attributes
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["usbfilter", "add", "0",
        "--target", :id,
        "--name", "Any USB Flash Disk",
        "--vendorid", "0x8644",
        "--productid", "0x800b"]
  end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL

  config.vm.synced_folder "../", "/git"

  # Custom bootstrap provisioning file.
  config.vm.provision "shell", privileged: false,
    inline: "/bin/bash /vagrant/scripts/guest/bootstrap-vm.sh"
end

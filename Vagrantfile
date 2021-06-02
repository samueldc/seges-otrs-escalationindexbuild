# -*- mode: ruby -*-
# vi: set ft=ruby :

# https://docs.ansible.com/ansible/latest/user_guide/index.html
    
# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  config.vm.provider "libvirt"
  config.vm.provider "virtualbox"
  config.vm.box = "generic/debian10"
  
  config.vm.provider :libvirt do |provider, override|
    override.vagrant.plugins = ["vagrant-libvirt"]
    provider.driver = "kvm"
    provider.cpus = "2"
    provider.memory = "2048"
  end

  config.vm.provider :virtualbox do |provider, override|
    override.vagrant.plugins = ["vagrant-vbguest"]
    provider.cpus = "2"
    provider.memory = "2048"
  end

# Provision Znuny development vm
  config.vm.define "znuny-dv", primary: true do |znunydv|
    znunydv.vm.network "private_network", ip: "10.0.0.11"
    znunydv.vm.network "forwarded_port", guest: 80, host: 8081
    znunydv.vm.hostname = "znuny-dv.localhost"
    znunydv.vm.synced_folder ".", "/opt/otrs-module/"
    znunydv.vm.provision "file", source: "./playbook.znuny-dv.yml", destination: "/home/vagrant/"
    znunydv.vm.provision "shell", 
      inline: 'printf "\ndeb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" | sudo tee /etc/apt/sources.list.d/ansible.list'
    znunydv.vm.provision "shell", inline: "sudo apt-get install -y gnupg"
    znunydv.vm.provision "shell", inline: "sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367"
    znunydv.vm.provision "shell", inline: "sudo apt-get update && sudo apt-get install -y ansible"
    znunydv.vm.provision "shell", inline: "sudo ansible-galaxy collection install community.mysql"
    znunydv.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.znuny-dv.yml"
      ansible.provisioning_path = "/home/vagrant/"
      ansible.host_vars = {
        "znuny-dv" => {"ansible_python_interpreter" => "/usr/bin/python3"}
      }
      ansible.verbose = "-vvv"        
    end
    znunydv.vm.provision "shell", run: "always", inline: <<-SHELL
    #   cd /opt
    #   sudo git clone https://github.com/OTRS/module-tools.git
    #   cd /opt/module-tools
    #   sudo git checkout rel-1_0
      /opt/module-tools/link.pl /opt/otrs-module/ /opt/otrs/
    SHELL
    znunydv.vm.provision "shell", inline: "sudo systemctl restart apache2", run: "always"
  end  

end
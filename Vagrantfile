# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.hostname = "vm-docker"
  config.vm.synced_folder "./provision", "/home/vagrant/provision",
    owner: "vagrant", group: "vagrant"
  config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--cpus", "2"]
    vb.customize ["modifyvm", :id, "--cpuexecutioncap", "32"]
    vb.customize ["modifyvm", :id, "--memory", "1024"]
    vb.name = "vm-docker"
  end

  $script = <<-SCRIPT
  sudo apt-get update
  sudo apt-get upgrade -y
  sudo apt-get -y install mc tree curl
  sudo curl -fsSL https://get.docker.com/ | sh
  SCRIPT

  config.vm.provision "shell", inline: $script
end

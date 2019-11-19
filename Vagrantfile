# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.hostname = "vm-docker"
  config.vm.network "public_network", type: "dhcp", bridge: "wlp2s0"
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
  sudo echo "Install Docker..."
  sudo curl -sSL https://get.docker.com/ | sh > /dev/null 2>&1
  sudo docker --version
  sudo echo "Install Docker Compose..."
  sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose > /dev/null 2>&1
  sudo chmod +x /usr/local/bin/docker-compose
  sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
  sudo docker-compose --version
  sudo usermod -aG docker vagrant && sudo su vagrant
  sudo usermod -aG dialout vagrant
  sudo reboot
  SCRIPT

  config.vm.provision "shell", inline: $script
end

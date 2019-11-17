# vm-docker
sudo apt update

sudo apt upgrade

wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -

wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] http://download.virtualbox.org/virtualbox/debian bionic contrib"

sudo apt update

sudo apt install virtualbox-6.0
virtualbox

wget https://releases.hashicorp.com/vagrant/2.2.6/vagrant_2.2.6_x86_64.deb

sudo dpkg -i vagrant_2.2.6_x86_64.deb

sudo apt -f install
